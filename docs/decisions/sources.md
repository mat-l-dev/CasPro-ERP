# Fuentes que sostienen decisiones

Consulta: **2026-09-10**. Fuentes primarias técnicas, sin copiar su documentación. Los datos de versión son un corte de consulta, no lockfiles ni validación de instalación. Las recomendaciones de arquitectura son inferencias propias apoyadas en estas capacidades y en el dominio, no recomendaciones atribuidas a los proveedores.

| ID | Fuente oficial | Qué sostiene / límite |
|---|---|---|
| S01 | [Django: versiones y soporte](https://www.djangoproject.com/download/) | Comparación de ramas actuales y horizonte de soporte; la elección 6.1 es juicio para CasPro |
| S02 | [Django: novedades 6.0 en documentación 6.1](https://docs.djangoproject.com/en/6.1/releases/6.0/) | CSP y template partials nativos; no implica que CasPro los implemente |
| S03 | [Compatibilidad Django/Python](https://docs.djangoproject.com/en/6.1/faq/install/) y [UUID en Python 3.14](https://docs.python.org/3.14/library/uuid.html) | Python 3.14 en la rama elegida y UUIDv7 estándar; UUID no es secreto |
| S04 | [Django: transacciones, atomic y on_commit](https://docs.djangoproject.com/en/6.0/topics/db/transactions/) | Semántica documentada de transacción exterior/savepoints/callbacks. Se consultó 6.0 porque la página equivalente 6.1 devolvió error en esta consulta; compatibilidad exacta 6.1 pendiente de validación posterior |
| S05 | [PostgreSQL 17: explicit locking](https://www.postgresql.org/docs/17/explicit-locking.html) | Locks y deadlocks; el orden concreto de CasPro debe comprobarse, no lo prescribe PostgreSQL |
| S06 | [PostgreSQL 17: SET](https://www.postgresql.org/docs/17/sql-set.html) | Duración transaccional de SET LOCAL y efecto de rollback/savepoint |
| S07 | [PostgreSQL 17: row security](https://www.postgresql.org/docs/17/ddl-rowsecurity.html) | Propietarios/BYPASSRLS, políticas y límites de comprobaciones referenciales |
| S08 | [Supabase: securing your API](https://supabase.com/docs/guides/api/securing-your-api) | Desactivar Data API, grants y separación de exposición; no asumir defaults |
| S09 | [Conectar PostgreSQL](https://supabase.com/docs/guides/database/connecting-to-postgres), [pooling](https://supabase.com/docs/guides/database/connecting-to-postgres/pooling-and-limits) y [upgrades](https://supabase.com/docs/guides/platform/upgrading) | Conexión persistente directa/session, diferencias transaccionales y versiones PostgreSQL del proveedor; major exacto se comprueba al provisionar |
| S10 | [Django Tasks](https://docs.djangoproject.com/en/6.1/topics/tasks/) y [referencia](https://docs.djangoproject.com/en/6.0/ref/tasks/) | Contrato de tareas y necesidad de motor de ejecución externo; no equivalencia con una outbox garantizada |
| S11 | [Tailwind: compatibilidad](https://tailwindcss.com/docs/compatibility) y [Node 24 LTS](https://nodejs.org/en/blog/migrations/v22-to-v24) | Build CSS y navegador moderno; Node como herramienta de construcción, no requisito del runtime Django |
| S12 | [HTMX: documentación y seguridad](https://htmx.org/docs/) | Opciones de eval/scripts/origen/historial; sus límites deben probarse con la UI real |
| S13 | [Alpine: CSP build](https://alpinejs.dev/advanced/csp) | Coste de adoptar Alpine bajo CSP; no habilitar unsafe-eval por conveniencia |
| S14 | [W3C WCAG 2.2](https://www.w3.org/TR/WCAG22/) | Objetivo de accesibilidad AA; una decisión de diseño no certifica conformidad |
| S15 | [Hypothesis: stateful tests](https://hypothesis.readthedocs.io/en/latest/stateful.html) | Secuencias y comprobación de invariantes; modelo de referencia independiente de la implementación |
| S16 | [Render: imágenes](https://render.com/docs/deploying-an-image), [regiones](https://render.com/docs/regions) y [regiones Supabase](https://supabase.com/docs/guides/platform/regions) | Despliegue por digest y región común candidata; no acredita red privada, latencia, contrato ni precio |
| S17 | [Playwright Python: traces](https://playwright.dev/python/docs/trace-viewer) | Retención de evidencia al fallar; no se ejecutó navegador de pruebas |
| S18 | [OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/) | Marco de selección de comprobaciones de seguridad; no checklist de cumplimiento rellenada |
| S19 | [GitHub: protección de Actions](https://docs.github.com/en/code-security/tutorials/secure-your-organization/protect-against-threats) y [OIDC](https://docs.github.com/en/actions/how-tos/secure-your-work/security-harden-deployments/oidc-in-cloud-providers) | Mínimo privilegio, pin por SHA y credenciales breves donde exista soporte |
| S20 | [Supabase: backups](https://supabase.com/docs/guides/platform/backups) | DB backup no contiene blobs de Storage ni resuelve toda la recuperación de credenciales/configuración |

## Evidencia interna

El mandato CasPro y la auditoría previa de esta conversación sustentan restricciones de esta fase y contraejemplos V1. No son normas tributarias ni benchmarks. El repositorio V1 se utiliza conforme a la [política de extracción](../v1-reference/policy.md).

No se investigaron ni aprobaron aquí reglas PCGE, tasas, marcos NIIF/NPIF, régimen, emisión electrónica o tratamientos de socios. Para esas afirmaciones se exige norma/fuente aplicable, vigencia, ámbito y validación profesional cuando corresponda: PENDING DOMAIN/REGULATORY VALIDATION.

Una fuente oficial de software prueba características de ese software, no una regla legal. Una fuente jurídica antigua puede seguir vigente; su edad por sí sola no la invalida. Una síntesis de IA sirve para localizar evidencia, no la reemplaza.
