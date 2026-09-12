---
name: caspro-platform
description: "Trabajar plataforma M01, maestros M02, acceso/configuración, privacidad técnica y restore CasPro; elegir modo sin construir infraestructura ni ejecutar recuperación por defecto."
---

# caspro-platform

Consulta el [estado](../../../docs/review.md) para la fase vigente y aplica el [protocolo](../../../.ai/README.md#autoridad-y-autorización). Esta skill no concede permiso: implementación solo con fase habilitada y WO regenerada explícitamente autorizada, respetando todos sus límites. Preparar WOs también requiere autorización vigente. Docs poseen las reglas; ante contradicción, detener la parte afectada y escalar.

## Entrada y contexto por modo

Requiere alcance, componente/entrypoint y WO autorizada antes de implementación. Leer sección correspondiente de [M01–M02](../../../docs/specs/milestones/runtime-masters.md), [gaps](../../../docs/roadmap/decisions-gaps.md) y la fila necesaria:

| Modo | Añadir |
|---|---|
| Runtime M01 | [Tecnología](../../../docs/architecture/technology.md), [QA](../../../docs/quality/strategy.md); verificar compatibilidad exacta cuando se autorice esa ejecución |
| Party/Catalog/importación | M02 + [C11/C12/preview](../../../docs/specs/flows/first-operational-circuit.md), [data](../../../docs/architecture/data.md), acceso aplicado al dato |
| RLS/autorización/seguridad | [Tenancy/access](../../../docs/architecture/tenancy-access.md), [threat model](../../../docs/security/threat-model.md), QA y entrypoints afectados |
| Roles, comandos o autoridad de configuración | [Registro exacto](../../../docs/architecture/capability-registry.md), [roles/delegación](../../../docs/architecture/roles-delegation.md) y [gobierno](../../../docs/architecture/configuration-governance.md) según efecto; no derivar permisos del puesto |
| Privacidad/restricciones/incidente | [Ciclo de datos](../../../docs/security/personal-data-lifecycle.md), [dueños](../../../docs/architecture/boundaries.md#propiedad-de-hechos-de-privacidad) y [conjunción de contexto](../../../docs/architecture/capability-registry.md#preparación-de-contexto-por-finalidad); compliance solo por interpretación/aplicabilidad legal |
| Restore/operación/migración | [Delivery](../../../docs/operations/delivery.md), recuperación M01, QA, entorno/manifiesto y mandato específicos |

Restore con datos personales añade la [barrera de privacidad](../../../docs/security/personal-data-lifecycle.md#restore-sin-reexposición), incluidas lecturas normales OFF hasta reconciliación. Aislamiento del proveedor IA runtime añade [AIService](../../../docs/architecture/ai-assistance.md#frontera); no cargarlo para un alta de maestro sin ese efecto. Para privacidad/configuración fuera de M01–M02, entrar directamente al contrato de la fila, sin cargar ambos hitos.

## Trabajo y límites

Campo nuevo de Party: establecer significado, owner, entidad/visibilidad y consumidores antes de schema; no inventar regla ausente. RLS: mapear entradas/roles y negativas que la garantía exige; no declarar aislamiento por filtro UI ni usar bypass para hacer pasar prueba. Restore: no ejecutar por tener skill; exige entorno/manifest/mandato y gates, con efectos externos tratados por contrato.

Seleccionar B01/B02/B13/B15, C10/C12/C13 y demás aplicables; leer transacciones solo si hay concurrencia/corrección. Cambiar frontera, identidad o política requiere owner/Architecture. No fijar versión, contraseña, infraestructura o permiso por copiar ejemplos de proveedor.

## Salida / revisión

Contexto, superficie afectada, análisis o cambio encargado, evidencia obtenida/pendiente y gates. Reviewer independiente seguridad para acceso y operaciones/seguridad para recuperación; Architect ante frontera. Sin runtime, fixtures o autorización, describir validación pendiente en vez de ejecutar DB/Docker/builds.
