# SP2 — Compromiso, stock, dinero y entrega

Propietarios: Sales (propuesta/venta/acto comercial), Inventory (posiciones/reservas/costes/movimientos), Treasury (cuentas/dinero/aplicaciones). Coordinadores nombrados componen contratos, sin tablas de hechos propias ni llamadas entre modelos ajenos. Fuente de estados de estos propietarios para la slice; [CM0 y orden](../cross-cutting/command-matrix.md) completan sus fichas. [HP1–HP3](first-operational-circuit.md) distinguen decisiones cerradas y validaciones pendientes.

## De observado a aceptado

Sales conserva un caso por `(entidad, conexión, external order ID)` y sus observaciones inmutables. Tiene revisión local monotónica y puntero a observación seleccionada; el tiempo externo no es versión confiable. Recibos/inbox son de integración, no la venta. Las etapas técnicas y de recepción están en [integraciones](jumpseller-external-work.md); aquí solo vive la decisión comercial.

| Dimensión / estado | Significado |
|---|---|
| Resolución: UNRESOLVED / BLOCKED / READY | Campos, correspondencias y consistencia de la propuesta; READY es elegible para intentar aceptación, no reserva ni deuda |
| Decisión: UNDECIDED / ACCEPTED / DECLINED | Decisión empresarial explícita; ACCEPTED referencia una única venta, incluso si luego se cancela |
| Discrepancia: NONE / REVIEW_REQUIRED | Observación material no representada en el compromiso, identidad/estado externo incierto o cancelación recibida |
| Venta: OPEN / CLOSED / CANCELED | OPEN tiene compromisos/remanentes; CLOSED no tiene ejecución/corrección pendiente según hechos; CANCELED solo sin unidades entregadas netas ni compromisos restantes. Reabrir se deriva de corrección autorizada, no de webhook |
| Progreso físico | Cantidades comprometidas, reservadas, entregadas, retornadas y canceladas por línea; NO otro enum de pago/CPE mezclado |
| Progreso financiero | Pendiente/parcial/liquidado derivado de T y aplicaciones; PAID del canal no lo modifica |

| FROM → TO | Comando / guarda decisiva / fallo / corrección |
|---|---|
| UNRESOLVED/BLOCKED → READY | C04 evalúa snapshot fresco y referencias resueltas; stock es precheck informativo, se decide nuevamente en C14. Falta de dato conserva BLOCKED |
| READY/UNDECIDED → ACCEPTED + venta OPEN | C14, aceptación humana con revisión; compromiso + reserva íntegra + T + auditoría/hechos atómicos. Fallo de una línea deja propuesta sin venta |
| UNDECIDED → DECLINED | C15 con razón, sin saldo/stock cambiado. No se reabre automáticamente por otro webhook |
| ACCEPTED → ACCEPTED + REVIEW_REQUIRED | C04 conserva nueva observación material; no reescribe venta/reserva. Cancelado externamente también exige revisión local |
| OPEN → OPEN/CLOSED/CANCELED | C15/C20/C21 según remanentes y hechos. Cancelación de lo entregado no se simula borrando líneas |

Una propuesta ya cancelada/abandonada en lectura remota seleccionada no es READY. Evento retrasado no la reactiva: discrepancia y nueva lectura reconciliada. Un pedido previamente aceptado se identifica antes de crear raíces; repetir C14 devuelve su venta si es la misma intención/versión aceptada, y responde ALREADY_ACCEPTED_CONFLICT si se pretende sustituir sus términos. Revisión comercial relevante pendiente bloquea nueva entrega; no bloquea registrar cobro/refund/retorno ya ocurridos con evidencia.

