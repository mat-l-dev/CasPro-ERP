# CasPro Master Program

Propietario: Product/Architecture. Estado: programa documental ampliado por [ADR-012](../decisions/adr-012-global-documentation-freeze.md), no autorización de implementación. **Deep specs M01–M09 → GLOBAL DOCUMENTATION FREEZE → skills justificadas → entrega mediante WOs autorizadas.** IDs ordenan dependencias de entrega, no aplazan especificación ni prometen fechas. El [índice profundo](../specs/deep-spec-index.md) dirige revisión transversal.

## Cuatro vistas coordinadas

| ID | Product outcome | Documentation gate | Delivery increment | AI execution |
|---|---|---|---|---|
| M00 | Visión y contratos completos antes de código | Auditoría/research y deep specs M01–M09; freeze GLOBAL pendiente | Solo documentación | Astra analiza/refuta; aceptación independiente por riesgo; sin runtime IA |
| M01 | Plataforma aislada y recuperable | Runtime/access/audit/operations specs congeladas | Bootstrap + entidad/acceso/audit + restore base | Sol 5.6 orquesta WOs; Astra checkpoint de seguridad |
| M02 | Maestros confiables | Parties/Catalog/import specs | Party, bienes/SKU/precios, import preview | IA no necesaria |
| M03 | Stock/dinero observables y pedido externo durable | Inventory/Treasury/Jumpseller specs | Apertura, movimientos/cobros base, inbox/propuesta | IA no confirma; evaluación futura recopila casos |
| M04 | Primera venta B2C segura | SP2 actualizado + CPE/delivery/UX policy | Pedido, cobro íntegro y reserva habilitan despacho; CPE externo se obtiene en su oportunidad legal, incluso antes del despacho; entrega documental por aprobación | Solo explicación de excepción, si existe piloto separado |
| M05 | Compra a pago controlado | P2P + Tax de compra + conteo specs | PO/receipt/service/CPE/match/payable/payment | Matching IA solo candidato después del determinista |
| M06 | Control financiero y corporate | Treasury reconciliation + Corporate/Mutuo validation | Extractos, conciliación, cash position; expediente corporate | Primer piloto de candidatos bancarios, humano obligatorio |
| M07 | Ledger y cierre | Accounting policies/R2R/PCGE specs + revisión profesional | Posting, GL, conciliaciones, períodos, ajustes/cierre | Sugerencia contable opcional sin escritura |
| M08 | EEFF NPIF completos | Reporting/notas/transición spec + golden cases | Cuatro estados, notas, comparativos y drill-down | Explicación de cifras con fuente, revisión humana |
| M09 | Operación tributaria preparada | RER/IGV/SIRE/SPOT policy specs validadas | Registros/conciliaciones/calendario, sin presentación automática | Clasificación candidata de excepciones; sin determinación/presentación |
| M10 | Madurez y expansión por trigger | Gate de necesidad para cada capability | maker/checker, otros canales/marcos solo si activados | proveedor se renueva por evaluación, no permanencia automática |

Ruta crítica: **M00 → M01 → M02 → M03 → M04 → M05 → M07 → M08**. M06 puede avanzar tras M04 y alimenta M07; la parte Mutuo no bloquea ventas ni Accounting general si permanece inactiva. M09 investiga en paralelo, pero su salida operativa necesita hechos de M04/M05 y ledger de M07.

Ruta explícita de entrega: **repositorio documental (M00) → primer ERP ejecutable con acceso, maestros y hechos base (M01–M03) → primera venta segura (M04) → operación diaria y conciliación básica (tramo Treasury de M06) → P2P (M05) → ledger/cierre (M07) → EEFF completos (M08) → madurez por trigger (M10)**. La numeración agrupa capacidades; no obliga a esperar M05 para iniciar el control diario de cobros. M09 investiga desde M00 y solo activa salidas cuando sus hechos y políticas estén disponibles.

## Milestone cards

### M00 — Architecture and roadmap freeze candidate

| Campo | Contrato |
|---|---|
| Business outcome / why now | Una visión empresarial completa antes de código; evita que SP2 se ejecute como única visión |
| Dependencies | Gate 1 cerrado, amendment, SP2 y mandato Grand Master |
| Canonical docs | [capabilities](capabilities.md), este programa, [gaps](decisions-gaps.md), research y arquitecturas enlazadas |
| Research / human decisions | Resolver solo las cinco agrupadas; mantener el resto provisional |
| Regulatory / technical / security gates | Registro con fechas; links/IDs/grafo/contradicciones; sin secretos ni claims ejecutables |
| UX deliverable / AI role | Dirección UX; arquitectura IA provider-neutral, sin ejecución |
| WO family | DOC-M00; ningún WO-SP2 ejecutado |
| Future skill family | Ninguna todavía; derivar `caspro-orchestration` solo después del freeze |
| Orchestrator / implementer / reviewer / Astra | Architect actual / editor documental / revisión adversarial independiente futura / Astra obligatorio |
| Canonical inputs / allowed / forbidden | Docs actuales+fuentes; corregir arquitectura con evidencia; prohibido código/skills finales |
| Validation profile | STATIC-GMP: referencias, fuente/fecha, ownership, diff y refutación |
| Exit criteria / remains | Deep specs M01–M09 revisadas, blockers resueltos y freeze global aceptado sobre candidato exacto; PR abierto. Arquitectura sola no cierra M00 |

