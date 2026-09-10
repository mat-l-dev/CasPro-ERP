# Índice y autoridad documental

Fecha de corte: 2026-09-10. Los documentos describen la fundación, no acreditan implementación. El [registro](decisions/index.md) enlaza cada ADR, cuya tabla de alcances es la única fuente autoritativa de sus estados. La condición global y el cierre de Gate 1 se consultan en [review](review.md).

## Cinco fuentes de verdad

| Verdad | Fuente canónica | No puede sustituirse por |
|---|---|---|
| BUSINESS — qué debe ocurrir | [Producto](product/charter.md), [modelo](domain/model.md), [invariantes](domain/invariants.md); [spec del primer circuito](specs/first-operational-circuit.md) | Un test, un prompt o una interpretación del implementador |
| ARCHITECTURE — organización y motivos | [Arquitectura](architecture/overview.md), contratos enlazados y ADRs | Un árbol de carpetas o una instrucción histórica |
| IMPLEMENTATION — qué existe | Futuro código, migraciones y configuración; hoy no existen | Una decisión ACCEPTED |
| VERIFICATION — qué se ha demostrado | Futuras pruebas y evidencia vinculada al candidato; hoy solo [revisión estática documental](review.md) | Generación de IA, coverage o una checklist rellenada |
| OPERATIONAL — qué está desplegado | Futuro manifiesto de release y registro por entorno | HEAD, un merge o una imagen construida |

## Rutas de lectura

| Tema | Documento |
|---|---|
| Producto, hechos y non-goals | [Charter](product/charter.md) |
| Agregados y ciclos | [Modelo conceptual](domain/model.md) |
| Conservación y estados | [Invariantes](domain/invariants.md) |
| Primer circuito Jumpseller–venta–cobro–entrega–CPE–email | [Spec local](specs/first-operational-circuit.md), con matriz, aceptación y primeras WOs enlazadas |
| Principios y estructura futura | [Overview](architecture/overview.md) |
| Ownership y dependencias | [Boundaries](architecture/boundaries.md) |
| Comparación tecnológica | [Technology](architecture/technology.md) |
| Dinero, cantidades, fechas e identidad | [Data](architecture/data.md) |
| Tenancy, autenticación y autorización | [Tenancy/access](architecture/tenancy-access.md) |
| Comandos, bloqueos y reversión | [Transactions](architecture/transactions.md) |
| Integraciones, eventos y trabajo durable | [Integrations](architecture/integrations.md) |
| Frontend, sistema visual y UX | [UI](architecture/ui.md) |
| Taxonomía, perfiles y evidencia | [Quality](quality/strategy.md) |
| Amenazas y controles | [Threat model](security/threat-model.md) |
| CI/CD, recuperación y observabilidad | [Delivery](operations/delivery.md) |
| Decisiones y fuentes primarias | [ADRs](decisions/index.md), [fuentes](decisions/sources.md) |
| Extracción de V1 | [Política](v1-reference/policy.md) |
| IA y contexto local | [Protocolo](../.ai/README.md), [flujo](../.ai/workflow.md) |
| Pendientes y revisión de la fundación | [Review](review.md) |

## Mantenimiento mínimo

Una regla vive una vez, en el documento de su propietario. Un ADR explica la elección y enlaza su contrato detallado. Un resumen enlaza ese contenido; no mantiene otra versión de la regla.

Un cambio actualiza la fuente afectada y sus referencias. Cualquier reutilización de evidencia sigue el contrato de equivalencia de [calidad](quality/strategy.md); el índice no define una excepción alternativa. Las decisiones históricas se sustituyen mediante un ADR explícito, no se reescribe su motivo. La desagregación de estados de esta fundación durante Gate 1 se registra en el índice de decisiones.

No hay plantilla enciclopédica obligatoria: título, propósito, contenido decisional y enlaces relevantes bastan. Cada especificación posterior tendrá propietario, invariantes, criterios de aceptación y preguntas bloqueantes. Su aprobación no se infiere de esta fundación.
