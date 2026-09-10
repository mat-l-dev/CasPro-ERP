# ADR-004 — SSR, Tailwind y mejora progresiva

Fecha: 2026-09-10. **Estado autoritativo por alcance.** ACCEPTED acepta el contrato de diseño, no acredita ejecución ni aprobación empresarial.

| Alcance | Estado | Condición o límite |
|---|---|---|
| SSR, Tailwind compilado y HTMX selectivo; servidor autoritativo | ACCEPTED | Componentes compartidos por necesidad; sin estado empresarial paralelo |
| Versiones/configuración concreta de assets, CSP y compatibilidad de navegador | PROVISIONAL | Validar build y tareas accesibles en fase autorizada; WCAG es objetivo, no conformidad demostrada |

## Context

Se necesita UX de ERP densa y operable; no una SPA por apariencia moderna ni un lenguaje visual distinto por agente.

## Decision

Django SSR, Tailwind 4 compilado, HTMX 2 selectivo y JS nativo pequeño como selección de diseño, con configuración/versiones pendientes de validación. Definir componentes semánticos comunes para los primeros recorridos, sin construir una biblioteca exhaustiva antes de sus consumidores. [UI](../architecture/ui.md) define estados, accesibilidad, CSP y criterio de grid.

## Alternatives

CSS propio es viable pero requiere más mantenimiento de convenciones. React integral añade estado/API y pruebas; una isla futura se admite por necesidad. Alpine no se añade sin consumidor y compatibilidad CSP demostrada.

## Consequences

Se acepta build de assets y navegador moderno, con Node solo en construcción. La UI no decide dinero ni permisos. WCAG 2.2 AA es objetivo a demostrar, no conformidad actual. Fuentes: [S02/S11–S14](sources.md).
