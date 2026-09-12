---
name: caspro-compliance
description: "Trabajar Tax, filing mirror, Corporate y aplicabilidad legal de privacidad/IA CasPro; no sustituir dueños técnicos, investigación específica ni aprobación profesional."
---

# caspro-compliance

Consulta el [estado](../../../docs/review.md) para la fase vigente y aplica el [protocolo](../../../.ai/README.md#autoridad-y-autorización). Esta skill no concede permiso: implementación solo con fase habilitada y WO regenerada explícitamente autorizada, respetando todos sus límites. Preparar WOs también requiere autorización vigente. Docs poseen las reglas; ante contradicción, detener la parte afectada y escalar.

## Entrada y ramas

Requiere función, jurisdicción/período y hechos autorizados disponibles o faltantes; nunca rellenar RUC, régimen, vinculaciones o poderes con supuestos. Leer [gaps](../../../docs/roadmap/decisions-gaps.md) y elegir rama:

| Rama | Contexto requerido |
|---|---|
| Tax/determinación/expediente | [Tax](../../../docs/tax/architecture.md), [M09](../../../docs/specs/milestones/tax-deep.md) y fuente vigente identificada por el contrato |
| Acto Corporate / Beneficiario Final | [Corporate](../../../docs/corporate/architecture.md), sección Corporate de [M06](../../../docs/specs/milestones/treasury-corporate-deep.md); C09/Tax cuando la obligación lo requiera |
| Mutuo / financiación | Corporate/M06, sección mutuos de Tax, C06; Treasury/Accounting solo por el efecto que se estudia |
| Declaración externa, casillas o discrepancias | [External Tax Filing Mirror](../../../docs/specs/flows/external-tax-filing-mirror.md): dueño Tax, captura/preparación/presentación/eficacia/liquidación y revisión profesional; no emisión ni presentación SUNAT por el ERP |
| Aplicabilidad legal de privacidad o IA | [Privacidad](../../../docs/security/personal-data-lifecycle.md) y, solo para finalidad IA, [matriz peruana por propósito](../../../docs/research/normative/ai-peru-applicability.md). Implementación de restricciones/restore va a platform; esta ruta no transfiere hechos a Corporate |

## Trabajo, opcionales y escalación

Separar especificación con fixtures, preparación de expediente, validación profesional y activación real. Si cambia norma/vigencia/interpretación o se solicita validar una RTF, usar normative-research; no releer toda normativa para un cambio de presentación con regla vigente fijada. Si falta fuente aplicable, no emitir conclusión fiscal/legal.

Para versión de formulario, componente tributario o plazo aplicable, partir del [registro normativo](../../../docs/research/normative/normative-register.md) y memo del período; no fijar versiones PLAME ni componentes IGV/IPM en esta skill. Si cambia actor/comando/aprobación, contrastar el [registro exacto](../../../docs/architecture/capability-registry.md); facultad legal y capability no son equivalentes.

Enlazar gates C06–09 y demás pertinentes, actor competente y momento; no cerrar gates por completar campos. Implementar mutuo no autoriza contrato/desembolso; preparar Beneficiario Final no autoriza declaración. No cambiar hechos operativos o ledger para cuadrar impuesto, ni actuar como profesional que aprueba su propia salida.

## Salida / revisión

Resultado permitido con fundamento canónico, hechos faltantes, condición de activación, responsables y evidencia necesaria. Reviewer independiente Tax/Corporate y profesional competente en decisiones reales; Architecture si excede contrato. Acciones externas o incertidumbre de aplicabilidad quedan explícitamente retenidas, sin detener análisis independiente autorizado.
