# SP2 — Contrato común y matriz de comandos

Propietario: arquitectura del circuito; reglas privadas en las fichas de [alcance](../flows/first-operational-circuit.md), [negocio](../flows/sales-stock-treasury.md), [Documents](../flows/cpe-document-delivery.md) e [integraciones](../flows/jumpseller-external-work.md). Concreta la hipótesis de [transacciones](../../architecture/transactions.md), sin declarar locks/constraints implementados. El mecanismo conserva PROVISIONAL en ADR-007 hasta evidencia de intercalación y creación concurrente.

<a id="cm0"></a>
## CM0 — Herencia explícita de cada ficha

Cada ficha define NAME, OWNER/PURPOSE, INPUT/READS, LOCKS/LOCK ORDER, WRITES/PRE/POST, IDEMPOTENCY/RETRY/FAILURES, EVENTS/AUDIT y EXTERNAL I/O/REVERSAL/CORRECTION. La conjunción de esta sección y la ficha es el contrato completo; no se infieren defaults de otra operación.

Coordinadores por caso de uso nombrado, junto a sus contratos; no un mega services.py, dispatcher de reglas configurables o API pública que permita ejecutar participantes aislados. Compartir primitivas no combina las decisiones Sales, Inventory, Treasury y Documents en un nuevo propietario.

- INPUT común: contexto verificado, identidad de intención cuando D, versión de contrato, revisiones esperadas, origen/correlación y motivo para correcciones/aprobaciones. Respuesta: ID estable del resultado, revisiones, estado/código, efectos confirmados y pendientes; nunca excepción interna/PII.
- PRE común: miembro/principal y mandato vigentes, capacidad de la matriz, pertenencia de cada referencia, política requerida completa. RLS/contexto antes de leer datos empresariales; autorización vuelve a comprobarse bajo los recursos del comando.
- READS previas solo descubren IDs. Se ordena el conjunto completo, se toman locks, se releen relaciones/guardas. Cambio de conjunto → rollback y redescubrimiento, sin añadir una raíz de rango anterior bajo locks.
- WRITES/POST: un comando completo posee la transacción exterior; participantes no hacen commit. Persistir estado, hecho económico cuando lo haya, auditoría crítica y trabajo durable requerido juntos. Nada de HTTP, lectura de objetos, render PDF, SMTP o parser grande dentro de esa transacción. La respuesta exitosa viene después del commit conocido.
- EVENTS: los nombres en fichas son contratos locales versionados, no tópicos nuevos por convención. Envelope: ID, entidad, productor, tipo/versión, raíz/revisión, tiempo empresarial/registro, correlación/causación y payload mínimo. No crear consumidores Accounting/Tax en esta tranche.
- AUDIT: actor/mandato, recurso, propósito, revisiones, evidencia referenciada, antes/después pertinente y correlación. Fallo de auditoría crítica revierte aceptación. Rechazo se audita en transacción separada tras rollback exterior; DB caída → señal operativa, sin fingir persistencia.
- FAILURES comunes: AUTH_DENIED/NOT_FOUND sin revelar recursos ajenos; POLICY_UNRESOLVED; REVISION_CONFLICT; IDEMPOTENCY_CONFLICT; BUSY_RETRYABLE; INVARIANT_VIOLATION; DEPENDENCY_UNAVAILABLE; EXTERNAL_UNKNOWN. Ninguno autoriza continuar con defaults. Un error de negocio produce rollback completo del comando, excepto la evidencia de recepción/observación previa ya confirmada en su propia fase.
- RETRY local: solo deadlock, serialización abortada, timeout de lock o pérdida de conexión sin resultado confirmado; reautorizar/releer y reutilizar la misma intención. Candidato inicial: máximo 3 intentos totales por invocación, espera acotada con jitter; agotado devuelve BUSY_RETRYABLE, nunca loop oculto. Es un parámetro técnico PROVISIONAL medible, no budget QA. Resultado de commit desconocido se busca por identidad antes de ejecutar de nuevo. Guardas fallidas o revisión desactualizada no se arreglan mediante retry automático.
- REVERSAL/CORRECTION: nunca borrar un hecho confirmado; usar comando/referencia compensatoria indicado por su ficha. Retry no es corrección. Ningún error técnico confirma una decisión comercial o fiscal.

