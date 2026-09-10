# SP2 — Primer circuito operativo B2C

Propósito: especificación implementable de venta de mercadería existente por Jumpseller, dinero confirmado en Treasury, entrega física, CPE emitido externamente y entrega documental por Resend. Mandato: SUPERPROMPT 2, 2026-09-10. Especificar y publicar esta rama está autorizado; implementar, ejecutar WOs o activar cuentas no lo está. Estado documental de la fase: [review](../review.md). Gate 1 y el amendment conservan su cierre.

## Lectura local y autoridad

| Necesidad | Fuente canónica de esta slice |
|---|---|
| Alcance, decisiones humanas, maestros, capacidades y operación | Este archivo |
| Aceptación comercial, reservas, dinero, entrega y correcciones | [Sales/Inventory/Treasury](sales-stock-treasury.md) |
| CPE, archivo, aprobación y entrega documental | [CPE/Documents](cpe-document-delivery.md) |
| Jumpseller, Resend, inbox/jobs, reconciliación y fallos externos | [Integraciones](integrations.md) |
| Orden común, atomicidad y catálogo de comandos | [Matriz](command-matrix.md) |
| Casos futuros verificables | [Aceptación](acceptance.md) |
| Primeros encargos y evidencia requerida | [Work Orders](work-orders.md) |

La spec concreta la fundación; no sustituye [invariantes](../domain/invariants.md), [ownership](../architecture/boundaries.md), [acceso](../architecture/tenancy-access.md) ni [QA](../quality/strategy.md). Las fichas de comandos viven junto a su dueño y heredan únicamente CM0 de la matriz. No hay tablas de estados duplicadas en ADRs o WOs. Los IDs de comando identifican contratos, no clases o tablas obligatorias.

## Resultado y límites

Un pedido observado puede quedar pendiente o rechazado sin crear venta, reserva ni dinero. Aceptarlo explícitamente confirma snapshots, compromiso, reserva completa y objetivo de liquidación en una sola transacción. Treasury registra evidencia de un cobro real y sus aplicaciones. La entrega consume reserva y stock bajo cobertura vigente. Documents vincula artefactos al CPE de Sales, congela una intención aprobada y ejecuta email fuera de la transacción. Reconciliación y correcciones conservan historia.

El orden de esos pasos es causal, no una regla fiscal: el CPE puede adquirirse antes del despacho. La condición CPE previa a entrega se decide en HP4; no se presume legal emitir después de entregar. El circuito soporta parcialidades físicas y financieras; no incluye crédito automático, contracargos bancarios automatizados, compras, garantías completas, multiempresa consolidada ni otro canal. Procurement es el siguiente circuito, sin paquetes o contratos ficticios en esta tranche.

Supuestos visibles: una conexión Jumpseller activa de TILMUX y un destino publicable inicial; las posiciones internas pueden ser varias. Son límites de activación de esta slice, no unicidades globales de CasPro. IDs externos siempre incluyen conexión/entidad. Mercadería de unidad discreta para publicación inicial; una SKU fraccionaria se conserva en Catalog pero queda BLOCKING para este canal hasta contrato de conversión validado. No se inventan existencias, costes, RUC, cuentas o operaciones reales.

## Decisiones de diseño cerradas para especificar

- Aceptación manual explícita, íntegra por pedido; observar/validar no equivale a aceptar. No vencimiento automático de reservas en esta slice: cancelación/liberación explícita y pendientes visibles. Automatizar esas decisiones sería otro alcance.
- Una venta interna por identidad de pedido externo, incluso tras cancelación; una actualización no crea otra venta. No ampliación automática de una venta aceptada por datos del canal.
- Party común y referencias neutrales bajo sus propietarios; snapshots de Sales inmutables tras aceptación salvo corrección versionada explícita.
- PostgreSQL y worker simple son suficientes como diseño inicial por volumen/topología del circuito, sin broker. Representación, límites y garantías ejecutables siguen en ADR-008 como PROVISIONAL.
- Stock absoluto versionado, dinero explícito y primera entrega documental única; la ambigüedad externa se conserva y no se convierte en éxito ni en permiso para repetir.

