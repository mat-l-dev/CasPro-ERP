# Evaluación tecnológica al 2026-09-10

Recomendaciones independientes del stack de V1. Las capacidades citadas se contrastaron con [fuentes oficiales](../decisions/sources.md). Las ventajas de productividad/operación son juicio de diseño para este producto; no benchmarks realizados.

GOOD/ACCEPTABLE/QUESTIONABLE son juicios comparativos, no estados de aceptación. Los alcances autoritativos viven en los [ADRs](../decisions/index.md): combinaciones/versiones concretas, configuración de acceso, backend de trabajo y proveedores de infraestructura conservan sus condiciones provisionales. Jumpseller y Resend son elecciones iniciales del propietario en ADR-008, con activación técnica pendiente.

## Evaluación y coste de propiedad

| Área / juicio | Selección y necesidad | Alternativas evaluadas | Coste operativo/cognitivo, QA/IA y portabilidad |
|---|---|---|---|
| Arquitectura — GOOD | Monolito modular: transacciones entre dinero/stock, un despliegue | Monolito sin fronteras; servicios; microservicios | Las APIs pequeñas facilitan contexto local y revisión. Un DB conserva atomicidad; disciplina interna necesaria. Distribución añadirá fallos sin necesidad actual |
| Backend — GOOD | Python 3.14 estándar con GIL; Django 6.1, parche vigente; uv | Python 3.13; Django 5.2 LTS/6.0; FastAPI; .NET/Java | Forms, ORM, auth y SSR evitan ensamblar múltiples sistemas. 6.1 aporta plataforma actual; exige actualización planificada. Compatibilidad de dependencias y rendimiento REQUIRES LATER VALIDATION |
| DB — GOOD | PostgreSQL 17 como línea inicial portable; psycopg 3 mediante ORM | PostgreSQL 18; MySQL; SQLite | Integridad relacional, RLS y locks verificables. 17 evita exigir de partida una versión distinta a la línea comprobable del proveedor; revisar major al provisionar. No SQLite para evidencia PostgreSQL |
| Hosting DB — ACCEPTABLE | Supabase Cloud como PostgreSQL administrado, opción A | PostgreSQL managed de otro proveedor; VPS; plataforma Supabase completa | Menor operación propia, coste recurrente y dependencia de control plane. El dominio usa protocolo PostgreSQL; salida exige restore real |
| Identidad — GOOD | Django Auth + capacidades/membresías de Workspace | Supabase Auth; identidad OIDC externa | Una sesión SSR y un responsable de identidad. MFA/recuperación requiere selección acotada posterior. Portabilidad sin acoplar usuarios al proveedor de DB |
| UI — GOOD | Django SSR + Tailwind 4 compilado + HTMX 2 selectivo + JS nativo pequeño | CSS propio; React SPA/API; Alpine obligatorio; islas | Una validación autoritativa y un despliegue. Node solo en build. Templates/componentes compartidos reducen divergencia de IA; CSP/accesibilidad deben validarse |
| Async — ACCEPTABLE | Síncrono para comandos locales; outbox/jobs PostgreSQL al primer consumidor durable | Celery/Redis; broker externo; callbacks on_commit solos | Worker pequeño sigue teniendo leasing/retry/observación que mantener; no existe hoy. No prometer que Django Tasks incorpora motor productivo |
| Testing — GOOD | pytest, Hypothesis selectivo, PostgreSQL y pocos Playwright | Solo ejemplos; mocks de DB; E2E masivo | Propiedades puras baratas, integración real donde importa. Separar fixtures y categorías. No poner tiempos objetivo sin baseline |
| Análisis — GOOD | Ruff + mypy con tipado fuerte en fronteras; escaneo de secretos/dependencias | AST que intenta demostrar algoritmos; lint solo | Reglas pequeñas sobre imports/contratos, sin prohibir patrones por nombre de archivo. IA debe entregar tipos y evidencia; configuración se validará después |
| Entrega — ACCEPTABLE | GitHub Actions → imagen OCI por digest → Render como candidato inicial | Git deploy con instalación cambiante; VPS desde el inicio | Un artefacto para staging/prod; CI y build añaden operación limitada. Render es reemplazable por VPS/contenedor; precio, región y acceso contractual requieren decisión humana |
| Observabilidad — ACCEPTABLE | Logs estructurados, métricas agregadas y correlación; OTLP como frontera si hace falta trazado | Plataforma completa de telemetría desde el inicio | Evitar spans por función y PII como etiquetas. Elegir backend según incidente/necesidad, no instalar OpenTelemetry por disponibilidad |

