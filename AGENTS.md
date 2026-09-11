# CasPro — router del repositorio

CasPro es el ERP interno de TILMUX y entidades autorizadas del propietario. Lee el [estado vigente](docs/review.md), única fuente de la fase global permitida. Un freeze documental o merge no habilita por sí mismo código, datos reales ni producción.

## Qué leer después

1. Identifica objetivo, acción solicitada y autorización vigente. Lee [review](docs/review.md); no infieras permiso de una skill, PASS o merge.
2. Selecciona una skill primaria en el [catálogo](.ai/skills.md). Lee su SKILL.md y el [protocolo común](.ai/README.md) si aún no están en contexto. Añade otra skill solo por un riesgo/frontera concreta.
3. Carga contrato del dueño → spec/sección local → gates pertinentes. El [índice por función](docs/index.md) resuelve fuentes; no cargues carpetas completas. History solo por trazabilidad; research por vigencia/procedencia; evidence por una afirmación que deba demostrarse.
4. Aplica el [workflow](.ai/workflow.md) correspondiente: rama → trabajo autorizado → PR → revisión separada → correcciones → merge autorizado. Preparar una WO no autoriza ejecutarla.

## Autoridad y límites

La instrucción directa del propietario gobierna alcance dentro de las políticas del sistema/harness. [Docs canónicos](docs/index.md#mapa-de-autoridad) poseen producto, reglas, ADRs y specs; las skills seleccionan contexto y nunca los redefinen. Si difieren, usa la fuente canónica, registra la contradicción y detén el efecto afectado. Roles/modelos, escalación y salida ante bloqueo están en el [protocolo](.ai/README.md).

No inventar hechos, políticas ni aprobaciones; no guardar secretos, datos reales de terceros o expedientes privados en Git/prompts. Todo hecho empresarial conserva su dueño y autorización; ningún atajo técnico/UI/IA los sustituye.

Wbpro sigue READ-ONLY, solo por lectura concreta autorizada conforme a la [política](docs/architecture/wbpro-reference-policy.md). `archive`, `15-history`, legacy y Webrax quedan fuera de lectura/modificación; no copiar Wbpro como implementación ni dependencia runtime.

Preparar WOs requiere encargo y fase que lo permitan. Implementar requiere fase habilitada y WO regenerada explícitamente autorizada, dentro de sus límites conforme al [protocolo](.ai/README.md#autoridad-y-autorización). Cada ejecución o efecto necesita autorización explícita; no inferirla de un PASS, merge, skill, modelo o herramienta. Autor ≠ reviewer; capacidad de una herramienta ≠ permiso.