## Cinco decisiones humanas pendientes

Estas son las únicas elevaciones nuevas del circuito; precisan H1 y se relacionan con H2–H5 de [review](../review.md), sin sustituirlos. No requieren respuesta para terminar esta spec. Una política desconocida produce POLICY_UNRESOLVED en la operación indicada; un implementador puede usar una política sintética explícita para aceptación futura, nunca presentarla como aprobación productiva.

| ID | Decisión / recomendación | Qué queda bloqueado hasta resolverla |
|---|---|---|
| HP1 | Ratificar cobertura inicial al contado y desglose comercial. Recomendación: cobrar íntegramente el objetivo vigente antes de cualquier despacho, aunque el despacho sea parcial; precios discrepantes exigen importe/desglose autorizado, sin tolerancia silenciosa | Confirmar entrega y aceptar un desglose no validado. La spec no permite que el implementador elija prorrateo de envío/descuentos o cambie tolerancias |
| HP2 | Cuentas operativas y evidencia suficiente de cobro/refund. Recomendación: cuenta identificada y comprobación del operador sobre referencia bancaria/pasarela; una etiqueta PAID aislada no basta | Confirmar dinero real sin fuente/fecha/importe/moneda y política de evidencia. No inventar cuenta de tránsito, saldo o liquidación de pasarela |
| HP3 | Apertura/coste, posiciones elegibles/buffer publicable y elegibilidad de devoluciones. Recomendación: apertura autorizada con cantidades y coste atribuible identificado; coste desconocido visible; devolución física entra no vendible hasta revisión | Apertura/ajuste real sin sustento, publicación sin política de disponibilidad, reposición vendible o refund sin política autorizada; no imponer FIFO/promedio ni valoración fiscal |
| HP4 | Política CPE del circuito: momento respecto del despacho, identidad exigible al comprador, verificación y artefactos requeridos por finalidad. Recomendación: vínculo inequívoco y evidencia oficial revisada; conservar PDF y XML original disponible, sin reconstrucción sustitutiva | Despacho si su condición fiscal es desconocida y entrega documental con política incompleta. Exigir ambos artefactos o admitir PDF sin XML requiere decisión explícita; no es una norma inferida |
| HP5 | Retención/recuperación y excepción de segregación para operación inicial, conforme H2–H4. Recomendación: retención diferenciada, recuperación DB+objetos y autoaprobación visible, nunca dos personas ficticias | Purga de evidencia de negocio, activación productiva sin recuperación y autoaprobación sin excepción registrada. Presupuesto/región y RPO/RTO existentes siguen pendientes |

Las políticas tienen propietario, versión, vigencia y actor de aprobación: HP1 en Sales; HP2 en Treasury; HP3 en Inventory/Sales según decisión; HP4 en Sales y política de entrega en Documents; HP5 en cada dueño y operación. No tabla global de parámetros arbitrarios. Una política técnica candidata no es un FACT ni TAX_RULE.

## Workspace mínimo y capacidades

Identity conserva usuario/principal, sesión y recuperación; Organization, entidad/directorio mínimo y establecimientos; Access, membresía, capacidades y mandato de sistema. Alta/selección/revocación deben distinguir el directorio global mínimo del perfil empresarial. La elección de entidad solo lista membresías del actor; perfil requiere contexto autorizado. Revocar bloquea nuevas actuaciones, conforme al contrato fundacional; el worker reautoriza al despachar. Agrupación Workspace y RLS no se promueven a ACCEPTED aquí.

Cada lectura usa `<owner>.view` para recursos del dueño, con entidad y alcance; `documents.view` es adicional para bytes/preview. Búsqueda no amplía esos permisos. Administrar conexión no permite confirmar ventas/dinero ni ver documentos. Las capacidades de mutación de la matriz no implican automáticamente lectura general o exportación. No is_staff ni Django admin como bypass económico.

