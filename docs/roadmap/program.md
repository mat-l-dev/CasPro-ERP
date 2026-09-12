# CasPro Master Program

Delta acotado posterior al PASS inicial de PR #7: [Case Flow/preview](../specs/cross-cutting/case-flow-preview.md), [automatización](../architecture/automation.md), [Accounting IA/shadow](../accounting/templates-automation-shadow.md). M01 solo primitives de Access/config/jobs/audit; M02–M03 listas y relaciones con objetos existentes; M04 grafo/preview/vista guardada/dossier; M05–M06 expanden compras/tesorería; M07 templates/reglas/recurrencia/AI→draft y shadow on-demand; M08 comparación mensual y lote acotado; M09 nodos Tax. Sin framework vacío M01 ni shadow antes de hechos. Implementar estas capacidades requiere misión/WO autorizadas; D01 controla activación IA, otros pilotos siguen opcionales.

Propietario: Product/Architecture. [ADR-012](../decisions/adr-012-global-documentation-freeze.md) rige la secuencia, [review](../review.md) el estado global y el [índice profundo](../specs/index.md) la readiness por hito. **Deep specs M01–M09 → aceptación independiente del GLOBAL DOCUMENTATION FREEZE → investigación dedicada de skills → regeneración de WOs → implementación expresamente autorizada.** IDs ordenan dependencias de entrega, no aplazan especificación ni prometen fechas. Las tarjetas distinguen resultados futuros de entrega de criterios documentales; no exigen ejecutar esos resultados para revisar el diseño. Los pendientes se clasifican únicamente en [gaps](decisions-gaps.md).

## Cuatro vistas coordinadas

| ID | Product outcome | Documentation gate | Delivery increment | AI execution |
|---|---|---|---|---|
| M00 | Visión y contratos completos antes de código | Auditoría/research, deep specs M01–M09 y candidato exacto para revisión global | Solo documentación | Astra analiza/refuta; aceptación independiente por riesgo; sin runtime IA |
| M01 | Plataforma aislada y recuperable | Runtime/access/audit/operations más enmienda de gobierno propuesta | Bootstrap + entidad/roles/delegación/SoD/configuración/audit + restore base | Sol 5.6 orquesta WOs autorizadas; Astra checkpoint de seguridad |
| M02 | Maestros confiables | Parties/Catalog/import specs | Party, bienes/SKU/precios, import preview | IA no necesaria |
| M03 | Stock/dinero observables y pedido externo durable | Inventory/Treasury/Jumpseller specs | Apertura, movimientos/cobros base, inbox/propuesta | IA no confirma; evaluación futura recopila casos |
| M04 | Primera venta B2C segura | SP2 actualizado + CPE/delivery/UX policy | Pedido, cobro íntegro y reserva habilitan despacho; CPE externo se obtiene en su oportunidad legal, incluso antes del despacho; entrega documental por aprobación | Solo explicación de excepción, si existe piloto separado |
| M05 | Compra a pago controlado | P2P + Tax de compra + conteo specs | PO/receipt/service/CPE/match/payable/payment | Matching IA solo candidato después del determinista |
| M06 | Control financiero y corporate | Contratos Treasury/Corporate; C06 antes de financiar realmente | Extractos, conciliación, cash position; expediente corporate | Piloto opcional D01 de candidatos bancarios, humano obligatorio |
| M07 | Ledger y cierre | Accounting policies/R2R/PCGE specs; C01–03 antes de activar políticas/libro reales | Posting, GL, conciliaciones, períodos, ajustes/cierre | Templates/reglas/recurrencia, AI_SUGGEST→DRAFT y shadow aislado requeridos en diseño; activación D01 |
| M08 | EEFF NPIF completos | Reporting/notas/transición spec + golden cases | Cuatro estados, notas, comparativos y drill-down | Comparador mensual oficial/shadow experimental y explicación con fuente; no sustituye EEFF |
| M09 | Operación tributaria preparada | Contratos tipados RER/IGV/SIRE/SPOT; perfiles reales C07–09 | Registros/conciliaciones/calendario, sin presentación automática | Clasificación candidata de excepciones; sin determinación/presentación |
| M10 | Madurez y expansión por trigger | Gate de necesidad para cada capability | otros canales/marcos por trigger; roles/SoD base pertenecen a M01 y cada flujo, crédito confirmado tiene incremento propio | proveedor se renueva por evaluación, no permanencia automática |

