---
name: caspro-work-order
description: "Preparar Work Orders CasPro acotadas desde specs y gates, cuando exista encargo de preparación; no implementar ni copiar WOs históricas."
---

# caspro-work-order

Consulta el [estado](../../../docs/review.md) para la fase vigente y aplica el [protocolo](../../../.ai/README.md#autoridad-y-autorización). Esta skill no concede permiso: implementación solo con fase habilitada y WO regenerada explícitamente autorizada, respetando todos sus límites. Preparar WOs también requiere autorización vigente. Docs poseen las reglas; ante contradicción, detener la parte afectada y escalar.

## Entrada y selección

Requiere objetivo/hito, encargo de preparación, candidato/base y alcance permitido. Si solo se solicita código sin WO, señalar el requisito; no convertir esta skill en autorización. Si la preparación no está autorizada por encargo y fase vigente, entregar únicamente ruta y análisis permitido de campos faltantes, no una WO real.

## Contexto y procedimiento

Leer [plantilla](../../../.ai/work-order.md), tarjeta pertinente del [programa](../../../docs/roadmap/program.md), [spec/hito](../../../docs/specs/index.md), contrato del dueño y [gaps](../../../docs/roadmap/decisions-gaps.md). Leer [QA](../../../docs/quality/strategy.md) y casos/perfil del alcance para seleccionar evidencia; no todas las specs.

Cuando se autorice preparar: derivar resultado observable y non-goals; identificar dependencias aceptadas y archivos propios; enlazar invariantes/comandos sin reescribirlos; seleccionar gates por efecto/momento y preservar estado pendiente. Completar la plantilla con perfil proporcionado por QA y reviewer. Una duda de política va al dueño/profesional; una de frontera a Architecture. No proponer código para resolver ausencia de contrato.

Completar el núcleo obligatorio de la plantilla y solo sus secciones activadas por riesgo. Roles/comandos/principales → [registro exacto](../../../docs/architecture/capability-registry.md); datos personales/restore/IA → [privacidad](../../../docs/security/personal-data-lifecycle.md); propiedad → [boundaries](../../../docs/architecture/boundaries.md). Enlazar efecto/proveedor, transacciones/correcciones y evidencia desde sus dueños, sin copiar tablas. Registrar watch items con trigger, responsable y efecto retenido; nunca disfrazar un contrato ausente como prueba futura.

## Límites y salida

History SP2 no es input por defecto; solo por comparación histórica solicitada. No cerrar B/C/D, elegir parámetros empresariales ni producir Authorization: IMPLEMENTATION por inferencia. La WO preparada es candidata, requiere revisión separada de alcance/perfil y posterior autorización del propietario para ejecutar.

Salida: WO candidata solo si preparación autorizada; en otro caso objetivo, ruta canónica y faltantes. Incluir dependencias, contexto mínimo/descartado, gates, reviewer y acciones todavía prohibidas. No duplicar campos fuera de la plantilla.
