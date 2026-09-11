---
name: caspro-review
description: "Revisar PRs o candidatos CasPro contra spec, alcance y evidencia con independencia del autor; no reparar el candidato durante la revisión."
---

# caspro-review

Lee el [protocolo](../../../.ai/README.md) y el [estado](../../../docs/review.md) si no están en contexto. Esta skill no concede permiso: implementación requiere WO regenerada y autorización explícita; hoy solo análisis/documentación del alcance encargado. No generar WOs reales en la misión de agentes. Docs poseen las reglas; ante contradicción detener el efecto afectado y escalar, sin editar el contrato silenciosamente.

## Entrada y contexto

Requiere base/head/tree, diff, encargo/WO y claims del autor. Leer [rúbrica](../../../.ai/review.md), [Quality](../../../docs/quality/strategy.md) y únicamente contrato/spec/gates que el delta toque. Sin identidad o evidencia suficiente, reportar qué falta; no inventar PASS. No es skill de implementación.

## Procedimiento

Determinar perfiles por riesgo. Separar conformidad de spec, corrección, invariantes, seguridad, evidencia, scope creep y cierre alegado de gates. Seguir consumidores afectados, no todo el ERP. Pedir skill de dominio solo como checklist de lectura cuando no baste el contrato; no activar su modo de escritura. Reutilizar evidencia por afirmación conforme a QA; rerun únicamente por invalidación/incertidumbre autorizada.

Un contraejemplo de dinero/stock, acceso, Accounting/Tax/Corporate, CPE, efectos externos o migración exige contexto canónico y especialista proporcional. Gate permanece pendiente si no hay prueba o aprobación de la función competente. Si el reviewer edita, es autor del delta y necesita otro reviewer.

## Salida y límites

Emitir identidad, alcance, hallazgos verificables, evidencia real/pendiente y veredicto de la rúbrica. No certificar runtime desde lectura ni cumplimiento desde fixtures. No fusionar por PASS propio; [workflow](../../../.ai/workflow.md) exige aceptación y mandato para merge. Sin reviewer separado, entregar paquete PENDING INDEPENDENT REVIEW.
