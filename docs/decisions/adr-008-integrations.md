# ADR-008 — Adaptadores y durabilidad bajo demanda

Fecha: 2026-09-10. **Estado autoritativo por alcance.** ACCEPTED acepta el contrato de diseño, no acredita ejecución ni aprobación empresarial.

| Alcance | Estado | Condición o límite |
|---|---|---|
| Adaptadores, hechos versionados e intención durable necesaria | ACCEPTED | Estado empresarial en su dueño; efectos externos fuera de la transacción crítica |
| Backend outbox/jobs PostgreSQL, representación y worker concretos | PROVISIONAL | Primer consumidor, propietario de cada registro y evidencia de caída/reanudación/deduplicación; sin framework genérico previo |

## Context

Las integraciones fallan, repiten mensajes y pueden producir resultados ambiguos. Accounting necesita hechos sin acoplar el ledger a ventas.

## Decision

Adaptadores externos separados, hechos versionados e intención durable cuando el efecto lo requiera; outbox/jobs PostgreSQL es el backend candidato. Síncrono local por defecto. El [contrato de integración](../architecture/integrations.md) asigna la persistencia por propietario y delimita seguimiento técnico, leasing, duplicados, orden y conciliación.

## Alternatives

Broker/Celery inicial añade componentes sin necesidad demostrada. HTTP dentro del lock extiende la transacción. Django Tasks no reemplaza por sí mismo worker/backend productivo [S10](sources.md).

## Consequences

At-least-once e idempotencia/conciliación explícitas; no prometer exactly-once con un proveedor. No construir cola, worker o puertos vacíos antes de su caso de uso. Las presentaciones externas irreversibles requieren decisión empresarial adicional.
