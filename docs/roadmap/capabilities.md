# Master Capability Map

Este mapa asigna propósito, dueño, dependencias, hito y trigger; no conserva otra readiness. La matriz vigente vive únicamente en [deep-spec-index](../specs/index.md), el estado global en [review](../review.md) y los pendientes en [gaps](decisions-gaps.md). El mapa no autoriza tablas, carpetas ni implementación.

| Capability / purpose | Owner | Inputs → outputs | Dependencies | Value / risk / regulatory sensitivity | Phase / required spec / expansion trigger |
|---|---|---|---|---|---|
| Identity/session | Identity | credential→principal/session | runtime | acceso; HIGH security | M01 / auth spec / nuevos métodos |
| Legal entity directory | Organization | evidence→entity/context | Identity | separación; HIGH legal | M01 / entity spec / otra entidad |
| Membership/capability | Access | grants→authorized context | Identity, Organization, Audit | deny-by-default; HIGH | M01 / access spec / maker-checker |
| Audit | Audit | actor+transition→append-only event | access primitives | accountability; HIGH | M01 / audit spec / external archive |
| Private documents | Documents | bytes+metadata→version/evidence | Access, object storage | evidence; HIGH privacy/retention | M03 / storage spec / volume/retention |
| Document delivery | Documents | deliverable+approval→email attempt/result | email adapter | CPE delivery; HIGH | M04 / SP2 / new channel |
| Parties | Parties | identity evidence→roles/version | Access, Documents | one counterparty; MEDIUM | M02 / master spec / richer CRM |
| Goods catalog | Catalog | product/SKU/unit/price→version | Access | commerce; MEDIUM | M02 / SP2 / variants/serials |
| Purchased service concepts | Procurement | description/period→nonstock line | Parties, Accounting policy later | expenses; MEDIUM tax | M05 / P2P spec / recurring contracts |
| Operational inventory | Inventory | movements→positions/kardex | Catalog | fulfilment; HIGH money/stock | M03 / inventory spec / multiwarehouse |
| Moving average cost | Inventory | entry costs→output cost | operational inventory | margin/COGS source; HIGH accounting | M03 / costing spec / landed costs |
| Physical count | Inventory | plan/count→difference/adjustment | inventory, Audit | integrity; HIGH | M03/M05 / inventory-deep / scanners |
| ATS/publication | Inventory/integration | eligible stock+buffer→Jumpseller quantity | reservations, channel | availability; HIGH external | M03–M04 / SP2, B11/C11 / second channel |
| External order intake | Sales/Jumpseller | webhook/API→durable proposal | inbox, Parties, Catalog | first sales; HIGH | M03 / SP2 / second channel |
| B2C sale/dispatch/return | Sales coordinator | order+money+stock→sale/delivery/returns | Treasury, Inventory | operation; CRITICAL | M04 / SP2 / B2B/credit |
| Commercial obligation | Sales/Procurement | document terms→receivable/payable | Parties | settlement; HIGH | M04/M05 / domain specs / credit terms |
| CPE sales/supplier dossiers | Sales/Procurement | external identity+facts→dossier | Documents, Tax | fiscal evidence; HIGH | M04/M05 / CPE y P2P specs, C07 / acquisition API |
| Purchase order/receipt | Procurement/Inventory | demand→commitment/receipt | Parties, Catalog | replenishment; HIGH | M05 / P2P spec / approvals/RFQ |
| Matching/payability | Procurement | PO+receipt/service+CPE→match/block | Tax, Documents | prevent wrong pay; HIGH | M05 / tolerance spec / automation |
| Accounts/movements | Treasury | bank/cash evidence→confirmed movement | Parties, Documents | money truth; CRITICAL | M03 / SP2 / multiple banks |
| Applications/refunds | Treasury | movement+target→settlement | commercial obligations | outstanding truth; CRITICAL | M04/M05 / SP2 y Procurement settlement / nuevos tipos de liquidación |
| Statement reconciliation | Treasury | statement+movements→matches/exceptions | import, Audit | daily control; CRITICAL | M06 / bank spec / feeds |
| Corporate records | Corporate capability | acts/contracts→legal facts | Organization, Parties, Documents | governance; HIGH legal | M06 / corporate spec / more shareholders |
| Related-party financing | Corporate/Treasury | approved contract+bank events→loan lifecycle | Accounting, Tax | funding; CRITICAL | M06 / professional mutuo spec / actual agreement |
| Accounting policies/posting | Accounting | source facts+policy→interpretations/asientos | domains, PCGE adapter | financial truth; CRITICAL | M07 / policy catalog / new fact/framework |
| GL/subledgers/reconciliation | Accounting | postings→balances/control | policies, periods | explainability; CRITICAL | M07 / R2R spec / scale |
| Close/adjust/reverse | Accounting | open balances→approved close | reconciliations | reliable period; CRITICAL | M07 / close spec / maker-checker |
| NPIF package | Accounting | closed ledger→4 statements+notes | mappings, Documents | formal reporting; CRITICAL | M08 / reporting spec / first real period |
| Framework transition | Accounting | prior framework→reconciled opening | normative register | growth; HIGH | M07/M08 / opening/transition specs; M10 / marco destino completo por trigger / eligibility or formal choice |
| Tax profile/rules | Tax | entity+period+law→applicable policy | Research | compliance; CRITICAL | M09 / RER policy / regime change |
| IGV/SIRE/reconciliation | Tax | CPE+facts+ledger→tax registers/positions | Sales, Procurement, Accounting | compliance; CRITICAL | M09 / tax specs / obligation verified |
| Operational inbox | UI projection | owner exceptions→prioritized queue | public queries | daily efficiency; HIGH leakage | M04+ / query/UX spec / volume |
| Search/document flow | UI projection | authorized indexes/links→results/graph | all owners | explainability; HIGH privacy | M04+ / search spec / external engine |
| CSV/Excel import | each owner | file→validate/preview/confirm | Documents, Audit | onboarding; HIGH bulk | M03/M05 / per-domain schema / volume |
| AI suggestion service | AI platform/domain | minimized case→candidate/evidence | provider adapter, evaluation | efficiency; CRITICAL misuse | M06 pilot / PROVISIONAL / AI pilot spec / proven KPI |
| Backup/restore | Operations | DB+objects+config→recoverable service | deployment | continuity; CRITICAL | M01/M04 gates / restore spec / target RPO/RTO |

