# Master Capability Map

Estado: visión objetivo, no módulos implementados. `Phase` referencia [programa](program.md). `Readiness`: `SPECIFIED`, `ARCHITECTED`, `RESEARCHED`, `CONCEPT`, `BLOCKED`. Cada capability se construye solo en su hito y spec; el mapa no autoriza tablas o carpetas.

| Capability / purpose | Owner | Inputs → outputs | Dependencies | Value / risk / regulatory sensitivity | Phase / status / required spec / expansion trigger |
|---|---|---|---|---|---|
| Identity/session | Identity | credential→principal/session | runtime | acceso; HIGH security | M01 / ARCHITECTED / auth spec / nuevos métodos |
| Legal entity directory | Organization | evidence→entity/context | Identity | separación; HIGH legal | M01 / ARCHITECTED / entity spec / otra entidad |
| Membership/capability | Access | grants→authorized context | Identity, Organization, Audit | deny-by-default; HIGH | M01 / ARCHITECTED / access spec / maker-checker |
| Audit | Audit | actor+transition→append-only event | access primitives | accountability; HIGH | M01 / ARCHITECTED / audit spec / external archive |
| Private documents | Documents | bytes+metadata→version/evidence | Access, object storage | evidence; HIGH privacy/retention | M03 / SPECIFIED / storage spec / volume/retention |
| Document delivery | Documents | deliverable+approval→email attempt/result | email adapter | CPE delivery; HIGH | M04 / SPECIFIED / SP2 / new channel |
| Parties | Parties | identity evidence→roles/version | Access, Documents | one counterparty; MEDIUM | M02 / ARCHITECTED / master spec / richer CRM |
| Goods catalog | Catalog | product/SKU/unit/price→version | Access | commerce; MEDIUM | M02 / SPECIFIED / SP2 / variants/serials |
| Purchased service concepts | Procurement | description/period→nonstock line | Parties, Accounting policy later | expenses; MEDIUM tax | M05 / ARCHITECTED / P2P spec / recurring contracts |
| Operational inventory | Inventory | movements→positions/kardex | Catalog | fulfilment; HIGH money/stock | M03 / ARCHITECTED / inventory spec / multiwarehouse |
| Moving average cost | Inventory | entry costs→output cost | operational inventory | margin/COGS source; HIGH accounting | M03 / ARCHITECTED / costing spec / landed costs |
| Physical count | Inventory | plan/count→difference/adjustment | inventory, Audit | integrity; HIGH | M05 / ARCHITECTED / count spec / scanners |
| ATS/publication | Inventory/integration | eligible stock+buffer→Jumpseller quantity | reservations, channel | availability; HIGH external | M03–M04 / SPECIFIED BUT GATED / SP2 / second channel |
| External order intake | Sales/Jumpseller | webhook/API→durable proposal | inbox, Parties, Catalog | first sales; HIGH | M03 / SPECIFIED / SP2 / second channel |
| B2C sale/dispatch/return | Sales coordinator | order+money+stock→sale/delivery/returns | Treasury, Inventory | operation; CRITICAL | M04 / SPECIFIED / SP2 / B2B/credit |
| Commercial obligation | Sales/Procurement | document terms→receivable/payable | Parties | settlement; HIGH | M04/M05 / ARCHITECTED / domain specs / credit terms |
| CPE sales/supplier dossiers | Sales/Procurement | external identity+facts→dossier | Documents, Tax | fiscal evidence; HIGH | M04/M05 / SPECIFIED partial / policy spec / acquisition API |
| Purchase order/receipt | Procurement/Inventory | demand→commitment/receipt | Parties, Catalog | replenishment; HIGH | M05 / ARCHITECTED / P2P spec / approvals/RFQ |
| Matching/payability | Procurement | PO+receipt/service+CPE→match/block | Tax, Documents | prevent wrong pay; HIGH | M05 / ARCHITECTED / tolerance spec / automation |
| Accounts/movements | Treasury | bank/cash evidence→confirmed movement | Parties, Documents | money truth; CRITICAL | M03 / SPECIFIED base / SP2 / multiple banks |
| Applications/refunds | Treasury | movement+target→settlement | commercial obligations | outstanding truth; CRITICAL | M04/M05 / SPECIFIED B2C / settlement spec / AP |
| Statement reconciliation | Treasury | statement+movements→matches/exceptions | import, Audit | daily control; CRITICAL | M06 / ARCHITECTED / bank spec / feeds |
| Corporate records | Corporate capability | acts/contracts→legal facts | Organization, Parties, Documents | governance; HIGH legal | M06 / ARCHITECTED / corporate spec / more shareholders |
| Related-party financing | Corporate/Treasury | approved contract+bank events→loan lifecycle | Accounting, Tax | funding; CRITICAL | M06 / BLOCKED / professional mutuo spec / actual agreement |
| Accounting policies/posting | Accounting | source facts+policy→interpretations/asientos | domains, PCGE adapter | financial truth; CRITICAL | M07 / ARCHITECTED / policy catalog / new fact/framework |
| GL/subledgers/reconciliation | Accounting | postings→balances/control | policies, periods | explainability; CRITICAL | M07 / ARCHITECTED / R2R spec / scale |
| Close/adjust/reverse | Accounting | open balances→approved close | reconciliations | reliable period; CRITICAL | M07 / ARCHITECTED / close spec / maker-checker |
| NPIF package | Accounting | closed ledger→4 statements+notes | mappings, Documents | formal reporting; CRITICAL | M08 / ARCHITECTED / reporting spec / first real period |
| Framework transition | Accounting | prior framework→reconciled opening | normative register | growth; HIGH | later / CONCEPT / transition spec / >150 UIT or choice |
| Tax profile/rules | Tax | entity+period+law→applicable policy | Research | compliance; CRITICAL | M09 / RESEARCHED / RER policy / regime change |
| IGV/SIRE/reconciliation | Tax | CPE+facts+ledger→tax registers/positions | Sales, Procurement, Accounting | compliance; CRITICAL | M09 / RESEARCHED / tax specs / obligation verified |
| Operational inbox | UI projection | owner exceptions→prioritized queue | public queries | daily efficiency; HIGH leakage | M04+ / ARCHITECTED / query/UX spec / volume |
| Search/document flow | UI projection | authorized indexes/links→results/graph | all owners | explainability; HIGH privacy | M04+ / ARCHITECTED / search spec / external engine |
| CSV/Excel import | each owner | file→validate/preview/confirm | Documents, Audit | onboarding; HIGH bulk | M03/M05 / ARCHITECTED / per-domain schema / volume |
| AI suggestion service | AI platform/domain | minimized case→candidate/evidence | provider adapter, evaluation | efficiency; CRITICAL misuse | M06 pilot / PROVISIONAL / AI pilot spec / proven KPI |
| Backup/restore | Operations | DB+objects+config→recoverable service | deployment | continuity; CRITICAL | M01/M04 gates / ARCHITECTED / restore spec / target RPO/RTO |

## Expansion rule

Capabilities marked later/CONCEPT preserve only source facts and an explicit trigger. They do not justify a package, field, provider or abstraction today. Every activation updates this map, produces a local spec and names its validation profile.