## Identidad de intención y creación

| Clase | Uso y garantía |
|---|---|
| R | Lectura materializada autorizada sin cambio empresarial; no clave de negocio adicional. Acceso sensible puede auditarse |
| V | Edición/estado con revisión esperada y valor solicitado: misma revisión aplicada y mismo cambio devuelve resultado; otra revisión/contenido en conflicto. No duplica hechos/jobs al repetir |
| D | Repetición puede duplicar efectos: unicidad durable `(entidad, operación, clave)` y fingerprint de inputs normalizados + versión de contrato. Clave no vacía; resultado se conserva/reautoriza antes de devolverlo. Mandato/conexión restringe quién puede consultar esa intención |

Una clave nueva tampoco evade unicidades naturales: pedido por conexión, referencia bancaria identificada, fila de apertura/import, consumo de reserva, primera entrega CPE. La deduplicación D se confirma junto al efecto local. Para filas aún inexistentes: INSERT protegido por UNIQUE o creación bajo raíz existente que todas las operaciones comparten; la colisión relee resultado/pertenencia, no captura IntegrityError para continuar a medias. No SELECT FOR UPDATE de una inexistencia como protección. Las FKs compuestas/pertenencia, índices y traducción ORM se demostrarán posteriormente [S28](../../research/technical-sources.md).

Retención: identidad de efecto confirmado permanece al menos mientras su hecho y la posibilidad de replay/restore; purgar payload/PII no elimina la protección (conservar identidad mínima/tombstone si procede). HP5 fija plazos. Sin política aprobada no hay purga de esos registros. Tras rechazo sin commit no existe efecto: la misma solicitud idéntica puede revalidarse cuando se resuelva el bloqueo; para cambiar inputs se exige intención nueva. Intención en curso devuelve pendiente/BUSY, no otro ejecutor concurrente.

## Recursos reales y orden local candidato