## Capacidades contables explícitas del primer paquete

Este desglose hereda owner Accounting, M07 para medición/registro y M08 para presentación, contratos de diseño y gates de activación C01/C03 de [M07](../specs/milestones/accounting-deep.md), [NPIF](../accounting/npif-policy-catalog.md) y [M08](../specs/acceptance/reporting-goldens.md). No exige activos, trabajadores o contratos ficticios: cuando no existe el hecho, se conserva trigger y se documenta inaplicabilidad. Los datos fuente los aportan los dueños indicados; ningún auxiliar crea dinero ni stock.

| Capability / purpose | Inputs / dependency → outputs | Trigger / valor / riesgo y política |
|---|---|---|
| PPE / depreciación por componentes | Procurement y disponibilidad para uso, coste/vida/residual → auxiliar, cargos, bajas, roll-forward y nota | Bien controlado usado más de un período; HIGH; NPIF12, no tasas fiscales automáticas |
| Intangibles / amortización | Derechos, control, fases/costes y vida → reconocimiento o gasto, auxiliar y nota | Software/licencia/desarrollo propio real; HIGH; política supletoria NPIF3.1 por edición, no capitalizar suscripciones por nombre |
| Devengos y gastos acumulados | Servicio recibido/período/estimación Procurement → pasivo, gasto y reversión/aplicación posterior | Obligación antes del CPE/pago; HIGH; no esperar factura para toda interpretación |
| Anticipos y gastos pagados por adelantado | Treasury y período/condición contractual → activo/obligación y consumo trazable | Pago antes de entrega/servicio; HIGH; no gasto/ingreso automático al cobrar/pagar |
| Provisiones y contingencias | Legal/Corporate, obligación/probabilidad/estimación → medición o revelación y revisiones | Obligación incierta o exposición real; CRITICAL; no convertir ejemplo 51% en umbral universal |
| Arrendamientos | Contrato/opción/cuotas Procurement → calendario contable, gasto o PPE/pasivo y notas | Contrato real; HIGH; NPIF17, no NIIF16 universal |
| Beneficios a empleados | Servicios y derechos devengados → obligaciones, gasto y nota | Existencia de trabajadores/beneficio; HIGH; NPIF15, sin construir nómina completa por anticipado |
| FX y diferencias de cambio | Treasury/fechas/moneda/fuente de tipos → reexpresión y resultados por versión | Hechos/saldos en moneda extranjera; HIGH; NPIF2.54–55 y aprobación de ambigüedades |
| Inversiones e instrumentos financieros | Contratos/coste/cotización/plazo y Treasury → auxiliares, intereses/deterioro y nota | Instrumento real; HIGH; NPIF9/10/14, no importar medición NIIF9 automáticamente |
| Inventario, COGS y VNR | Inventory coste y movimientos, vendibilidad/evidencia comercial → COGS, correctora de deterioro y conciliación | Stock propio; CRITICAL; VNR/deterioro no modifica kardex físico ni coste operativo |
| CxC/CxP y deterioro | Obligaciones comerciales, aplicaciones y estimaciones → saldos auxiliares/control y notas | Derecho/obligación real; CRITICAL; ledger no sustituye saldo operativo de Treasury |
| Patrimonio / resultados acumulados | Corporate acuerdos, aportes sustentados, resultado y distribuciones → ECP y nota | Constitución, cierre o acuerdo real; CRITICAL; pago del socio no se vuelve ingreso/aporte por identidad |
| Partes relacionadas | Corporate vínculos/contratos y transacciones → disclosure y evaluaciones contables | Relación acreditada; HIGH; NPIF3.1 supletoria, Tax32-A tiene evaluación separada |
| Impuesto corriente / diferido y RER | Tax determinaciones/base fiscal y política Accounting → gasto/pasivo/activo solo si aplica | Tributo/hecho/marco aplicable; CRITICAL; RER no igual impuesto a ganancia ni genera diferido por defecto |
| Apertura / ESFA / transición | Balance sustentado, hechos, marco y elecciones → ajustes/conciliación versionados | Primera adopción o cambio formal; CRITICAL; primer uso del ERP no equivale a primera adopción |
| Cierre / correcciones / hechos posteriores | Conciliaciones, errores/estimaciones y autorización → paquete cerrado, ajustes y nueva versión | Período y materialidad aprobados; CRITICAL; NPIF errores no hereda retrospectividad NIC8 |
| Revelaciones / comparativos / cuatro EEFF | GL, auxiliares, narrativas y mappings → paquete completo y evidencia navegable | Cada cierre; CRITICAL; faltante no cero, profesional valida notas, sin dependencia de Excel |

## Expansion rule

Capabilities assigned to a later triggered scope preserve only source facts and an explicit trigger. They do not justify a package, field, provider or abstraction today. Every activation updates this map, produces a local spec and names its validation profile.