| Función | Capacidad mínima de comando |
|---|---|
| Entidades / acceso | organization.manage / access.manage, según actuación C00; altas iniciales por bootstrap administrativo explícito y auditable |
| Maestros | parties.manage; catalog.manage para datos; catalog.map para correspondencias |
| Inventario | inventory.opening; inventory.adjust; inventory.prepare; inventory.confirm_delivery; inventory.receive_return |
| Sales | sales.accept_external_order; sales.correct; sales.prepare_delivery; sales.confirm_delivery; sales.accept_return |
| Treasury | treasury.manage_account; treasury.propose_receipt; treasury.confirm_receipt; treasury.apply; treasury.correct; treasury.refund |
| Documents | documents.upload; documents.verify_artifact; documents.prepare_delivery; documents.approve_delivery; documents.send; documents.resend; documents.manage_policy; documents.hold; documents.release_hold |
| CPE de venta | sales.register_cpe; sales.verify_cpe; sales.correct_cpe |
| Integraciones | integration.manage_connection; integration.reconcile; integration.replay. Consumidores: integration.receive/process; principal limitado a su conexión y comandos mandatados |
| Operación | imports.prepare/confirm, además de capacidades de los dueños; reports.view/snapshot, además de permisos sobre sus fuentes |

Comandos compuestos exigen todas las capacidades indicadas en la matriz. Un worker ejecuta con principal de sistema y mandato específico; una aprobación humana no le concede los permisos de su autor para siempre. Preparador=aprobador exige excepción de segregación vigente y queda expuesto en intención/auditoría; en su ausencia, SEGREGATION_REQUIRED. ADMIN técnico no es rol operativo. MFA/recuperación para exposición pública conservan su validación habilitante.

## Parties y snapshots mínimos

Party: ID público/entidad, tipo PERSON/ORGANIZATION/UNRESOLVED, nombre declarado, identidades documentarias tipadas con fuente/vigencia, contactos email/teléfono y direcciones versionados; estados ACTIVE/RETIRED. No se exige RUC a toda persona ni se deduce validez de identidad de un formato. UNRESOLVED se usa solo en captura, no en aceptación final.

Resolución: referencia externa ya LINKED y compatible → Party conocida; sin vínculo → candidatos visibles para un operador, nunca fusión por email/nombre. Una identidad documentaria coincidente es evidencia para revisión, no fusión interempresa. El operador elige una Party existente o crea una con identidad declarada y procedencia; ambiguo queda pendiente. Dos creaciones contra la misma referencia compiten por su unicidad en Parties. Invitado sin ID de cliente: referencia de contraparte restringida a ese pedido/conexión, sin inventar cliente global del canal. Un contacto ausente no se rellena con el del operador.

Sales acepta snapshots separados: identidad utilizada; identidad fiscal cuando corresponde; contacto/billing email utilizado; dirección de entrega; referencia a Party y revisión. Email ausente permite aceptar si los demás requisitos están resueltos y la política comercial no lo exige, pero bloquea email documental. Dirección de envío incompleta bloquea aceptación para envío físico; retiro requiere modalidad/lugar explícitos y no inventa dirección postal. Cambiar Party no altera snapshots; corregirlos exige C15 y puede invalidar aprobación documental.

## Catalog y correspondencias

Product agrupa SKU; SKU tiene ID público, código local único por entidad, unidad/paso, estado DRAFT/ACTIVE/RETIRED y precio comercial versionado/moneda/base de componentes. No campos por proveedor en Product/SKU. Product no posee stock, ni el precio vigente reescribe ventas anteriores. Requerimiento de serial se declara por SKU antes de apertura.