Ruta crítica: **M00 → M01 → M02 → M03 → M04 → M05 → M07 → M08**. M06 puede avanzar tras M04 y alimenta M07; la parte Mutuo no bloquea ventas ni Accounting general si permanece inactiva. M09 investiga en paralelo, pero su salida operativa necesita hechos de M04/M05 y ledger de M07.

Ruta explícita de entrega: **repositorio documental (M00) → primer ERP ejecutable con acceso, maestros y hechos base (M01–M03) → primera venta segura (M04) → operación diaria y conciliación básica (tramo Treasury de M06) → P2P (M05) → ledger/cierre (M07) → EEFF completos (M08) → madurez por trigger (M10)**. La numeración agrupa capacidades; no obliga a esperar M05 para iniciar el control diario de cobros. M09 investiga desde M00 y solo activa salidas cuando sus hechos y políticas estén disponibles.

## Milestone cards

### Delta de secuencia aceptado — amendment B2B y financiación

El [amendment aceptado](../evidence/b2b-financing-amendment.md), conforme a [review](../review.md), conserva numeración y M04 B2C. Se elige **incremento B2B posterior a M04**, con [spec Sales propia](../specs/flows/b2b-commercial-dossier.md), porque requiere misma plataforma/maestros, dinero, reservas y CPE pero añade entrada comercial/OC/revisiones. Ampliar M04 mezclaría aceptación de primera venta por canal con nuevo compromiso B2B; diferirlo íntegro a M10 dejaría sin producto una necesidad confirmada.

Dependencias: M01–M04 para B2B prepago con existencias; tramo Treasury M06 para conciliación bancaria completa. B2B inicial puede entregarse antes de M05 sin compras ni crédito. Crédito B2B tiene incremento obligatorio descrito abajo y activación D03; abastecimiento sin reserva y contraentrega conservan triggers propios. La fecha/orden relativo con M05 se decide al autorizar la entrega; no renumerar M05–M10. Evidencia de salida futura: OC opcional revisada→compromiso→parciales/CPE→cobros/aplicaciones→conciliación y dossier explicable, con casos1–15. No se emite WO ahora.

M06 añade [eventos y estados de financiación](../specs/flows/financing-events-statements.md); pago por cuenta requiere obligación M05 para reconocer su extinción completa, aunque su evidencia pueda capturarse antes. M07–M08 consumen esos hechos sin repetir caja/gasto y concilian sub-saldos. C06 precede a modalidad/financiación real. Registro de entrega externa y Resend opcional pertenecen a Documents M04; WhatsApp Business queda D03/M10 con research actualizado al trigger. M01/M02 conservan contrato.

### Delta propuesto — gobierno y crédito obligatorio

