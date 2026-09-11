# Reorganización documental posterior al freeze

**POST-FREEZE NON-SEMANTIC DOCUMENTATION IA AMENDMENT.** Registro de inventario, migración y verificación editorial; clase primaria G (AUDIT / REVIEW EVIDENCE), owner Architecture. No posee reglas ni estado global: consultar [review](../review.md). No crea skills, Work Orders ni código.

## A. Merge del freeze

PR #2 se fusionó mediante merge commit `dbb1224d99f4dbdac61da25daf32f1fed872b4fa`, con padres `5c925e2acb1487c68dab2738e969cef6afe33539` y `6bec2f78b6a0df3def503f674858eb7d769b465b`. Main/origin-main quedaron en ese commit, tree `66184f5714d0130f6cc14a306160bf7a5472ab6c`, sin diferencia local/remota. PR2: MERGED, 2026-09-11T20:53:23Z. La rama de esta enmienda es `docs/final-information-architecture`; su PR quedará abierto.

## B. Inventario inicial completo

79 Markdown rastreados en la baseline main anterior. Cada fila tiene exactamente una clase primaria; que contenga un resumen o una referencia secundaria no cambia su función. Paths originales en código son identificadores históricos del inventario, no enlaces de navegación. El destino se usa en el índice final.

| Clase | Función | Antes |
|---|---|---:|
| A | ENTRYPOINT / NAVIGATION | 4 |
| B | CURRENT CANONICAL CONTRACT | 20 |
| C | ADR / DECISION RATIONALE | 12 |
| D | DEEP SPECIFICATION | 14 |
| E | CURRENT ROADMAP / GATE | 4 |
| F | ACTIVE RESEARCH / NORMATIVE EVIDENCE | 7 |
| G | AUDIT / REVIEW EVIDENCE | 4 |
| H | HISTORICAL / SUPERSEDED MATERIAL | 3 |
| I | AGENT / CONTRIBUTOR OPERATING INSTRUCTION | 7 |
| J | QUALITY / SECURITY / OPERATIONS CONTRACT | 4 |

