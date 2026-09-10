# ADR-001 — Monolito modular y coordinación por flujo

Fecha: 2026-09-10. **Estado autoritativo por alcance.** ACCEPTED acepta el contrato de diseño, no acredita ejecución ni aprobación empresarial.

| Alcance | Estado | Condición o límite |
|---|---|---|
| Monolito modular, propiedad explícita y coordinación transversal | ACCEPTED | Contratos pequeños y sin ownership empresarial en workflows |
| Workspace como agrupación de Identity, Organization y Access | PROVISIONAL | Especificar los recorridos administrativos y su visibilidad sin ciclos; validar acceso en una fase ejecutable autorizada |

## Context

Un operador y desarrollo asistido por IA; dinero/stock necesitan transacciones comunes. V1 demuestra que imports acíclicos pueden esconder coordinación mediante callbacks y contratos que exponen ORM.

## Decision

Un monolito modular con APIs pequeñas y workflows transversales explícitos. Workspace agrupa provisionalmente Identity/Organization/Access sin fusionar sus propietarios ni políticas; Configuration deja de ser módulo genérico. Audit no llama negocio. [Matriz y límites](../architecture/boundaries.md) es el contrato detallado.

## Alternatives

Monolito libre reduce estructura pero amplía acoplamiento; servicios/microservicios añaden operación y consistencia distribuida sin consumidor actual. Mantener trece módulos por herencia no aporta garantía.

## Consequences

Un despliegue y transacciones compartidas; exige revisión de contratos y propiedad. Workflows pueden degradarse a nuevos mega-servicios: deben coordinar, no duplicar políticas. Reevaluar ante separación real de equipos/cargas. Esta selección no implica portar paquetes V1.
