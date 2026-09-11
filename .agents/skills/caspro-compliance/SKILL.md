---
name: caspro-compliance
description: "Preparar trabajo CasPro de Tax o Corporate, mutuo y Beneficiario Final bajo sus contratos y gates profesionales; no investigar normas en cada tarea ni presentar/declarar por inferencia."
---

# caspro-compliance

Lee el [protocolo](../../../.ai/README.md) y el [estado](../../../docs/review.md) si no están en contexto. Esta skill no concede permiso: implementación requiere WO regenerada y autorización explícita; hoy solo análisis/documentación del alcance encargado. No generar WOs reales en la misión de agentes. Docs poseen las reglas; ante contradicción detener el efecto afectado y escalar, sin editar el contrato silenciosamente.

## Entrada y ramas

Requiere función, jurisdicción/período y hechos autorizados disponibles o faltantes; nunca rellenar RUC, régimen, vinculaciones o poderes con supuestos. Leer [gaps](../../../docs/roadmap/decisions-gaps.md) y elegir rama:

| Rama | Contexto requerido |
|---|---|
| Tax/determinación/expediente | [Tax](../../../docs/tax/architecture.md), [M09](../../../docs/specs/milestones/tax-deep.md) y fuente vigente identificada por el contrato |
| Acto Corporate / Beneficiario Final | [Corporate](../../../docs/corporate/architecture.md), sección Corporate de [M06](../../../docs/specs/milestones/treasury-corporate-deep.md); C09/Tax cuando la obligación lo requiera |
| Mutuo / financiación | Corporate/M06, sección mutuos de Tax, C06; Treasury/Accounting solo por el efecto que se estudia |

## Trabajo, opcionales y escalación

Separar especificación con fixtures, preparación de expediente, validación profesional y activación real. Si cambia norma/vigencia/interpretación o se solicita validar una RTF, usar normative-research; no releer toda normativa para un cambio de presentación con regla vigente fijada. Si falta fuente aplicable, no emitir conclusión fiscal/legal.

Enlazar gates C06–09 y demás pertinentes, actor competente y momento; no cerrar gates por completar campos. Implementar mutuo no autoriza contrato/desembolso; preparar Beneficiario Final no autoriza declaración. No cambiar hechos operativos o ledger para cuadrar impuesto, ni actuar como profesional que aprueba su propia salida.

## Salida / revisión

Resultado permitido con fundamento canónico, hechos faltantes, condición de activación, responsables y evidencia necesaria. Reviewer independiente Tax/Corporate y profesional competente en decisiones reales; Architecture si excede contrato. Acciones externas o incertidumbre de aplicabilidad quedan explícitamente retenidas, sin detener análisis independiente autorizado.
