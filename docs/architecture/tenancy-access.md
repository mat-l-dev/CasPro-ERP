# Tenancy, autenticación y autorización

La autorización explícita es un principio de diseño; el mecanismo RLS es PROVISIONAL, con evidencia PENDING VALIDATION según el estado autoritativo por alcance de [ADR-005](../decisions/adr-005-access.md). No está aceptada su aptitud ejecutable hasta demostrar las condiciones de este contrato.

## Qué garantiza cada capa

Enmienda de gobierno propuesta: [catálogo de 21 roles, composición por capability, SoD y delegación](roles-delegation.md) concreta este contrato; [configuración](configuration-governance.md) separa mandato administrativo de aprobación empresarial. Access conserva grants/mandatos; ninguna pantalla, is_staff o rol técnico concede autoridad económica. RA1–4 y CG1–5 amplían la especificación, con validación ejecutable pendiente y fase en [review](../review.md).

| Capa | Garantía buscada | Límite explícito |
|---|---|---|
| Django authentication | Identidad, sesión y recuperación | Autenticado no significa autorizado para una entidad |
| Workspace | Membresía vigente, capacidad y alcance de recurso | No reemplaza guardas del estado empresarial |
| API/caso de uso | Autoridad de la intención y pertenencia de IDs | No protege contra SQL arbitrario con credenciales administrativas |
| Queries explícitas | Alcance visible y consultas eficientes | Un programador puede olvidar un filtro |
| RLS y rol runtime limitado | Una consulta empresarial accidental sin filtro no devuelve otra entidad | No resiste control total del proceso que puede cambiar su contexto de DB |
| FK/UNIQUE/CHECK | Pertenencia referencial y estructura válida | No demuestran sumas concurrentes ni autorización |

## Contexto de ejecución

Cada operación recibe identidad verificada, entidad elegida y capacidades/alcances derivados del servidor. El navegador solo propone la entidad; nunca concede membresía ni entrega un contexto confiable. Los IDs de recursos se contrastan contra esa entidad. Ausencia o error produce denegación, no selección global.

Web, comandos, workers e imports utilizan la misma frontera pública. Cada job vuelve a construir contexto con principal de sistema y mandato explícito; no transporta una sesión del operador ni hereda su permiso indefinidamente. Un subcomando no cambia de entidad dentro de una transacción.

La revocación impide nuevas operaciones tras confirmarse. Una operación corta ya autorizada puede terminar; exportaciones, jobs y actuaciones privilegiadas revalidan antes del efecto o la descarga. Si se exige revocación instantánea de operaciones en curso, habrá que diseñar esa garantía expresamente y medir su bloqueo.

## RLS seleccionada

- Esquema empresarial privado, fuera de Data API. Usar rol runtime dedicado, sin propiedad de tablas, superusuario ni BYPASSRLS; sin credencial postgres/service_role en el servidor web.
- Las tablas con propiedad empresarial exigen legal_entity_id, políticas de lectura/escritura y protección de la pertenencia. FORCE RLS donde corresponda; el rol de migración es distinto y no se distribuye al runtime.
- La frontera abre una transacción corta, establece la entidad mediante SET LOCAL y ejecuta todas las lecturas protegidas dentro de ese alcance. El valor expira al terminar la transacción [S06](../research/technical-sources.md).
- No usar SET persistente por sesión. No devolver QuerySets perezosos ni cargar relaciones al render fuera de la transacción; materializar DTOs/páginas limitadas antes de salir.
- Sin contexto, la aplicación lanza un error explícito. RLS por sí sola puede devolver cero filas, no necesariamente una excepción: el contrato no confunde ambos comportamientos.
- Conexión directa o pool de sesión inicial. Pool transaccional no se activa sin validar contexto, cursores, prepared statements y reutilización de conexiones.
- La evolución del esquema debe impedir habilitar acceso empresarial a una tabla nueva sin protección y clasificación explícita. La aceptación requiere inventariar todas las tablas de negocio y excepciones, y detectar permisos/políticas que amplíen acceso. La presencia de legal_entity_id o de una política cualquiera no demuestra aislamiento; el verificador futuro y su integración en entrega siguen pendientes.

