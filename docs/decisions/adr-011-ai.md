# ADR-011 — Roles estables, modelos configurables y contexto local

Fecha: 2026-09-10. **Estado autoritativo por alcance.** ACCEPTED acepta el contrato de diseño, no acredita ejecución ni aprobación empresarial.

| Alcance | Estado | Condición o límite |
|---|---|---|
| Router, roles delimitados, WO y rúbrica única | ACCEPTED | Carga según tarea; no ampliar permisos ni duplicar el contrato de evidencia |
| Adecuación real de modelos/herramientas y carga de contexto | PROVISIONAL | Revisar disponibilidad y resultado de la primera WO autorizada; las preferencias no acreditan eficacia |

## Context

La IA acelera producción de código/texto y también puede repetir supuestos o modificar pruebas para confirmar su propia salida. V1 muestra instrucciones duplicadas y contexto excesivo.

## Decision

AGENTS como router; un protocolo, una plantilla de WO y una rúbrica. Architect/orchestrator/implementer/reviewer/refuter tienen autoridad distinta; la configuración del modelo vive una sola vez en [.ai](../../.ai/README.md).

## Alternatives

Skills por modelo duplican capacidades; seis revisores por cambio añaden ceremonia; implementador que acepta su propia interpretación elimina independencia.

## Consequences

Revisión por riesgo, refutación para garantías críticas y evidencia reutilizada sobre candidato exacto. La IA no crea Business Truth sin fuente/aprobación ni amplía ejecución mediante un prompt interno. La próxima fase requiere revisión humana de esta fundación.
