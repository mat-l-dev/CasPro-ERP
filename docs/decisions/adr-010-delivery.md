# ADR-010 — Artefacto portable y operación gestionada inicial

Fecha: 2026-09-10. **Estado autoritativo por alcance.** ACCEPTED acepta el contrato de diseño, no acredita ejecución ni aprobación empresarial.

| Alcance | Estado | Condición o límite |
|---|---|---|
| Artefacto identificado, entornos separados y recuperación integral | ACCEPTED | El registro operativo describe lo realmente desplegado y recuperado |
| Render/proveedores, topología y planes de continuidad concretos | PROVISIONAL | H2/H3, conectividad y evidencia posterior de despliegue/restore; no contratar ni provisionar ahora |

## Context

Un ERP requiere saber qué versión opera y poder recuperarla. Self-host completo traslada mantenimiento al propietario; cloud no elimina esa responsabilidad de aceptación.

## Decision

GitHub Actions y artefacto OCI por digest; Render como candidato de aplicación, PostgreSQL managed, entornos separados y DB+blobs recuperables. [Delivery](../operations/delivery.md) define release, migraciones y operación.

## Alternatives

VPS inicial es posible si se acepta operación propia. Desplegar código latest con dependencias cambiantes impide reproducibilidad. Supabase self-host completo no aporta valor cuando solo se usa DB.

## Consequences

Build once/deploy same artifact; rollback condicionado por compatibilidad de schema. Presupuesto/región, RPO/RTO y restore pendientes antes de producción. No Docker ni infraestructura real durante la fundación. Fuentes: [S16/S19/S20](sources.md).