### M01 — Runtime, access and recoverability

| Campo | Contrato |
|---|---|
| Business outcome / why now | Base donde ninguna entidad ve o modifica otra y un candidato puede restaurarse |
| Dependencies | GLOBAL DOCUMENTATION FREEZE M01–M09 aceptado y WO autorizada; WO-SP2-01/02 ajustadas al candidato |
| Canonical docs | technology, tenancy-access, security, quality, operations, data |
| Research / human decisions | Hosting/storage, RPO/RTO; no política contable |
| Regulatory / technical / security gates | RLS PROVISIONAL demostrado con rol no-owner/no-BYPASS y entry paths; DB+objects restore; secret isolation |
| UX deliverable / AI role | selector de entidad/acceso accesible; ninguna IA |
| WO family | RUNTIME, ACCESS, AUDIT, RESTORE |
| Future skill family | `caspro-runtime-access`, derivada de spec/gates congelados |
| Orchestrator / implementer / reviewer / Astra | Sol 5.6 / agente código / Sol reviewer separado / Astra checkpoint seguridad |
| Canonical inputs / allowed / forbidden | solo contratos M01; puede crear runtime; no negocio ni Supabase features anticipadas |
| Validation profile | unit/integration PostgreSQL + isolation adversarial + restore rehearsal |
| Exit criteria / remains | roles/tenancy/audit/restore demostrados; maestros y operación ausentes |

### M02 — Party and goods masters

| Campo | Contrato |
|---|---|
| Business outcome / why now | Identidades, bienes y precios versionados antes de pedidos/stock |
| Dependencies | M01 |
| Canonical docs | model, boundaries, data, charter y [maestros profundos](../specs/runtime-masters.md) |
| Research / human decisions | atributos reales mínimos y unidades; no crear Customer duplicado |
| Regulatory / technical / security gates | PII/identidad fiscal, exactitud Decimal, bulk validate→preview→confirm |
| UX deliverable / AI role | selectores, búsqueda, import preview; IA fuera |
| WO family | PARTIES, CATALOG, BULK-IMPORT |
| Future skill family | `caspro-master-data`, sin copiar reglas empresariales |
| Orchestrator / implementer / reviewer / Astra | Sol / agente código / Sol reviewer / Astra solo si cambia frontera |
| Canonical inputs / allowed / forbidden | implementar maestros; prohibido stock/CRM/servicios vendidos/mappings futuros |
| Validation profile | constraints, isolation, versioning, CSV adversarial, keyboard |
| Exit criteria / remains | masters usables y trazables; Inventory/Sales no construidos |

### M03 — Operational stock, money and channel intake

| Campo | Contrato |
|---|---|
| Business outcome / why now | Ver existencias/coste y cobros evidenciados; recibir pedidos sin aceptarlos |
| Dependencies | M02; infraestructura durable M01 |
| Canonical docs | inventory-costing, treasury-finance, SP2 integrations/matrix |
| Research / human decisions | precisión/coste inicial, evidencia de cobro, sandbox Jumpseller |
| Regulatory / technical / security gates | UNKNOWN; promedio móvil; webhook auth/inbox/dedupe; PAID≠money; RLS extendida |
| UX deliverable / AI role | aperturas, pendientes de mapping/cobro; IA no necesaria |
| WO family | INVENTORY-BASE, TREASURY-BASE, JUMPSELLER-INBOUND |
| Future skill family | `caspro-inventory-treasury-integration`, después de las specs locales |
| Orchestrator / implementer / reviewer / Astra | Sol / agentes por frontera / Sol integration reviewer / Astra en stock+money gate |
| Canonical inputs / allowed / forbidden | construir hechos base; prohibido aceptar/dispatch, PUT positivo o auto-money |
| Validation profile | PostgreSQL races, conservation/property tests, signed replay, provider contract sandbox |
| Exit criteria / remains | P/N/cost and confirmed money explainable; order only proposal; sale circuit remains |

### M04 — Safe first B2C sale

