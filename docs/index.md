# Índice y autoridad documental

CasPro es un ERP interno para TILMUX y entidades autorizadas del propietario. Empieza por [producto](product/charter.md) y [estado vigente](review.md): allí están el freeze, sus identidades, los gates abiertos y el proceso aún requerido para implementar. Este índice selecciona fuentes; no mantiene otro estado global.

## Rutas de lectura por función

Cada secuencia es un punto de entrada. Cargar las dependencias concretas que cite la spec local, no todo el repositorio.

| Función | Contexto mínimo y siguiente lectura |
|---|---|
| NEW CONTRIBUTOR | [Producto](product/charter.md) → [estado](review.md) → [arquitectura](architecture/overview.md); este mapa resuelve la autoridad restante |
| IMPLEMENTER | [Estado/autorización](review.md) → [hito/spec local](specs/index.md) → contrato del dueño y dependencias citadas → [gates](roadmap/decisions-gaps.md) / [calidad](quality/strategy.md) / [contrato de WO](../.ai/work-order.md). No hay WO regenerada ni autorización de implementación; [M03 tiene una ruta concreta](specs/index.md#navegar-por-función) |
| REVIEWER | [Estado e identidad](review.md) → contrato y delta del alcance → [ADRs pertinentes](decisions/index.md) si necesita motivos → [protocolo de revisión](../.ai/review.md) / [calidad](quality/strategy.md). Seleccionar el expediente del candidato en [evidence](evidence/index.md) |
| ACCOUNTING / FINANCE | [Estado](review.md) → [Accounting](accounting/architecture.md) → [políticas NPIF](accounting/npif-policy-catalog.md) / [reporting](accounting/npif-reporting.md) según tarea → [M07](specs/milestones/accounting-deep.md) / [M08 y goldens](specs/acceptance/reporting-goldens.md) → [gates](roadmap/decisions-gaps.md). Para movimientos financieros: [Treasury](domain/treasury-finance.md) / [M06](specs/milestones/treasury-corporate-deep.md). Procedencia: [research](research/index.md) |
| TAX / COMPLIANCE | [Estado](review.md) → [Tax](tax/architecture.md) → [M09](specs/milestones/tax-deep.md) → [registro normativo](research/normative/normative-register.md) y fuente aplicable → [gates](roadmap/decisions-gaps.md). Financiación: añadir [Corporate](corporate/architecture.md) / [Mutuo](research/normative/mutuo-tax-corporate.md) |
| DOMAIN OWNER | [Estado](review.md) → [modelo](domain/model.md) / [invariantes](domain/invariants.md) → dueño local: [P2P](domain/procure-to-pay.md), [Inventory](domain/inventory-costing.md), [Treasury](domain/treasury-finance.md) u otro módulo → [spec del hito](specs/index.md) / [gates](roadmap/decisions-gaps.md) |
| SECURITY / OPERATIONS | [Estado](review.md) → [acceso](architecture/tenancy-access.md) / [amenazas](security/threat-model.md) o [operación](operations/delivery.md) según tarea → [M01–M02](specs/milestones/runtime-masters.md) → [calidad](quality/strategy.md) / [gates](roadmap/decisions-gaps.md) |
| AI ORCHESTRATOR | [AGENTS](../AGENTS.md) → [estado](review.md) → [catálogo de skills](../.ai/skills.md) / [protocolo](../.ai/README.md) → contrato, spec y gates de la tarea. La evaluación del sistema de agentes está en su [expediente](evidence/agent-system-research.md) |

## Mapa de autoridad

| Verdad | Fuente canónica | Fuentes secundarias | Qué no la puede sustituir |
|---|---|---|---|
| GLOBAL STATUS | [Review](review.md) | Expediente de aceptación, [historia](history/index.md) | Un PASS anterior, readiness local, este índice o un merge |
| BUSINESS | [Producto](product/charter.md) | Capabilities, contexto de specs | Un prompt, test o interpretación del implementador |
| ARCHITECTURE | [Overview](architecture/overview.md) y contratos de arquitectura enlazados | ADRs para motivos/alcances | Árbol de carpetas o instrucción histórica |
| DOMAIN | [Modelo](domain/model.md), [invariantes](domain/invariants.md), contrato del dueño y [spec local](specs/index.md) | Resúmenes de UI, roadmap y ejemplos | Estado importado del canal, conveniencia técnica o evidencia normativa convertida en regla |
| DECISIONS | Cada ADR y su tabla de alcances en [decisions](decisions/index.md) | Fuentes técnicas y contrato detallado | Un resumen que convierta PROVISIONAL en demostrado |
| IMPLEMENTATION | Futuro código, migraciones y configuración; todavía no existen | Specs describen lo que deberá ocurrir | Una decisión ACCEPTED o un documento generado |
| VERIFICATION | [Calidad](quality/strategy.md) para el contrato; evidencia vinculada al candidato para lo demostrado | [Evidence](evidence/index.md), perfiles y criterios de aceptación | Checklist, coverage, generación de IA o PASS fuera de equivalencia |
| OPERATION | [Delivery](operations/delivery.md) para contrato; futuro manifiesto de release/registro por entorno para despliegue real | Evidencia operativa futura | HEAD, merge o imagen construida |
| NORMATIVE EVIDENCE | [Registro normativo](research/normative/normative-register.md) y fuentes/edición/vigencia enlazadas | [Research](research/index.md), procedencia PCGE | Benchmarks o historia como prueba de vigencia; research no decide la política CasPro |
| ROADMAP / GATES | [Programa](roadmap/program.md), [capabilities](roadmap/capabilities.md), [gaps A/B/C/D](roadmap/decisions-gaps.md) | Matriz M01–M09 y resúmenes locales | WO histórica, calendario supuesto o skill como autorización |
| HISTORY | [Registros de historia](history/index.md), solo para hechos de su período | Git y expedientes de evidencia | Reinterpretación de un pendiente histórico como estado vigente |

## Contratos por tema

Enmienda de gobierno propuesta: [roles/alcances/delegación/SoD](architecture/roles-delegation.md) y [configuración/impacto/UX](architecture/configuration-governance.md) → [TILMUX Policy Register/readiness](product/company-policy-register.md) → [manual contable futuro](accounting/tilmux-policy-manual.md). [Expediente A–AF](evidence/governance-roles-configuration-policies.md) demuestra cobertura documental y [benchmark oficial](research/governance-authorization-benchmark.md) conserva fuentes/límites. Aceptación y autorización solo en review.

| Tema | Fuentes |
|---|---|
| Arquitectura | [Ownership/boundaries](architecture/boundaries.md), [tecnología](architecture/technology.md), [datos](architecture/data.md), [transacciones](architecture/transactions.md), [integraciones](architecture/integrations.md), [acceso](architecture/tenancy-access.md) |
| Experiencia y asistencia | [UI](architecture/ui.md), [IA en producto](architecture/ai-assistance.md) |
| Accounting, Tax y Corporate | Los contratos permanecen en [accounting](accounting/architecture.md), [tax](tax/architecture.md) y [corporate](corporate/architecture.md); no se trasladan a research |
| Reutilización Wbpro | [Política de referencia](architecture/wbpro-reference-policy.md) y [evidencia clasificada](evidence/wbpro-knowledge.md); nunca dependencia runtime |
| Decisiones y criterios | [ADRs](decisions/index.md), [specs/aceptación](specs/index.md), [calidad](quality/strategy.md) |
| Procedencia y trazabilidad | [Research](research/index.md), [evidence](evidence/index.md), [history](history/index.md), cada uno con función distinta |

## Mantenimiento mínimo

Amendment semántico aceptado: [expediente B2B/financiación](evidence/b2b-financing-amendment.md) → [Sales B2B](specs/flows/b2b-commercial-dossier.md), [M06 hechos/estados](specs/flows/financing-events-statements.md), [Documents entrega externa](specs/flows/cpe-document-delivery.md#c40), [research oficial](research/normative/b2b-financing-evidence.md). Estado y autorización únicamente en [review](review.md); estas rutas no habilitan código.

Una regla vive una vez, en el documento de su propietario. Un ADR explica la elección y enlaza su contrato detallado. Un resumen enlaza ese contenido; no mantiene otra versión de la regla.

Un cambio actualiza la fuente afectada y sus referencias. Cualquier reutilización de evidencia sigue el contrato de equivalencia de [calidad](quality/strategy.md); el índice no define una excepción alternativa. Las decisiones históricas se sustituyen mediante un ADR explícito, no se reescribe su motivo. La desagregación de estados de esta fundación durante Gate 1 se registra en el índice de decisiones.

No hay plantilla enciclopédica obligatoria: título, propósito, contenido decisional y enlaces relevantes bastan. Cada especificación posterior tendrá propietario, invariantes, criterios de aceptación y preguntas bloqueantes. Su aprobación no se infiere de esta fundación.

## Propuesta profesional posterior al freeze

[Informe A–AR y matriz de cobertura](evidence/professional-operational-completeness.md) → [seis specs por dueño](specs/index.md#amendment-profesional-propuesto) → [benchmark](research/professional-erp-benchmark.md), [normativa operacional](research/normative/operational-completeness.md), [libros](research/normative/tax-book-universe.md) y [Jumpseller/CDI](research/normative/jumpseller-portugal-service.md). Amendment aceptado por re-revisión independiente según [review](review.md); conserva las aceptaciones anteriores y no autoriza implementación.
