# ADR-002 — Python 3.14 y Django 6.1

Fecha: 2026-09-10. **Estado autoritativo por alcance.** ACCEPTED acepta el contrato de diseño, no acredita ejecución ni aprobación empresarial.

| Alcance | Estado | Condición o límite |
|---|---|---|
| Python/Django, SSR integrado y uv | ACCEPTED | Elección arquitectónica para el producto |
| Combinación concreta Python 3.14/Django 6.1/driver/tipado/QA | PROVISIONAL | Resolver compatibilidad y locks; demostrar el conjunto en una fase ejecutable autorizada |

## Context

ERP documental con formularios, sesiones, ORM y transacciones; sin código CasPro ni dependencia que imponga una rama antigua.

## Decision

Python 3.14 estándar y Django 6.1 al parche vigente son la combinación candidata; uv para entorno/locks futuros. Servidor WSGI persistente inicialmente. Comparación, soporte y plan de revisión: [technology](../architecture/technology.md).

## Alternatives

Django 5.2 LTS es válido para priorizar soporte extendido; 6.0 ya no es la rama principal. FastAPI obliga a ensamblar más piezas para SSR/forms/auth. Otra plataforma no presenta una ventaja demostrada para este workload.

## Consequences

Se aprovechan capacidades nativas recientes sin copiar V1. Se acepta una actualización planificada hacia 6.2 cuando sea estable, no una dependencia de su roadmap. Locks y compatibilidad con psycopg/tipado/QA: REQUIRES LATER VALIDATION antes del primer código. Fuentes: [S01–S03](../research/technical-sources.md).