| CURRENT PATH (baseline) | TITLE | PRIMARY CLASS | OWNER | AUTHORITATIVE? | CURRENT OR HISTORICAL? | CONSUMERS | PROPOSED ACTION | PROPOSED PATH |
|---|---|---|---|---|---|---|---|---|
| `.ai/README.md` | Roles, carga y configuración de modelos | I | Architecture / coordinación IA | Sí, en su alcance | CURRENT | Agentes / contribuidores | KEEP; enlaces si afectados | `.ai/README.md` |
| `.ai/review.md` | Rúbrica única de revisión y refutación | I | Architecture / coordinación IA | Sí, en su alcance | CURRENT | Agentes / contribuidores | KEEP; enlaces si afectados | `.ai/review.md` |
| `.ai/work-order.md` | Plantilla de Work Order | I | Architecture / coordinación IA | Sí, en su alcance | CURRENT | Agentes / contribuidores | KEEP; enlaces si afectados | `.ai/work-order.md` |
| `.ai/workflow.md` | Workflow mínimo | I | Architecture / coordinación IA | Sí, en su alcance | CURRENT | Agentes / contribuidores | KEEP; enlaces si afectados | `.ai/workflow.md` |
| `AGENTS.md` | CasPro — mapa para agentes | I | Architecture / coordinación IA | Sí, en su alcance | CURRENT | Agentes / contribuidores | KEEP; enlaces si afectados | `AGENTS.md` |
| `CLAUDE.md` | Adaptador de Claude | I | Architecture / coordinación IA | Sí, en su alcance | CURRENT | Agentes / contribuidores | KEEP; enlaces si afectados | `CLAUDE.md` |
| `GEMINI.md` | Adaptador de Gemini | I | Architecture / coordinación IA | Sí, en su alcance | CURRENT | Agentes / contribuidores | KEEP; enlaces si afectados | `GEMINI.md` |
| `README.md` | CasPro ERP | A | Architecture | No; navegación/evidencia | CURRENT | Todos, según ruta | SPLIT historia; entrada breve | `README.md` |
| `docs/accounting/architecture.md` | Arquitectura objetivo de Accounting | B | Accounting | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | KEEP; enlaces si afectados | `docs/accounting/architecture.md` |
| `docs/accounting/npif-policy-catalog.md` | NPIF — catálogo de políticas y refutación de la guía | B | Accounting | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | KEEP; enlaces si afectados | `docs/accounting/npif-policy-catalog.md` |
| `docs/accounting/npif-reporting.md` | Información financiera inicial bajo NPIF | B | Accounting | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | KEEP; enlaces si afectados | `docs/accounting/npif-reporting.md` |
| `docs/architecture/ai-assistance.md` | Arquitectura de IA asistida | B | Architecture | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | KEEP; enlaces si afectados | `docs/architecture/ai-assistance.md` |
| `docs/architecture/boundaries.md` | Propietarios y dependencias | B | Architecture | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | KEEP; enlaces si afectados | `docs/architecture/boundaries.md` |
| `docs/architecture/data.md` | Datos, precisión y evolución | B | Architecture | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | KEEP; enlaces si afectados | `docs/architecture/data.md` |
| `docs/architecture/integrations.md` | Integraciones, eventos y trabajo durable | B | Architecture | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | KEEP; enlaces si afectados | `docs/architecture/integrations.md` |
| `docs/architecture/overview.md` | Arquitectura general | B | Architecture | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | KEEP; enlaces si afectados | `docs/architecture/overview.md` |
| `docs/architecture/technology.md` | Evaluación tecnológica al 2026-09-11 | B | Architecture | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | KEEP; enlaces si afectados | `docs/architecture/technology.md` |
| `docs/architecture/tenancy-access.md` | Tenancy, autenticación y autorización | J | Architecture | Sí, en su alcance | CURRENT | Seguridad / QA / Operations | KEEP; enlaces si afectados | `docs/architecture/tenancy-access.md` |
| `docs/architecture/transactions.md` | Transacciones, concurrencia e idempotencia | B | Architecture | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | KEEP; enlaces si afectados | `docs/architecture/transactions.md` |
| `docs/architecture/ui.md` | Frontend, sistema visual y UX | B | Architecture | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | KEEP; enlaces si afectados | `docs/architecture/ui.md` |
| `docs/corporate/architecture.md` | Corporate/Legal y mutuos | B | Corporate | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | KEEP; enlaces si afectados | `docs/corporate/architecture.md` |
| `docs/decisions/adr-001-modularity.md` | ADR-001 — Monolito modular y coordinación por flujo | C | Architecture | Sí, en su alcance | CURRENT | Arquitecto / reviewer | KEEP; enlaces si afectados | `docs/decisions/adr-001-modularity.md` |
| `docs/decisions/adr-002-backend.md` | ADR-002 — Python 3.14 y Django 6.1 | C | Architecture | Sí, en su alcance | CURRENT | Arquitecto / reviewer | KEEP; enlaces si afectados | `docs/decisions/adr-002-backend.md` |
| `docs/decisions/adr-003-platform.md` | ADR-003 — PostgreSQL-first; Supabase como DB administrada | C | Architecture | Sí, en su alcance | CURRENT | Arquitecto / reviewer | KEEP; enlaces si afectados | `docs/decisions/adr-003-platform.md` |
| `docs/decisions/adr-004-ui.md` | ADR-004 — SSR, Tailwind y mejora progresiva | C | Architecture | Sí, en su alcance | CURRENT | Arquitecto / reviewer | KEEP; enlaces si afectados | `docs/decisions/adr-004-ui.md` |
| `docs/decisions/adr-005-access.md` | ADR-005 — Autorización explícita y RLS | C | Architecture | Sí, en su alcance | CURRENT | Arquitecto / reviewer | KEEP; enlaces si afectados | `docs/decisions/adr-005-access.md` |
| `docs/decisions/adr-006-data.md` | ADR-006 — Primitivas exactas e identidad proporcional | C | Architecture | Sí, en su alcance | CURRENT | Arquitecto / reviewer | KEEP; enlaces si afectados | `docs/decisions/adr-006-data.md` |
| `docs/decisions/adr-007-transactions.md` | ADR-007 — Una transacción y recursos compartidos explícitos | C | Architecture | Sí, en su alcance | CURRENT | Arquitecto / reviewer | KEEP; enlaces si afectados | `docs/decisions/adr-007-transactions.md` |
| `docs/decisions/adr-008-integrations.md` | ADR-008 — Adaptadores y durabilidad bajo demanda | C | Architecture | Sí, en su alcance | CURRENT | Arquitecto / reviewer | KEEP; enlaces si afectados | `docs/decisions/adr-008-integrations.md` |
| `docs/decisions/adr-009-quality.md` | ADR-009 — Calidad como conjunto de evidencia | C | Architecture | Sí, en su alcance | CURRENT | Arquitecto / reviewer | KEEP; enlaces si afectados | `docs/decisions/adr-009-quality.md` |
| `docs/decisions/adr-010-delivery.md` | ADR-010 — Artefacto portable y operación gestionada inicial | C | Architecture | Sí, en su alcance | CURRENT | Arquitecto / reviewer | KEEP; enlaces si afectados | `docs/decisions/adr-010-delivery.md` |
| `docs/decisions/adr-011-ai.md` | ADR-011 — Roles estables, modelos configurables y contexto local | C | Architecture | Sí, en su alcance | CURRENT | Arquitecto / reviewer | KEEP; enlaces si afectados | `docs/decisions/adr-011-ai.md` |
| `docs/decisions/adr-012-global-documentation-freeze.md` | ADR-012 — Especificar M01–M09 antes de implementar | C | Architecture | Sí, en su alcance | CURRENT | Arquitecto / reviewer | KEEP; enlaces si afectados | `docs/decisions/adr-012-global-documentation-freeze.md` |
| `docs/decisions/index.md` | Registro de decisiones fundacionales | A | Architecture | No; navegación/evidencia | CURRENT | Todos, según ruta | KEEP; enlaces si afectados | `docs/decisions/index.md` |
| `docs/decisions/sources.md` | Fuentes que sostienen decisiones | F | Architecture / Research | Solo procedencia; no regla | CURRENT | Profesional / investigación dirigida | MOVE + enlaces | `docs/research/technical-sources.md` |
| `docs/domain/invariants.md` | Invariantes fundacionales | B | Architecture | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | KEEP; enlaces si afectados | `docs/domain/invariants.md` |
| `docs/domain/inventory-costing.md` | Inventory, kardex y frontera contable | B | Inventory / Accounting | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | KEEP; enlaces si afectados | `docs/domain/inventory-costing.md` |
| `docs/domain/model.md` | Modelo conceptual | B | Architecture | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | KEEP; enlaces si afectados | `docs/domain/model.md` |
| `docs/domain/procure-to-pay.md` | Procure-to-Pay objetivo | B | Procurement | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | KEEP; enlaces si afectados | `docs/domain/procure-to-pay.md` |
| `docs/domain/treasury-finance.md` | Treasury y finanzas objetivo | B | Treasury | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | KEEP; enlaces si afectados | `docs/domain/treasury-finance.md` |
| `docs/index.md` | Índice y autoridad documental | A | Architecture | No; navegación/evidencia | CURRENT | Todos, según ruta | REBUILD navegación/autoridad | `docs/index.md` |
| `docs/operations/delivery.md` | Entrega, operación y recuperación | J | Operations | Sí, en su alcance | CURRENT | Seguridad / QA / Operations | KEEP; enlaces si afectados | `docs/operations/delivery.md` |
| `docs/product/charter.md` | Producto y alcance | B | Product | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | KEEP; enlaces si afectados | `docs/product/charter.md` |
| `docs/quality/strategy.md` | Calidad por riesgo, alcance y evidencia | J | Quality | Sí, en su alcance | CURRENT | Seguridad / QA / Operations | KEEP; enlaces si afectados | `docs/quality/strategy.md` |
| `docs/research/astra-master-audit.md` | Astra Master Audit — cierre documental del encargo | H | Architecture / Research | No; navegación/evidencia | HISTORICAL | Consulta histórica explícita | MOVE + enlaces | `docs/history/astra-master-audit.md` |
| `docs/research/erp-benchmark.md` | Benchmark ERP orientado a problemas | F | Architecture / Research | Solo procedencia; no regla | CURRENT | Profesional / investigación dirigida | KEEP; enlaces si afectados | `docs/research/erp-benchmark.md` |
| `docs/research/final-documentation-closure.md` | Cierre final documental — expediente para revisión independiente | H | Architecture / Research | No; navegación/evidencia | HISTORICAL | Consulta histórica explícita | MOVE + enlaces | `docs/history/final-documentation-closure.md` |
| `docs/research/ifrs-2025-2026-delta.md` | Delta normativo real: ediciones 2025/2026 y ejercicio 2027 | F | Accounting Research | Solo procedencia; no regla | CURRENT | Profesional / investigación dirigida | MOVE + enlaces | `docs/research/normative/ifrs-2025-2026-delta.md` |
| `docs/research/ifrs-applicability.md` | Matriz NIIF/NIC/CINIIF/SIC 2026 → 2027 | F | Accounting Research | Solo procedencia; no regla | CURRENT | Profesional / investigación dirigida | MOVE + enlaces | `docs/research/normative/ifrs-applicability.md` |
| `docs/research/mutuo-tax-corporate.md` | Mutuo de socio: validación temprana de dominio | F | Corporate / Tax / Accounting | Solo procedencia; no regla | CURRENT | Profesional / investigación dirigida | MOVE + enlaces | `docs/research/normative/mutuo-tax-corporate.md` |
| `docs/research/normative-register.md` | Registro normativo y de vigencia | F | Research / Tax | Solo procedencia; no regla | CURRENT | Profesional / investigación dirigida | MOVE + enlaces | `docs/research/normative/normative-register.md` |
| `docs/research/pcge-code-audit.md` | Auditoría de pcge-peru 0.2.0 | G | Architecture / Research | No; navegación/evidencia | EVIDENCE; corte identificado | Reviewer / investigación dirigida | MOVE + enlaces | `docs/evidence/pcge-code-audit.md` |
| `docs/research/repository-audit.md` | Auditoría de repositorios — Astra 2026-09-11 | G | Architecture / Research | No; navegación/evidencia | EVIDENCE; corte identificado | Reviewer / investigación dirigida | MOVE + enlaces | `docs/evidence/repository-audit.md` |
| `docs/research/tax-current-review.md` | Perú: revisión tributaria operativa al 11-09-2026 | F | Research / Tax | Solo procedencia; no regla | CURRENT | Profesional / investigación dirigida | MOVE + enlaces | `docs/research/normative/tax-current-review.md` |
| `docs/research/ux-reconciliation.md` | Reconciliación del UX Blueprint v0.1 | G | Architecture / UX | No; navegación/evidencia | EVIDENCE; corte identificado | Reviewer / investigación dirigida | MOVE + enlaces | `docs/evidence/ux-reconciliation.md` |
| `docs/research/wbpro-knowledge.md` | Extracción de conocimiento Wbpro | G | Architecture / Research | No; navegación/evidencia | EVIDENCE; corte identificado | Reviewer / investigación dirigida | MOVE + enlaces | `docs/evidence/wbpro-knowledge.md` |
| `docs/review.md` | Revisión y condición de avance | E | Architecture / registro del propietario | Sí, en su alcance | CURRENT | Propietario / orquestador | SPLIT historia; conservar estado | `docs/review.md` |
| `docs/roadmap/capabilities.md` | Master Capability Map | E | Product / Architecture | Sí, en su alcance | CURRENT | Propietario / orquestador | KEEP; enlaces si afectados | `docs/roadmap/capabilities.md` |
| `docs/roadmap/decisions-gaps.md` | Cambios fundacionales, gaps y decisiones pendientes | E | Product / Architecture | Sí, en su alcance | CURRENT | Propietario / orquestador | KEEP; enlaces si afectados | `docs/roadmap/decisions-gaps.md` |
| `docs/roadmap/program.md` | CasPro Master Program | E | Product / Architecture | Sí, en su alcance | CURRENT | Propietario / orquestador | KEEP; enlaces si afectados | `docs/roadmap/program.md` |
| `docs/security/threat-model.md` | Threat model inicial | J | Security | Sí, en su alcance | CURRENT | Seguridad / QA / Operations | KEEP; enlaces si afectados | `docs/security/threat-model.md` |
| `docs/specs/acceptance.md` | SP2 — Escenarios de aceptación futuros | D | Architecture | Sí, en su alcance | CURRENT | Implementador autorizado / reviewer | MOVE + enlaces | `docs/specs/acceptance/operational-scenarios.md` |
| `docs/specs/accounting-deep.md` | M07 — Accounting, políticas y control del mayor | D | Accounting | Sí, en su alcance | CURRENT | Implementador autorizado / reviewer | MOVE + enlaces | `docs/specs/milestones/accounting-deep.md` |
| `docs/specs/command-matrix.md` | SP2 — Contrato común y matriz de comandos | D | Architecture | Sí, en su alcance | CURRENT | Implementador autorizado / reviewer | MOVE + enlaces | `docs/specs/cross-cutting/command-matrix.md` |
| `docs/specs/cpe-document-delivery.md` | SP2 — CPE externo, archivo y entrega documental | D | Sales / Documents | Sí, en su alcance | CURRENT | Implementador autorizado / reviewer | MOVE + enlaces | `docs/specs/flows/cpe-document-delivery.md` |
| `docs/specs/deep-spec-index.md` | Deep specs y readiness documental | A | Architecture | No; navegación/evidencia | CURRENT | Todos, según ruta | MOVE; ampliar navegación sin cambiar matriz | `docs/specs/index.md` |
| `docs/specs/economic-facts.md` | Contrato de hechos y extensiones transaccionales M01–M09 | D | Architecture | Sí, en su alcance | CURRENT | Implementador autorizado / reviewer | MOVE + enlaces | `docs/specs/cross-cutting/economic-facts.md` |
| `docs/specs/first-operational-circuit.md` | SP2 — Primer circuito operativo B2C | D | Architecture | Sí, en su alcance | CURRENT | Implementador autorizado / reviewer | MOVE + enlaces | `docs/specs/flows/first-operational-circuit.md` |
| `docs/specs/integrations.md` | SP2 — Jumpseller y trabajo externo durable | D | Architecture | Sí, en su alcance | CURRENT | Implementador autorizado / reviewer | MOVE + enlaces | `docs/specs/flows/jumpseller-external-work.md` |
| `docs/specs/inventory-deep.md` | M03–M04 — Inventario, valoración y cierre del circuito B2C | D | Inventory / Accounting | Sí, en su alcance | CURRENT | Implementador autorizado / reviewer | MOVE + enlaces | `docs/specs/milestones/inventory-deep.md` |
| `docs/specs/procurement-deep.md` | M05 — Procure-to-Pay: contrato ejecutable futuro | D | Procurement | Sí, en su alcance | CURRENT | Implementador autorizado / reviewer | MOVE + enlaces | `docs/specs/milestones/procurement-deep.md` |
| `docs/specs/reporting-goldens.md` | M08 — Cuatro estados, notas y goldens de aceptación | D | Accounting | Sí, en su alcance | CURRENT | Implementador autorizado / reviewer | MOVE + enlaces | `docs/specs/acceptance/reporting-goldens.md` |
| `docs/specs/runtime-masters.md` | M01–M02 — Runtime, acceso, recuperación y maestros | D | Architecture / Access / maestros | Sí, en su alcance | CURRENT | Implementador autorizado / reviewer | MOVE + enlaces | `docs/specs/milestones/runtime-masters.md` |
| `docs/specs/sales-stock-treasury.md` | SP2 — Compromiso, stock, dinero y entrega | D | Sales / Inventory / Treasury | Sí, en su alcance | CURRENT | Implementador autorizado / reviewer | MOVE + enlaces | `docs/specs/flows/sales-stock-treasury.md` |
| `docs/specs/tax-deep.md` | M09 — Tax Perú: fundamento, determinación y expediente | D | Tax | Sí, en su alcance | CURRENT | Implementador autorizado / reviewer | MOVE + enlaces | `docs/specs/milestones/tax-deep.md` |
| `docs/specs/treasury-corporate-deep.md` | M06 — Treasury, conciliación y Corporate | D | Treasury / Corporate | Sí, en su alcance | CURRENT | Implementador autorizado / reviewer | MOVE + enlaces | `docs/specs/milestones/treasury-corporate-deep.md` |
| `docs/specs/work-orders.md` | SP2 — Primera tranche y Validation Profiles | H | Architecture / Research | No; navegación/evidencia | HISTORICAL | Consulta histórica explícita | MOVE; SPLIT perfiles existentes | `docs/history/work-orders-sp2.md` |
| `docs/tax/architecture.md` | Arquitectura Tax Perú | B | Tax | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | KEEP; enlaces si afectados | `docs/tax/architecture.md` |
| `docs/v1-reference/policy.md` | Extracción de Wbpro hacia CasPro | B | Architecture | Sí, en su alcance | CURRENT | Dueño, arquitecto, implementador autorizado | MOVE + enlaces | `docs/architecture/wbpro-reference-policy.md` |

