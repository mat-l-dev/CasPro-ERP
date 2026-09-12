---
name: caspro-accounting
description: "Trabajar ledger, cierre, EEFF, templates, automatización y Shadow Accounting CasPro; no mover dinero ni sustituir investigación normativa o aprobación profesional."
---

# caspro-accounting

Consulta el [estado](../../../docs/review.md) para la fase vigente y aplica el [protocolo](../../../.ai/README.md#autoridad-y-autorización). Esta skill no concede permiso: implementación solo con fase habilitada y WO regenerada explícitamente autorizada, respetando todos sus límites. Preparar WOs también requiere autorización vigente. Docs poseen las reglas; ante contradicción, detener la parte afectada y escalar.

## Entrada y contexto selectivo

Requiere caso/afirmación, período/marco/política como inputs identificados, candidato y alcance. Leer [Accounting](../../../docs/accounting/architecture.md), [M07](../../../docs/specs/milestones/accounting-deep.md), sección de [políticas NPIF](../../../docs/accounting/npif-policy-catalog.md) aplicable y [gaps](../../../docs/roadmap/decisions-gaps.md). Marco real o política ausentes no se deducen del nombre de la empresa.

- Posting: añadir [hechos económicos](../../../docs/specs/cross-cutting/economic-facts.md) y productor solo si su contrato cambia.
- Cierre: secciones de período/corrección/completitud de M07 y políticas afectadas.
- EEFF: añadir [reporting](../../../docs/accounting/npif-reporting.md) y [M08/G1–G7](../../../docs/specs/acceptance/reporting-goldens.md); no todos los ejemplos por defecto.
- Cambio PCGE/marco/vigencia: activar normative-research para procedencia/aplicabilidad; [auditoría PCGE](../../../docs/evidence/pcge-code-audit.md) solo si la afirmación depende de ella.
- Templates/reglas, AI→draft, cuentas aplicadas o comparación shadow: sección correspondiente de [templates y automatización](../../../docs/accounting/templates-automation-shadow.md), en especial [aislamiento](../../../docs/accounting/templates-automation-shadow.md#shadow-accounting-e-aislamiento). Permisos/principales → [registro exacto](../../../docs/architecture/capability-registry.md); proveedor/prompt/datos → [AIService](../../../docs/architecture/ai-assistance.md) y [privacidad](../../../docs/security/personal-data-lifecycle.md). No trasladar autoridad del ledger experimental al oficial ni preferencias del agente de desarrollo al proveedor del producto.

## Trabajo y límites

Relacionar hecho, política/versiones, posting, mayor y salida mediante fuentes, sin inventar código de cuenta, mapping, tasa, política o aprobación. Aplicar comandos/guardas del dueño; no corregir directamente el estado de Treasury/Inventory. No convertir catálogo PCGE ni research en política.

Leer QA al seleccionar goldens/evidencia. Revisar B03/B04/B07/B08 y C01/C02/C03/C06 según el caso; datos/políticas reales siguen gate profesional antes de activación. Si una decisión excede superficie tipada, escalar al dueño/amendment, no añadir parámetro arbitrario.

## Salida / revisión

Fuentes/contexto, linaje/claim analizado, cambio permitido, evidencia y pendientes con owner. Reviewer independiente Accounting/integridad; profesional para política/activación, Architecture si cambia contrato. No autoasentar, certificar EEFF producidos por software ausente ni aprobar cifras reales desde un ejemplo sintético.
