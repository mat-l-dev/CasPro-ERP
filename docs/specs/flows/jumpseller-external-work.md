# SP2 — Jumpseller y trabajo externo durable

Propietarios: cada adaptador/inbox técnico por conexión; Sales conserva pedidos observados; Inventory solicita publicación; Documents solicita email/objetos; Sales solicita verificación CPE. Ningún registro de integración sustituye esos hechos. [CM0](../cross-cutting/command-matrix.md#cm0) gobierna comandos y fases. No SDK de proveedor en políticas de dominio, framework multicanal ni worker implementado en esta fase.

## Capacidades verificadas y contrato del adaptador

VERIFIED significa documentación pública consultada, no cuenta validada. INTERPRETATION identifica decisiones de diseño. ASSUMPTION debe permanecer visible; PENDING VALIDATION bloquea activar el mecanismo dependiente, no la documentación independiente.

| Frontera pública comprobada | Uso delimitado en la slice |
|---|---|
| Jumpseller API v1, GET `/orders.json`, `/orders/{id}.json`, `/products/{id}.json` | Lectura y reconciliación; `read_orders`, `read_products`. Status de respuesta traducido, distinto de filtros; fijar locale y aceptar solo traducciones documentadas/validadas [S22](../../research/technical-sources.md) |
| PUT producto/variante o `/products_locations` | Stock absoluto entero; `write_products`, sin actualizar precio/pedido. Endpoint según producto/variante/ubicación comprobados; nunca inventar location_id [S22](../../research/technical-sources.md) |
| OAuth Authorization Code; scopes de hooks separados | Preferencia técnica OAuth para conexión registrada; no tokens en URL. Basic con token de tienda solo como alternativa explícitamente revisada si no se usa app OAuth; habilitación/cuenta PENDING VALIDATION [S22](../../research/technical-sources.md) |
| Resend envío con adjuntos e ID de email, clave idempotente de 24 h | Puerto email con payload congelado; retención local independiente. Consultar por email ID conocido para conciliar, no deducir inexistencia por falta de ID [S25/S27](../../research/technical-sources.md) |
| SUNAT Consulta Integrada | Consulta de identidad conocida; no emisión ni adquisición masiva SOL. Baseline manual en [CPE](cpe-document-delivery.md) [S23](../../research/technical-sources.md) |

El puerto inbound traduce a `ObservedOrder`: conexión/ID opaco, estado comercial observado/raw, referencia de receipt/lectura, instante externo si existe, instante/corte local, líneas/referencias SKU, moneda/componentes, cliente/identidades/contactos/direcciones y estado de pago/refund observado si llega. Números JSON se parsean exactamente a Decimal, aunque OpenAPI los describa float; NaN, Infinity, pérdida de precisión y valores fuera del contrato se rechazan. No deserializar a float y convertirlo después. Datos extras acotados no se convierten en columnas empresariales o URLs a seguir.

El puerto outbound stock recibe destino/resolución remota validada, entero no negativo, revisión del objetivo, generación de reconciliación y attempt ID. El puerto email recibe remitente autorizado, destinatario efectivo, contenido/adjuntos congelados, propósito, clave idempotente y correlación opaca. Respuesta común tipada: CONFIRMED(external ID/observación), REJECTED_KNOWN, TRANSIENT_NOT_SENT o UNKNOWN. Error del SDK no define por sí mismo si se ejecutó el efecto.

ProductsLocations requiere location_id, product_id, stock_unlimited y stock en el esquema leído; variant_id según destino comprobado. El adapter de stock finito fija `stock_unlimited=false` explícitamente y verifica esa condición al reconciliar; nunca copia el `true` del ejemplo oficial. No manda campos de precio/descripción ni adopta credenciales de los ejemplos.

Las páginas oficiales describen reducción al pasar New→Pending, sin otro descuento al pagar, y reposición por abandono/cancelación; otra página habla de descuento al fulfillment. También hay cifras de retries incompatibles entre secciones. Se registra la discrepancia [S21/S26](../../research/technical-sources.md). No se fija una semántica de stock por intuición: cuenta/plan/checkout/ubicación y transiciones deben comprobarse en una validación autorizada posterior.

Revalidación documental 2026-09-11: [OpenAPI oficial](https://api.jumpseller.com/swagger.json), enlazado desde [API support](https://jumpseller.com/support/api/), versión declarada1.0.0, SHA256 del JSON descargado `51f95c9c2586ea3980894b79f360d1f04e0db1974ab4eba0ec2ebacd63b2697d`. PUT producto/variante/ProductsLocations documenta stock y scope `write_products`; esas operaciones no documentan parámetro/encabezado de precondición de versión. Búsqueda de If-Match/ETag/compare-and-set en ese artefacto sin coincidencias: prueba ausencia en el contrato leído, **no imposibilidad universal del proveedor**. [Locations](https://jumpseller.com/support/locations/) sigue describiendo descuento al fulfillment y [webhooks](https://jumpseller.com/support/webhooks/) conserva firma HMAC/raw body y cifras de retry contradictorias. Se mantiene PENDING VALIDATION del protocolo de stock; no se hizo petición autenticada, PUT ni prueba contra tienda.

## Recepción y selección de pedidos

La URL de recepción selecciona conexión conocida por configuración del servidor. Verificar firma antes de interpretar negocio; entidad/cuenta nunca viene confiada del payload. El body se conserva como bytes con hash/procedencia y acceso/retención limitados. Payload demasiado grande/tipo inválido → rechazo acotado sin ejecutar parse o negocio. Firma falsa → rechazo y auditoría técnica sin conservar PII indiscriminada. Un 2xx solo sigue al commit del inbox durable, no a confirmación del pedido.

Bootstrap de esa frontera: binding de despliegue controlado entre ruta opaca, principal/mandato, entidad y referencia al secreto; sin datos comerciales ni consulta global a tablas de conexiones. La firma acredita ese binding, después Workspace verifica el mandato y se abre contexto RLS para consultar K/inbox. Si binding/mandato no coinciden con la conexión empresarial vigente, denegar. No eludir RLS para «descubrir tenant» ni leer todas las conexiones/secretos antes de autenticar. La extensión de aislamiento de WO-SP2-06 debe demostrar este recorrido.

Resend valida raw body y todos los headers firmados mediante su contrato oficial, incluida comprobación de timestamp/replay que soporte el verificador; reloj/ventana se verifican antes de activación. svix-id repetido con otro hash es conflicto de integridad. Un rechazo de antigüedad no permite perder el estado externo: conciliación por ID conocido conserva la vía de recuperación.

Jumpseller: HMAC SHA-256/base64 sobre raw body con secreto de hooks de esa conexión, comparación constante [S21](../../research/technical-sources.md). No confundirlo con token OAuth. Store-code/event/triggered-at son pistas; no asumir que están incluidos en la firma del body ni usarlos solos para cancelar/pagar o seleccionar entidad. No hay ID único de evento acreditado: cada recepción tiene ID local, fingerprint y procedencia. Coalescer trabajo pendiente por recurso bajo K, no deduplicar para siempre por order_id o hash del body (A→B→A puede ser legítimo). Mismo snapshot vigente no produce otra revisión/hecho; mismos bytes antiguos disparan lectura/reconciliación, no restauran historia.

El webhook señala que hay que refrescar el recurso; la selección empresarial usa lectura API individual o reconciliación completa registrada, nunca orden de llegada de callbacks. El contenido recibido sigue siendo evidencia de observación. Una lectura por recurso tiene generación local monotónica asignada antes del HTTP; respuesta de generación superada se conserva como observación tardía y no sustituye la seleccionada. Nuevos avisos durante lectura dejan DIRTY y solicitan otra lectura, sin declarar freshness por haber recibido 200.

Estados remotos normalizados de esta conexión: PAYMENT_PENDING, PAID_OBSERVED, CANCELED_OBSERVED, ABANDONED_OBSERVED, UNKNOWN. Conservan texto original/locale; los filtros de API no se toman como enum universal. Otros valores o fulfillment inesperado quedan UNKNOWN/REVIEW_REQUIRED, no se reinterpretan como cobro/entrega local. Refund reportado no modifica N. La traducción se valida con fixtures sanitizadas reales de contrato, sin diseñar otros marketplaces.

Reconciliación: recuperar pedidos paginados y stock/mappings, reconsultar recursos conocidos pendientes/discrepantes y realizar barrido completo periódico de la ventana de datos retenida para detectar eventos perdidos. Paginación no es snapshot atómico ni cursor de modificaciones; `after ID` o fecha de creación solos no detectan cambios en pedidos antiguos. Registrar páginas/IDs/corte/incompletos y generación; error/página ausente no avanza checkpoint ni acredita ausencia de un pedido. Frecuencia/ventana/límites deben ser parámetros operativos completos antes de activar, calibrados sin inventar SLA del proveedor. 429 reduce ritmo y respeta indicación de espera si viene; 401/403 bloquea conexión, no genera dinero ni retry sin límite.

<a id="stock-publication"></a>
## Publicación de disponibilidad

La fórmula y ownership de P/N/R/X/B/Q viven en [Inventory](sales-stock-treasury.md). Cada plan fija conexión/destino, mappings/revisiones, posiciones y casos fuente, Q, generación/corte de reconciliación y motivo. Estado del destino: DIRTY, RECONCILING, READY, PUBLISHING, UNKNOWN o BLOCKED; resultado técnico no equivale a saldo físico.

- C02/C04/C12/C13/C14/C15/C20/C21 que cambien inputs invalidan generación/revisión bajo K y solicitan recálculo; no copian deltas a la API. READY requiere inputs íntegros, sin mapping/orden pendiente que pueda cambiar el objetivo ni un intento previo desconocido.
- Comparar último objetivo/observación: si Q ya coincide y no hay incertidumbre, no crear otro envío. Eco de stock solo actualiza observación; no produce movimiento, reserva, nuevo objetivo por sí mismo o publicación infinita. Cancelación remota que repone stock no repone P.
- Antes de autorizar HTTP, releer revisiones/mandato/frescura y comprobar que es el objetivo vigente. Trabajo viejo → SUPERSEDED, no publicar. Respuesta vieja nunca marca el destino READY para el objetivo nuevo; conserva evidencia y reconcilia.
- Inbox atrasado, scan incompleto o pedidos sin mapping → BLOCKING para aumento. Si falta cualquier input de Q, no publicar un valor inventado. Se puede pedir publicación de cero como reducción conservadora con mandato vigente; timeout de esa reducción sigue siendo UNKNOWN, no garantía de tienda cerrada.
- **Límite de escritura concurrente:** no se ha acreditado compare-and-set/fence remoto para stock. Incluso un valor que parecía reducir stock puede aumentarlo frente a un checkout ocurrido entre GET y PUT. Ninguna lease local soluciona esa carrera. Para activar escrituras positivas automáticas hay que demostrar un protocolo compatible con checkout/reservas remotas. Hasta entonces, baseline positivo solo en ventana operativa controlada y acreditada sin cambios remotos competidores, gestionada por el operador fuera de CasPro; sin esa condición, queda BLOCKED. No se inventa API para cerrar checkout. Q se calcula y la bandeja explica el pendiente.

El gate técnico STOCK-PUBLISH exige: semántica real de descuento/reposición por estado; mapeo de ubicación/plan; doble pedido mientras cambia Q; escritura/respuesta tardía; evento perdido; timeout con PUT aplicado; ausencia de loops y reanudación sin reponer compromisos remotos. Su falta no impide importar/aceptar prudentemente pedidos con stock local, pero impide prometer prevención total de sobreventa del canal o activar publicación positiva desatendida. Rechazo por falta de stock tras orden externa queda excepción comercial visible; no compra o dinero ficticios.

## Persistencia mínima y estados técnicos

| Registro conceptual / dueño | Contenido necesario |
|---|---|
| Receipt/inbox / integración receptora | Conexión/entidad, identidad de entrega acreditada o ID local, hash/procedencia y payload privado acotado, instante/headers pertinentes, generación y resultado local |
| Job/outbox / solicitante del efecto | Tipo concreto (refresh order, publish stock, reevaluate document delivery, send document, verify CPE, artifact processing, report), referencia al dueño/revisión, mandato, destino, identidad de intención y epoch operativo |
| Attempt / mismo responsable técnico | Número/token, claim/lease/deadline, dispatch registrado, resultado/error clasificado, referencia externa y fecha; no guarda autorización perpetua ni hechos económicos |

No se exige tabla por fila de esta tabla ni engine configurable: backend PostgreSQL y worker simple candidato; comandos por caso explícitos. Inbox no posee decisión Sales, outbox no posee entregabilidad Documents. RAW payload no sustituye relaciones. Errores diagnósticos sanitizados; cuerpo/email/XML no va a logs.

Un trabajo local (procesar receipt, reevaluar Documents) confirma su resultado junto al comando dueño sin fase DISPATCHED externa; C06 solo reclama, libera locks y después se ejecuta el plan completo C04/C09/C34. C07/C08 corresponden a I/O externo, no a un motor que envuelva indiscriminadamente toda llamada local.

| Transición técnica | Comando / condición / significado |
|---|---|
| Sin receipt → RECEIVED | C02 autentica y confirma durable; recepción válida puede ser negocio inválido |
| RECEIVED → APPLIED / REJECTED / BLOCKED | C04/C09, deduplicación y efecto local en el mismo commit; bloqueo reanudable según causa |
| Sin job → READY | Comando dueño confirma intención con el cambio que la requiere; on_commit solo despierta |
| READY/RETRY_WAIT → CLAIMED | C06, vencimiento y mandato/epoch elegibles, token nuevo; no efecto externo |
| CLAIMED → DISPATCHED | C07, reautoriza y fija payload/revisiones; commit antes de HTTP |
| CLAIMED → READY o SUPERSEDED | Lease sin dispatch y prueba de no ejecución / inputs obsoletos; no reenviar DISPATCHED por lease vencida |
| DISPATCHED → SUCCEEDED / REJECTED / UNKNOWN | C08, clasificación por evidencia del efecto; timeout/proceso caído después de dispatch queda UNKNOWN |
| Fallo probado sin efecto → RETRY_WAIT | C08, error transitorio y calendario/límite no agotado; misma intención |
| Fallo permanente/límite agotado → BLOCKED/DEAD_LETTER | C08, causa y acción humana; no pérdida de la intención |
| BLOCKED/DEAD_LETTER/UNKNOWN → elegible para nueva evaluación | C10 con evidencia/mandato/revisión; nunca transforma UNKNOWN en READY por deseo de reintentar |

Lease: claim y renovación breves por token; consumidor viejo no cambia fila vigente. El deadline total de HTTP debe ser menor que lease con margen de persistencia; si esa relación/configuración no está definida y verificada, no activar envío. El shutdown deja de reclamar, termina fase corta y conserva DISPATCHED incierto si no conoce resultado. No llevar una transacción abierta durante HTTP, generación o espera.

Retry externo no sigue automáticamente el retry local CM0. Configuración por conexión/versionada: connect/read/total deadlines, máximo intentos, backoff con jitter, tope y tratamiento de Retry-After; propuesta técnica acotada se fija en la WO de adaptador y se demuestra antes de habilitar. Lecturas puras pueden reintentarse dentro de esos límites. Escritura con resultado incierto primero se concilia; en email no se autoriza reenvío ciego ni siquiera por disponer de clave de proveedor. El puerto distingue prueba de no envío de simple excepción.

Restore: credenciales y efectos externos deshabilitados antes de arrancar workers; epoch nuevo invalidará claims antiguos. Conciliar recibos y todas las intenciones que podrían haber sido ejecutadas después del corte restaurado usando proveedor/evidencia externa retenida; historial local restaurado no prueba ausencia de efecto. No reactivar en bloque outbox histórica. Sin prueba suficiente, UNKNOWN/HOLD. Email de restore nunca sale a cliente real; DB y objetos se verifican por separado conforme [operación](../../operations/delivery.md).

## Fichas técnicas (CM0)

<a id="c01"></a>
### C01 — Configurar o suspender conexión

- **OWNER / PURPOSE:** integración concreta; conexión/mandato de una entidad, sin datos empresariales globales.
- **INPUT / READS:** contexto, proveedor/cuenta/entidad, endpoints allowlist, referencias a secretos, capacidades/destino/configuración de límites, revisión y motivo; conexión/mandato previos.
- **LOCKS / LOCK ORDER:** I → K; identidad proveedor/cuenta/entidad única. No reasignar conexión usada a otra entidad.
- **WRITES / PRE / POST:** DRAFT/DISABLED/ACTIVE según validación habilitante, revisión/epoch; ACTIVE solo con autorización y capacidad comprobada. Cambio/suspensión invalida jobs pendientes, no hechos.
- **IDEMPOTENCY / RETRY / FAILURES:** D alta; V cambio; CM0; CONNECTION_CONFLICT/UNVALIDATED_CAPABILITY/INVALID_CONFIGURATION.
- **EVENTS / AUDIT:** ConnectionChanged con campos no secretos, actor/alcance y motivo.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; OAuth/consulta futura mediante fase externa autorizada. Rotación guarda referencia/versiones, nunca token en docs/logs.

<a id="c02"></a>
### C02 — Recibir webhook autenticado

- **OWNER / PURPOSE:** integración receptora Jumpseller o Resend; recepción durable y acuse sin confirmar negocio.
- **INPUT / READS:** raw body/headers, ruta de conexión conocida, hash, verificación criptográfica y tamaño; configuración/mandato y duplicados acreditados.
- **LOCKS / LOCK ORDER:** I si hay identidad de entrega acreditada → K → J. Resend UNIQUE conexión+svix-id con mismo hash; Jumpseller recepción local y coalescencia, sin unicidad eterna de body/order_id.
- **WRITES / PRE / POST:** inbox, marca DIRTY/generación cuando proceda y trabajo de procesar; firma/cuenta válidas; 2xx tras commit, duplicado acreditado devuelve acuse sin repetir trabajo/efecto.
- **IDEMPOTENCY / RETRY / FAILURES:** identidad natural para Resend; Jumpseller deduplica trabajo/efecto por recurso y snapshot vigente; CM0; SIGNATURE_INVALID/PAYLOAD_TOO_LARGE/CONNECTION_MISMATCH; DB fallida no acusa recepción durable.
- **EVENTS / AUDIT:** WebhookReceived/ReceiptDuplicate o rechazo técnico mínimo; no SaleCommitted/ReceiptConfirmed.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno durante transacción; verificación raw antes de parse, sin GET remoto al recibir. C10/C03 recuperan mensajes perdidos/bloqueados.

<a id="c03"></a>
### C03 — Reconciliar Jumpseller

- **OWNER / PURPOSE:** integración coordina lecturas remotas y entrega observaciones a Sales/Catalog/Inventory; no acepta ventas ni saldos.
- **INPUT / READS:** conexión, recurso/alcance del barrido, checkpoint/generación y mandato; jobs/casos/mappings/último corte.
- **LOCKS / LOCK ORDER:** I → K → E → M → J para plan/aplicación local; soltar antes de HTTP. Cada resultado se aplica por C04 o contrato de observación/mapping; no un scan gigante transaccional.
- **WRITES / PRE / POST:** plan/generación, páginas/IDs/observaciones/cursor de completitud; solo lectura completa compatible marca reconciliación apta. Respuesta antigua no sustituye la generación nueva.
- **IDEMPOTENCY / RETRY / FAILURES:** D del barrido/lectura; CM0 local y política externa de lecturas; PARTIAL_SCAN/RATE_LIMITED/AUTH_FAILED/UNKNOWN_REMOTE_STATE mantienen incertidumbre.
- **EVENTS / AUDIT:** ReconciliationObserved/Incomplete, sin hechos financieros; actor/mandato, corte y discrepancias.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** GET público autenticado autorizado posteriormente, mediante C06–C08; nuevo barrido conserva evidencia anterior, nunca borra pedido ausente de una página.

<a id="c04"></a>
### C04 — Aplicar observación de pedido

- **OWNER / PURPOSE:** Sales mediante consumidor autenticado; seleccionar propuesta/estado observado sin compromiso automático.
- **INPUT / READS:** receipt o resultado GET, o solicitud de reevaluar selección vigente tras C11/C12/C15; conexión/ID, snapshot normalizado y generación/corte; caso, términos revisados contra esa observación, Party/mapping referenciados y venta asociada si existe.
- **LOCKS / LOCK ORDER:** I → K → E → M → J; E se crea bajo K/UNIQUE. No modifica venta aceptada ni toma S para alterar términos.
- **WRITES / PRE / POST:** observación, selección/revisión, resolución/discrepancia y receipt procesado; snapshot igual no duplica observación, pero cambios de referencias/términos pueden cambiar readiness con revisión nueva. Términos humanos solo vienen de C15, nunca los autoriza el consumidor. Conflicto/tardío conserva historia y pide refresco. Nunca crea reserva/dinero/venta aceptada.
- **IDEMPOTENCY / RETRY / FAILURES:** D de procesamiento con generación, identidad natural de caso; CM0; MAPPING_UNRESOLVED/PARTY_UNRESOLVED/TOTAL_MISMATCH/STALE_OBSERVATION producen BLOCKED o revisión, no pérdida del receipt.
- **EVENTS / AUDIT:** ExternalOrderObserved/ProposalReadinessChanged; referencia de origen y motivos; aceptación humana solo C14.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; nueva selección reconciliada conserva antigua; efecto comercial requiere C14/C15.

<a id="c05"></a>
### C05 — Planificar objetivo publicable

- **OWNER / PURPOSE:** coordinador de Inventory con lecturas públicas de Sales/Catalog; calcular Q y solicitar efecto del destino.
- **INPUT / READS:** conexión/destino/SKUs, política/revisión/corte, mappings, P/N/R/V, casos que forman X, B y último resultado/claim.
- **LOCKS / LOCK ORDER:** I → K → E → M → S → P → U → V → J para snapshot/plan coherente; solo raíces fuente afectadas.
- **WRITES / PRE / POST:** objetivo absoluto/revisión y job único o no-op si ya coincide; stock físicamente válido, mapeo/inputs/frescura/ventana de publicación completos para habilitar envío. Si incierto, BLOCKED con Q candidato separado.
- **IDEMPOTENCY / RETRY / FAILURES:** D o unicidad destino+revisión del objetivo; CM0; STALE_RECONCILIATION/UNKNOWN_DEMAND/MAPPING_CONFLICT/POSITIVE_PUBLICATION_NOT_VALIDATED.
- **EVENTS / AUDIT:** StockPublicationPlanned/Blocked, fuentes y motivo; no StockAdjusted por respuesta remota.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; C07 publica solo plan vigente; plan nuevo sustituye trabajo obsoleto sin editar resultado anterior.

<a id="c06"></a>
### C06 — Reclamar trabajo

- **OWNER / PURPOSE:** infraestructura técnica bajo solicitante; elegir trabajo sin confirmar negocio.
- **INPUT / READS:** principal/entidad/consumidor/epoch y tiempo DB; READY/RETRY_WAIT vencidos, configuración de lease y mandato.
- **LOCKS / LOCK ORDER:** J únicamente, claim corto SKIP LOCKED candidato; no I de negocio ni otros locks después.
- **WRITES / PRE / POST:** token/lease/attempt y CLAIMED; un claim vigente por trabajo. Un DISPATCHED con lease vencida no vuelve a READY: recuperación lo considera UNKNOWN.
- **IDEMPOTENCY / RETRY / FAILURES:** V por token/generación; contención devuelve sin trabajo, CM0 para DB; INVALID_EPOCH/LEASE_CONFIG_INVALID.
- **EVENTS / AUDIT:** seguimiento técnico WorkClaimed; no evento económico. Registro durable del intento mínimo.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; claim vencido no despachado puede recuperarse con token nuevo y reautorización, sin efecto duplicado.

<a id="c07"></a>
### C07 — Autorizar y despachar efecto externo

- **OWNER / PURPOSE:** coordinador específico del job; integración para GET Jumpseller, Inventory para stock, Documents para email, Sales para consulta CPE. Adaptador solo ejecuta payload autorizado.
- **INPUT / READS:** job/claim/epoch, intención/revisiones y payload esperado; conexión/mandato actual y todas las guardas del propietario, incluidos HOLD/aprobación/destinatario/ambigüedad o frescura/ventana stock.
- **LOCKS / LOCK ORDER:** I de efecto → K → raíces del caso → J: E/M/S/P/U/V para stock; S/C/D/N para email; S/C para consulta CPE; E/M afectados para GET Jumpseller. Se omiten raíces no usadas; no engine configurable ni locks durante la consulta.
- **WRITES / PRE / POST:** claim vigente y política completa; registrar DISPATCHED, fingerprint/clave y attempt antes de salir. Commit no afirma ejecución remota. Configuración de entorno se comprueba además justo en frontera de adaptador.
- **IDEMPOTENCY / RETRY / FAILURES:** D de intención; CM0 solo fase local antes de dispatch. Payload/permiso/revisión cambiados → BLOCKED/SUPERSEDED; timeout después de dispatch → UNKNOWN, nunca retry directo.
- **EVENTS / AUDIT:** ExternalDispatchAuthorized con propósito/actor/mandato y huella; aún no EmailDelivered ni StockSynchronized.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** una llamada fuera de transacción tras commit conocido; caída entre commit y HTTP es conservadoramente UNKNOWN salvo prueba de no envío. C08 registra; C10 resuelve, no «cancelación remota» ficticia.

<a id="c08"></a>
### C08 — Registrar resultado externo

- **OWNER / PURPOSE:** solicitante del efecto mediante consumidor autorizado; separar observación remota y estado de su intento.
- **INPUT / READS:** resultado tipado, external ID si existe, attempt token/generación, hash/fecha; job/mandato/epoch, intención y revisiones vigentes.
- **LOCKS / LOCK ORDER:** K → E/S/C/D/N según dueño → J; token identifica intento. En stock, K protege estado del destino; no editar P desde resultado.
- **WRITES / PRE / POST:** guardar evidencia del intento incluso tardía; solo intento/generación vigente puede avanzar resultado actual. Contradicción/falta de certeza → UNKNOWN y pendiente. Email confirmado asocia external ID inequívoco; no depende de orden de callback. Resultados GET de pedidos y verificación CPE quedan como evidencia con trabajo durable para C04/C33 en transacción posterior y plan propio; no invocar esos comandos completos después de tomar J ni declarar verificado un CPE por HTTP 200.
- **IDEMPOTENCY / RETRY / FAILURES:** unicidad de resultado/attempt; CM0 DB. Lease antiguo nunca sobrescribe vigente, pero su resultado no se pierde: dispara conciliación. Rechazo transitorio probado sin efecto sigue calendario; incertidumbre no.
- **EVENTS / AUDIT:** ExternalResultRecorded/ExternalOutcomeUnknown y cambio de disponibilidad/resultado documental pertinente; sin alterar venta, dinero o estado fiscal por éxito de HTTP.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; consultas de reconciliación se planifican como trabajo nuevo de lectura; jamás borrar un resultado tardío contradictorio.

<a id="c09"></a>
### C09 — Aplicar callback de email

- **OWNER / PURPOSE:** integración Resend y Documents; preservar resultado observado de intento propio.
- **INPUT / READS:** receipt firmado, svix-id/email_id/tipo/fecha, conexión y datos mínimos; vínculo external ID→intento, observaciones previas y estado derivado.
- **LOCKS / LOCK ORDER:** I de receipt → K → D → N → J; el receipt ya fue confirmado por C02.
- **WRITES / PRE / POST:** dedupe+observación+derivación de Documents atómicos. ID no asociado permanece BLOCKED pendiente de C08/reconciliación, no adivinar por destinatario/asunto ni descartar callback temprano.
- **IDEMPOTENCY / RETRY / FAILURES:** UNIQUE conexión+svix-id y hash coherente; CM0; UNKNOWN_EMAIL_ID/CONTRADICTORY_PROVIDER_RESULT. Orden parcial según [Documents](cpe-document-delivery.md), no last-arrival-wins.
- **EVENTS / AUDIT:** DocumentDeliveryObserved, sin invalidar CPE/venta ni inferir lectura del cliente.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; corregir derivación mediante nueva evidencia conciliada, sin suprimir observaciones.

<a id="c10"></a>
### C10 — Autorizar replay o resolver resultado incierto

- **OWNER / PURPOSE:** solicitante de trabajo con integración; resolver un fallo técnico sin apropiar decisión empresarial.
- **INPUT / READS:** trabajo/intención/revisión/epoch, motivo, evidencia y resolución solicitada; attempts/IDs, estado del dueño y permisos actuales.
- **LOCKS / LOCK ORDER:** I → K → D/N para email → J; otros dueños se reevalúan por su comando completo posterior, nunca se confirman desde esta ficha.
- **WRITES / PRE / POST:** registrar resolución y habilitar únicamente lectura/revaluación o retry probado sin efecto; UNKNOWN no pasa a «no enviado» por ausencia de callback. Restore antiguo requiere conciliación/epoch actual.
- **IDEMPOTENCY / RETRY / FAILURES:** D; CM0; INSUFFICIENT_RECONCILIATION/STALE_EPOCH/PERMISSION_REVOKED. Retry conserva intención; reenvío documental nuevo solo C37.
- **EVENTS / AUDIT:** ReplayAuthorized/UnknownOutcomeReviewed con evidencia/actor; no efecto económico ni bypass HOLD.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; C07 futuro ejecuta solo tras nuevas guardas. Resolver fallidamente no borra incertidumbre previa.
