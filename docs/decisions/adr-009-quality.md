# ADR-009 — Calidad como conjunto de evidencia

Fecha: 2026-09-10. **Estado autoritativo por alcance.** ACCEPTED acepta el contrato de diseño, no acredita ejecución ni aprobación empresarial.

| Alcance | Estado | Condición o límite |
|---|---|---|
| Evidencia por riesgo y contrato explícito de equivalencia | ACCEPTED | El resultado histórico solo acredita afirmaciones cuyo alcance e insumos siguen siendo equivalentes |
| Runner, deduplicación y selección parcial automática entre candidatos | PROVISIONAL | Validar manifiesto transitivo y detección de invalidaciones adversariales antes de permitir esa reutilización |

## Context

V1 repite suites/subconjuntos para perfiles y reporting; las marcas no distinguen de forma fiable el coste de DB. Repetir no resuelve un contraejemplo ausente.

## Decision

Validation Profile por WO: riesgo + alcance + evidencia. Una ejecución puede alimentar varios informes; no se fusionan variantes requeridas distintas. [Quality](../quality/strategy.md) es la fuente del contrato de equivalencia, causas de invalidación y condiciones para reutilización automática o excepción editorial manual.

## Alternatives

Suite universal por edición, E2E para cada formulario y porcentaje de coverage como aprobación generan coste sin garantía proporcional. Mocks de PostgreSQL no acreditan su comportamiento.

## Consequences

Fixtures locales, propiedades donde aportan, carreras controladas y candidato trazable. Primero instrumentación/baseline, luego presupuestos de tiempo. No se ejecuta evidencia dinámica en esta fase. Fuentes: [S15/S17](../research/technical-sources.md) y auditoría previa.
