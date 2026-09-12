# M05 — Procure-to-Pay: contrato ejecutable futuro

Estado: **SPECIFIED — candidato; políticas tributarias/operativas pendientes según hechos**. Owner Procurement, con Inventory/Treasury/Documents/Accounting/Tax participantes. Hereda [CM0 extendido](../cross-cutting/economic-facts.md), [P2P](../../domain/procure-to-pay.md) y [costeo](inventory-deep.md). No vende servicios ni crea stock para servicios comprados.

## Dimensiones separadas

Pedido de compra: DRAFT→APPROVED→CLOSED/CANCELLED; revisiones aprobadas no se editan. Recepción física y conformidad de servicio son hechos parciales por línea. Documento de proveedor tiene identidad, preservación, verificación fiscal y estado comercial independientes. Match: PENDING/MATCHED/EXCEPTION; payability: HOLD/RELEASED/CLOSED; liquidación Treasury: pendiente/parcial/completa derivada de aplicaciones. Pagar no confirma recepción ni deducibilidad.

Bien inventariable: match cantidad/precio entre PO, recepción y factura. Servicio: PO/contrato + conformidad del período/hito y factura, sin recepción ficticia de almacén. Bien no stock: evidencia de entrega al responsable/activo/gasto, sin kardex vendible. Compra directa requiere autorización con motivo y condiciones antes del compromiso cuando es planificable; si el hecho ya ocurrió se registra como excepción, no se falsifica una PO retroactiva aprobada.

Cada línea mantiene cantidades ordenadas, recibidas/conformes, devueltas, facturadas y anuladas por nota con unidades y referencias. Asignación N:M explícita entre líneas compatibles, limitada por remanentes; una recepción parcial admite varias facturas y una factura varias recepciones. Match no fuerza igualdad de total factura y PO completa. Impuestos, flete, descuento y moneda se comparan por componente; diferencias de moneda no se “toleran” por igualdad numérica.

Tolerancia inicial propuesta: cero diferencias inexplicadas. Una diferencia genera excepción clasificada (precio/cantidad/impuesto/moneda/identidad/duplicado/servicio). Aprobación humana de excepción conserva importe, evidencia, motivo y límites; no es permiso de alterar documento fiscal ni crédito fiscal. Una tolerancia futura exige política versionada, autoridad y casos de borde; no copia defaults ERP.

## Comandos

Además de las guardas comunes, cada confirmación exige moneda/parte propietaria coherentes, revisiones vigentes y documento sellado cuando se invoque como evidencia. D incluye I. No hay pago bancario automático; todo I/O documental se hace en fases Documents.

| ID / capacidad / clase | Inputs/reads y locks en orden | Writes / postcondición / corrección |
|---|---|---|
| P01 proponer/aprobar PO / procurement.prepare / procurement.approve / V | Líneas, proveedor, presupuesto si existe, condiciones, aprobador M→O | Revisión aprobada y compromiso; aprobación solo dentro de mandato. Autoaprobación de operador único explícita y auditada, no segundo actor inventado. Cambios materiales nueva revisión invalidan aprobación |
| P02 autorizar compra directa / procurement.approve_direct / D | Motivo, naturaleza, parte, cantidad/precio y evidencia I→M→O | Expediente de compra directa con control equivalente pertinente; no PO artificial. Excepción ex post se identifica y no acredita aprobación previa |
| P03 recibir bienes / procurement.receive + inventory.receive / D | Compra, entregas previas, unidades/serial, condición, fecha I→M→O→W→P→U→C si vínculo→D | Recepción y movimiento Inventory atómicos; exceso no autorizado rechaza confirmación comercial y deja observación física pendiente de resolver, no desaparece mercancía. Coste conocido/UNKNOWN; reversión posterior mediante devolución/ajuste con soporte |
| P04 conformar servicio/no stock / procurement.accept_service / D | Contrato/PO, período, entregable, responsable I→M→O→D | Conformidad parcial con cantidad/hito y período; no escribe P/W. Rechazo/disputa documentados; corrección referencia conformidad, conserva fecha de conocimiento |
| P05 adquirir factura/nota / procurement.record_document / D | Identidad emisor/receptor, archivos y líneas I→M→O si link→C→D | Identidad única + documento preservado/verificación separada. Puede existir antes de recepción; no genera por sí sola stock ni “pagable”. Duplicado con bytes distintos crea conflicto, no nueva deuda |
| P06 asignar/matchear / procurement.match / D | Set completo de líneas PO/recepción/conformidad/factura/notas I→M→O→T si objetivo existe→C→D | Asignaciones revisadas, residuales y excepciones; no sobreasigna recepción o factura ni compensa tributo con precio. Corrección deshace asignación por revisión, invalida liberación/pago preparado |
| P07 resolver excepción/liberar / procurement.release_payability / D | Evidencia de match, impuestos/restricciones, mandato de aprobador I→M→O→T→C→D | Decisión por excepción, obligación/objetivo Treasury con importe bruto, vencimiento y destinatario autorizado. HOLD legal/fiscal requerido no se elimina por match comercial; liberar no confirma dinero |
| P08 proponer anticipo / procurement.approve_advance / D | Contrato/compra, límite, destinatario, moneda y condiciones I→M→O→T→D | Objetivo de anticipo distinto de AP por recepción; pendiente de liquidación/documentos, sin inventar gasto/inventario. Treasury confirma pago/aplicación con su comando |
| P09 devolver/nota / procurement.return / D | Recepción/remanente y nota si existe I→M→O→T→W→P→U→V→C | INV06 para salida física; crédito del proveedor y ajuste de obligación separados. Dinero ya pagado genera derecho de devolución/anticipo según acuerdo, no pago negativo automático |
| P10 cerrar compra / procurement.close / V | Recepciones, facturas, anticipos, disputas y pendientes O→T→C | Cierre declara saldos y compromisos cancelados, no borra recepción por facturar. Reapertura exige motivo/nueva revisión; obligación impaga conserva exigibilidad aunque PO cerrada |

