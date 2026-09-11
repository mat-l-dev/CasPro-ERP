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

Research mezclaba cinco fuentes normativas, benchmark, auditorías y relatos de sesiones. Specs mezclaba flujos, contratos transversales, hitos, aceptación y WOs históricas. Review y README exigían atravesar historia para encontrar el estado. `v1-reference/policy.md` podía interpretarse como versión de CasPro; `integrations.md` no distinguía fácilmente arquitectura de fichas operativas. Las repeticiones útiles de invariantes en fichas no se eliminan: conservan su contexto y dueño. No se reabre el diseño.

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

## F–I. Autoridad, research, historia y especificaciones

La clasificación primaria B/J/D identifica contratos, C los motivos/alcances ADR, E estado/roadmap/gates y F evidencia de fuentes sin autoridad para cambiar reglas. G es evidencia de revisión con corte/limitaciones. H nunca autoriza ejecución. A e I dirigen lectura local. Los índices finales enlazan cada documento por función; este inventario no debe cargarse en tareas operativas ordinarias.