## C. Problemas de organización

Research mezclaba cinco fuentes normativas, benchmark, auditorías y relatos de sesiones. Specs mezclaba flujos, contratos transversales, hitos, aceptación y WOs históricas. Review y README concentraban estado e historia en la misma superficie de entrada. `v1-reference/policy.md` podía interpretarse como versión de CasPro; `integrations.md` no distinguía fácilmente arquitectura de fichas operativas. Las repeticiones útiles de invariantes en fichas no se eliminan: conservan su contexto y dueño. No se reabre el diseño.

## D. Taxonomía objetivo

Mantener contratos en product/architecture/domain/accounting/tax/corporate y controles en quality/security/operations. Research separa normativa en un subdirectorio de cinco fuentes; benchmark y fuentes técnicas quedan en su índice común. Evidence conserva auditorías reutilizables; history conserva cómo se llegó al freeze y WOs antiguas. Specs usa flows, milestones, cross-cutting y acceptance, con índice M01–M09. No nuevas carpetas de un archivo, vacías, numeradas ni profundidad superior a categoría/subcategoría/documento.

## E. Mapa de movimientos

Movimiento mediante git mv, seguido de actualización mecánica de referencias en todos los Markdown; refinamientos y extracciones en un checkpoint posterior. El inventario B registra también los KEEP.

