---
name: caspro-architecture
description: "Preparar amendments de arquitectura o contratos CasPro y explicar decisiones históricas concretas; no cambiar reglas dentro de una skill ni hacer mantenimiento local sin impacto de contrato."
---

# caspro-architecture

Consulta el [estado](../../../docs/review.md) para la fase vigente y aplica el [protocolo](../../../.ai/README.md#autoridad-y-autorización). Esta skill no concede permiso: implementación solo con fase habilitada y WO regenerada explícitamente autorizada, respetando todos sus límites. Preparar WOs también requiere autorización vigente. Docs poseen las reglas; ante contradicción, detener la parte afectada y escalar.

## Entrada y contexto

Requiere pregunta/contraejemplo, fuente afectada, resultado buscado y permiso de edición si se pide amendment. Leer [overview](../../../docs/architecture/overview.md), [boundaries](../../../docs/architecture/boundaries.md), ADR pertinente desde [decisions](../../../docs/decisions/index.md), spec del dueño y [gaps](../../../docs/roadmap/decisions-gaps.md). Para una pregunta documental menor, leer solo la fuente y sus referencias afectadas.

## Procedimiento por modo

Por frontera: permisos/comandos → [registro exacto](../../../docs/architecture/capability-registry.md); configuración → [gobierno y descriptores](../../../docs/architecture/configuration-governance.md); hechos de privacidad → [ownership canónico](../../../docs/architecture/boundaries.md#propiedad-de-hechos-de-privacidad) y [ciclo](../../../docs/security/personal-data-lifecycle.md#contexto-y-dueños); proyección de expediente → [Case Flow](../../../docs/specs/cross-cutting/case-flow-preview.md). Comprobar dueño del registro/ciclo frente a ejecutor/custodio/coordinador; no crear módulos genéricos para suplir falta de lectura del contrato. Una auditoría del sistema de instrucciones usa protocolo, catálogo y adapters; no reabre negocio salvo contradicción concreta.

- Amendment: identificar OLD/NEW, owner, invariantes/consumidores/evidencia afectados y alternativas; separar propuesta de aceptación. No cambiar una regla congelada sin encargo y revisión de ese cambio; una incompatibilidad real se reporta con owner/impacto, no se oculta en playbook.
- Trazabilidad: empezar por ADR actual. Leer únicamente el registro/candidato histórico que explique la pregunta, marcado HISTORICAL; no promover su estado a vigente. History es opcional, nunca contexto base.
- Referencia Wbpro: comprobar [política](../../../docs/architecture/wbpro-reference-policy.md) y autorización concreta antes de cualquier lectura. Copiar implementación o usarlo como runtime no es transferencia autorizada; conservar procedencia committed/uncommitted si se autoriza una consulta.

## Salida y revisión

Propuesta/explicación con fuentes, delta, motivo, incertidumbres, dueño, gates y criterio de validación; no decisión empresarial inventada. Architecture checkpoint y dueño revisan cambios materiales; seguridad/Accounting/Tax/Legal según frontera, no por nombre de modelo. Solo corregir documentos canónicos si el encargo explícito abarca esa fuente.
