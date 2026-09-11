# ADR-003 — PostgreSQL-first; Supabase como DB administrada

Fecha: 2026-09-10. **Estado autoritativo por alcance.** ACCEPTED acepta el contrato de diseño, no acredita ejecución ni aprobación empresarial.

| Alcance | Estado | Condición o límite |
|---|---|---|
| PostgreSQL y dominio independiente del proveedor | ACCEPTED | Separar servicios de plataforma y responsabilidades de recuperación |
| PostgreSQL 17, Supabase Cloud y conexión/pool concretos | PROVISIONAL | Contratación, compatibilidad, roles, conectividad y restore con evidencia posterior |

## Context

La operación de DB tiene coste propio; usar servicios managed puede reducirlo, pero no debe condicionar las reglas del ERP.

## Decision

PostgreSQL 17 como baseline inicial y Supabase Cloud opción A como proveedor candidato. Roles separados, schema privado, Data API desactivada, conexión directa o pool de sesión. [Evaluación por servicio y portabilidad](../architecture/technology.md).

## Alternatives

Otro PostgreSQL managed es intercambiable conceptualmente. VPS exige asumir backups/parches. Supabase Auth/Realtime/Edge Functions no resuelven una necesidad inicial identificada; Storage se evalúa al activar Documents.

## Consequences

No usar SDK ni funciones de proveedor para el dominio. Mover DB no mueve la plataforma completa. Aceptación contractual/presupuestaria y roles/conectividad/restore pendientes, sin contratación automática. Fuentes: [S07–S09/S20](../research/technical-sources.md).