| Campo | Contrato |
|---|---|
| Business outcome / why now | Primera venta bienes con pago íntegro, stock, entrega y CPE externo trazables |
| Dependencies | M03; CPE policy and storage/email gates |
| Canonical docs | all SP2 specs, integrations, invariants, UI, NPIF event needs |
| Research / human decisions | momento/artefactos CPE, safe email config, stock publication gate |
| Regulatory / technical / security gates | no SUNAT emission; coverage full; reservation/dispatch concurrency; email idempotency/HOLD; authorization |
| UX deliverable / AI role | work queue, document flow, split preview, keyboard-safe confirmation; AI read-only explanation only |
| WO family | SALES-ACCEPT, RESERVE-DISPATCH, RETURNS, CPE-LINK, DOCUMENT-DELIVERY, STOCK-PUBLISH |
| Future skill family | `caspro-sales-documents`, limitada a SP2 congelado |
| Orchestrator / implementer / reviewer / Astra | Sol / agents per WO / separate Sol + adversarial / Astra milestone checkpoint |
| Canonical inputs / allowed / forbidden | SP2 exact commands; no credit/service sales/other channels/real SUNAT submission |
| Validation profile | full B2C E2E, concurrent payment/stock/returns, webhook/email ambiguity, accessibility/browser, restore |
| Exit criteria / remains | synthetic then authorized pilot sale; P2P/ledger/tax filing remain |

### M05 — Controlled Procure-to-Pay

| Campo | Contrato |
|---|---|
| Business outcome / why now | Comprar mercancía y servicios y pagar solo obligaciones válidas |
| Dependencies | M04 operation stable; M02/M03 |
| Canonical docs | procure-to-pay, inventory-costing, treasury-finance, tax architecture |
| Research / human decisions | direct-buy policy, tolerances, approvals, service acceptance, SPOT applicability |
| Regulatory / technical / security gates | CPE supplier, tax evidence, match/block, bancarization, concurrency and SoD exception |
| UX deliverable / AI role | PO chain, match exception cockpit, batch review; AI candidate only after deterministic rules |
| WO family | PURCHASE, RECEIPT, SERVICE-ACCEPTANCE, AP-INVOICE, MATCH, AP-PAYMENT, RETURNS |
| Future skill family | `caspro-procure-to-pay`, después de validación Tax/profesional |
| Orchestrator / implementer / reviewer / Astra | Sol / agents per owner / Sol reviewer / Astra P2P/accounting boundary checkpoint |
| Canonical inputs / allowed / forbidden | goods+nonstock services; no RFQ/portal/workflow engine unless separately triggered |
| Validation profile | line-level partials/tolerances/duplicates, stock-money conservation, Tax evidence and E2E |
| Exit criteria / remains | chain navigable and reconciled; formal postings may queue until M07 |

### M06 — Treasury reconciliation and Corporate

| Campo | Contrato |
|---|---|
| Business outcome / why now | Control diario de bancos y expediente societario/financiación sin confusiones |
| Dependencies | M04; P2P payment consumers for full AP path |
| Canonical docs | treasury-finance, corporate architecture, AI assistance, normative N016–N019 |
| Research / human decisions | formato/evidencia bancaria; mutuo validado profesionalmente durante documentación y antes de financiación, aunque su implementación sea M06; provider/VPS solo piloto separado |
| Regulatory / technical / security gates | bancarization, related-party facts, beneficial owner, data minimization, no AI writes |
| UX deliverable / AI role | reconciliation split view, candidates/contraevidence; first synthetic AI pilot |
| WO family | STATEMENT-IMPORT, RECONCILIATION, CASH-POSITION, CORPORATE-RECORDS; MUTUO only after approval |
| Future skill family | `caspro-treasury-corporate`; piloto IA conserva skill/evaluación separada si se aprueba |
| Orchestrator / implementer / reviewer / Astra | Sol / agents / financial+security reviewer / Astra required for Mutuo and AI pilot |
| Canonical inputs / allowed / forbidden | statement lines/candidates; forbidden auto-confirmation, transfer execution, unvalidated loan |
| Validation profile | N:M/replay/unreconcile, ambiguity/abstention, privacy/prompt injection, professional checklist |
| Exit criteria / remains | daily reconciliation explainable; Mutuo can remain not activated; ledger follows M07 |

### M07 — Accounting ledger and close

| Campo | Contrato |
|---|---|
| Business outcome / why now | Convertir hechos de ventas/compras/tesorería/inventario en libros reproducibles |
| Dependencies | M04/M05 source facts; M06 bank controls useful; approved policies/opening |
| Canonical docs | accounting architecture, normative register/matrix, inventory, Tax boundary |
| Research / human decisions | professional policy catalog, PCGE version, opening, RER presentation, precision |
| Regulatory / technical / security gates | balanced immutable postings; period locks; source version; PCGE adapter; separation Tax; approvals |
| UX deliverable / AI role | journals, trial balance, close cockpit and drillback; AI candidates never post |
| WO family | ACCOUNTING-CORE, POSTING-POLICIES, SUBLEDGER-CONTROLS, PERIOD-CLOSE |
| Future skill family | `caspro-accounting`, enlaza políticas vigentes sin copiarlas |
| Orchestrator / implementer / reviewer / Astra | Sol / accounting implementer / accounting reviewer + professional / Astra mandatory |
| Canonical inputs / allowed / forbidden | approved policies/events; forbidden operational module posting, generic formula DSL, silent retro edits |
| Validation profile | golden events, balance/property, idempotence, close/reopen/races, framework/version mutation |
| Exit criteria / remains | trial balance and reconciliations reproduce; formal package M08 remains |