Correspondencia: conexión/entidad + external product + external variant (ausencia explícita cuando sea producto simple) → SKU y revisión. Estados LINKED, UNLINKED, AMBIGUOUS y MISSING_REMOTE. LINKED requiere existencia remota observada, unidad compatible y un solo destino SKU; un ID externo no se reasigna silenciosamente. No enlazar por nombre o por texto sku recibido sin correspondencia aprobada. MISSING_REMOTE suspende nueva publicación/aceptación; no borra movimientos o ventas. Varios anuncios hacia una SKU quedan bloqueados en la primera activación hasta demostrar asignación conjunta que no multiplique disponibilidad.

## Operación transversal sin nuevos propietarios

La bandeja es lectura/proyección, no tabla de estados de negocio. Cada ítem: entidad, tipo, referencia pública al dueño, origen, antigüedad desde condición fuente, severidad, causa/código, acción permitida y capacidad/responsable. ID derivado de dueño+recurso+condición; resolver invoca un comando de esta spec. Al desaparecer la condición se retira de pendientes; su explicación permanece en hechos/auditoría del dueño, sin UPDATE de una tarea para simular resolución.

| Condición | Severidad y acción |
|---|---|
| Mapping/Party/importe/dirección no resueltos | BLOCKING aceptación; C11/C12 o corrección comercial C15; C04 reevalúa y después C14 decide |
| Stock insuficiente o sync divergente/atrasado | BLOCKING aceptación sin stock o aumento publicable; C03/C05/C13 según causa; otras ventas válidas no se bloquean globalmente |
| Cobro propuesto/parcial, cobertura insuficiente | WARNING de cobranza; BLOCKING confirmar entrega según HP1; C17/C18 |
| CPE pendiente/ambiguo, PDF/XML requerido ausente | BLOCKING la actuación dependiente; C30–C33; no bloquea registrar hechos físicos/monetarios ya ocurridos |
| Espera aprobación / HOLD | BLOCKING email; C35/C36, sin ocultar motivo o excepción de segregación |
| Bounced/failed, conexión vencida, job dead-letter | WARNING para ERP, BLOCKING ese envío/trabajo; C09/C10/C36/C37 según resultado |

Búsqueda global: PostgreSQL primero, consultas públicas paginadas por número de venta/CPE, SKU, Party y referencia externa con conexión. Contexto obligatorio; permisos filtran filas, snippets, sugerencias y conteos antes de responder. Cache incluye entidad/actor o huella de capacidades vigente. Abrir reautoriza; sin permiso no confirma existencia de otro recurso. No Elasticsearch, índice multientidad indiscriminado ni escaneo sin límites.

Importación inicial: CSV UTF-8 o XLSX sin macros; UPLOADED → PARSED → VALIDATED → PREVIEW_READY → CONFIRMED/BLOCKED. Un archivo/tipo/lote pertenece a un dueño (Parties, Catalog o Inventory), con hash, versión de parser/contrato, entidad, actor, revisiones base y filas con clave de procedencia. Errores clasificados NEW/CHANGE/VALID/INVALID/DUPLICATE/CONFLICT. No ejecutar fórmulas ni enlaces externos; las celdas con fórmula en campos requeridos son inválidas, no confiar en su valor cacheado. Exportaciones neutralizan spreadsheet formula injection.

C24/C25 confirman un lote acotado completo o nada; archivos grandes se dividen en lotes identificados con resultado por lote, nunca falsa atomicidad de todo el archivo. Límite de lote debe fijarse/validarse en su WO antes de ejecución; sin límite no se activa import. Reconfirmar un lote devuelve resultado anterior; usar otro ID no duplica una misma fila de apertura gracias a su identidad de origen. Preview caduca por cambio de insumos/permisos/política relevante, no por un plazo arbitrario.

Margen bruto operativo: `M = ingresos comerciales de mercadería netos de descuentos y ajustes/devoluciones atribuibles − coste de las unidades incluidas`, misma moneda y corte. La definición de ingresos declara si excluye los impuestos explícitamente identificados; si no puede separar impuestos con evidencia, no etiqueta el valor como margen neto de impuestos. Envío/cargos ajenos a mercadería se muestran aparte, salvo política HP1 que los asigne explícitamente. Devolución física por sí sola no reduce ingreso: se muestra mercancía retornada pendiente de ajuste comercial. Coste de Inventory desconocido produce UNKNOWN/INCOMPLETE, no cero. Preservar cantidades, importes/componentes, coste total de origen, asignaciones/repartos y correcciones permite explicación futura; no asientos, utilidad neta ni política fiscal.

