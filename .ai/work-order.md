# Plantilla de Work Order

Plantilla reutilizable, no una orden de implementación activa ni una cola de tareas. Preparar o regenerar WOs requiere encargo explícito y una fase que lo permita según el [estado vigente](../docs/review.md). Preparación y ejecución son autorizaciones distintas, conforme al [protocolo](README.md#autoridad-y-autorización).

## Núcleo obligatorio

Completar cada campo; una exclusión lleva razón breve. Los detalles por riesgo se seleccionan en la tabla condicional, no se copian a toda WO.

| Campo | Contenido |
|---|---|
| WO-ID / Goal | Identidad y resultado concreto |
| Authorization / Mode | Encargo que autoriza; estático/documental/implementación; ejecuciones y efectos permitidos |
| Git candidate / dependencies | Base/head/tree e insumos pertinentes, dependencias aceptadas y evidencia que se invoca; no HEAD aislado como prueba |
| Owner / domain | Dueño canónico de cada hecho/ciclo afectado y coordinador si cruza contratos; no dueño inferido del archivo |
| Local gates | IDs aplicables del registro, owner, momento/trigger, evidencia pendiente y efecto que sigue desactivado; no copiar ni cerrar el registro |
| Canonical spec | Enlaces y revisión de la fuente de comportamiento; ADRs relevantes |
| Context required | Contratos y secciones mínimas; evitar cargar el ERP completo |
| Files expected | Archivos/módulos propios del cambio; justificar ampliación |
| Files / effects forbidden | Áreas ajenas; Wbpro solo lectura concreta autorizada conforme a su política; archive/15-history/legacy/Webrax fuera de lectura/modificación. Efectos no autorizados expresos |
| Required behavior | Antes/después observable y errores esperados |
| Invariants | Referencias a propiedades canónicas y recursos compartidos |
| Acceptance criteria | Casos concretos que aceptan/rechazan el trabajo |
| Validation Profile | Categorías + casos + configuración; evidencia reutilizable y ampliación condicionada |
| Risk triggers | Marcar secciones condicionales necesarias y justificar brevemente las no aplicables |
| Documentation impact | Fuente que cambia; no copiar la regla en la WO |
| Explicit non-goals | Qué no se adelanta aunque parezca sencillo |
| Review | Rol/perfil independiente requerido; refuter si corresponde |
| Return format | Resumen del efecto, diff/archivos, evidencia real con identidad, fallos y pendientes |

## Secciones condicionales

| Trigger | Contenido mínimo y fuente |
|---|---|
| Roles/comandos/permisos/configuración/automatización | [IDs exactos y conjunciones](../docs/architecture/capability-registry.md), principal humano/técnico, tenant/entidad/recursos/revisión, SoD y negativas; [roles](../docs/architecture/roles-delegation.md) y [gobierno](../docs/architecture/configuration-governance.md) solo si afectados |
| Datos personales, prompts, lectura/export o restore sensible | Clasificación/finalidad, datos sintéticos permitidos, [dueños](../docs/architecture/boundaries.md#propiedad-de-hechos-de-privacidad), sección del [ciclo de privacidad](../docs/security/personal-data-lifecycle.md), retención/evidencia y barrera de restore pertinente; permiso técnico separado de validación legal |
| Escritura durable, concurrencia, hechos económicos | Comando/atomicidad, idempotencia, recursos/orden de locks, auditoría, error/replay y reversión/corrección desde [CM0](../docs/specs/cross-cutting/command-matrix.md#cm0) y spec del dueño |
| Proveedor/integración/efecto externo | Dirección/entorno/adapter, efectos permitidos y retenidos, secretos por referencia, llamada fuera de locks, intención/outbox/UNKNOWN/conciliación según [integraciones](../docs/architecture/integrations.md); IA runtime añade [AIService](../docs/architecture/ai-assistance.md) y propósito |
| Schema/datos/migración/recuperación | Ownership/constraints, origen de datos, clean/upgrade/reversión, manifiesto/entorno y límites de despliegue de [delivery](../docs/operations/delivery.md); no migración ni restore por plantilla |
| Norma/política/aprobación profesional | Fuente/edición/período, hechos pendientes, responsable competente y C/D de activación; [registro normativo](../docs/research/normative/normative-register.md) cuando haya afirmación normativa |
| Rendimiento/UX/proyección | Volumen/corte, hipótesis y presupuesto a medir, negativa segura, accesibilidad y evidencia seleccionada desde QA/spec; no segundos arbitrarios ni catálogo completo de navegadores |
| Watch items de implementación | Incertidumbre compatible, dueño, trigger, evidencia requerida y efecto retenido; un hueco semántico exige amendment, no un watch item para autorizarlo |

Paquete para reviewer: candidato final/base/tree y diff, fuentes cambiadas, resultados del Validation Profile (ejecutados, reutilizados con fundamento o pendientes), límites y gates abiertos. No copiar prompts históricos ni declarar aceptación propia.

El implementador declara qué no ejecutó y por qué. No rellena PASSED con supuestos ni oculta un fallo mediante retry. Si el caso requiere una regla empresarial que falta, formula la decisión y no la implementa unilateralmente.