### M08 — Complete NPIF reporting

| Campo | Contrato |
|---|---|
| Business outcome / why now | Paquete formal completo, comparativo y explicable sin Excel obligatorio |
| Dependencies | M07 closed synthetic period; approved NPIF eligibility/policies |
| Canonical docs | npif-reporting, accounting architecture, normative register |
| Research / human decisions | note applicability, EFE mapping, authorization, materiality and exact comparative transition |
| Regulatory / technical / security gates | NPIF 18 sections; four owner-required statements+notes; reproducibility; document authorization |
| UX deliverable / AI role | statement→evidence drilldown and persisted PDF snapshot; IA may explain only sourced figures |
| WO family | REPORTING-MAPPINGS, STATEMENTS, NOTES, PACKAGE, DRILLDOWN |
| Future skill family | `caspro-financial-reporting`, solo con políticas NPIF aprobadas |
| Orchestrator / implementer / reviewer / Astra | Sol / reporting implementer / accountant reviewer / Astra final financial checkpoint |
| Canonical inputs / allowed / forbidden | frozen ledger/policies; no mixed-framework compliance or AI-authored compliance claim |
| Validation profile | synthetic full year, cross-statement reconciliations, comparatives, permissions, reproducible snapshot |
| Exit criteria / remains | complete approved synthetic package; real operation and framework transitions need own gate |

### M09 — Tax operations foundation

| Campo | Contrato |
|---|---|
| Business outcome / why now | Preparar/reconciliar obligaciones peruanas desde hechos íntegros |
| Dependencies | Research starts M00; operational output after M04/M05/M07 |
| Canonical docs | tax architecture, normative register, CPE specs |
| Research / human decisions | verify RUC/RER/SIRE, operation matrix, SPOT/padrones, filing mandate |
| Regulatory / technical / security gates | sources+vigency; book≠tax; no automatic SUNAT write; secrets/evidence |
| UX deliverable / AI role | tax exceptions, registers and reconciliation; AI classifies candidates only |
| WO family | TAX-PROFILE, IGV, SIRE-PREP, SPOT, TAX-RECONCILIATION, CALENDAR |
| Future skill family | `caspro-tax-peru`, deriva reglas verificadas por período y fuente |
| Orchestrator / implementer / reviewer / Astra | Sol / tax implementer / professional+Sol / Astra required at regulatory gate |
| Canonical inputs / allowed / forbidden | verified policies/facts; no invented casillas, submission or tax-driven mutation of ledger |
| Validation profile | period examples, source-version mutation, CPE/ledger/register reconciliation, access |
| Exit criteria / remains | outputs prepared/reviewable; actual filing/integration separately authorized |

### M10 — Triggered maturity

| Campo | Contrato |
|---|---|
| Business outcome / why now | Evolucionar sin reconstrucción cuando volumen, entidad, marco o riesgo cambie |
| Dependencies | Stable operation and measured trigger |
| Canonical docs | capabilities, gaps, updated research and new local spec |
| Research / human decisions | concrete trigger and business case; framework/channel/provider choice |
| Regulatory / technical / security gates | new applicable set, migration, SoD, scale, portability |
| UX deliverable / AI role | measured tasks; provider renewed by benchmark |
| WO family | created per activated capability, never empty package |
| Future skill family | Derivar únicamente la capability activada; no paquete genérico de madurez |
| Orchestrator / implementer / reviewer / Astra | Sol / chosen implementer / independent reviewer / Astra when high-risk boundary changes |
| Canonical inputs / allowed / forbidden | frozen current truth+trigger; forbidden speculative platform/microservice/general engine |
| Validation profile | migration/backward compatibility/operational rehearsal by risk |
| Exit criteria / remains | trigger satisfied and capability deployed; other concepts remain dormant |

## Future skill derivation, after freeze

No skill is created in this program. After the **GLOBAL DOCUMENTATION FREEZE of M01–M09**, derive a short skill only if repeated execution benefits from it. Candidate families: orchestration, Accounting, Tax, P2P, Inventory, Treasury, Sales/Documents/Integrations, security/QA, UI and AI assistance. Each skill links canonical docs, names allowed decisions/escalations and contains no copied business or regulatory rules. AGENTS remains the router. Changing a skill never changes the domain truth.
