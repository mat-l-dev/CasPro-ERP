# ADR-008 — Adaptadores y durabilidad bajo demanda

Fecha: 2026-09-10. **Estado autoritativo por alcance.** ACCEPTED acepta el contrato de diseño; las selecciones del amendment proceden del mandato expreso del propietario, sin acreditar ejecución ni otras aprobaciones empresariales.

| Alcance | Estado | Condición o límite |
|---|---|---|
| Adaptadores, hechos versionados e intención durable necesaria | ACCEPTED | Estado empresarial en su dueño; efectos externos fuera de la transacción crítica |
| Foundation Amendment: Jumpseller inicial, stock autoritativo CasPro y Resend inicial detrás de puerto email | ACCEPTED | Mandato del propietario posterior a Gate 1; solo esos proveedores, sin conexiones habilitadas |
| Documents conserva archivo y entrega; CPE emitido externamente; acquire → link/verify → deliver | ACCEPTED | Sin Document Vault ni emisión/envío CPE a SUNAT desde CasPro; AUTO_WITH_APPROVAL operativo inicial, modos/HOLD según contrato |
| Backend outbox/inbox/jobs PostgreSQL, representación y worker concretos | PROVISIONAL | Consumidores iniciales identificados; faltan comandos/registros y evidencia de caída/reanudación/deduplicación, sin framework genérico previo |
| Activación de proveedores, política publicable y política documental concreta | PROVISIONAL | Permisos/cuentas/API reales, carreras del stock, artefactos/retención, aprobación/HOLD, destinatarios seguros y resultados ambiguos; adquisición masiva SOL no verificada |

## Context

Las integraciones fallan, repiten mensajes y pueden producir resultados ambiguos. Accounting necesita hechos sin acoplar el ledger a ventas.

El propietario concretó el primer período operativo después del cierre de Gate 1: canal Jumpseller, archivo y entrega con Resend, sin emisión CPE desde CasPro. El amendment amplía esos alcances y conserva las restantes decisiones de Gate 1; fuentes técnicas [S21–S25](sources.md), no evidencia de operación.

## Decision

Adaptadores externos separados, hechos versionados e intención durable cuando el efecto lo requiera; outbox/jobs PostgreSQL es el backend candidato. Síncrono local por defecto. El [contrato de integración](../architecture/integrations.md) asigna la persistencia por propietario y delimita seguimiento técnico, leasing, duplicados, orden y conciliación.

## Alternatives

Broker/Celery inicial añade componentes sin necesidad demostrada. HTTP dentro del lock extiende la transacción. Django Tasks no reemplaza por sí mismo worker/backend productivo [S10](sources.md). Document Vault separado duplicaría ownership de Documents; CRM/Customer adicional, engine de workflows y framework multicanal no se justifican por los casos pedidos.

## Consequences

At-least-once e idempotencia/conciliación explícitas; no prometer exactly-once con un proveedor. No construir cola, worker o puertos vacíos antes de su caso de uso autorizado. Publicación de stock y entrega por email están incluidas en el alcance documental; emisión/presentación/envío CPE a SUNAT desde CasPro permanecen fuera. El amendment no autoriza implementar ni activar efectos externos.