| Origen histórico | Destino |
|---|---|
| `docs/research/normative-register.md` | `docs/research/normative/normative-register.md` |
| `docs/research/ifrs-applicability.md` | `docs/research/normative/ifrs-applicability.md` |
| `docs/research/ifrs-2025-2026-delta.md` | `docs/research/normative/ifrs-2025-2026-delta.md` |
| `docs/research/tax-current-review.md` | `docs/research/normative/tax-current-review.md` |
| `docs/research/mutuo-tax-corporate.md` | `docs/research/normative/mutuo-tax-corporate.md` |
| `docs/research/pcge-code-audit.md` | `docs/evidence/pcge-code-audit.md` |
| `docs/research/repository-audit.md` | `docs/evidence/repository-audit.md` |
| `docs/research/ux-reconciliation.md` | `docs/evidence/ux-reconciliation.md` |
| `docs/research/wbpro-knowledge.md` | `docs/evidence/wbpro-knowledge.md` |
| `docs/research/astra-master-audit.md` | `docs/history/astra-master-audit.md` |
| `docs/research/final-documentation-closure.md` | `docs/history/final-documentation-closure.md` |
| `docs/decisions/sources.md` | `docs/research/technical-sources.md` |
| `docs/v1-reference/policy.md` | `docs/architecture/wbpro-reference-policy.md` |
| `docs/specs/first-operational-circuit.md` | `docs/specs/flows/first-operational-circuit.md` |
| `docs/specs/sales-stock-treasury.md` | `docs/specs/flows/sales-stock-treasury.md` |
| `docs/specs/cpe-document-delivery.md` | `docs/specs/flows/cpe-document-delivery.md` |
| `docs/specs/integrations.md` | `docs/specs/flows/jumpseller-external-work.md` |
| `docs/specs/runtime-masters.md` | `docs/specs/milestones/runtime-masters.md` |
| `docs/specs/inventory-deep.md` | `docs/specs/milestones/inventory-deep.md` |
| `docs/specs/procurement-deep.md` | `docs/specs/milestones/procurement-deep.md` |
| `docs/specs/treasury-corporate-deep.md` | `docs/specs/milestones/treasury-corporate-deep.md` |
| `docs/specs/accounting-deep.md` | `docs/specs/milestones/accounting-deep.md` |
| `docs/specs/tax-deep.md` | `docs/specs/milestones/tax-deep.md` |
| `docs/specs/command-matrix.md` | `docs/specs/cross-cutting/command-matrix.md` |
| `docs/specs/economic-facts.md` | `docs/specs/cross-cutting/economic-facts.md` |
| `docs/specs/acceptance.md` | `docs/specs/acceptance/operational-scenarios.md` |
| `docs/specs/reporting-goldens.md` | `docs/specs/acceptance/reporting-goldens.md` |
| `docs/specs/deep-spec-index.md` | `docs/specs/index.md` |
| `docs/specs/work-orders.md` | `docs/history/work-orders-sp2.md` |

