---
name: caspro-work-order
description: "Preparar Work Orders CasPro acotadas desde specs y gates, cuando exista encargo de preparación; no implementar ni copiar WOs históricas."
---

# caspro-work-order

Lee el [protocolo](../../../.ai/README.md) y el [estado](../../../docs/review.md) si no están en contexto. Esta skill no concede permiso: implementación requiere WO regenerada y autorización explícita; hoy solo análisis/documentación del alcance encargado. No generar WOs reales en la misión de agentes. Docs poseen las reglas; ante contradicción detener el efecto afectado y escalar, sin editar el contrato silenciosamente.

## Entrada y selección

Requiere objetivo/hito, encargo de preparación, candidato/base y alcance permitido. Si solo se solicita código sin WO, señalar el requisito; no convertir esta skill en autorización. En la misión de agentes entregar únicamente ruta y análisis de campos faltantes, no una WO real.

## Contexto y procedimiento

Leer [plantilla](../../../.ai/work-order.md), tarjeta pertinente del [programa](../../../docs/roadmap/program.md), [spec/hito](../../../docs/specs/index.md), contrato del dueño y [gaps](../../../docs/roadmap/decisions-gaps.md). Leer [QA](../../../docs/quality/strategy.md) y casos/perfil del alcance para seleccionar evidencia; no todas las specs.

Cuando se autorice preparar: derivar resultado observable y non-goals; identificar dependencias aceptadas y archivos propios; enlazar invariantes/comandos sin reescribirlos; seleccionar gates por efecto/momento y preservar estado pendiente. Completar la plantilla con perfil proporcionado por QA y reviewer. Una duda de política va al dueño/profesional; una de frontera a Architecture. No proponer código para resolver ausencia de contrato.

## Límites y salida

History SP2 no es input por defecto; solo por comparación histórica solicitada. No cerrar B/C/D, elegir parámetros empresariales ni producir Authorization: IMPLEMENTATION por inferencia. La WO preparada es candidata, requiere revisión separada de alcance/perfil y posterior autorización del propietario para ejecutar.

Salida: WO candidata solo si preparación autorizada; en otro caso objetivo, ruta canónica y faltantes. Incluir dependencias, contexto mínimo/descartado, gates, reviewer y acciones todavía prohibidas. No duplicar campos fuera de la plantilla.
