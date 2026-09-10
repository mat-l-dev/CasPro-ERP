# ADR-007 — Una transacción y recursos compartidos explícitos

Fecha: 2026-09-10. **Estado autoritativo por alcance.** ACCEPTED acepta el contrato de diseño, no acredita ejecución ni aprobación empresarial.

| Alcance | Estado | Condición o límite |
|---|---|---|
| Dueño de transacción, recursos comunes, guardas y atomicidad económica | ACCEPTED | READ COMMITTED con constraints/exclusión según propiedad; idempotencia según efecto de repetición |
| Orden concreto de locks y mecanismo por comando de creación/deduplicación | PROVISIONAL | Matriz completa de recursos e intenciones; demostrar intercalación, creación concurrente, fallo y retry antes de aceptar la implementación |

## Context

Aplicar cobros a distintos documentos y devolver mientras se entrega requieren exclusión sobre recursos compartidos distintos. El lock de una request o de una sola raíz no acredita ambos límites.

## Decision

READ COMMITTED con constraints y locks por propiedad; coordinador dueño de la transacción exterior, idempotencia según el efecto de repetir la intención y auditoría/hechos atómicos. [Transactions](../architecture/transactions.md) distingue los principios de la hipótesis local de orden y define clasificación, descubrimiento, replay y fallos. No impone registro de deduplicación a toda lectura o comando.

## Alternatives

SERIALIZABLE global introduce abortos/operación sin reemplazar la modelación. SELECT FOR UPDATE en todo añade contención. On_commit como única intención durable puede perder trabajo.

## Consequences

La matriz de locks forma parte de la spec, con pruebas de intercalación real. No se acepta un control sintáctico como prueba de conservación. Rechazos se auditan tras rollback exterior, con limitación explícita si falla DB. Fuentes: [S04–S05](sources.md).