Validación para READY: Party concreta, SKU LINKED/activo con unidad válida, modalidad/dirección utilizable, cantidades positivas y desglose de precios/totales explicable en una moneda. Se conservan componentes del canal como observaciones; no se infiere impuesto o descuento faltante del total. El adaptador proporciona ecuación/desglose interpretado y su versión; diferencia exacta no explicada → TOTAL_MISMATCH. HP1 ya exige cobertura total y base comercial autorizada; la asignación exacta de componentes no expresados sigue bloqueante. Precio distinto de Catalog no se reemplaza ni se acepta por defecto: propuesta corregida/autorizada conserva ambos orígenes, motivo y revisión.

C15 REVISE_PROPOSAL registra términos comerciales revisados por el operador contra una observación concreta; conserva el original y su explicación/desglose. No altera el payload externo ni permite saltar políticas incompletas. Resolver Party/mapping o revisar términos habilita C04 para reevaluar la propuesta sin exigir otro webhook. Una observación material posterior invalida esa conformidad. RESOLVE_DISCREPANCY registra qué diferencia se acepta mantener o corrige con evidencia; no borra demanda X aún no representada ni acredita una corrección remota que no se observó.

Líneas repetidas del mismo SKU son líneas distintas de evidencia. Se agrega su demanda para reservar sin perder cada línea/snapshot; no deduplicar líneas por SKU ni por nombre. Si no hay ID externo de línea fiable, la revisión seleccionada conserva ordinal/fingerprint de línea; el update reemplaza la propuesta completa, no aplica deltas a líneas adivinadas. Una venta aceptada no crece por un update; reducción/corrección explícita por C15, ampliación requiere caso comercial posterior y queda fuera de esta slice.

## Cantidades, reservas y disponibilidad

Para una SKU y conjunto explícito de posiciones elegibles de la entidad:

Una posición identifica SKU/unidad y ubicación física interna declarada bajo Inventory; C13 puede darla de alta con esos datos y pertenencia verificada antes de abrir existencia. No se necesita jerarquía de almacenes por anticipación ni confundir la ubicación interna con location_id remoto. Cambiar ubicación de una posición usada no mueve mercancía: ese traslado requiere un movimiento posterior autorizado, fuera de esta apertura.

- P = existencia física confirmada en esas posiciones; N = parte física no vendible, incluida cuarentena/daño. N es subconjunto de P, no descuento adicional de posiciones ya excluidas.
- R = remanente de reservas activas sobre la parte vendible. A = P − N − R; exigir P ≥ 0, N ≥ 0, R ≥ 0, N + R ≤ P. No usar max(0) para ocultar violación de esa invariante.
- X = demanda externa observada todavía no representada en reservas/consumos internos, calculada por el coordinador desde casos Sales reconciliados; no es reserva ni stock físico. Solo cantidades inequívocamente mapeadas; incertidumbre bloquea aumento publicable.
- B = buffer de seguridad explícito y no negativo, si la política aprobada lo activa. Sin política no se inventa B=0 para habilitar publicación; el cálculo puede mostrarse como candidato, no enviarse.
- Objetivo publicable Q = max(0, A − X − B), en unidades publicables exactas. En la primera slice hay un destino activo; asignación multicanal está fuera. No restar una supuesta «asignación al canal» de nuevo, ni publicar A completo en dos anuncios de la misma SKU.

X incluye pedidos remotos abiertos no aceptados y aumentos observados no aceptados de un compromiso. Una cantidad ya reservada/entregada internamente no sigue en X. Al aceptar, retirar esa contribución X y aumentar R ocurre bajo el mismo plan K/E/S/P/V: no hay doble descuento de disponibilidad. X es una proyección de observaciones seleccionadas, con IDs/revisiones Sales, no un nuevo hecho de Inventory ni un permiso de despachar. Cancelar externamente no libera R de una venta; C15 decide su remanente.

