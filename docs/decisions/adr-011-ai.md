# ADR-011 — Roles estables, modelos configurables y contexto local

Fecha: 2026-09-10. **Estado autoritativo por alcance.** ACCEPTED acepta el contrato de diseño, no acredita ejecución ni aprobación empresarial.

| Alcance | Estado | Condición o límite |
|---|---|---|
| Router, roles delimitados, WO y rúbrica única | ACCEPTED | Carga según tarea; no ampliar permisos ni duplicar el contrato de evidencia |
| Frontera provider-neutral y salida de IA como candidato sin efectos críticos | ACCEPTED | Validación determinista/humana; dominios no importan SDK ni conceden comandos críticos |
| Adecuación real de modelos/herramientas y carga de contexto | PROVISIONAL | Revisar disponibilidad y resultado de la primera WO autorizada; las preferencias no acreditan eficacia |
| Herramientas/modelos de desarrollo, Hermes, VPS/local y pilotos no confirmados | PROVISIONAL | Recursos, licencia, seguridad y eficacia por WO; no seleccionados por la decisión de IA runtime |
| IA runtime: proveedor/modelo inicial DeepSeek API / V4.1-Flash | DECISIÓN POSTERIOR DEL PROPIETARIO; ACTIVACIÓN PENDIENTE | [Contrato vigente](../architecture/ai-assistance.md); arquitectura neutral aceptada, gates de propósito/privacidad/contrato/evaluación abiertos |

La fila antigua mezclaba herramientas de desarrollo y proveedor del producto. Se aclara prospectivamente por F07: las preferencias Astra/Sol u otros recursos de desarrollo en [.ai](../../.ai/README.md) no cambian; solo la lectura de «proveedor runtime aún sin seleccionar» queda supersedida por la decisión posterior. Ninguna idoneidad técnica, VPS, piloto opcional ni gate se convierte mecánicamente en ACCEPTED.

## Context

La IA acelera producción de código/texto y también puede repetir supuestos o modificar pruebas para confirmar su propia salida. V1 muestra instrucciones duplicadas y contexto excesivo.

## Decision

AGENTS como router; un protocolo, una plantilla de WO y una rúbrica. Architect/orchestrator/implementer/reviewer/refuter tienen autoridad distinta; la configuración del modelo vive una sola vez en [.ai](../../.ai/README.md). La [arquitectura IA](../architecture/ai-assistance.md) define un puerto neutral, evidencia por inferencia y ausencia de efectos críticos directos.

## Alternatives

Skills por modelo duplican capacidades; seis revisores por cambio añaden ceremonia; implementador que acepta su propia interpretación elimina independencia.

## Consequences

Revisión por riesgo, refutación para garantías críticas y evidencia reutilizada sobre candidato exacto. La IA no crea Business Truth sin fuente/aprobación ni amplía ejecución mediante un prompt interno. La próxima fase requiere revisión humana de esta fundación.
