# Plantilla de Work Order

Plantilla conceptual. No es una orden de implementación activa ni una cola de tareas. Su uso para regenerar WOs de implementación queda pendiente de aceptar el sistema de agentes y de un encargo de preparación; esta misión solo crea el mecanismo.

| Campo | Contenido obligatorio cuando aplique |
|---|---|
| WO-ID / Goal | Identidad y resultado concreto |
| Authorization / Mode | Encargo que autoriza; estático/documental/implementación; ejecuciones y efectos permitidos |
| Git candidate / dependencies | Base/head/tree e insumos pertinentes, dependencias aceptadas y evidencia que se invoca; no HEAD aislado como prueba |
| Local gates | IDs aplicables del registro, owner, momento/trigger, evidencia pendiente y efecto que sigue desactivado; no copiar ni cerrar el registro |
| Canonical spec | Enlaces y revisión de la fuente de comportamiento; ADRs relevantes |
| Context required | Contratos y secciones mínimas; evitar cargar el ERP completo |
| Files expected | Archivos/módulos propios del cambio; justificar ampliación |
| Files forbidden | Áreas ajenas, Wbpro y legacy salvo lectura específica autorizada |
| Required behavior | Antes/después observable y errores esperados |
| Invariants | Referencias a propiedades canónicas y recursos compartidos |
| Acceptance criteria | Casos concretos que aceptan/rechazan el trabajo |
| Validation Profile | Categorías + casos + configuración; evidencia reutilizable y ampliación condicionada |
| Security impact | Actor/entidad/permisos/secretos/PII afectados o razón de no aplicación |
| Data/migration impact | Ownership, constraints, datos anteriores, reversión y despliegue si aplica |
| Documentation impact | Fuente que cambia; no copiar la regla en la WO |
| Explicit non-goals | Qué no se adelanta aunque parezca sencillo |
| Review | Rol/perfil independiente requerido; refuter si corresponde |
| Return format | Resumen del efecto, diff/archivos, evidencia real con identidad, fallos y pendientes |

El implementador declara qué no ejecutó y por qué. No rellena PASSED con supuestos ni oculta un fallo mediante retry. Si el caso requiere una regla empresarial que falta, formula la decisión y no la implementa unilateralmente.