Las deep specs M01–M09 añaden recursos y precisiones mediante [extensiones canónicas](economic-facts.md#recursos-adicionales-y-orden). Cualquier comando SP2 que confirme movimiento físico o coste toma también W55 antes de P60; W protege valoración, P protege cantidades/reservas. Los comandos de mera reserva/lectura de disponibilidad no toman W salvo que consuman valoración. La tabla SP2 enumera su ámbito original y se lee con esta ampliación, no como permiso para omitirla.

Orden ascendente; dentro de clase, identidad canónica `(entidad, tipo de raíz, ID estable)` o clave natural normalizada, nunca orden recibido del cliente. Bloqueo exclusivo para recursos que limitan sumas/transiciones; lectura protegida de maestros puede usar SHARE si no hay upgrade, con evidencia de compatibilidad. En esta matriz «lock» no implica bloqueo en cada SELECT informativo.

| Rango / símbolo | Recurso que existe en esta spec | Creación y exclusión |
|---|---|---|
| 0 I | Registro de intención D / identidades naturales del comando | Adquirir todas las claves ordenadas antes de raíces; UNIQUE serializa creación. No FKs a raíces no bloqueadas en esta primera fase |
| 5 A | Entidad/membresía/concesión administrada por C00 | Alta por identidad única; acceso ordinario sigue semántica de revocación fundacional, no mutex universal de usuario |
| 10 K | Conexión/mandato, revisión de reconciliación y publicación del destino | Ya creada por C01; corta exclusión por conexión en ingestión, mapping y planificación/registro de stock. No se mantiene durante HTTP |
| 15 B | Lote de importación y revisión de preview | Creación única por intención; C25 bloquea lote antes de maestros/stock |
| 20 E | Caso de pedido externo en Sales, por conexión+ID | Creación bajo K y UNIQUE; serializa observación/aceptación/cancelación para ese pedido |
| 25 M | Party, SKU y correspondencias de maestros | Identidad externa bajo K; SKU/código UNIQUE. No cambiar maestros dentro de aceptación: resolverlos antes |
| 30 S | Venta/entrega/retorno comercial bajo su raíz Sales | Venta nueva bajo E + UNIQUE por pedido; hijos protegidos por raíz existente |
| 40 T | Objetivo de liquidación de Treasury | UNIQUE dueño+obligación+moneda; creación participante bajo S. Bloquear todos los objetivos afectados |
| 45 F | Cuenta financiera de Treasury | Alta por identidad empresarial única; C23 serializa cierre y cambios permitidos. Confirmaciones que exigen cuenta operativa toman esta misma raíz |
| 50 R | Cobros y correcciones vinculadas de Treasury | Cobro nuevo por intención/referencia única; bloquear originales que limitan dinero y todas sus aplicaciones relevantes |
| 60 P | Posición de stock y asignaciones de coste de Inventory | Alta de posición bajo SKU M + UNIQUE de dimensiones. Posición limita saldo y reservas |
| 61 U | Unidad serial, cuando el SKU lo exige | Alta bajo M/P + UNIQUE de identidad compatible; posesión y movimiento original explícitos |
| 62 V | Reserva de Inventory por línea/posición | Creación bajo S/P y unicidad; su remanente se cambia con la posición que limita disponibilidad |
| 70 C | Expediente/identidad CPE de Sales; documentos de proveedor pertenecen a Procurement | Identidad natural protegida en I + UNIQUE; puede preceder a aceptación Sales. Vínculo/asignación posterior bajo S/C; nunca lock de CPE inexistente |
| 80 D | Documento/artefactos/versiones y política de Documents | Nuevo archivo por intención; dossier de entrega por CPE bajo C y unicidad de vínculo. Versiones se bloquean por ID estable |
| 90 N | Intención/aprobación/HOLD de entrega documental | Primera intención bajo C/D y UNIQUE de entidad+CPE+finalidad; reenvío nuevo bajo mismo dossier. No nueva tabla «familia» obligatoria |
| 100 J | Inbox/job/attempt técnico que se procesa o confirma | Claim corto solo sobre J; liberar antes de abrir transacción empresarial, que vuelve a tomar J al final |

Claim J es una fase aislada que no confirma negocio ni toma después recursos de rango menor. FOR UPDATE SKIP LOCKED es candidato para cola, nunca para omitir stock/cobros ocupados; ofrece una vista incompleta [S28](../../research/technical-sources.md). El lease no es fence remoto. Publicación/email reautorizan en C07 y registran resultado en otra transacción C08.

El plan incluye locks implícitos de FK/UNIQUE y orden de INSERT/UPDATE, no solo llamadas explícitas. Si el ORM/constraint exige otro recurso o cambia este orden, se actualiza la matriz y su evidencia antes de aceptar el comando. Triggers/servicios no pueden tomar locks empresariales ocultos. No exclusión global de todas las ventas de una entidad.

## Catálogo común

Todas las filas heredan I si D; se listan los demás recursos potenciales en orden. La ficha concreta cuándo se omiten recursos no afectados. `J al final` solo si el comando consume/crea seguimiento durable; nuevas filas de eventos/auditoría no introducen una lectura empresarial inversa.

| Comando / fuente | Capacidad de actuación | Recursos competidos después de I |
|---|---|---|
| [C00](../flows/first-operational-circuit.md#c00) Acceso | organization.manage o access.manage según objeto | A |
| [C01](../flows/jumpseller-external-work.md#c01) Conexión | integration.manage_connection | K |
| [C02](../flows/jumpseller-external-work.md#c02) Recibir webhook | principal autenticado integration.receive de conexión | K, J |
| [C03](../flows/jumpseller-external-work.md#c03) Reconciliar | integration.reconcile o mandato equivalente | K, E, M, J; HTTP en fase separada |
| [C04](../flows/jumpseller-external-work.md#c04) Observar pedido | integration.process, limitado a observaciones | K, E, M, J |
| [C05](../flows/jumpseller-external-work.md#c05) Planificar stock | inventory.view + integration.reconcile o mandato de publicación | K, E, M, S, P, U, V, J |
| [C06](../flows/jumpseller-external-work.md#c06) Claim | mandato de consumidor/entidad | J únicamente |
| [C07](../flows/jumpseller-external-work.md#c07) Autorizar/despachar efecto | mandato específico: publicar stock / documents.send / consultar | K, E, M, S, P, U, V, C, D, N, J según efecto |
| [C08](../flows/jumpseller-external-work.md#c08) Registrar resultado | mismo mandato y attempt token | K, E, S, C, D, N, J según efecto |
| [C09](../flows/jumpseller-external-work.md#c09) Observación email | integration.process limitado a conexión Resend | K, D, N, J |
| [C10](../flows/jumpseller-external-work.md#c10) Replay/resolución | integration.replay + capacidad del efecto si se solicita nuevamente | K, D, N, J; efecto posterior por su comando |
| [C11](../flows/first-operational-circuit.md#c11) Party | parties.manage | K, M |
| [C12](../flows/first-operational-circuit.md#c12) Catalog/mapping | catalog.manage / catalog.map según operación | K, M, J |
| [C13](../flows/sales-stock-treasury.md#c13) Apertura/ajuste | inventory.opening / inventory.adjust | K, M, P, U, V, J |
| [C14](../flows/sales-stock-treasury.md#c14) Aceptar pedido | sales.accept_external_order | K, E, M, S, T, P, U, V, J |
| [C15](../flows/sales-stock-treasury.md#c15) Revisar/corregir/cancelar | sales.correct; treasury.apply si hay des-aplicación | K, E, M, S, T, R, P, U, V, C, J |
| [C16](../flows/sales-stock-treasury.md#c16) Proponer cobro | treasury.propose_receipt | F, R |
| [C17](../flows/sales-stock-treasury.md#c17) Confirmar cobro | treasury.confirm_receipt | F, R, D si evidencia de archivo |
| [C18](../flows/sales-stock-treasury.md#c18) Aplicar/des-aplicar | treasury.apply | S, T, R |
| [C19](../flows/sales-stock-treasury.md#c19) Preparar entrega | sales.prepare_delivery + inventory.prepare | K, E, S, T, R, P, U, V |
| [C20](../flows/sales-stock-treasury.md#c20) Confirmar entrega | sales.confirm_delivery + inventory.confirm_delivery | K, E, S, T, R, P, U, V, C, J |
| [C21](../flows/sales-stock-treasury.md#c21) Retorno físico | sales.accept_return + inventory.receive_return; CORRECT_RETURN añade sales.correct + inventory.adjust | K, S, P, U, V, J |
| [C22](../flows/sales-stock-treasury.md#c22) Refund/corrección de cobro | treasury.refund / treasury.correct + treasury.apply cuando proceda | S, T, F, R, D si evidencia |
| [C23](../flows/sales-stock-treasury.md#c23) Cuenta financiera | treasury.manage_account | F, D si evidencia |
| [C24](../flows/first-operational-circuit.md#c24) Preview import | imports.prepare + lectura de dueños | B |
| [C25](../flows/first-operational-circuit.md#c25) Confirmar import | imports.confirm + capacidad de cada participante | K, B, M, P, U, V, J |
| [C26](../flows/first-operational-circuit.md#c26) Reporte | reports.view/snapshot + permisos de fuentes | D, J; dataset fuera de locks económicos |
| [C30](../flows/cpe-document-delivery.md#c30) Identidad CPE | sales.register_cpe / sales.correct_cpe | E si caso previo, S si venta, C |
| [C31](../flows/cpe-document-delivery.md#c31) Adquirir artefacto | documents.upload | D, J |
| [C32](../flows/cpe-document-delivery.md#c32) Disponibilidad | documents.verify_artifact o mandato de análisis | D, J |
| [C33](../flows/cpe-document-delivery.md#c33) Vincular/verificar CPE | sales.verify_cpe + documents.view; sales.correct_cpe además para retractar/corregir | S, C, D, J |
| [C34](../flows/cpe-document-delivery.md#c34) Preparar original / dispatch manual | documents.prepare_delivery; documents.send además si solicita dispatch MANUAL | S, C, D, N, J |
| [C35](../flows/cpe-document-delivery.md#c35) Aprobar | documents.approve_delivery | S, C, D, N, J |
| [C36](../flows/cpe-document-delivery.md#c36) Política/HOLD | documents.manage_policy / documents.hold / documents.release_hold | D, N, J |
| [C37](../flows/cpe-document-delivery.md#c37) Reenvío | documents.resend; documents.send además para dispatch MANUAL | S, C, D, N, J |
| [C38](../flows/cpe-document-delivery.md#c38) Preview/descarga | documents.view y permiso del hecho vinculado | D en fase corta; no lock durante bytes |
| [C39](../flows/cpe-document-delivery.md#c39) Cambiar insumos | documents.prepare_delivery | S, C, D, N, J si reevaluación |
| [C40](../flows/cpe-document-delivery.md#c40) Registro de entrega externa — delta propuesto | documents.record_external_delivery | S/C cuando CPE, D/N y J si invalida; ningún envío |

## Intercalaciones que deberán demostrar compatibilidad

| Competidores | Exclusión / observación que decide | Criterio futuro |
|---|---|---|
| C02/C04/C14 duplicados de pedido | K/E + unicidad de identidad externa | Una venta/reserva/objetivo; inbox no se confunde con venta |
| C14/C14 por último stock | P/U y remanente después de locks | Solo uno acepta; el otro STOCK_INSUFFICIENT |
| C15 contra C14/C20 | E/S/T/P/V | Cancelar no deja reserva huérfana ni borra despacho; entrega no ignora cancelación confirmada |
| C02/C04 contra C05/C07 stock | K y generación de reconciliación, E/S/P/V | Entrada nueva invalida plan; HTTP ya en curso se reconcilia, no fence remoto ficticio |
| C18/C22 y dos objetivos/cobro | todos S/T/R afectados | No gastar el mismo cobro dos veces; redescubrir aplicaciones nuevas antes de refund |
| C20 contra C18/C22 | S/T/R comunes | Cobertura se verifica vigente; refund posterior deja déficit visible y bloquea nueva entrega |
| C33/C39 contra C35/C07 | S/C/D/N y fingerprint aprobado | No despacho con CPE/recipient/artifact cambiado |
| C34/C34 y C37 | C/D/N + UNIQUE primera finalidad | Dos claves/doble click no crean dos originales |
| C40 contra C34/C35/C07 | C/D/N y lectura de historia/fingerprint | Registro externo anterior bloquea nueva primera entrega; dispatch ya autorizado deja carrera/duplicidad visible, no callback inventado |
| C06/C07/C08 tras timeout/lease | J + token/generación y regla de ambigüedad | Lease vencido no vuelve a enviar ni sobrescribe intento actual |
| C09 tardío contra C08 | K/D/N/J | Observaciones preservadas, sin regresión ciega de estado ni dinero/CPE alterados |
| Restore contra cualquier job antiguo | entorno/epoch de recuperación y permisos | Cero efectos externos hasta reconciliación y reactivación autorizadas |

Esto es análisis estático del diseño, no evidencia de DB. Las [familias de aceptación](../acceptance/operational-scenarios.md) y [perfiles](../acceptance/validation-profiles.md) determinan las pruebas posteriores y el gate habilitante de RLS.
