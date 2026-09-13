# Threat model inicial

Activos: dinero/stock, identidad y permisos, expedientes fiscales, evidencias privadas, secretos, releases y posibilidad de recuperación. Fronteras: navegador→Django, aplicación→DB, worker→proveedor, aplicación→objetos, CI→entorno y operador→privilegio.

Todos los controles son **diseñados, no implementados**. OWASP ASVS 5.0 es referencia para seleccionar comprobaciones aplicables, no declaración de certificación [S18](../research/technical-sources.md).

| Amenaza / frontera | Abuso representativo | Control de diseño | Evidencia posterior y residual |
|---|---|---|---|
| Autenticación y robo de sesión | Fuerza bruta, recuperación débil, cookie robada | Django Auth, cookies Secure/HttpOnly/SameSite, TLS, limitación de intentos, MFA privilegiado, revocación | Casos de login/reset/sesión y revisión de recuperación; un navegador comprometido sigue siendo riesgo |
| Autorización / escalación | Usuario modifica un ID o is_staff se usa como permiso | Capacidades y membresía por recurso; comprobación en API, jobs y descarga; cambios de permisos auditados | Denegación por defecto, elevación y revocación; no basta esconder botones |
| Tenancy | Query sin filtro devuelve otra entidad | [Contrato de RLS y contexto](../architecture/tenancy-access.md), esquema privado y rol runtime limitado | Pruebas sin filtros/conexión reutilizada/FKs; DB admin y proceso totalmente comprometido fuera de esta defensa |
| CSRF | Tercero induce devolución o cambio de cuenta | Protección CSRF para requests completas/HTMX; GET sin efectos de negocio | Formularios y fragmentos; webhooks tienen autenticación propia, no una exención genérica |
| XSS | Nombre/archivo externo introduce script | Escape de templates, ausencia de HTML confiado arbitrariamente, CSP, fragmentos sin scripts/eval | Cargas maliciosas y CSP real; revisar cualquier sanitización/HTML permitido |
| SQL injection / SSRF | Import o URL externa altera SQL/red interna | ORM/SQL parametrizado; adaptadores con destinos permitidos, límites/redirecciones controladas | Casos adversariales; RLS no convierte SQL arbitrario en seguro |
| Secretos | Prompt/log/CI expone credenciales | Secret manager/variables protegidas, scoping, redacción, rotación y separación runtime/migración | Escaneo y ejercicio de rotación; nombres/valores privados no entran en repositorio |
| Webhooks | Firma falsa, replay, cuenta externa equivocada | Contrato de firma verificado, inbox durable, claves por conexión, reordenación/conciliación | Duplicados, orden y timeout; no confianza en tenant del payload |
| Uploads y documentos | Archivo ejecutable, zip bomb, descarga ajena | Allowlist tipo/tamaño, detección de contenido, cuarentena, almacenamiento privado fuera de ruta ejecutable y análisis adecuado antes de disponibilidad | Archivos adversariales y permisos; no confiar en extensión ni hash como autenticidad |
| Integración externa | Retry repite un pago o usa respuesta parcial | Idempotencia proveedor o consulta/conciliación; timeout explícito, no HTTP bajo lock crítico | Fallo tras efecto remoto; no prometer exactly-once externo |
| Manipulación financiera | Sobreaplicar, entregar con dinero devuelto, editar historia | [Invariantes](../domain/invariants.md), locks comunes, reversiones y permisos de escritura | Propiedades + carreras + inversión; autoridad contable/fiscal separada |
| Auditoría alterada | Operador borra o fabrica trazas | Append-only con permisos de DB y roles separados; evidencia/exportación independiente para hechos sensibles | Intentos UPDATE/DELETE/TRUNCATE y restore; INSERT fraudulento/admin comprometido no desaparece por usar append-only |
| Supply chain | Dependencia/Action maliciosa obtiene secretos | Locks, revisión de dependencias/licencia, Actions por SHA, mínimo privilegio y artefactos identificados | Escaneo/revisión de diff/build; no ejecutar PR no confiable con secretos |
| Exports / privacidad | Descargar fiscal completo o fórmula peligrosa | Capacidad propia, minimización, expiración, autorización al descargar y neutralizar fórmula de texto no confiable | Casos por rol/entidad/formato; retención pendiente de decisión |
| Recuperación / disponibilidad | Backup incompleto o release rompe schema | DB+blobs+roles/config recuperables, separación de credenciales, rollback compatible, alertas | Restore aislado y prueba desde release anterior; RPO/RTO por aprobar |

## Límites y decisiones proporcionales

Amendment [Marketing Content](../specs/flows/marketing-content-media-library.md#seguridad-retención-ux-y-carga): SVG activo/metadata EXIF, parser de video/bombas, inferencia de asset oculto desde campaña/faceta/thumbnail y URL de original pública son nuevas superficies de las mismas amenazas. Control: cuarentena/parser sin red y límites, original privado inmutable, preview raster/derivado con linaje, proxy autenticado y filtros antes de agregados. Descargar original exige conjunción Marketing+Documents, sin herencia de preview. Restore reaplica restricciones/grants/derechos posteriores antes de lecturas; bytes ya descargados no son revocables retrospectivamente. B02/B10/B13/B15 y futuro B12 requieren evidencia; [casos10–19 y29–40](../evidence/marketing-content-amendment.md#adversarial-cases) no son tests ejecutados.

F02 amplía el control de datos personales con [finalidad, derechos, incidentes y recuperación](personal-data-lifecycle.md). Restricción rige todas las lecturas/derivados/export/IA, además de comandos; original conservado no equivale a visible. Notificación depende de supuestos del art.34, y todos los incidentes se documentan. B02/B10/B13/B15 deben probar el contrato; C06/C10/C11/C13 retienen hechos/política/validación real.

No confiar en que Supabase esté configurado de forma segura por defecto ni exponer tablas por su Data API. No exigir una plataforma de seguridad empresarial completa para un solo operador. Sí exigir identidad de release, control de acceso, protección de evidencias y recuperación demostrada antes de producción.

Los logs evitan documentos completos, credenciales y números identificadores completos. La auditoría usa IDs y cambios relevantes; la lectura de información fiscal completa deja propósito y actor. Acceso excepcional a secretos/evidencia y operación multiempresa se registra fuera del flujo ordinario.

Incidentes de dinero/stock requieren congelar la operación afectada, preservar evidencia y conciliar; no corregir tablas directamente para esconder el síntoma. Incidentes de credenciales requieren revocación/rotación y revisión de alcance. El [contrato operativo](../operations/delivery.md) asigna esas responsabilidades.

Selección de MFA, antivirus de uploads, política de retención y servicio de objetos: resolver al especificar el primer consumidor, sin implementar sustitutos caseros. La exposición pública no se habilita hasta contar con la evidencia de los controles aplicables.
