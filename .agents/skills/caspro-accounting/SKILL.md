---
name: caspro-accounting
description: "Trabajar contratos de posting, cierre, políticas representadas o estados financieros CasPro; no mover dinero operativo ni resolver vigencia normativa sin investigación específica."
---

# caspro-accounting

Lee el [protocolo](../../../.ai/README.md) y el [estado](../../../docs/review.md) si no están en contexto. Esta skill no concede permiso: implementación requiere WO regenerada y autorización explícita; hoy solo análisis/documentación del alcance encargado. No generar WOs reales en la misión de agentes. Docs poseen las reglas; ante contradicción detener el efecto afectado y escalar, sin editar el contrato silenciosamente.

## Entrada y contexto selectivo

Requiere caso/afirmación, período/marco/política como inputs identificados, candidato y alcance. Leer [Accounting](../../../docs/accounting/architecture.md), [M07](../../../docs/specs/milestones/accounting-deep.md), sección de [políticas NPIF](../../../docs/accounting/npif-policy-catalog.md) aplicable y [gaps](../../../docs/roadmap/decisions-gaps.md). Marco real o política ausentes no se deducen del nombre de la empresa.

- Posting: añadir [hechos económicos](../../../docs/specs/cross-cutting/economic-facts.md) y productor solo si su contrato cambia.
- Cierre: secciones de período/corrección/completitud de M07 y políticas afectadas.
- EEFF: añadir [reporting](../../../docs/accounting/npif-reporting.md) y [M08/G1–G7](../../../docs/specs/acceptance/reporting-goldens.md); no todos los ejemplos por defecto.
- Cambio PCGE/marco/vigencia: activar normative-research para procedencia/aplicabilidad; [auditoría PCGE](../../../docs/evidence/pcge-code-audit.md) solo si la afirmación depende de ella.

## Trabajo y límites

Relacionar hecho, política/versiones, posting, mayor y salida mediante fuentes, sin inventar código de cuenta, mapping, tasa, política o aprobación. Aplicar comandos/guardas del dueño; no corregir directamente el estado de Treasury/Inventory. No convertir catálogo PCGE ni research en política.

Leer QA al seleccionar goldens/evidencia. Revisar B03/B04/B07/B08 y C01/C02/C03/C06 según el caso; datos/políticas reales siguen gate profesional antes de activación. Si una decisión excede superficie tipada, escalar al dueño/amendment, no añadir parámetro arbitrario.

## Salida / revisión

Fuentes/contexto, linaje/claim analizado, cambio permitido, evidencia y pendientes con owner. Reviewer independiente Accounting/integridad; profesional para política/activación, Architecture si cambia contrato. No autoasentar, certificar EEFF producidos por software ausente ni aprobar cifras reales desde un ejemplo sintético.