P07 no debe crear una segunda AP por cada repetición de match: identidad natural `(entidad, dueño Procurement, obligación, moneda)`. Cambiar factura/beneficiario después de preparar pago invalida la preparación; confirmar pago compite con O/T y revisiones de payability. Treasury registra un pago real descubierto aunque haya incumplido proceso, marcado como excepción; no falsifica liberación previa para regularizarlo.

## AP, coste, devengo e impuesto

La [extensión M06 aceptada](../flows/financing-events-statements.md) añade liquidación acreditada por pago de tercero: el pendiente AP deriva de aplicaciones propias **y extinciones autorizadas por tercero separadas**, cada una con fuente/porciones/remanentes. P07 y todo pago/corrección posterior deben releer esas asignaciones para no pagar dos veces. Pagar por cuenta no borra HOLD ni prueba deducibilidad; el hecho ocurrido se registra como excepción si faltó aprobación. Corregirlo puede reabrir obligación proveedor y ajustar derecho socio, preservando reembolso ya ocurrido. Este delta no cambia la naturaleza de la OC Procurement ni la confunde con OC Sales.

Recibir mercancía sin factura puede activar valoración estimada documentada y devengo Accounting; “sin factura” no implica coste cero ni ausencia de pasivo. Invoice-before-receipt puede representar anticipo, obligación o documento prematuro según contrato: revisión específica, no posting genérico a inventario. Parte del impuesto recuperable pendiente se conserva separada hasta decisión Tax; importe bruto pagado sigue siendo un hecho.

Servicio contratado por doce meses requiere período/cobertura, conformidad y calendario de consumo. Prepago no es gasto completo al pagar. Coste adicional admisible se asigna con base explícita (cantidad/peso/valor según política), residual reproducible y vínculos a recepciones; su validación NPIF distingue flete de compra de interés/FX y descuentos posteriores. No activar landed cost arbitrario.

Impuestos aplicables (IGV, SPOT, retención, percepción, no domiciliado) son determinaciones Tax versionadas con evidencia del hecho. Un pago puede dividirse entre proveedor/depósito/autoridad según obligación verificada; las piernas deben sumar la liquidación y seguir identidades distintas, sin neteo oculto. Un servicio SaaS extranjero activa revisión temprana [RS 047-2026](../../research/normative/tax-current-review.md), aunque M09 todavía no tenga UI.

## Lecturas, UX y aceptación

Cockpit por excepción: recibir pendiente, conformidad vencida, factura duplicada, match discrepante, AP bloqueada, anticipo sin liquidar, devolución sin nota y recepción sin factura. Split preview muestra documento original junto a asignaciones y remanentes. Document Flow PO/directa→recepción/conformidad→movimiento si stock→factura→AP→pago→banco→asiento; no oculta pasos faltantes ni inventa nodos. Acciones por teclado preparan, no liberan/pagan directamente.

Casos obligatorios: PO10, recepción6, factura4→match4 y recepción pendiente de facturar2; segunda factura4 solo puede usar2 sin otra recepción o excepción válida; recepción4 posterior completa remanente. PO servicio sin almacén; factura antes de recepción; factura duplicada con nueva intención; factura con proveedor ajeno; nota mayor que factura; devolución física45/crédito60; anticipo118 y factura118 con aplicación única; impuesto pendiente; cambio de cuenta bancaria tras preparación; dos pagos compitiendo por saldo; cierre con recepción no facturada visible; ex post sin aprobación fingida.

Evidencia futura: DOMAIN sumas N:M, PostgreSQL unicidad/atomicidad y CONCURRENCY match/pago/cambio de documento, CONTRACT artefactos y un E2E excepción→resolución. Golden Accounting de recepción por facturar y servicio prepagado en M07–M08; Tax golden por operación activada. No necesita probar SAP/Oracle ni una suite de todos los módulos.

Handoff: Astra architect/checkpoint P2P/Tax; Sol orquesta; implementador y reviewer separados. Entradas esta spec, CM0, NPIF §§10–12/15/17, memo fiscal y tarjeta M05. Permitido elegir presentación/índices; prohibido inferir tolerancias, crédito fiscal, facultades, recepción desde CPE, servicio como SKU stock o automatizar pago. Gate de salida: revisión de casos/políticas aplicables, contrato de Treasury y evidencia candidata exacta; sin esto no FROZEN.
