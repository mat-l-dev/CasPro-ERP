# Benchmark ERP orientado a problemas

Corte: 2026-09-10. Fuentes: documentación oficial pública de SAP S/4HANA, Oracle Fusion Cloud 26B, Microsoft Dynamics 365, NetSuite, Odoo 19 y ERPNext. Se extraen técnicas, no código, UI, activos ni configuración propietaria. Una función de proveedor prueba que existe un patrón, no que sea correcto para CasPro.

| Problema | ERP(s) / patrón observado | Por qué funciona; coste | CasPro fit / decisión / dueño / riesgo |
|---|---|---|---|
| Factura antes/después de recepción | SAP y ERPNext vinculan PO, recepción/conformidad y factura; factura puede postear y quedar bloqueada | Mantiene reconocimiento y pagabilidad separados; exige matching por línea | ADAPT → P2P. Compra directa y servicios necesitan rutas; no forzar documento ficticio |
| Diferencia de cantidad/precio | SAP payment block; tolerancias y excepción | Excepción explícita evita “cuadrar” | ADOPT → Procurement. Tolerancias tipadas/versionadas; SoD inicial visible |
| Cadena documental | SAP document flow y vínculos ERPNext | Grafo derivado permite navegar sin propietario central | ADOPT → UI/proyecciones. Riesgo: workflow engine espejo |
| Fuente a mayor | Oracle subledger drilldown y ERPNext voucher→GL | Identidad causal permite explicar y corregir | ADOPT → Accounting. Acceso se reautoriza en cada dueño |
| Reglas contables por fecha | Oracle accounting methods/rules versionados | Separa operación de interpretación; aumenta gobernanza | ADAPT → Accounting. Rechazar editor/DSL universal inicial |
| Ajuste contable | Oracle subledger journal adjustments; ERPNext reversals | Conserva original y motivo | ADOPT → Accounting. Ajuste manual tipificado/aprobado, nunca editar línea |
| Cierre | NetSuite checklist; ERPNext separa cierre de resultados, Accounting Period y frozen date | Hace visibles tareas y controles diferentes | ADAPT → Accounting cockpit. No copiar checklist fijo |
| Movimiento retroactivo de stock | Dynamics inventory close y ERPNext repost valuation | Reconoce que una fecha anterior cambia coste posterior | ADAPT → Inventory. Recalculo/ajuste necesita spec; no I/O largo dentro de transacción |
| Promedio móvil | Dynamics trata recibos/salidas y diferencias tardías explícitamente | Mantiene operación continua; costos tardíos generan ajuste | ADAPT → Inventory/Accounting. No copiar fórmulas/vendor variance sin validar NPIF |
| Extracto bancario | NetSuite y ERPNext separan importación, matching y conciliación | Preserva observación bancaria y asignación | ADOPT → Treasury. Línea no crea dinero automáticamente |
| Cobro sin factura identificada | ERPNext payment ledger/unallocated payment | Dinero existe antes de asignación | ADOPT → Treasury. Aplicación N:M y reversión explícita |
| Matching bancario | Odoo ordered reconciliation models; ERPNext filtros y revisión | Determinismo primero reduce ambigüedad | ADAPT → Treasury. Rechazar write-off o pago creados automáticamente por regla genérica |
| Excepciones operativas | Oracle accounting automation workspace | Una bandeja prioriza pendientes sin poseerlos | ADOPT → UI. Query/proyección por dueño, no workflow engine |
| Corrección de documentos | ERPNext immutable ledger y devoluciones/créditos | Reversión conserva auditoría | ADOPT → dominios. La forma fiscal concreta se valida en Perú |
| Compra de servicios | ERPNext permite factura directa de utilidad/renta/servicio y conformidad según flujo | Evita SKU de stock para gasto | ADOPT → Procurement. Accounting decide gasto/prepago/activo |
| Vistas/densidad/teclado | Dynamics/Business Central: vistas/filtros guardados y atajos | Reduce repetición; configuración y accesibilidad cuestan | ADOPT → UI. Atajos no confirman acciones peligrosas sin revisión |
| Conteo físico | Patrones ERP de sesión/recuento/ajuste separado | Evita contaminar expectativa y saldo | ADOPT → Inventory. Aprobación distinta futura; autoaprobación visible inicial |
| Plan/cuentas locales | Odoo/ERPNext plantillas por localización | Datos versionables, no `if country` disperso | ADAPT → Accounting/Tax. PCGE oficial y `pcge` prevalecen; no copiar localización extranjera |

## Fuentes primarias consultadas

- SAP: [bloqueo de pago](https://help.sap.com/docs/SAP_S4HANA_ON-PREMISE/af9ef57f504840d2b81be8667206d485/8470b6531de6b64ce10000000a174cb4.html), [factura de proveedor](https://help.sap.com/docs/sap_s4hana_cloud/0e602d466b99490187fcbb30d1dc897c/83d119f21d55487aa237972f22643d02.html).
- Oracle 26B: [método contable](https://docs.oracle.com/en/cloud/saas/financials/26b/faisl/accounting-method.html), [automatización/excepciones](https://docs.oracle.com/en/cloud/saas/financials/26b/faigl/accounting-automation.html), [reconciliación y subledgers](https://docs.oracle.com/en/cloud/saas/financials/26b/faugl/account-reconciliation-and-subledgers.html), [ajustes](https://docs.oracle.com/en/cloud/saas/financials/26b/fausl/how-you-manage-subledger-journal-adjustments.html).
- Microsoft: [costeo](https://learn.microsoft.com/en-us/dynamics365/supply-chain/cost-management/inventory-costing-faq), [inventory close](https://learn.microsoft.com/en-us/dynamics365/supply-chain/cost-management/inventory-close), [restricción de backdating](https://learn.microsoft.com/en-us/dynamics365/business-central/finance-restrict-backdated-cost-postings).
- NetSuite: [banking/reconciliation](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_90174746588.html), [matching](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/article_32131451402.html), [period close](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_N1455781.html), [audit trail](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_N556825.html).
- Odoo 19: [modelos de conciliación](https://www.odoo.com/documentation/19.0/applications/finance/accounting/bank/reconciliation_models.html).
- ERPNext: [purchase invoice](https://docs.frappe.io/erpnext/purchase-invoice), [immutable ledger](https://docs.frappe.io/erpnext/immutable-ledger-in-erpnext), [payment reconciliation](https://docs.frappe.io/erpnext/payment-reconciliation), [period close](https://docs.frappe.io/erpnext/period-closing-voucher), [bank transaction](https://docs.frappe.io/erpnext/bank-transaction).

## Patrones rechazados

No se adopta un ledger universal tipo megatabla, accounting formula DSL, BPM/workflow engine, creación automática de write-offs/pagos, cierre que oculta diferencias, MRP/material ledger, portal proveedor, dimensiones ilimitadas ni microservicios por semejanza empresarial. CasPro necesita el principio de cada técnica y el control mínimo para TILMUX.
