---
name: caspro-review
description: "Revisar PRs o candidatos CasPro contra spec, alcance y evidencia con independencia del autor; no reparar el candidato durante la revisión."
---

# caspro-review

Consulta el [estado](../../../docs/review.md) para la fase vigente y aplica el [protocolo](../../../.ai/README.md#autoridad-y-autorización). Esta skill no concede permiso: implementación solo con fase habilitada y WO regenerada explícitamente autorizada, respetando todos sus límites. Preparar WOs también requiere autorización vigente. Docs poseen las reglas; ante contradicción, detener la parte afectada y escalar.

## Entrada y contexto

Requiere base/head/tree, diff, encargo/WO y claims del autor. Leer [rúbrica](../../../.ai/review.md), [Quality](../../../docs/quality/strategy.md) y únicamente contrato/spec/gates que el delta toque. Sin identidad o evidencia suficiente, reportar qué falta; no inventar PASS. No es skill de implementación.

## Procedimiento

Determinar perfiles por riesgo. Separar conformidad de spec, corrección, invariantes, seguridad, evidencia, scope creep y cierre alegado de gates. Seguir consumidores afectados, no todo el ERP. Pedir skill de dominio solo como checklist de lectura cuando no baste el contrato; no activar su modo de escritura. Reutilizar evidencia por afirmación conforme a QA; rerun únicamente por invalidación/incertidumbre autorizada.

Aplicar los checks condicionales de la rúbrica: diff real y candidato inalterado, [ownership canónico](../../../docs/architecture/boundaries.md), [IDs/conjunciones](../../../docs/architecture/capability-registry.md) y [privacidad](../../../docs/security/personal-data-lifecycle.md) solo si afectados. Distinguir corrección factual de arquitectura y comprobar fuentes oficiales cuando sean materiales. Un PASS previo no sustituye esa evaluación; devolver corrección acotada o STOP con requisito faltante, sin reabrir todo el ERP.

Un contraejemplo de dinero/stock, acceso, Accounting/Tax/Corporate, CPE, efectos externos o migración exige contexto canónico y especialista proporcional. Gate permanece pendiente si no hay prueba o aprobación de la función competente. Si el reviewer edita, es autor del delta y necesita otro reviewer.

## Salida y límites

Emitir identidad, alcance, hallazgos verificables, evidencia real/pendiente y veredicto de la rúbrica. No certificar runtime desde lectura ni cumplimiento desde fixtures. No fusionar por PASS propio; [workflow](../../../.ai/workflow.md) exige aceptación y mandato para merge. Sin reviewer separado, entregar paquete PENDING INDEPENDENT REVIEW.