## Fichas locales (heredan CM0)

<a id="c00"></a>
### C00 — Administrar entidad o acceso

- **OWNER / PURPOSE:** Organization o Access según operación tipada; alta/suspensión de entidad, concesión/revocación de membresía/capacidad. Identity permanece responsable de autenticación.
- **INPUT / READS:** contexto administrativo, actuación, identidad/entidad/membresía, revisión y motivo; directorio mínimo y permisos administrativos vigentes.
- **LOCKS / LOCK ORDER:** I → A; creación por identidad única, nunca lock de fila inexistente. Actualizar perfil empresarial exige contexto de esa entidad.
- **WRITES / PRE / POST:** directorio/perfil o membresía con revisión; autoridad explícita y propiedad; revocación impide nuevas actuaciones y mandatos posteriores, sin prometer cancelar la transacción corta ya autorizada.
- **IDEMPOTENCY / RETRY / FAILURES:** D para alta/concesión; V para cambio de estado con revisión. CM0; AUTH_DENIED/REVISION_CONFLICT, rollback completo.
- **EVENTS / AUDIT:** EntityChanged o AccessChanged, rastro administrativo sin credenciales; sin hecho económico ni jobs genéricos.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; nueva concesión/estado autorizado conserva revocación anterior. Bootstrap inicial requiere mandato administrativo independiente del rol runtime.

<a id="c11"></a>
### C11 — Resolver o mantener Party

- **OWNER / PURPOSE:** Parties; crear/actualizar identidad declarada y resolver referencia externa sin duplicarla.
- **INPUT / READS:** contexto, datos tipados, revisión, referencia de conexión opcional, Party elegida y motivo; candidatos/identidad y vínculo actuales.
- **LOCKS / LOCK ORDER:** I → K si hay vínculo → M; unicidad de referencia externa; alta sin vínculo usa ID de intención y restricciones documentarias aplicables, nunca fusión automática.
- **WRITES / PRE / POST:** Party/contactos/versiones y mapping de contraparte; same entity, tipo conocido; un vínculo queda único y el pedido histórico conserva su snapshot.
- **IDEMPOTENCY / RETRY / FAILURES:** D para creación/resolución, V para edición; CM0; AMBIGUOUS_PARTY/REFERENCE_CONFLICT/REVISION_CONFLICT.
- **EVENTS / AUDIT:** PartyResolved/PartyChanged, actor/fuente/campos relevantes sin PII completa en logs.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; retirar/corregir referencia con historia. No merge masivo ni CRM.

<a id="c12"></a>
### C12 — Mantener Catalog o mapping

- **OWNER / PURPOSE:** Catalog; datos SKU/precio o correspondencia externa, operaciones tipadas y capacidades distintas.
- **INPUT / READS:** contexto, Product/SKU/unidad/precio con base y revisión, o conexión/IDs externos/SKU/observación remota; mappings y compromisos referenciados publicados.
- **LOCKS / LOCK ORDER:** I → K para mapping/destino afectado → M → J si trabajo afectado; identidad SKU única y mapping único; creación de mapping bajo K.
- **WRITES / PRE / POST:** maestro/precio versionado o mapping; no adivinanza por nombre; LINKED solo tras compatibilidad, conflictos quedan visibles; revisar publicación si cambia mapping.
- **IDEMPOTENCY / RETRY / FAILURES:** D alta/vínculo; V edición; CM0; MAPPING_CONFLICT/MISSING_REMOTE/UNIT_INCOMPATIBLE. No reasignar un vínculo usado sin historial y reconciliación.
- **EVENTS / AUDIT:** CatalogChanged/MappingChanged, revisión de publicación invalidada bajo K y trabajo necesario deduplicado, sin copiar catálogo al canal.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; observación remota viene de C03; nueva versión/retirada, sin alterar snapshots o stock confirmado.

