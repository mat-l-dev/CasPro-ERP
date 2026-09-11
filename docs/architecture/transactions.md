# Transacciones, concurrencia e idempotencia

Contrato de [ADR-007](../decisions/adr-007-transactions.md). Propiedades empresariales canónicas: [invariantes](../domain/invariants.md). PostgreSQL READ COMMITTED es la base; no se adopta SERIALIZABLE global ni bloqueo universal.

## Un propietario de la transacción

El punto público de un comando declara si es una operación propia de módulo o un workflow transversal. Este propietario abre la transacción exterior; los participantes no confirman por separado. No existe ATOMIC_REQUESTS global: la autorización, la carga controlada de datos, el render y el trabajo externo tienen límites explícitos.

La futura implementación usará atomic con garantía de frontera exterior para comandos críticos (durable cuando corresponda); una llamada con transacción exterior desconocida se rechaza o utiliza un participante interno explícito. Así puede saberse cuándo terminó realmente el commit y cuándo persistir un rechazo. Savepoints internos no constituyen confirmaciones empresariales [S04](../decisions/sources.md).

Protocolo: autenticar y verificar membresía/capacidad inicial mediante Workspace → abrir contexto/transacción → cargar datos protegidos y verificar autorización sobre el recurso → tomar exclusiones necesarias → releer y validar guardas y revisiones relevantes → persistir estado + hechos + auditoría crítica + intención durable necesaria → commit → responder. La comprobación inicial no autoriza lecturas empresariales antes de establecer el contexto de DB. Un ID de correlación enlaza todo; no contiene PII.

## Preparar y ejecutar

**PREPARE ≠ EXECUTE.** Preparar una propuesta, abrir revisión, seleccionar filas, extraer datos o aceptar una sugerencia de IA no confirma un hecho económico ni autoriza un efecto externo. La preparación identifica entidad, intención, entradas/revisiones, impacto, evidencia y acciones del dueño. Puede persistir un borrador o propuesta explícitamente identificados; nunca simula pago, posting, despacho o envío.

Ejecutar exige el comando público del dueño, capacidad actual, revisión explícita del impacto y las guardas/idempotencia anteriores. Una preparación obsoleta se invalida; no se ejecuta reinterpretando silenciosamente sus entradas. La revisión y su activación deliberada deben poder completarse con teclado. El gesto que abre la revisión no puede confirmar también su acción. El resultado incierto conserva la misma intención y conduce a consultar/conciliar su efecto antes de otra ejecución; la UI y la IA no eligen una nueva clave para eludir ese control. El patrón no exige un diálogo adicional para cada edición reversible de maestro; cada comando mantiene su frontera semántica.

La revisión es humana en el caso interactivo; un modo automático solo puede consumir el mandato de política explícitamente admitido por su spec, con alcance/versión/evidencia y guardas vigentes. Por ejemplo, preparar una entrega CPE no la envía: el dispatch posterior verifica por separado el mandato AUTO permitido por Documents. Este principio no elimina esos modos ya especificados ni crea automatismos nuevos para dinero, stock o Accounting.

## Ficha de cada comando crítico

| Campo | Qué debe declarar |
|---|---|
| READS | Datos autoritativos y revisiones; qué lectura es solo descubrimiento |
| LOCKS / LOCK ORDER | Recurso compartido real, modo y orden común entre todos sus consumidores |
| WRITES | Raíces modificadas, historia, proyecciones, eventos, auditoría y jobs |
| PRE / POST | Guardas y propiedades verificables antes/después |
| IDEMPOTENCY | Efecto de repetir la intención; garantía natural o deduplicación durable; espacio de clave, fingerprint, resultado, retención y conflicto cuando proceda |
| RETRY | Errores transitorios concretos, límite y efecto de reautorizar/releer |
| FAILURES | Qué revierte, qué queda como rechazo y qué requiere conciliación |
| EVENTS | Hechos y destinos necesarios; ausencia de consumidor no inventa un worker |

## Bloqueos por recurso, no por función

Una restricción UNIQUE resuelve identidad/deduplicación; CHECK, propiedades de la fila; FK, pertenencia y referencia. Una suma que cruza varias filas necesita serializar el recurso que limita esa suma. Dos requests válidas individualmente no justifican aceptar ambas.

SUPERPROMPT 2 concreta los recursos competidos del primer circuito en su [matriz local](../specs/command-matrix.md). Esa matriz es la fuente del orden candidato para esos comandos y sustituye la hipótesis ilustrativa anterior; sigue PROVISIONAL, pendiente de validación ejecutable conforme ADR-007.

