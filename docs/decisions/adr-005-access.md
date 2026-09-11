# ADR-005 — Autorización explícita y RLS

Fecha: 2026-09-10. **Estado autoritativo por alcance.** ACCEPTED acepta el contrato de diseño, no acredita ejecución ni aprobación empresarial.

| Alcance | Estado | Condición o límite |
|---|---|---|
| Autenticación y autorización explícitas, pertenencia y denegación por defecto | ACCEPTED | La agrupación Workspace sigue el alcance provisional de ADR-001 |
| RLS y configuración real de roles/políticas/conexiones | PROVISIONAL | Evidencia PENDING VALIDATION: satisfacer las condiciones de tenancy/access antes de aceptar el mecanismo y habilitar negocio sensible |

## Context

Confiar en que todo caller recuerde filtrar por entidad permite errores de aislamiento. RLS tampoco protege si se usa propietario/BYPASSRLS o se deja contexto de sesión.

## Decision

Seleccionar Django Auth y membresías/capacidades en Access dentro de la agrupación provisional Workspace. RLS es el mecanismo candidato para datos empresariales con rol limitado y contexto transaccional. Excepciones globales, cobertura del esquema, condiciones de aceptación y evidencia faltante: [tenancy/access](../architecture/tenancy-access.md).

## Alternatives

Solo aplicación tiene menos configuración pero conserva el bypass accidental. Schema/DB por entidad aumenta despliegue/migraciones/operación sin necesidad actual. Supabase Auth no se justifica por usar su DB.

## Consequences

La lectura empresarial también necesita frontera transaccional y resultados materializados. Se asume coste de roles/políticas/pruebas por una defensa concreta. REQUIRES LATER VALIDATION; no se habilita negocio sensible sobre una aproximación no probada. Si falla, revisar diseño antes de degradar garantías. Fuentes: [S06–S09](../research/technical-sources.md).