<a id="c24"></a>
### C24 — Preparar preview de importación

- **OWNER / PURPOSE:** dueño del lote; preparar cambios revisables, sin confirmar maestros/stock.
- **INPUT / READS:** archivo privado, hash, entidad, tipo/contrato y actor; parser limitado, maestros/mappings/revisiones y políticas publicadas.
- **LOCKS / LOCK ORDER:** I → B para fijar resultado; lecturas de negocio materializadas bajo contexto sin lock económico prolongado.
- **WRITES / PRE / POST:** lote/filas temporales, clasificación y manifiesto de preview; archivo seguro y límites activos; ningún movimiento, saldo o reserva cambia.
- **IDEMPOTENCY / RETRY / FAILURES:** D por intención de preparación; CM0; UNSAFE_FILE/LIMIT_EXCEEDED/PARSE_ERROR conservan resultado de validación, no éxito de negocio.
- **EVENTS / AUDIT:** ImportPreviewPrepared, auditoría de acceso/preparación, sin hecho económico.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** lectura de objeto/parse fuera de transacción larga; descartar conforme retención o preparar nueva versión invalida preview anterior.

<a id="c25"></a>
### C25 — Confirmar lote revisado

- **OWNER / PURPOSE:** dueño del lote; aplicar exclusivamente filas autorizadas de un preview vigente.
- **INPUT / READS:** ID/revisión/hash de preview, claves estables por fila, política y actor; fuentes y revisiones actuales, resultados previos de esas filas.
- **LOCKS / LOCK ORDER:** todas I de lote/filas ordenadas → K si mappings/publicación → B → M → P → U → V → J según dueño/recursos afectados; participantes C11/C12/C13 bajo la misma transacción y plan completo, sin comando anidado que abra otra.
- **WRITES / PRE / POST:** cambios del dueño + lote/filas confirmados; todas las filas del lote válidas y permiso vigente; cualquiera falla → ninguna nueva fila se confirma.
- **IDEMPOTENCY / RETRY / FAILURES:** D por lote y unicidad durable de procedencia de fila; CM0; PREVIEW_STALE/ROW_CONFLICT/OPENING_DUPLICATE. No retry cambiando silenciosamente las filas aprobadas.
- **EVENTS / AUDIT:** ImportBatchConfirmed y hechos de participantes, con procedencia y resultado exactos; auditoría crítica si mueve stock.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; corrección por comandos del dueño, no borrar import para reimportar existencias.

<a id="c26"></a>
### C26 — Preparar informe o snapshot

- **OWNER / PURPOSE:** proyección de lectura de dueños; Documents posee snapshot persistido, no cálculo de ingresos/coste.
- **INPUT / READS:** entidad/actor, filtros, corte, definición/versión del indicador y modo temporal/persistido; contratos de Sales/Inventory y permisos actuales.
- **LOCKS / LOCK ORDER:** I → D → J si trabajo durable para registrar snapshot; sin locks económicos durante generación. Dataset consistente o revisión/cursor comprobado; cambio durante lectura sin snapshot fiable invalida resultado.
- **WRITES / PRE / POST:** trabajo acotado y preview temporal o artifact generado con parámetros/corte/actor/hash; datos incompletos explícitos, nunca coste cero por ausencia.
- **IDEMPOTENCY / RETRY / FAILURES:** R para lectura corta; D para snapshot/trabajo durable; CM0; DATASET_CHANGED/INCOMPLETE/ACCESS_REVOKED.
- **EVENTS / AUDIT:** ReportPrepared/ReportSnapshotAvailable según modo; acceso auditado, no evento económico ni asiento.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** generación/objetos fuera de transacción operativa; snapshot usa C31/C32 y preview C38; regenerar conserva versión anterior y procedencia GENERATED_REPRESENTATION.