Ejemplo sintético: P=10, N=2, R=3, X=2 y B=0 aprobado para el ejemplo → A=5, Q=3. Aceptar las 2 observadas produce R=5, X=0, Q=3. Despacharlas produce P=8, R=3, Q=3. Descontar nuevamente al recibir PAID daría un resultado incorrecto. Las carreras/remoto se rigen por [publicación](jumpseller-external-work.md#stock-publication), que no promete atomicidad entre sistemas.

Reserva identifica venta/línea, SKU, posición y cantidad original; `remaining = allocated − consumed − released`, siempre no negativo. Tiene ACTIVE mientras remaining>0; EXHAUSTED si todo consumido, RELEASED si todo liberado, CLOSED_MIXED si ambos agotaron el total. No tabla universal de estados. Una reserva mixta conserva componentes exactos, no un status que pierda parcialidades.

| Transición | Comando / condición |
|---|---|
| Sin reserva → ACTIVE | C14 reserva todas las líneas en posiciones elegibles bajo P; falta de stock revierte todas |
| ACTIVE → ACTIVE/EXHAUSTED/CLOSED_MIXED | C20 consume solo el remanente preparado vigente y baja P por la misma cantidad |
| ACTIVE → ACTIVE/RELEASED/CLOSED_MIXED | C15 cancela solo compromiso no ejecutado y libera R, sin subir P |
| Retorno después del consumo | C21 crea entrada contra salida original; nunca «desconsume» reserva antigua ni vuelve a vender automáticamente |

Preparación asigna posiciones y, cuando corresponda, seriales de una reserva; no baja P ni confirma entrega. Dos preparaciones no pueden asignar simultáneamente la misma porción/serial: esas cantidades quedan en la asignación activa de la reserva bajo S/P/U/V. Cancelar la preparación libera asignación, no el compromiso ni R. Cancelar remanente comercial invalida las preparaciones que lo excedan y libera R coordinadamente. Un ajuste negativo/daño no roba unidades reservadas: si dejaría N+R>P, RESERVATION_CONFLICT hasta resolver la reserva por su dueño comercial.

La selección de posiciones es parte de la propuesta de preparación, verificable por pertenencia/disponibilidad; no algoritmo de optimización de almacenes. El coste de salida usa el promedio ponderado móvil operativo de Inventory y conserva cantidad/valor/orígenes suficientes para explicar cada cálculo; reparto de parcialidades con residuo exacto según invariante fundacional. UNKNOWN no se sustituye por unitario cero ni se mezcla silenciosamente en el promedio. Accounting decide VNR/deterioro/cierre sin reescribir el kardex. Seriales siguen dirección, salida original y ciclo de posesión; SKU retirado permite ejecutar/corregir compromiso previo, no nuevas aceptaciones/aperturas.

## Treasury sin dinero inventado

Cuenta: entidad, identidad pública, moneda, tipo declarado, titularidad/evidencia y ACTIVE/CLOSED. No se confirma un cobro real hacia cuenta desconocida o de otra entidad. Para la slice, sin conversión FX automática ni conciliación bancaria automática. Un depósito en cuenta del socio no se reclasifica por comodidad.

| Dimensión / transición | Contrato |
|---|---|
| Cobro PROPOSED → CONFIRMED | C17, cantidad positiva/moneda/cuenta/fecha/referencia/evidencia HP2. PROPOSED no contribuye a N ni cobertura |
| PROPOSED → REJECTED | C16, razón/versión; no hay movimiento confirmado que revertir |
| CONFIRMED → corregido/refund parcial o total | C22 registra nuevo movimiento/reversión referenciada; conserva original y N neto, sin editar su importe |
| Objetivo OPEN/PARTIAL/SETTLED | Derivado de L vigente y A(o), creado/actualizado únicamente por participante del dueño Sales en C14/C15 |
| Aplicación confirmada → des-aplicación parcial/total | C18/C15/C22, nueva relación compensatoria acotada; nunca borrar fila histórica |

C16 recibe observación PAID como una referencia de procedencia posible. C17 exige además evidencia de dinero y confirmación humana; el importe/fecha/cuenta no se rellenan desde flags del canal. Una referencia transaccional de banco/pasarela tiene namespace por entidad/cuenta/proveedor y evita duplicados aunque cambie la clave de intención. Referencia ausente no prueba duplicación ni unicidad: HP2 debe definir comprobación; sin ella se conserva propuesta, no confirmación. Mismo monto/fecha no basta para deduplicar dos cobros reales ni para confirmar uno.

Las invariantes N/A/U de [dinero](../../domain/invariants.md) gobiernan C17/C18/C22. Exceso confirmado queda sin aplicar, nunca ingreso ficticio. Aplicar tiene importe/objetivo explícitos; no se reparte automáticamente ni se mezcla moneda. Des-aplicar no devuelve dinero. Un refund confirmado es registro de devolución monetaria efectuada externamente con evidencia; CasPro no ordena transferir. Si se trata de un error de captura sin devolución real se registra corrección contable-operativa de captura, con tipo/referencia/motivo distinguibles, nunca se etiqueta refund bancario.

Refund descubre todos los objetivos/aplicaciones del cobro y las ventas de su cobertura. Bloquear S/T/R en el orden común, releer el conjunto; una aplicación nueva obliga a replanificar. Si N disminuye por debajo de A(r), des-aplicar exactamente el exceso con referencias explícitas; luego actualizar cobertura. Puede quedar venta ya entregada con deuda/retorno pendiente: eso se registra y bloquea nueva entrega al contado, sin borrar entrega ni convertirla a crédito. No forzar modificación de CPE ni retorno físico.

## Entrega y principales correcciones

Preparación DRAFT → READY por C19: remanente asignado, dirección/snapshots disponibles, stock/reserva y política conocidas. READY no acredita pago definitivo ni permiso futuro; C20 reevalúa todo. C19 puede cancelar preparación antes de confirmar, liberando asignación. CONFIRMED es un hecho inmutable; fallo anterior al commit no produce salida ni entrega. Faltante de evidencia legal/comercial HP4 bloquea nueva confirmación, sin inventar fecha de emisión.

Cobertura inicial cerrada por HP1: A(o) ≥ L(o) del objetivo vigente para la venta antes de cualquier despacho; L puede reducirse solo por corrección comercial autorizada. Se registran cobros parciales sin despachar. El circuito no ofrece cobertura proporcional ni crédito implícito. La asignación de descuentos/envío que el canal no explique permanece bloqueante hasta su regla, sin reducir silenciosamente L.

Cancelación parcial solo quita cantidades aún no entregadas/ya canceladas; no borra retorno previo. C15 publica importe comercial nuevo y sincroniza T; cualquier A(o)>L nuevo se resuelve mediante des-aplicaciones explícitas en la misma transacción, dejando U disponible. No refund automático. Un update remoto cancelado deja discrepancia hasta esa decisión. Una devolución física C21 requiere salida original y cantidades/seriales pendientes de retornar; conserva coste atribuible y entra no vendible. Una revisión posterior puede cambiar condición con nuevo hecho. Ajuste comercial/CPE y refund se deciden separadamente.

## Fichas críticas (CM0)

<a id="c13"></a>
### C13 — Confirmar apertura o ajuste de stock

- **OWNER / PURPOSE:** Inventory; registrar existencia inicial o corrección sustentada, nunca editar saldo bruto.
- **INPUT / READS:** contexto, tipo OPENING/ADJUSTMENT/CONDITION_CHANGE, SKU/posición, cantidades/dirección, seriales, coste de origen conocido o UNKNOWN, fecha/evidencia/motivo y revisión; posición, reservas y política HP3.
- **LOCKS / LOCK ORDER:** I → K de destino afectado → M para alta/estado SKU → P → U → V → J. Nueva posición bajo M y UNIQUE; apertura única por expediente/fila de origen.
- **WRITES / PRE / POST:** movimiento/condición, asignaciones de coste y posición; no negativo ni N+R>P, serial compatible, apertura autorizada; actualizar revisión de disponibilidad y trabajo de publicación, no HTTP.
- **IDEMPOTENCY / RETRY / FAILURES:** D; CM0; OPENING_DUPLICATE/RESERVATION_CONFLICT/SERIAL_CONFLICT/COST_UNKNOWN visible. UNKNOWN no autoriza margen definitivo.
- **EVENTS / AUDIT:** StockOpened/StockAdjusted/StockConditionChanged, cantidad/coste/procedencia y actor críticos; AVAILABLE recalculable.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; contramovimiento/ajuste con referencia y guardas. Purga/reimport no repite apertura.

<a id="c14"></a>
### C14 — Aceptar pedido externo

- **OWNER / PURPOSE:** coordinador de aceptación; Sales decide compromiso, Inventory reserva y Treasury publica objetivo mediante participantes identificados.
- **INPUT / READS:** caso/observación/revisión, Party/mappings/snapshots aprobados, posiciones/cantidades y desglose/moneda HP1; última observación seleccionada, política, disponibilidad y aceptación previa.
- **LOCKS / LOCK ORDER:** I → K → E → M → S nueva bajo E → T nuevo bajo S → P → U si asignado → V → J. La ausencia de S/T/V no se bloquea como fila; creación exclusiva por padres/UNIQUE.
- **WRITES / PRE / POST:** UNDECIDED+READY sin cancelación/discrepancia, todos los datos y stock suficientes; crear exactamente una venta/snapshots/obligación, reserva íntegra y T con el mismo L/moneda/revisión. Aceptación y reducción de X se reflejan juntas.
- **IDEMPOTENCY / RETRY / FAILURES:** D + UNIQUE del pedido; CM0; STOCK_INSUFFICIENT/TOTAL_MISMATCH/UNRESOLVED_REFERENCE/EXTERNAL_STALE/ALREADY_ACCEPTED_CONFLICT. Ninguna línea confirma si otra falla.
- **EVENTS / AUDIT:** SaleCommitted, StockReserved, SettlementTargetPublished e intención de recalcular stock, con actor/observación base; sin cobro automático.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; actualización/cancelación posterior C15, no repetir webhook como nueva venta.

<a id="c15"></a>
### C15 — Rechazar propuesta o corregir/cancelar remanente

- **OWNER / PURPOSE:** Sales o coordinador Sales/Inventory/Treasury si ya aceptado; decisión explícita sobre compromiso, nunca sobre pago remoto.
- **INPUT / READS:** caso/venta/revisión, tipo REVISE_PROPOSAL/RESOLVE_DISCREPANCY/DECLINE/CANCEL_REMAINDER/COMMERCIAL_ADJUSTMENT/SNAPSHOT_CORRECTION, observación base, cantidades/importes/snapshots propuestos, motivo/evidencia y aplicaciones a deshacer; raíces y política vigentes.
- **LOCKS / LOCK ORDER:** I → K → E → M si referencias de propuesta → S → T → R → P → U → V → C si expediente afectado → J. Sin venta solo K/E/M/J afectados; descubrir completo antes de locks.
- **WRITES / PRE / POST:** revisar/declinar propuesta no crea compromiso; revisión comercial exige base íntegra HP1, conserva observación y solicita reevaluación C04. Resolver discrepancia identifica revisión/razón y no elimina hechos o demanda no representada. En venta, cancelar solo remanente, liberar reserva/asignación correspondiente; L nuevo no negativo y T sincronizado con excesos des-aplicados; cambios documentarios alteran revisión relevante e invalidan aprobación derivada.
- **IDEMPOTENCY / RETRY / FAILURES:** D; CM0; EXCEEDS_REMAINDER/ADJUSTMENT_UNSUPPORTED/POLICY_UNRESOLVED/ALLOCATION_PLAN_STALE. No aumenta cantidades aceptadas ni anula físicamente entregas.
- **EVENTS / AUDIT:** ProposalRevised/DiscrepancyReviewed/ProposalDeclined o SaleCorrected/CommitmentCanceled, ReservationReleased/SettlementTargetChanged según cambios; historial de motivo, términos previos y nuevos.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; no cancela automáticamente pedido remoto, CPE ni transfiere refund. Nueva corrección conserva las anteriores; ampliar venta/reabrir pedido cancelado requiere alcance comercial separado.

<a id="c16"></a>
### C16 — Proponer o rechazar cobro

- **OWNER / PURPOSE:** Treasury; capturar evidencia pendiente sin aumentar dinero disponible.
- **INPUT / READS:** contexto, cuenta/moneda/importe/fecha/referencia/evidencia declaradas, o rechazo con revisión; cuenta y duplicados candidatos.
- **LOCKS / LOCK ORDER:** I → F → R; alta por intención única, cuenta ya identificada.
- **WRITES / PRE / POST:** propuesta o rechazo versionado; PROPOSED/REJECTED no cambia N/A/U. Datos incompletos permanecen explícitos.
- **IDEMPOTENCY / RETRY / FAILURES:** D alta, V rechazo/edición; CM0; INVALID_AMOUNT/WRONG_CURRENCY/REVISION_CONFLICT.
- **EVENTS / AUDIT:** ReceiptProposed/ReceiptProposalRejected, origen y actor sin afirmar cobro recibido.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; editar propuesta con revisión o rechazar; confirmada usa C22.

<a id="c17"></a>
### C17 — Confirmar cobro

- **OWNER / PURPOSE:** Treasury; constituir dinero confirmado por evidencia HP2.
- **INPUT / READS:** propuesta/revisión, cuenta, importe/moneda/fecha, referencia transaccional tipada y evidencia revisada; cuenta, propuesta, referencia duplicada y disponibilidad de evidencia.
- **LOCKS / LOCK ORDER:** I → F → R → D si archivo; UNIQUE de referencia identificada además de intención.
- **WRITES / PRE / POST:** PROPOSED válido y autorizado → movimiento confirmado, N positivo, A=0 y U=N; no aplicar implícitamente al pedido ni simular conciliación bancaria.
- **IDEMPOTENCY / RETRY / FAILURES:** D; CM0; DUPLICATE_RECEIPT_REFERENCE/INSUFFICIENT_EVIDENCE/WRONG_CURRENCY/ACCOUNT_INACTIVE. Una observación PAID aislada no satisface PRE.
- **EVENTS / AUDIT:** ReceiptConfirmed, fuente/referencia/fecha/importe/cuenta y confirmador; auditoría crítica atómica.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; C22 con referencia, sin editar movimiento ni llamar banco.

<a id="c18"></a>
### C18 — Aplicar o des-aplicar cobro

- **OWNER / PURPOSE:** Treasury, coordinado con Sales cuando cambia elegibilidad comercial; conserva límites de ambos extremos.
- **INPUT / READS:** acción APPLY/UNAPPLY, T y R, importe, revisión y referencia a aplicaciones originales para UNAPPLY; venta/objetivo, dinero neto y todas sus aplicaciones.
- **LOCKS / LOCK ORDER:** I → S afectadas → T ordenados → R ordenados. Releer distribución tras tomar locks; no sumar desde vista cacheada.
- **WRITES / PRE / POST:** misma entidad/moneda/dirección, U(r) suficiente y remanente L(o) suficiente; crear aplicación/des-aplicación referenciada, conservar 0≤A(r)≤N(r) y 0≤A(o)≤L(o); déficit posterior visible en Sales.
- **IDEMPOTENCY / RETRY / FAILURES:** D; CM0; INSUFFICIENT_UNAPPLIED/TARGET_LIMIT/WRONG_CURRENCY/EXCEEDS_APPLICATION. Exceso permanece U, no se fuerza.
- **EVENTS / AUDIT:** ReceiptApplied/ReceiptUnapplied y cobertura afectada, referencias exactas/actor/motivo; no otro movimiento de dinero.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; compensar aplicación con referencia, no borrar fila ni devolver dinero.

<a id="c19"></a>
### C19 — Preparar o retirar preparación de entrega

- **OWNER / PURPOSE:** coordinador Sales/Inventory; asignar una porción ejecutable sin salida física.
- **INPUT / READS:** venta/revisión, líneas/cantidades, posiciones/seriales, destinatario/modalidad y evidencia requerida; caso externo, remanentes, cobertura informativa y reservas/asignaciones actuales.
- **LOCKS / LOCK ORDER:** I → K → E → S → T → R → P → U → V; selección ya descubierta, sin retener locks para picking humano.
- **WRITES / PRE / POST:** preparar solo compromiso/reserva vigente; asignaciones exclusivas y preparación READY con revisiones. Retirar preparación libera asignación, no R/P. No más preparado que reserva restante.
- **IDEMPOTENCY / RETRY / FAILURES:** D; CM0; PREPARATION_CONFLICT/INSUFFICIENT_RESERVED/MATERIAL_REVIEW_REQUIRED. Preparación no garantiza cobertura futura.
- **EVENTS / AUDIT:** DeliveryPrepared/PreparationWithdrawn, actor y asignación; no StockDispatched.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; retirar antes de confirmar; después C21, no delete.

<a id="c20"></a>
### C20 — Confirmar entrega física

- **OWNER / PURPOSE:** coordinador Sales/Inventory/Treasury; confirmar acto comercial y salida correspondiente.
- **INPUT / READS:** preparación/revisión, cantidades/seriales y fecha real/evidencia; caso externo, venta, L/A/N vigentes, reservas/posiciones/costes, requisitos CPE HP4.
- **LOCKS / LOCK ORDER:** I → K → E → S → T → R → P → U → V → C si condición documental → J. Todos los cobros que sostienen cobertura y sus objetivos quedan en el mismo plan.
- **WRITES / PRE / POST:** READY vigente, sin cancelación/discrepancia bloqueante, cobertura HP1 y condición HP4 satisfechas; consumir asignación/reserva y P exactamente una vez, registrar entrega y costes/seriales. Parcial mantiene saldo pendiente; nunca stock negativo.
- **IDEMPOTENCY / RETRY / FAILURES:** D + unicidad de confirmación de preparación; CM0; COVERAGE_INSUFFICIENT/PREPARATION_STALE/CPE_REQUIRED/STOCK_CHANGED. Falla auditoría o participante → ninguna mitad confirma.
- **EVENTS / AUDIT:** DeliveryConfirmed + StockDispatched, origen/asignación/coste y trabajo de nueva disponibilidad; evidencia del confirmador.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; no marcar automáticamente shipped en Jumpseller ni enviar CPE; retorno C21/corrección autorizada con historia.

<a id="c21"></a>
### C21 — Registrar retorno físico autorizado

- **OWNER / PURPOSE:** coordinador Sales/Inventory; recibir contra salida original sin equivaler a refund.
- **INPUT / READS:** acción RECEIVE_RETURN/CORRECT_RETURN, venta/entrega/líneas originales, retorno que se corrige si procede, cantidades/seriales, condición, fecha/evidencia/motivo y autorización HP3; retornos netos previos y asignaciones de coste de salida.
- **LOCKS / LOCK ORDER:** I → K → S → P → U → V si coexisten otras reservas → J; salida/coste original bajo raíz/posición.
- **WRITES / PRE / POST:** no exceder unidades netas retornables ni duplicar serial/ciclo; registrar retorno y entrada con coste atribuible/resto exacto o UNKNOWN conservado. Condición no vendible mientras no haya revisión autorizada; no recrear reserva consumida. CORRECT_RETURN solo compensa error probado, con tope del retorno neto, unidades/ciclo aún disponibles y coste de esa entrada; registra salida correctiva y corrección comercial del retorno juntas. No permite retirar unidades ya revendidas o reservadas ni simular una nueva entrega.
- **IDEMPOTENCY / RETRY / FAILURES:** D; CM0; EXCEEDS_RETURNABLE/SERIAL_CYCLE_CONFLICT/RETURN_NOT_AUTHORIZED. CORRECT_RETURN exige sales.correct e inventory.adjust además de las capacidades de retorno. SKU retirado no impide corregir entrega previa válida.
- **EVENTS / AUDIT:** GoodsReturned + StockReturned, dirección entrada/original/ciclo/coste/motivo; no ReceiptRefunded ni nota fiscal automática.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; CORRECT_RETURN conserva retorno y compensación referenciados; elegibilidad de reventa separada C13 CONDITION_CHANGE. Una nueva entrega comercial no es corrección de error y queda sujeta al compromiso correspondiente.

<a id="c22"></a>
### C22 — Registrar refund o corrección de cobro

- **OWNER / PURPOSE:** Treasury; coordinador con Sales para cobertura de objetivos afectados. Tipos REFUND_EXTERNAL y CAPTURE_CORRECTION distintos.
- **INPUT / READS:** original, importe/moneda/fecha, tipo, evidencia/referencia/motivo y plan explícito de des-aplicaciones; todas las aplicaciones/objetivos/ventas y neto original.
- **LOCKS / LOCK ORDER:** I → S → T → F de cuenta cuando proceda → R → D si evidencia; redescubrir si alguna aplicación cambió. No empezar reteniendo R y añadir después S/T.
- **WRITES / PRE / POST:** importe≤neto corregible, HP2/HP3, prueba de devolución externa si REFUND_EXTERNAL; movimiento compensatorio + des-aplicación necesaria; conservar N/A/U y marcar déficit de cobertura de bienes ya entregados sin fingir crédito ni borrar entrega.
- **IDEMPOTENCY / RETRY / FAILURES:** D + referencia externa de devolución; CM0; REFUND_EXCEEDS_NET/ALLOCATION_PLAN_STALE/INSUFFICIENT_EVIDENCE. Repetición no duplica salida.
- **EVENTS / AUDIT:** ReceiptRefunded o ReceiptCaptureCorrected + ReceiptUnapplied/CoverageChanged; tipo/razón/original/excepción visibles, auditoría crítica.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; no orden bancaria; reversión de error por nuevo hecho probado y acotado. Compensaciones que excedan original son otro caso fuera de slice.

<a id="c23"></a>
### C23 — Registrar o cerrar cuenta financiera

- **OWNER / PURPOSE:** Treasury; identificar destino real del dinero sin inventar disponibilidad.
- **INPUT / READS:** entidad, identidad/tipo/cuenta/moneda, evidencia de titularidad HP2, estado/revisión y motivo; identidad previa y operaciones pendientes.
- **LOCKS / LOCK ORDER:** I → F → D si evidencia; creación por identidad única, sin cargar saldo de apertura como atributo editable.
- **WRITES / PRE / POST:** cuenta ACTIVE o CLOSED; cerrar impide nuevos cobros pero conserva lectura/correcciones históricas autorizadas. No crea movimiento ni saldo.
- **IDEMPOTENCY / RETRY / FAILURES:** D alta, V cierre; CM0; ACCOUNT_IDENTITY_CONFLICT/INSUFFICIENT_EVIDENCE/REVISION_CONFLICT.
- **EVENTS / AUDIT:** FinancialAccountRegistered/FinancialAccountClosed, actor/motivo y evidencia referenciada.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; reabrir/corregir metadata mediante versión autorizada; cambiar propietario/moneda de cuenta usada no permitido.