## Django: elección entre ramas actuales

La página oficial identifica 6.1.1 como versión principal actual, 5.2.17 como LTS y 6.0.8 como rama anterior. 5.2 conserva soporte extendido hasta abril de 2028; 6.1 hasta diciembre de 2027. 6.2 LTS está prevista para abril de 2027 [S01](../decisions/sources.md).

Se propone 6.1 como combinación candidata de ADR-002: CasPro no tiene dependencias ni código heredado que migrar; las capacidades nativas de CSP y fragmentos de templates encajan con SSR/HTMX sin añadir paquetes para esas funciones [S02](../decisions/sources.md). No se elige 6.0 cuando ya existe 6.1, ni 5.2 solo por ser la versión de V1. 5.2 sería aceptable si una dependencia esencial no soportara 6.1 o si se priorizara expresamente evitar la actualización prevista.

Revisar 6.2 cuando sea estable y compatible; no basar el diseño en APIs futuras. La versión exacta de cada paquete se fijará en lockfiles durante una fase autorizada de código. No se han generado lockfiles ni instalado dependencias.

## Servicios de Supabase por separado

| Servicio | Decisión | Motivo y salida |
|---|---|---|
| PostgreSQL | Seleccionado como candidato managed | Roles limitados, schema privado, SQL PostgreSQL normal; dump/restore, roles, extensiones y versiones evaluados |
| Auth | No adoptar | Django gestiona identidad; una migración de DB no obliga a migrar auth de proveedor |
| Storage | Object storage requerido inicialmente; Supabase Storage es candidato, proveedor aún sin elegir | Elegir retención, coste y API para Documents; metadata en PostgreSQL, bytes privados separados. Migrar blobs y ACLs es trabajo separado |
| Realtime | No adoptar inicialmente | No hay consumidor que justifique nueva entrega/seguridad de eventos al navegador |
| Edge Functions | No adoptar | Evita un segundo runtime para reglas que pertenecen a Django |
| Data API | Deshabilitar al provisionar CasPro | No se prevé acceso directo del navegador a tablas; la documentación permite desactivarla [S08](../decisions/sources.md) |

Migrar PostgreSQL no migra automáticamente Storage, Auth, Realtime, Edge Functions, secretos, políticas de plataforma o configuración. Se elige A; cualquier B necesita un consumidor y ADR de servicio concreto.

## Portabilidad y hosting

Conexión directa en backend persistente; pool de sesión si la red solo permite IPv4. Migración/backup usan conexión administrativa separada; pool transaccional no es el valor por defecto [S09](../decisions/sources.md).

Render permite imágenes preconstruidas por digest. Virginia está disponible tanto allí como en Supabase; es el par inicial candidato para reducir distancia aplicación-DB, no evidencia de red privada o baja latencia garantizada [S16](../decisions/sources.md). Validar latencia desde Perú, egress, IP estable y restricciones de red antes de contratar. Región de datos y términos quedan en H2, no se infieren de la cercanía geográfica.

Una VPS futura ejecutaría el mismo artefacto con proxy TLS y supervisión de procesos, más responsabilidad por parches y recuperación. PostgreSQL puede seguir managed. Self-hostear toda Supabase no se justifica cuando solo se usa PostgreSQL; un PostgreSQL estándar basta para ese destino.
