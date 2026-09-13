# Integraciones, eventos y trabajo durable

Contrato de [ADR-008](../decisions/adr-008-integrations.md). No hay integraciones ni workers implementados.

La concreción del primer circuito vive en [integraciones SP2](../specs/flows/jumpseller-external-work.md) y [CPE/Documents](../specs/flows/cpe-document-delivery.md): estados, comandos, permisos y escenarios se mantienen allí, sin promover a validados los mecanismos del ADR.

## Frontera externa

Los adaptadores viven fuera de Sales, Treasury y Procurement. Traducen HTTP/archivos del proveedor a valores conocidos; no deciden deuda, stock o tratamientos fiscales. La composición conecta adaptadores concretos con puertos explícitos; no registro global reemplazable durante una request.

| Integración | Primer uso conceptual | Condición de activación |
|---|---|---|
| SUNAT | Adquirir/importar, vincular y verificar CPE emitidos fuera de CasPro | Solo capacidades oficiales comprobadas; CasPro no emite, presenta ni envía CPE a SUNAT, tampoco desde un botón manual |
| Jumpseller | Primer canal real inicial: importar pedidos y publicar stock calculado por CasPro | Cuenta/permisos, correspondencias, inbox, reconciliación y política de disponibilidad validados antes de operar |
| Bancos | Importar extractos y registrar evidencia de movimientos | Conciliar no ordena transferir; pago externo automático fuera de alcance |
| Email / Resend opcional | Adaptador inicial de entrega documental bajo responsabilidad de Documents | AUTO_WITH_APPROVAL cuando habilitado; puerto email sin SDK en dominio. [Registro externo C40](../specs/flows/cpe-document-delivery.md#c40) funciona sin Resend, con evidencia y sin callback ficticio |
| WhatsApp Business futuro | DEFERRED / TRIGGERED INTEGRATION; sin conexión ni módulo | D03/M10: necesidad y autorización concretas, research vigente de capacidad/política y C11 antes de cualquier efecto |
| Object storage | Archivo privado de Documents, previews y snapshots | Bytes separados de metadata PostgreSQL; proveedor pendiente, acceso autorizado y recuperación separada |

Cada conexión declara proveedor/cuenta, entidad local vinculada, secreto externo a Git, URL permitida, timeouts de conexión/lectura, tamaño máximo, política de retry, identidad externa y traducción de errores. No aceptar una URL arbitraria recibida en webhook ni elegir entidad a partir del cuerpo sin verificar su conexión.

Webhooks: autenticar según contrato oficial, verificar antigüedad/replay cuando el proveedor lo permita y confirmar inbox durable antes del acuse de éxito. Cada integración receptora responde por su inbox técnico en PostgreSQL: conexión/entidad, procedencia, identidad o fingerprint, payload acotado y estado de procesamiento; el payload no es verdad empresarial. Procesar después mediante comandos completos y confirmar deduplicación local junto al efecto. Falta de versión/orden fiable obliga a reconciliar; recibir repetidamente no vuelve a confirmar negocio.

## Jumpseller: pedido observado y stock autoritativo

Sales recibe pedidos, líneas y estados comerciales útiles; Parties resuelve clientes hacia la Party común y Sales conserva direcciones/datos usados como snapshot. El ID de cliente del canal no crea otro Customer ni autoriza fusionar por email. Producto/variante externo debe corresponder inequívocamente a SKU de Catalog. Datos ambiguos quedan pendientes; importar no autoriza despacho. Pago/refund observado conserva fuente/fecha y se concilia con Treasury, sin crear o revertir dinero por el estado del canal.

Inventory es autoridad del stock interno y calcula available-to-sell por destino, descontando compromisos y cantidades no vendibles sin contarlos dos veces. El resultado no es negativo ni excede existencia elegible neta; reservar reduce disponibilidad, despachar consume reserva y existencia coordinadamente. Recepciones, anulaciones y devoluciones actualizan su hecho dueño antes de recalcular. [SP2](../specs/flows/sales-stock-treasury.md) concreta aceptación/reserva/liberación y fórmula para un destino inicial; posiciones elegibles, buffer y activación real conservan condiciones de política/validación. No se publica stock ilimitado como fallback.

Publicar un objetivo de stock versionado, no repetir deltas. Catalog posee la correspondencia producto/variante externo → SKU; Inventory posee objetivo publicable, destino y revisión, y la integración conserva intento/resultado técnico bajo su responsabilidad. Descarta trabajos obsoletos y reconcilia objetivo, observación remota y pedidos pendientes; una respuesta tardía o un webhook eco no genera un movimiento ni dispara un bucle de republicación. El descuento automático del canal se concilia con el compromiso local, sin descontarlo otra vez al importar y luego despachar. Antes de aumentar el stock publicado se requiere frescura suficiente de pedidos/disponibilidad; si es incierta se bloquea el incremento y se expone la discrepancia. No hay atomicidad CasPro–canal: carreras, demora y prevención de sobreventa requieren validación posterior, no promesa de cero sobreventa por usar outbox.

Capacidades documentadas: API de lectura de pedidos/productos y actualización de stock por producto/variante/ubicación [S22](../research/technical-sources.md); selección de endpoint, permisos mínimos, paginación y comportamiento de la tienda deben comprobarse al especificar Jumpseller. Webhooks usan HMAC SHA-256 sobre cuerpo crudo con token de la conexión [S21](../research/technical-sources.md). La página consultada no documenta ID único de evento: no usar solo order_id para deduplicar ni considerar Triggered-At un orden total. Conservar recepciones y comparar observaciones; fingerprint ayuda a reconocer repetición, no sustituye la idempotencia del comando o la reconciliación periódica/manual de pedidos y stock, incluidos eventos perdidos.

Canal/cuenta, referencia externa, SKU vinculado y stock publicable son los conceptos neutrales mínimos. Solo se especificará Jumpseller; sin modelo universal de estados ecommerce, conectores vacíos ni motor de sincronización configurable. Discrepancia → revisión/reconciliación; cualquier ajuste local exige motivo, capacidad y auditoría del dueño, nunca edición directa del saldo.

## Contenido Marketing — ampliación futura separada

[Marketing Content](../specs/flows/marketing-content-media-library.md#frontera-de-publicación-automática-futura) confirma biblioteca/planificación/registro **MANUAL_EXTERNAL** sin proveedor. Marketing posee plan/observación e intención empresarial futura; Integrations transporte/attempt, Documents evidencia. No reutilizar intención de entrega CPE como hecho de publicación social. Instagram/Facebook/Jumpseller son destinos de contenido; automatización requiere D03, futuro contrato/WO y C11/B12 por superficie. El alcance “solo Jumpseller” anterior sigue referido a pedido/stock; no autoriza automatizar contenido.

[Fuentes actuales](../research/marketing-content-providers.md) distinguen login/cuenta/superficie Meta, container/publicación, media de producto/página Jumpseller y banners de tema. ACK/programación no son publicación; UNKNOWN retiene intención y concilia. Proveedor recibe únicamente derivado/copia autorizada mediante entrega separada acotada, jamás URL de preview humano ni original/bucket privado público. Cambios de formato/cuenta/límites invalidan readiness de ese adaptador; no aprobación Marketing. WhatsApp conserva su trigger.

## CPE externo: acquire → link/verify → deliver

| Paso | Responsable y límite |
|---|---|
| acquire | El operador emite por SOL u otra vía externa autorizada. Documents adquiere/importa PDF, XML u otros artefactos privados con procedencia; un adaptador solo automatiza adquisición oficialmente comprobada. Un XML reconstruido es representación generada y no satisface un requisito de original |
| link/verify | El flujo coordina Sales para CPE de venta o Procurement para proveedor y Documents para artefactos. Vincula identidad del CPE y contrapartes/importes pertinentes; captura resultado/fuente/fecha de verificación sin confundirlo con autenticidad del archivo. Ambigüedad o faltante queda pendiente; Tax interpreta cuando corresponda, sin imponer construir Tax para almacenar un archivo |
| deliver | Documents determina entregabilidad documental con insumos verificados del dueño y versiones disponibles. Solicita email por puerto/adaptador; ni Sales ni el adaptador SUNAT llaman Resend. Entregar al destinatario no emite, presenta ni valida fiscalmente el CPE |

La Consulta Integrada oficial verifica un comprobante identificado por RUC emisor, tipo, serie, número, fecha e importe; devuelve estados/observaciones. Su operación HTTP POST es una consulta semántica, no emisión. El manual consultado no documenta enumeración ni descarga de todos los CPE emitidos en SOL [S23](../research/technical-sources.md). Esa adquisición masiva **no está verificada ni se presupone disponible**; el alcance puede usar importación del operador. Credenciales, habilitación de consulta y cualquier adquisición automática quedan PENDING VALIDATION de capacidad oficial y cuenta autorizada. No se investigan ni aprueban reglas tributarias por describir esta API.

## Entrega documental y Resend

Delta del [amendment semántico aceptado](../evidence/b2b-financing-amendment.md): **DOCUMENT DELIVERY ≠ RESEND**. Documents posee intención/historia, un adaptador sustituible ejecuta transportes, y C40 registra envío externo conocido. Deshabilitar Resend no bloquea ese registro ni el expediente. Cambiar adaptador no borra entregas anteriores, HOLD, resultados inciertos ni unicidad CPE/finalidad; se revalida configuración/aprobación pertinente y capacidad del nuevo proveedor. Los detalles de Resend siguientes solo aplican a ese adaptador, no son defaults universales de email.

Documents posee política, intención y resultado de entrega; el SDK queda en el adaptador de email. Los modos se aplican al propósito documental autorizado, no a cualquier CPE recibido: un CPE de proveedor no se envía a un cliente por estar archivado.

| Modo | Efecto permitido |
|---|---|
| MANUAL | Cada envío nace de una intención explícita del operador autorizado |
| AUTO_WITH_APPROVAL | Prepara la intención automáticamente y espera aprobación explícita antes de enviar; modo operativo inicial |
| AUTO | Puede enviar sin aprobación individual solo al cumplir todas las condiciones de entregabilidad |
| DISABLED | No ejecuta envíos del propósito configurado, tampoco manuales |

HOLD es un bloqueo persistido con motivo, ortogonal al modo: suspende envío/reintento hasta liberación explícita y auditada; ni un webhook ni un cambio de modo lo levanta. Para AUTO de CPE se exige vínculo inequívoco, artefactos requeridos disponibles, destinatario válido/autorizado, ninguna entrega original previa y ausencia de HOLD. La primera entrega de cada CPE/finalidad dentro de la entidad también se protege frente a otra intención original en curso o con resultado incierto; no basta buscar estado «delivered», ni cambiar destinatario/versión habilita otra primera entrega. Registrar entregas externas conocidas; historial insuficiente exige resolución explícita antes de habilitar una primera entrega automática. MANUAL y aprobación no permiten omitir vínculo, artefactos, autorización o HOLD. Qué artefactos son requeridos por propósito queda PROVISIONAL hasta validar necesidad y capacidad; una política incompleta bloquea automatización.

La intención conserva entidad, CPE/revisión cuando aplique, propósito (primera entrega/reenvío), versiones/hashes de artefactos, destinatario usado, contenido aprobado, actor/aprobación, estado, intentos e identificador externo. Aprobar fija esos insumos; cambiarlos invalida la aprobación. El comando completo vuelve a comprobar su vigencia, permisos, modo y HOLD al autorizar el despacho; confirma intención/intento antes del I/O, sin mantener locks durante el envío. Un HOLD posterior al despacho no puede retirar un correo ya aceptado: se registra la carrera y se concilia el resultado, sin prometer cancelación remota.

Reintento = misma intención, destinatario/contenido e identidad idempotente; reenvío = nueva intención explícita, relacionada con la anterior, con sus controles y clave nueva, nunca CPE nuevo. Con resultado ambiguo no se crea automáticamente otra primera entrega. Resend ofrece adjuntos y clave idempotente con retención de 24 horas [S25](../research/technical-sources.md): el historial y protección local persisten según su política, no dependen de ese plazo. Si vence la ventana con resultado desconocido, HOLD y conciliación/resolución autorizada antes de otro envío; no retry ciego. Retención local debe cubrir intención, replays y restauración antes de habilitar automatización.

Callbacks Resend: verificar firma sobre cuerpo crudo con secreto de la conexión; deduplicar svix-id y vincular email_id al intento propio. Hay entrega al menos una vez y orden no garantizado [S24](../research/technical-sources.md). Conservar observaciones y derivar estado conforme a su semántica parcial; llegada tardía no sobrescribe ciegamente un resultado, contradicción exige conciliación. Accepted/sent/delivered/bounce son resultados del correo: fallo o bounce no invalida CPE ni venta; delivered tampoco acredita lectura o aceptación fiscal. Los controles de [entornos](../operations/delivery.md) se aplican a cualquier modo y reenvío.

## Frontera futura WhatsApp Business

Solo se preservan Party/caso comercial, identidad externa por origen/cuenta cuando exista, propósito de comunicación y referencias a documentos/evidencia con procedencia. Sales decide aceptación, Treasury dinero, Documents intención/historia; un mensaje nunca confirma esos hechos por sí solo. No módulo WhatsApp, SDK, bus, CRM conversacional ni motor omnicanal. D03 exige caso de uso, mandato/destinatarios y research **actualizado al activarlo** de API, condiciones, privacidad y controles; no se anticipan precios, plantillas o automatización. Cambio de política/API futuro invalida supuestos de ese adaptador, no redefine los dueños. Especificación/WO y autorización posteriores por alcance, sin activación en este amendment.

## Tres clases de evento

| Clase | Qué representa | Propiedad |
|---|---|---|
| Hecho de dominio/económico | Algo confirmado y necesario para consumidores o explicación empresarial | Lo produce su dueño en la misma transacción del hecho |
| Mensaje de integración | Representación para un contrato externo | Versión y datos mínimos; no es automáticamente un hecho aceptado |
| Registro outbox/job | Intención durable de entregar/procesar un trabajo | Estado operativo y política de recuperación; no nueva regla de negocio |

El evento lleva ID, entidad, tipo/versión, raíz/revisión, fecha empresarial, instante de registro, correlación/causación y datos suficientes sin PII indiscriminada. Accounting consume hechos versionados y registra el ID consumido junto con el asiento en su transacción; no conoce modelos operativos ni publica asientos desde Sales. Tax separa su interpretación. Consumir un evento no prueba que la política contable/tributaria sea correcta.

## Síncrono primero; durable cuando haya consumidor

Dinero y stock locales se resuelven dentro de una transacción corta. Consultar proveedores, enviar correos o producir reportes largos sucede fuera de esa transacción. Para un efecto que deba sobrevivir al proceso, el cambio y su intención quedan en DB antes del commit; on_commit solo puede despertar un consumidor, nunca ser el único registro del trabajo.

Jumpseller y la entrega documental ya identifican consumidores iniciales de trabajo durable. Una cola/outbox PostgreSQL y un proceso worker simple siguen como candidato PROVISIONAL, sin broker inicial: [SP2](../specs/flows/jumpseller-external-work.md) especifica registros/comandos y requiere demostrar caída/reanudación antes de aceptar su mecanismo. Contrato de referencia: claim corto con exclusión, lease/vence, token de intento, contador/fecha de próximo intento, límite/backoff, resultado y dead-letter con replay autorizado. El worker no mantiene un lock DB durante HTTP. Un resultado de lease antiguo no puede sobrescribir al intento vigente.

La entrega es al menos una vez. La unicidad del ID procesado y el efecto de DB se confirman juntos. Frente a un proveedor, una lease no evita duplicación de un efecto externo: se exige clave idempotente del proveedor o conciliación antes de reenviar. Si repetir un resultado ambiguo puede duplicar o alterar el efecto esperado, se revisa/consulta estado antes de reintentar.

No se adopta Celery, Redis, RabbitMQ, Kafka ni SQS inicialmente. Se reconsidera si volumen, scheduling, topología o operación lo justifican. Django Tasks ofrece API/plumbing; no aporta por sí solo el worker productivo [S10](../research/technical-sources.md). Su backend se evaluará al especificar esos trabajos concretos, evitando implementar un framework general de colas.

## Dónde persiste la coordinación que debe sobrevivir

| Estado necesario | Propietario y persistencia conceptual |
|---|---|
| Progreso empresarial para reanudar | En PostgreSQL, en el caso del módulo dueño: Sales o Procurement cuando exista una devolución comercial. Una intención que solo afecta Treasury permanece allí; no crea un expediente comercial artificial. Conserva sus decisiones y referencias a hechos de otros propietarios, sin copiar sus saldos ni sustituirlos por flags |
| Hecho físico, monetario o documental | En su módulo propietario. Documents persiste archivo, disponibilidad e intención/resultado de entrega documental; Sales y Procurement conservan sus respectivos expedientes CPE |
| Entrega de un hecho producido / tarea solicitada | Registro técnico durable en PostgreSQL bajo responsabilidad del productor/solicitante; contiene identidad de intención, destino, intento y resultado técnico. El backend es infraestructura reemplazable, no dueño del hecho |
| Procesamiento de un consumidor | El consumidor persiste su recepción/deduplicación junto con su efecto; por ejemplo Accounting con el asiento. Un acuse de entrega del productor no demuestra ese efecto |

Si el progreso se deriva íntegramente de hechos persistidos, se reconstruye por referencias y no se almacena otra máquina de estados. Si hay una decisión empresarial indispensable no derivable, la especificación la asigna al caso del módulo dueño antes de implementarla. Workflows ejecuta coordinación sin tablas propias de hechos ni progreso empresarial en memoria como única copia.

Tablas, campos, esquema técnico compartido o por módulo y backend exacto permanecen PROVISIONAL hasta especificar y validar los primeros casos durables; esta asignación de responsabilidad no crea un workflow engine ni un nuevo módulo. Su aceptación requiere demostrar recuperación tras commit/caída, deduplicación y ausencia de divergencia con los propietarios. Si todo cabe en una transacción local, no se introduce seguimiento durable adicional.

## Fallos que el contrato debe admitir

Commit correcto + proceso muerto antes de publicar; duplicado; mensaje fuera de orden; respuesta tardía; credencial vencida; proveedor caído; timeout con efecto externo ya ejecutado; objeto subido con metadatos no confirmados; metadatos existentes con blob ausente.

Documents tratará DB y objetos como recursos no atómicos: carga temporal/cuarentena, confirmación de disponibilidad, reconciliación de huérfanos y política de limpieza. Una descarga usa autorización actual y enlace breve o proxy autenticado; URL opaca permanente no es permiso.

REQUIRES LATER VALIDATION: esquemas/payloads reales, autenticación del proveedor, replay, leasing y caída de proceso, contratos de storage y restauración DB+blobs. No se verificó ninguna cuenta externa en esta fase.

## Frontera del amendment profesional

**Amendment aceptado por revisión independiente**, conforme a review. [FX/Tax](../specs/flows/tax-workspace-books.md) añade adquisición autorizada de observaciones por finalidad, sin API inventada ni envío SUNAT. [Firma y reclamos](../specs/flows/records-signatures-site-packs.md) usan puertos neutrales, idempotencia/epoch/resultado incierto y gate por efecto. [Kits multialmacén](../specs/flows/catalog-sites-warehouses.md) afectan disponibilidad Jumpseller y mantienen B11/C11; Resend continúa opcional/C40, WhatsApp D03. Ninguna fuente leída en research constituye conexión empresarial activada.