## F. Documentos canónicos actuales

El [mapa de autoridad](../index.md#mapa-de-autoridad) identifica fuente canónica, secundaria y qué no la sustituye. Se conservan 20 contratos B, 4 documentos de estado/roadmap/gates E y 4 contratos de calidad/seguridad/operación J: **28 fuentes canónicas actuales en ese recuento estricto**. Los 12 ADRs C, 15 specs D y 7 instrucciones I tienen autoridad en su propio alcance; incluyendo esas clases son 62 documentos, sin contar navegación ni evidencia como reglas. Estas cifras no son readiness ni autorizaciones.

| Clase | Fuente actual | Owner del inventario |
|---|---|---|
| B | [docs/accounting/architecture.md](../accounting/architecture.md) | Accounting |
| B | [docs/accounting/npif-policy-catalog.md](../accounting/npif-policy-catalog.md) | Accounting |
| B | [docs/accounting/npif-reporting.md](../accounting/npif-reporting.md) | Accounting |
| B | [docs/architecture/ai-assistance.md](../architecture/ai-assistance.md) | Architecture |
| B | [docs/architecture/boundaries.md](../architecture/boundaries.md) | Architecture |
| B | [docs/architecture/data.md](../architecture/data.md) | Architecture |
| B | [docs/architecture/integrations.md](../architecture/integrations.md) | Architecture |
| B | [docs/architecture/overview.md](../architecture/overview.md) | Architecture |
| B | [docs/architecture/technology.md](../architecture/technology.md) | Architecture |
| J | [docs/architecture/tenancy-access.md](../architecture/tenancy-access.md) | Architecture |
| B | [docs/architecture/transactions.md](../architecture/transactions.md) | Architecture |
| B | [docs/architecture/ui.md](../architecture/ui.md) | Architecture |
| B | [docs/corporate/architecture.md](../corporate/architecture.md) | Corporate |
| B | [docs/domain/invariants.md](../domain/invariants.md) | Architecture |
| B | [docs/domain/inventory-costing.md](../domain/inventory-costing.md) | Inventory / Accounting |
| B | [docs/domain/model.md](../domain/model.md) | Architecture |
| B | [docs/domain/procure-to-pay.md](../domain/procure-to-pay.md) | Procurement |
| B | [docs/domain/treasury-finance.md](../domain/treasury-finance.md) | Treasury |
| J | [docs/operations/delivery.md](../operations/delivery.md) | Operations |
| B | [docs/product/charter.md](../product/charter.md) | Product |
| J | [docs/quality/strategy.md](../quality/strategy.md) | Quality |
| E | [docs/review.md](../review.md) | Architecture / registro del propietario |
| E | [docs/roadmap/capabilities.md](../roadmap/capabilities.md) | Product / Architecture |
| E | [docs/roadmap/decisions-gaps.md](../roadmap/decisions-gaps.md) | Product / Architecture |
| E | [docs/roadmap/program.md](../roadmap/program.md) | Product / Architecture |
| J | [docs/security/threat-model.md](../security/threat-model.md) | Security |
| B | [docs/tax/architecture.md](../tax/architecture.md) | Tax |
| B | [docs/architecture/wbpro-reference-policy.md](../architecture/wbpro-reference-policy.md) | Architecture |

## G. Clasificación del research

F conserva siete documentos: cinco en [research/normative](../research/index.md#evidencia-normativa), fuentes técnicas y benchmark en research. Sus fechas/ediciones/límites se mantienen; no hubo investigación nueva. Accounting, NPIF y Tax conservan sus decisiones en los contratos B y sus specs D. La [auditoría PCGE](pcge-code-audit.md) sigue descubrible directamente desde research, como evidencia G de procedencia, sin pasar por history. Auditorías de repositorios, Wbpro y UX también son G, no normativa ni regla.

## H. Clasificación histórica

[History](../history/index.md) contiene cinco registros H y un índice A: Astra anterior, expediente final del freeze, seis WOs SP2, historial de revisiones y origen del repositorio. Cada entrada identifica qué era, período, razón histórica y fuente vigente. No se borra evidencia única; README/review se dividen y sus bloques históricos se conservan íntegros con referencias migradas. No se crea un segundo contenedor archive.

## I. Clasificación de specs

[Specs](../specs/index.md) separa cuatro flows, seis archivos de hitos, dos contratos transversales y tres de aceptación: **15 specs D**. La matriz original M01–M09, sus criterios y handoff se preservan; M08 sigue siendo contrato financiero completo con goldens. No se fuerzan nueve nombres nuevos para contratos que cubren más de un hito. Los perfiles/gates SP2 existentes se extraen íntegros a aceptación; las seis WOs conservan IDs y tablas históricas, NEEDS REGENERATION AFTER FREEZE.

## J. Refactor de review y estado

[Review](../review.md) responde Current status, Freeze identity, Open gates, Next process y Canonical links. Conserva resultado independiente suministrado, candidato f6b64ae/tree0185 y cierre6bec/tree6618; registra el merge real de PR2. A0/B16/C13/D6 se explicita como los conteos existentes del registro, no cuatro nuevos IDs. La historia anterior se extrae a [reviews](../history/reviews.md); el [origen](../history/repository-origins.md) sale del README. La enmienda IA requiere revisión independiente propia y no modifica la aceptación del freeze ni autoriza implementar.

## K. Repeticiones y autoridad

| Repetición revisada | Clasificación | Tratamiento |
|---|---|---|
| README, AGENTS y .ai remiten al estado y límites | USEFUL SUMMARY | README breve; AGENTS solo cambia dos rutas. .ai/CLAUDE/GEMINI conservan instrucciones y enlaces válidos |
| Architecture/domain/specs repiten invariantes y límites aplicados al caso | USEFUL SUMMARY | Se conserva el texto; las fichas remiten a CM0, dueño y QA. No se elimina una guarda para reducir líneas |
| Programa, capabilities y matriz de hitos resumen dependencias/gates | USEFUL SUMMARY | Gaps conserva clasificación/IDs/trigger, review el estado y specs/index la readiness del candidato |
| Review y reportes anteriores contienen varios PASS/pendientes de fechas distintas | HISTORICAL EVIDENCE, no autoridad actual paralela | Extraer y ubicar en history; mantener el corte explícito y la fuente vigente |
| Perfiles y WOs coexistían bajo una sola entrada | Ambigüedad de navegación/autoridad, sin regla contradictoria demostrada | Una fuente de perfiles en aceptación y fichas históricas enlazadas; sin duplicar el bloque extraído |

**DUPLICATE AUTHORITY actual detectada: 0; residual: 0.** No se inventa un conflicto semántico para justificar la reorganización. Se eliminan superficies editoriales ambiguas mediante separación e índices, no mediante cambios de reglas.

## L. Referencias desde raíz y agentes

README apunta a producto, review e índice; su historia tiene destino explícito. AGENTS migra registro normativo y evidencia Wbpro. CLAUDE, GEMINI y los cuatro documentos .ai ya enlazaban fuentes estables: se revisaron y permanecen sin cambios. Una referencia narrativa a H1–H5 en gaps ahora enlaza el historial de review; no se alteran las filas de gates. No se diseñan skills ni se copia dominio a instrucciones.

## M. Auditoría de no cambio semántico

Baseline: main `dbb1224d99f4dbdac61da25daf32f1fed872b4fa`, tree `66184f5714d0130f6cc14a306160bf7a5472ab6c`. El checkpoint mecánico `2ddafe57d8bce04781e39aab1037f8bf406f3c6d` conserva **79/79 documentos** tras normalizar únicamente destinos de enlaces y paths conocidos.

En el resultado final se comparan los **76 cuerpos fuera de README/index/review** contra esa baseline: iguales al deshacer solamente navegación/metadata enumerada, incluida la reubicación de perfiles. Los tres bloques extraídos —historia de review, origen del README, perfiles/gates SP2— se comparan completos con su origen; las seis tablas WO y los criterios/matriz M01–M09 quedan íntegros. La sección de mantenimiento del índice se conserva. Las tres superficies editoriales reescritas se revisan por retención de identidad, estado, autorización y enlaces al dueño.

| Superficie protegida | Evidencia antes/después |
|---|---|
| A0/B16/C13/D6 | Filas y clasificación de gaps intactas; review conserva el resumen de conteos, sin gate nuevo |
| Contratos M01–M09 | Cuerpos de specs y matriz/criterios originales íntegros; solo navegación añadida |
| Domain ownership e invariantes | Modelo, boundaries y fuentes de dominio sin cambio de contenido |
| Commands, estados y atomicidad | Fichas y CM0 intactos; una referencia a perfiles se dirige al bloque extraído |
| Accounting policy architecture | Arquitectura, políticas NPIF y reporting intactos |
| NPIF / IFRS conclusions | Catálogo y las cinco fuentes normativas conservan sus conclusiones/ediciones/límites |
| Tax ownership | Arquitectura Tax y M09 íntegros |
| Mutuo gates | Corporate/Treasury, investigación y gates conservados |
| Jumpseller rules | Flow renombrado, cuerpo idéntico salvo rutas |
| UX safety | Contrato UI y memo DDR conservados |
| Security principles | Tenancy/access, threat model y controles de arquitectura intactos |
| Implementation authorization | Review conserva NOT AUTHORIZED, validaciones profesionales y proceso posterior; freeze no acredita producción |

**Resultado: sin cambio semántico identificado en esta comparación editorial.** No es una nueva refutación ni aceptación independiente. No se ejecutaron tests de CasPro, builds, Docker, migraciones, servicios o integraciones; no se leyó ni escribió Wbpro durante esta misión.

## N. Estadísticas y comprobaciones

| Clase primaria | Antes | Después |
|---|---:|---:|
| A — navegación | 4 | 7 |
| B — contrato canónico | 20 | 20 |
| C — ADR | 12 | 12 |
| D — specs | 14 | 15 |
| E — estado/roadmap/gates | 4 | 4 |
| F — research | 7 | 7 |
| G — evidencia | 4 | 5 |
| H — historia | 3 | 5 |
| I — instrucciones | 7 | 7 |
| J — calidad/seguridad/operación | 4 | 4 |
| **Total Markdown** | **79** | **86** |

Las 79 filas del inventario B conservan su única clase primaria en el destino. Los siete documentos añadidos completan la clasificación final sin superposiciones:

| Archivo añadido | Clase | Owner editorial | Autoridad / consumidores / motivo |
|---|---|---|---|
| [Research index](../research/index.md) | A | Architecture / Research | Navegación, no regla; profesionales/investigación dirigida; separar fuente de decisión |
| [Evidence index](index.md) | A | Architecture | Navegación, no regla; reviewers; distinguir evidencia reutilizable |
| [History index](../history/index.md) | A | Architecture | Navegación, no estado; consulta de trazabilidad; evitar historia sin contexto |
| [Revisiones históricas](../history/reviews.md) | H | Architecture | Registro de período; reviewer histórico; extracción íntegra |
| [Origen](../history/repository-origins.md) | H | Architecture | Registro de período; consulta de procedencia; extracción íntegra |
| [Perfiles de validación](../specs/acceptance/validation-profiles.md) | D | Quality / dueños SP2 | Criterios existentes subordinados a QA; implementador futuro/reviewer; extracción, no WO nueva |
| [Este informe](documentation-ia.md) | G | Architecture | Evidencia editorial; reviewer IA; inventario y trazabilidad de esta enmienda |

| Control estático | Antes | Final |
|---|---:|---:|
| Links locales examinados | 653 | 852 |
| Referencias a anchors examinadas | 83 | 87 |
| Broken links / anchors | 0 / 0 | 0 / 0 |
| Markdown huérfanos, incluidos canónicos | 0 | 0 |
| Casing incorrecto / archivos vacíos | — | 0 / 0 |
| Headings duplicados problemáticos | — | 0 |
| Referencias activas a rutas anteriores | — | 0 |
| Patrones de secretos detectados | — | 0 |
| Duplicate current authority | — | 0 |
| Diff whitespace errors | — | 0 |

Se recorre el grafo desde README, docs/index y entradas de agentes. Todos los documentos son alcanzables; los enlaces recíprocos de índices son navegación deliberada, sin cadena de redirecciones ni ciclo aislado que impida llegar al contrato. La revisión de rutas por función no exige consumir history para llegar a normativa, M03, Accounting o Tax. No se afirma una prueba de usuario cronometrada. Paths originales del inventario B/E son identificadores históricos deliberados, no links muertos. La revisión de datos privados combina inspección del delta y patrones razonables de credenciales; no es certificación de un escáner de seguridad.

## O. Preparación para investigación futura de skills

Las ocho [rutas por función](../index.md#rutas-de-lectura-por-función) son posibles bundles mínimos, no skills creadas ni una decisión sobre su número. Punto común: AGENTS → review → dueño/spec local → dependencias y gates pertinentes. Accounting separa contrato/política, M07/M08 y procedencia normativa; Tax separa contrato M09, fuente aplicable y validación profesional; M03 enlaza Inventory/CM0/hechos y la porción de flujo afectada.

No cargar normalmente este inventario, reportes Astra/cierre, historia de revisiones, origen, WOs antiguas, todas las specs o toda la matriz NIIF. Research/evidence se consultan por una pregunta de procedencia/equivalencia concreta; history nunca sustituye autoridad actual. Escalación: dueño del contrato y [gaps](../roadmap/decisions-gaps.md) para incertidumbres, [ADRs](../decisions/index.md) para alcances/motivos, [protocolo IA](../../.ai/README.md) y [rúbrica](../../.ai/review.md) para revisión; el propietario conserva autorización. La misión futura investiga las fuentes finales reales antes de derivar límites de skills.

## P. Archivos cambiados

El mapa E registra los 29 movimientos explícitos. Se conservan todas las identidades originales; los siete nuevos archivos están en N. Son 73 identidades documentales afectadas: 29 movimientos, 37 cambios en la misma ruta y 7 archivos nuevos. El diff agregado de Git con umbral de renombre por defecto cuenta 74 entradas porque presenta `docs/specs/deep-spec-index.md` → `docs/specs/index.md` como delete/add tras añadir navegación. El checkpoint de movimientos conserva ese rename explícito y la comparación confirma su matriz y criterios intactos; no hay eliminación de contenido.

Archivos conservados en su ruta que recibieron cambios de enlaces o edición autorizada:

- [AGENTS.md](../../AGENTS.md)
- [README.md](../../README.md)
- [docs/accounting/architecture.md](../accounting/architecture.md)
- [docs/accounting/npif-policy-catalog.md](../accounting/npif-policy-catalog.md)
- [docs/accounting/npif-reporting.md](../accounting/npif-reporting.md)
- [docs/architecture/boundaries.md](../architecture/boundaries.md)
- [docs/architecture/data.md](../architecture/data.md)
- [docs/architecture/integrations.md](../architecture/integrations.md)
- [docs/architecture/technology.md](../architecture/technology.md)
- [docs/architecture/tenancy-access.md](../architecture/tenancy-access.md)
- [docs/architecture/transactions.md](../architecture/transactions.md)
- [docs/architecture/ui.md](../architecture/ui.md)
- [docs/corporate/architecture.md](../corporate/architecture.md)
- [docs/decisions/adr-002-backend.md](../decisions/adr-002-backend.md)
- [docs/decisions/adr-003-platform.md](../decisions/adr-003-platform.md)
- [docs/decisions/adr-004-ui.md](../decisions/adr-004-ui.md)
- [docs/decisions/adr-005-access.md](../decisions/adr-005-access.md)
- [docs/decisions/adr-006-data.md](../decisions/adr-006-data.md)
- [docs/decisions/adr-007-transactions.md](../decisions/adr-007-transactions.md)
- [docs/decisions/adr-008-integrations.md](../decisions/adr-008-integrations.md)
- [docs/decisions/adr-009-quality.md](../decisions/adr-009-quality.md)
- [docs/decisions/adr-010-delivery.md](../decisions/adr-010-delivery.md)
- [docs/decisions/adr-012-global-documentation-freeze.md](../decisions/adr-012-global-documentation-freeze.md)
- [docs/decisions/index.md](../decisions/index.md)
- [docs/domain/invariants.md](../domain/invariants.md)
- [docs/domain/inventory-costing.md](../domain/inventory-costing.md)
- [docs/domain/procure-to-pay.md](../domain/procure-to-pay.md)
- [docs/domain/treasury-finance.md](../domain/treasury-finance.md)
- [docs/index.md](../index.md)
- [docs/operations/delivery.md](../operations/delivery.md)
- [docs/quality/strategy.md](../quality/strategy.md)
- [docs/review.md](../review.md)
- [docs/roadmap/capabilities.md](../roadmap/capabilities.md)
- [docs/roadmap/decisions-gaps.md](../roadmap/decisions-gaps.md)
- [docs/roadmap/program.md](../roadmap/program.md)
- [docs/security/threat-model.md](../security/threat-model.md)
- [docs/tax/architecture.md](../tax/architecture.md)

## Q. Checkpoints

| Commit | Alcance |
|---|---|
| `0ed51168db4853bc246efcee7a38b0a8d1c81804` | Inventario y clasificación inicial de los 79 documentos |
| `2ddafe57d8bce04781e39aab1037f8bf406f3c6d` | 29 movimientos y migración mecánica de rutas; 79/79 cuerpos preservados |
| `83efb684215e19a20a783610fcc9dde9cf50b30f` | Estado, extracciones históricas y perfiles existentes |
| `93528754b6509ee115dcdd16c22c7bcdc22a560d` | Rutas de lectura, índices y mapa de autoridad |
| Checkpoint final de este informe | Estadísticas y comprobación IA; su SHA/tree se publican fuera del contenido que identifican, en el PR y la entrega final |

## R. Publicación para revisión independiente

Rama: `docs/final-information-architecture`. Base: main `dbb1224d99f4dbdac61da25daf32f1fed872b4fa`. Título: **Finalize CasPro documentation information architecture**. El nuevo PR debe quedar OPEN, sin merge. Número, head/tree exactos y mergeable state se verifican en GitHub después del push final y se devuelven en la entrega; el informe no se autoatribuye aceptación independiente.

## S. Veredicto

**PASS — INFORMATION ARCHITECTURE READY FOR REVIEW.**

Veredicto del autor limitado a estructura, navegación y preservación editorial. La siguiente etapa es revisión independiente de este PR → merge → investigación dedicada de skills → skills → WOs regeneradas → autorización explícita de implementación → código. No continuar ampliando documentación por rutina.
