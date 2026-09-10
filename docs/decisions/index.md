# Registro de decisiones fundacionales

Corte 2026-09-10. **La única fuente autoritativa del estado de una decisión es la tabla de alcances de su ADR.** Este índice es navegación; no mantiene una segunda columna de estados. El contrato enlazado desarrolla la regla y las condiciones. Una discrepancia entre textos se corrige como defecto documental, no permite elegir el estado más conveniente.

ACCEPTED acepta el contrato de diseño de ese alcance, no acredita software ejecutado, aprobación empresarial/regulatoria ni aptitud productiva. PROVISIONAL identifica un candidato que no puede tratarse como mecanismo aceptado; PENDING VALIDATION describe su evidencia faltante, no otro grado de aprobación. PENDING HUMAN DECISION identifica las decisiones empresariales de la [revisión](../review.md).

| ADR: estado y motivo autoritativos | Contrato detallado | Materia que distingue |
|---|---|---|
| [001 Monolito y fronteras](adr-001-modularity.md) | [Boundaries](../architecture/boundaries.md) | Propietarios y agrupación Workspace |
| [002 Python/Django](adr-002-backend.md) | [Technology](../architecture/technology.md) | Elección arquitectónica y compatibilidad de versiones |
| [003 PostgreSQL/Supabase](adr-003-platform.md) | [Technology](../architecture/technology.md) | Base portable y proveedor/conexión candidatos |
| [004 Frontend](adr-004-ui.md) | [UI](../architecture/ui.md) | Servidor autoritativo y configuración de interacción |
| [005 Acceso/RLS](adr-005-access.md) | [Tenancy/access](../architecture/tenancy-access.md) | Principios de autorización y aceptación del mecanismo RLS |
| [006 Datos e identidad](adr-006-data.md) | [Data](../architecture/data.md) | Exactitud y parámetros numéricos/representación |
| [007 Transacciones](adr-007-transactions.md) | [Transactions](../architecture/transactions.md) | Atomicidad, idempotencia y matriz concreta de recursos |
| [008 Eventos/integraciones](adr-008-integrations.md) | [Integrations](../architecture/integrations.md) | Propietarios durables y backend técnico |
| [009 QA](adr-009-quality.md) | [Quality](../quality/strategy.md) | Equivalencia de evidencia y mecanismo de selección |
| [010 Entrega/operación](adr-010-delivery.md) | [Delivery](../operations/delivery.md) | Artefacto/recuperación y topología contratada |
| [011 Desarrollo con IA](adr-011-ai.md) | [Protocolo IA](../../.ai/README.md) | Autoridad de roles y adecuación de herramientas |

Gate 1 desagrega los estados globales iniciales en alcances dentro de los ADRs existentes, preservando sus motivos. Un principio aceptado no promueve sus detalles provisionales. Las decisiones posteriores que sustituyan una elección conservarán su antecedente. No se crean ADRs para nombres de carpetas triviales.

La condición de la fundación y el cierre del gate viven en [review](../review.md). Ningún estado autoriza ejecutar tests, construir software o avanzar de fase por sí solo.
