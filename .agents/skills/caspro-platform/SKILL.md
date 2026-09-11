---
name: caspro-platform
description: "Trabajar runtime M01, maestros M02, acceso/RLS, seguridad o recuperación CasPro; seleccionar el modo concreto sin construir infraestructura o ejecutar restore por defecto."
---

# caspro-platform

Lee el [protocolo](../../../.ai/README.md) y el [estado](../../../docs/review.md) si no están en contexto. Esta skill no concede permiso: implementación requiere WO regenerada y autorización explícita; hoy solo análisis/documentación del alcance encargado. No generar WOs reales en la misión de agentes. Docs poseen las reglas; ante contradicción detener el efecto afectado y escalar, sin editar el contrato silenciosamente.

## Entrada y contexto por modo

Requiere alcance, componente/entrypoint y WO autorizada antes de implementación. Leer sección correspondiente de [M01–M02](../../../docs/specs/milestones/runtime-masters.md), [gaps](../../../docs/roadmap/decisions-gaps.md) y la fila necesaria:

| Modo | Añadir |
|---|---|
| Runtime M01 | [Tecnología](../../../docs/architecture/technology.md), [QA](../../../docs/quality/strategy.md); compatibilidad exacta a verificar en ejecución futura |
| Party/Catalog/importación | M02 + [C11/C12/preview](../../../docs/specs/flows/first-operational-circuit.md), [data](../../../docs/architecture/data.md), acceso aplicado al dato |
| RLS/autorización/seguridad | [Tenancy/access](../../../docs/architecture/tenancy-access.md), [threat model](../../../docs/security/threat-model.md), QA y entrypoints afectados |
| Restore/operación/migración | [Delivery](../../../docs/operations/delivery.md), recuperación M01, QA, entorno/manifiesto y mandato específicos |

## Trabajo y límites

Campo nuevo de Party: establecer significado, owner, entidad/visibilidad y consumidores antes de schema; no inventar regla ausente. RLS: mapear entradas/roles y negativas que la garantía exige; no declarar aislamiento por filtro UI ni usar bypass para hacer pasar prueba. Restore: no ejecutar por tener skill; exige entorno/manifest/mandato y gates, con efectos externos tratados por contrato.

Seleccionar B01/B02/B13/B15, C10/C12/C13 y demás aplicables; leer transacciones solo si hay concurrencia/corrección. Cambiar frontera, identidad o política requiere owner/Architecture. No fijar versión, contraseña, infraestructura o permiso por copiar ejemplos de proveedor.

## Salida / revisión

Contexto, superficie afectada, análisis o cambio encargado, evidencia real/futura y gates. Reviewer independiente seguridad para acceso y operaciones/seguridad para recuperación; Architect ante frontera. Sin runtime, fixtures o autorización, describir validación pendiente en vez de ejecutar DB/Docker/builds.