Superusuarios y roles BYPASSRLS evaden RLS; los propietarios también pueden hacerlo según configuración. Las comprobaciones referenciales tienen particularidades que RLS no elimina [S07](../research/technical-sources.md). Por eso la prueba debe usar el rol runtime real y comprobar referencias entre entidades, no solo el propietario usado por migraciones.

## Excepciones globales limitadas

Identity, Organization y Access conservan los propietarios delimitados en [boundaries](boundaries.md), aunque Workspace sea una agrupación provisional. Identidad/sesiones, directorio mínimo de entidades para selección y acceso mínimo a membresías forman el control de plataforma. La búsqueda autorizada previa a elegir entidad no permite leer perfiles empresariales completos. Estas excepciones no quedan cubiertas por la promesa de RLS por entidad y no contienen dinero, stock, CPE ni expedientes.

Solo Workspace accede a ellas: búsqueda de credenciales, lista de membresías del usuario autenticado y administración autorizada. No existe una API pública para listar todos los usuarios o entidades. El establecimiento y demás datos empresariales sí se acotan. El acceso privilegiado a múltiples entidades usa rol separado, motivo, operador y evidencia; no un parámetro all=True.

## Capacidades proporcionadas al producto

Catálogo pequeño de capacidades por operación; roles son agrupaciones de esas capacidades, no expresiones de código dispersas. Membresía y permisos por almacén/establecimiento solo cuando la operación usa ese recurso. No RBAC universal con jerarquías arbitrarias.

Lectura fiscal completa, exportación masiva, devolución de dinero, elevación de permisos y cierre/reapertura de períodos tienen capacidad propia y auditoría. is_staff no autoriza actos económicos. Django admin queda reservado a administración técnica acotada; ningún editor genérico de movimientos confirmados.

Django Auth se selecciona por coherencia con sesiones SSR. Supabase Auth queda fuera: usar su base no exige usar su identidad. Antes de exponer el ERP a Internet se requerirán MFA para privilegios, recuperación revisada, limitación de intentos y revocación de sesiones; elegir el componente mantenido en la fase de acceso, sin inventar criptografía.

Un operador único no representa dos revisores. Se registra la excepción de segregación y se muestran preparación/aprobación por la misma persona. El propietario decide qué operaciones necesitan aprobación externa y qué riesgo acepta.

## Validación obligatoria posterior

| Condición para aceptar RLS | Evidencia ejecutable futura |
|---|---|
| Configuración reproducible | Instalación limpia y upgrade con rol runtime real, sin propiedad/BYPASSRLS/elevación indebida; permisos y políticas efectivos, Data API fuera de exposición |
| Aislamiento y pertenencia | Dos entidades; lectura sin filtro, contexto ausente, INSERT/UPDATE/DELETE/bulk/SQL ordinario y referencias cruzadas, incluidos hijos. Confirmar denegación sin depender del formulario |
| Ciclo de conexión | Entidad A → B → sin contexto; commit, rollback, savepoint, error y retry con la conexión/pool elegido; ningún resultado perezoso escapa del alcance |
| Todas las entradas del alcance | Web, administración, comandos, imports, workers y exports construidos; autenticación global mínima, autorización de recursos y revocación según el contrato |
| Detección de regresiones de configuración | Introducir deliberadamente una tabla desprotegida, una política permisiva o un privilegio indebido y demostrar que impiden aceptar/desplegar el candidato; no basta probar una tabla ejemplar |
| Recuperación y viabilidad | Restore con roles/políticas correctos, inventario de excepciones preservado y consultas/conexiones representativas; límites de aceptación definidos antes de medir |

PENDING VALIDATION: ninguna de estas comprobaciones se ejecutó en la fundación. Antes de promover el mecanismo a ACCEPTED debe existir evidencia trazable y revisión de los resultados; una entrada futura aún no construida queda pendiente y debe validarse antes de habilitarla. Si falla, corregir o revisar ADR-005 antes de implementar operaciones sensibles; no degradar silenciosamente a «recordar el manager». SET LOCAL no convierte un proceso comprometido en confiable. El gate documental puede cerrarse con estas condiciones abiertas, sin autorizar su ejecución ni declarar la garantía implementada.