El orden aceptable se deriva de comandos y recursos concretos compartidos, con desempate estable entre recursos de la misma clase. Debe incluir la identidad de intención cuando exista deduplicación, restricciones/FKs relevantes y creación concurrente de raíces: no se puede bloquear una fila todavía inexistente. El mecanismo para ese caso se especifica y valida, no se inventa aquí. La matriz debe ser compatible entre todos los comandos que compitan; después necesita evidencia ejecutable de intercalación, rollback y retry. Su orden puede cambiar con esa evidencia sin abandonar estos principios.

Una operación que descubre otra raíz no la añade violando el orden acordado: vuelve a empezar con el conjunto completo. La lectura inicial para descubrir relaciones no decide importes. Tras adquirir locks se releen relaciones/revisiones; si el conjunto cambió, rollback y reintento acotado. Esto es especialmente necesario para un refund que descubre aplicaciones nuevas.

Aplicar dinero bloquea el objetivo Y el movimiento: objetivos distintos siguen compitiendo por el mismo cobro. Entregar y devolver dinero deben usar los mismos recursos de liquidación si afectan su elegibilidad. Un lock exclusivo sobre el pedido no protege por sí solo un cambio concurrente de Treasury.

Las políticas puras y lecturas informativas no necesitan locks. Edición de borradores puede usar versión esperada y conflicto optimista. Deadlocks/timeouts se tratan como fallos transitorios acotados, reejecutando toda la intención idempotente; no como aprobación ni como bucle infinito [S05](../decisions/sources.md).

## Idempotencia real

La decisión depende del efecto de repetir una intención, no de que el hecho pueda revertirse después ni de usar POST.

| Tipo de intención | Garantía requerida |
|---|---|
| Lectura sin efectos empresariales | No requiere registro de deduplicación de negocio; autenticar y autorizar cada lectura |
| Operación naturalmente idempotente | Demostrar que repetirla no duplica cambios, hechos, auditoría de aceptación ni trabajos asociados; mantener sus precondiciones. No añadir otra clave solo por uniformidad |
| Repetición que puede duplicar dinero, stock, documentos o trabajo | Deduplicación durable en la entrada pública. Clave requerida y no vacía, o identidad natural de la intención con unicidad transaccional equivalente; la reversibilidad posterior no la exime |

Cada comando documenta su clasificación y contraejemplo. Cuando requiere deduplicación, persiste en la misma transacción identidad única, fingerprint canónico y resultado estable. Misma intención y contenido devuelve el efecto ya confirmado; contenido diferente produce conflicto. Se revalida autorización al consultar ese resultado. El fingerprint usa entradas solicitadas normalizadas y versión de contrato; el resultado conserva las decisiones ya aplicadas, sin recalcular el pasado al reintentar.

El caso concreto delimita entidad/operación y, cuando corresponda, principal o mandato. [CM0 de SP2](../specs/command-matrix.md#cm0) especifica identidad, solicitudes en curso, rechazo y protección de efectos del primer circuito; plazos de retención y mecanismo ejecutable conservan pendientes explícitos. No se reutiliza una clave caducada para duplicar un hecho confirmado. Un mecanismo incompleto no se declara naturalmente idempotente para evitar ese trabajo.

La deduplicación se resuelve junto con los locks/constraints, no solo mediante una consulta anterior al bloqueo. No asumir que on_commit garantiza entrega de trabajo externo: un fallo del proceso después del commit puede perder ese callback. La intención que deba sobrevivir queda persistida dentro de la transacción.

## Reversión y efectos parciales

Refund y des-aplicación son operaciones distintas, coordinadas cuando proceda. Las aplicaciones activas y los importes comerciales se ajustan antes de confirmar una salida que reduciría su cobertura. Una transferencia/pago externo de resultado incierto pasa a conciliación, no a reintento ciego.

La corrección contable/fiscal no se deduce automáticamente del refund. Los estados y referencias empresariales quedan persistidos en sus módulos propietarios; el coordinador los consulta para continuar. El [contrato de coordinación durable](integrations.md) asigna el progreso de negocio y el seguimiento técnico sin que workflows posea hechos ni una saga genérica.

## Auditoría de aceptación y rechazo

Un fallo al persistir auditoría crítica impide confirmar el cambio económico. Un rechazo se escribe tras salir de la transacción revertida, en una transacción breve independiente, con actor/motivo mínimo. Si esa escritura falla por caída de DB, registrar señal operativa y alerta; no afirmar que el rechazo quedó duradero ni convertir el error en permiso.

Esta garantía depende de conocer la transacción exterior. No se reutiliza el patrón de «auditar fuera del savepoint» si un caller aún puede hacer rollback de la misma conexión.

## Evidencia pendiente

REQUIRES LATER VALIDATION: carreras controladas de cobro compartido, obligación compartida, refund-entrega, ajuste comercial-aplicación, creación concurrente de raíces, claves iguales/diferentes, deadlock/retry, rollback de auditoría/evento y agotamiento exacto de parcialidades. El diseño no declara estas propiedades implementadas.