La enmienda de [roles/configuración/políticas](../evidence/governance-roles-configuration-policies.md) obtuvo PASS independiente para el candidato inicial; el delta posterior del propietario requiere re-revisión del nuevo HEAD conforme [review](../review.md). M01 incorpora estructuras de roles/mandatos/SoD/último-admin y configuración versionada; los valores reales se resuelven por [readiness](../product/company-policy-register.md#readiness-de-políticas), no todos antes del primer código. Separación maker/checker existe desde cada operación sensible, con excepción honesta de arranque; no se aplaza la estructura a M10.

**B2B CREDIT: CONFIRMED IMPLEMENTATION REQUIREMENT — REQUIRED TO IMPLEMENT, CONFIGURATION-CONTROLLED ACTIVATION.** Incremento acotado después de B2B prepago y Treasury base/aplicaciones/exposición (tramo M06), sin esperar M10. Conserva [CreditPolicyRevision y comandos](../specs/flows/professional-sales.md#crédito-diseñado-activación-posterior); entrega límites/exposición/aging/holds/override/cobranzas y pruebas B02/B03/B06 pertinentes aun si TILMUX inicia DISABLED. Cierre de entrega del incremento requiere capacidad construida y validada; operación real requiere POL-08 aprobada, permisos, D03 y C05/C07/C08/C13 aplicables. D03 ya no pregunta si construir crédito. OFF global bloquea nueva exposición; subset habilitado no hereda permiso económico. COD no está confirmado obligatorio y conserva trigger separado. No implica nueva venta sin reserva ni nueva política hoy activa.

M03 requiere política de costo/unidades y dinero real cuando aplique; M04 contratos/impuestos; M05 compras/importación; M06 instrumentos/financiación; M07 manual/cierre; M08 presentación; M09 salidas tributarias. C07/C08 se resuelven antes del hecho fiscal dependiente, aunque UI tributaria llegue después. No cambian IDs/conteos de gates ni se emiten WOs.

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
| Canonical docs | model, boundaries, data, charter y [maestros profundos](../specs/milestones/runtime-masters.md) |
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
| UX deliverable / AI role | journals/templates/rules, trial balance, close cockpit and drillback; AI candidates never official-post; shadow on-demand aislado |
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
| UX deliverable / AI role | statement→evidence drilldown and persisted PDF snapshot; comparación mensual shadow separada del paquete, explicación con fuentes |
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

No skill is created in this program. After independent acceptance of the **GLOBAL DOCUMENTATION FREEZE of M01–M09**, conduct a dedicated review of frozen canonical sources and repeated workflows. Derive a short skill only when it changes repeated execution for the better: identify mandatory context, allowed/forbidden decisions, escalation and a concrete behavioral check. Candidate families: orchestration, Accounting, Tax, P2P, Inventory, Treasury, Sales/Documents/Integrations, security/QA, UI and AI assistance. Families are not an instruction to create a file for each domain. Link canonical docs and avoid copying business/regulatory rules. AGENTS remains the router. Regenerate bounded WOs afterward; changing a skill never changes domain truth or authorizes code.

## Secuencia profesional propuesta

La fase vigente se consulta en [review](../review.md): PR #6 integrado y enmienda de gobierno propuesta para revisión independiente. WOs e implementación requieren sus misiones/autorizaciones posteriores. No renumera M01–M10 ni amplía el primer circuito con todas las entregas simultáneamente. [Specs](../specs/index.md#amendment-profesional-propuesto) conservan contratos; siguiente tabla define dependencia de entrega, no WOs.

| Hito/incremento | Resultado y dependencias / aceptación futura |
|---|---|
| M02 | Catálogo/perfiles/UOM/identificadores/kits, Party/supplier y Site; M01 acceso/Documents básicos. Maestros revisados antes de stock/compromiso |
| M03 | Transferencias/serial/tránsito/pool promedio y dinero base; depende M02. Primitivas cuenta/caja permiten posterior caja chica, sin rendición adelantada. Originales privados/derivados/custodia según consumidor |
| M04 y M04+ | M04 B2C prepago preservado. Incremento B2B/cotización/contrato/instalación/logística/reclamos usa M02–04; compra de instalación exige tramo M05; sitio/minería se entrega al pipeline concreto con diseño ya completo |
| M05/M05+ | Necesidad/RFQ/award/PO/match/pago y expediente importación cercano; M03 recibe/valora, Treasury base aplica. C07/C08 antes de la operación real, no esperar UI M09. Costos tardíos y parciales demuestran reconciliación |
| M06 | Conciliación, instrumentos/caja chica/renta/constancia individual; exige fuentes M03–05 según caso. Mapping GL se especifica aquí y se implementa con Accounting M07; no seleccionar GL manual antes del libro |
| Crédito B2B requerido | Implementación obligatoria en incremento posterior a B2B y Treasury/aplicaciones/exposición; inicialmente DISABLED, activación D03 con POL-08/permisos/pruebas. No depende de ser ORG ni activa compromiso sin reserva |
| COD | Diseño preservado, entrega/activación por trigger independiente D03; no mandato confirmado de obligatoriedad |
| M07–M08 | Consumidores nuevos, perfiles/posting/recurrencias acotadas, cierre/auxiliares y cuatro EEFF/notas; hechos M03–06 preservados desde origen |
| M09 | Datos de libros/FX/ND/importaciones desde origen, workspace/exportaciones por obligación. C08 y B08 antes de cada salida; sistemas SUNAT externos |
| M10/D | WhatsApp/otros canales, servicio independiente, RMA completo, consignación/producción y departamentos5–6 por hechos/nueva necesidad; sin módulos anticipados |

Imports y RFQ ya no son futuras incógnitas de producto. Lo no confirmado queda por trigger; no se difiere diseño de un flujo confirmado alegando entrega incremental. B14 invalida las evidencias afectadas del candidato anterior, sin reabrir las cuatro aceptaciones históricas.
