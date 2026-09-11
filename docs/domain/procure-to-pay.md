# Procure-to-Pay objetivo

Propietarios: Procurement para compromiso/obligación/CPE proveedor; Inventory para recepción; Treasury para pago; Accounting y Tax para sus interpretaciones; Documents para artefactos. Estado: arquitectura con [deep spec M05 candidata](../specs/milestones/procurement-deep.md); aprobación de políticas pendiente.

```text
necesidad aprobada → orden → recepción o conformidad de servicio
 → documento proveedor → matching/excepción → obligación aprobada
 → propuesta de pago → pago confirmado → aplicación
 → posting Accounting + tratamiento Tax → conciliación y cierre
```

## Goods y servicios comprados

La línea de compra declara `STOCK_GOOD`, `NON_STOCK_GOOD` o `SERVICE/EXPENSE_CONCEPT`, unidad, cantidad/importe, período o hitos del servicio y tratamiento esperado solo como dato operativo. Un servicio comprado no crea SKU almacenable ni catálogo de servicios vendidos. Puede ser directo sin orden/recepción cuando política y riesgo lo permitan, pero sigue teniendo aprobación, documento, período y evidencia.

## Documentos y matching

| Hecho | Dueño | Regla |
|---|---|---|
| Orden | Procurement | Términos y líneas congelados al aprobar; cambios crean revisión |
| Recepción física | Inventory | Parcial, condición, ubicación, serial/lote y referencia a línea; no reconoce deuda por sí sola |
| Conformidad de servicio | Procurement | Período/hito, aceptante y evidencia; no inventa stock |
| CPE/factura proveedor | Procurement | Identidad externa, emisor, fecha, líneas, importes y vínculos Documents; captura no acredita validez fiscal |
| Matching | Procurement | Comparación por líneas entre orden, recepción/conformidad y factura; tolerancias tipadas/versionadas; resultado `MATCHED`, `EXCEPTION`, `NOT_REQUIRED` |
| Obligación/pagabilidad | Procurement | El documento puede quedar reconocido y bloqueado para pago; bloque de pago no borra el hecho ni decide asiento |

Three-way match se aplica a bienes con orden+recepción+factura. Servicios usan orden+conformidad+factura cuando corresponda. Compra directa controlada no fabrica documentos faltantes. Tolerancias absolutas/porcentuales, moneda, cantidad, precio, impuesto y fecha se evalúan separadamente; exceder una crea excepción, nunca ajuste silencioso.

Una devolución a proveedor tiene salida física al coste operativo que corresponda y un ajuste/nota comercial por importe del proveedor. Las diferencias no deben forzarse a cero: Inventory, Procurement, Accounting y Tax conservan sus magnitudes y las concilian.

## Pago y cadena navegable

Procurement publica obligación versionada y estado de bloqueo. Treasury programa, confirma y aplica pagos con evidencia bancaria; pagar a tercero exige designación/evidencia y control fiscal. Una observación bancaria no crea factura. La vista relacionada navega PO → Receipt/Service Acceptance → Supplier CPE → Match → Payable → Payment/Application → Posting → Evidence, mediante referencias públicas y autorización en cada dueño; no es un workflow engine ni una tabla propietaria de todo.

## Excepciones y controles

Delta propuesto del [amendment](../evidence/b2b-financing-amendment.md): la OC recibida **del cliente** pertenece a Sales/B2B, no a esta compra. Cuando socio paga al proveedor, Procurement mantiene obligación y evidencia de adquisición/conformidad; [M06](../specs/flows/financing-events-statements.md) coordina extinción acreditada por tercero en Treasury y derecho de reembolso Corporate sin movimiento en cuenta TILMUX. Distinguir quién paga de tercero designado para recibir; no autorizar otro pago de una porción ya extinguida ni afirmar deducción por el reembolso.

Duplicado de factura por emisor/tipo/serie/número; factura sin recepción; exceso de cantidad/precio; servicio sin conformidad; impuesto/detracción pendiente; CPE inválido/no verificable; pago en HOLD; recepción con costo desconocido; período cerrado. Cada excepción tiene severidad WARNING/BLOCKING, recurso afectado, causa, responsable, edad y siguiente acción permitida.

M05 concreta rutas de compra directa, conformidad, tolerancias propuestas, aprobaciones, obligaciones parciales, notas/devoluciones y corte. El gate de políticas aplicables sigue abierto; [Tax M09](../specs/milestones/tax-deep.md) gobierna determinaciones. RFQ, portal proveedor, sourcing, contratos avanzados y recurring engine quedan fuera hasta caso real.
