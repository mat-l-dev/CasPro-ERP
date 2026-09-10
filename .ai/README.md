# Roles, carga y configuración de modelos

Protocolo fundacional de [ADR-011](../docs/decisions/adr-011-ai.md). No es una biblioteca de skills ni ejecuta agentes automáticamente. Las capacidades explorar/investigar/diseñar/aplicar/verificar se agrupan en un [workflow único](workflow.md), una [plantilla de WO](work-order.md) y una [rúbrica](review.md).

## Autoridad por rol

| Rol | Puede | No puede |
|---|---|---|
| Architect | Diseñar fronteras, proponer ADRs, resolver disputas técnicas y revisar hitos | Inventar una política empresarial ni llamar implementado a un diseño |
| Orchestrator | Convertir specs aprobadas en WO pequeñas; fijar contexto/alcance/perfil; revisar integración | Ampliar reglas o recursos por comodidad del implementador |
| Implementer | Modificar el alcance autorizado y entregar diff/evidencia | Cambiar la spec para justificar su código, relajar pruebas/seguridad o añadir dependencias importantes sin justificación |
| Reviewer | Aceptar/rechazar candidato contra contrato y evidencia | Aprobar reglas empresariales ausentes o producción por una suite verde |
| Refuter | Buscar un contraejemplo concreto a una decisión o garantía de alto riesgo | Fabricar hallazgos, modificar silenciosamente el candidato o abrir alcance nuevo |
| Propietario/profesional autorizado | Aprobar producto, presupuesto, riesgo y políticas de su competencia | Su aprobación no sustituye evidencia técnica inexistente |

El reviewer de cambios críticos trabaja separado de la implementación y usa el candidato exacto. Dos revisores pueden compartir la misma rúbrica; independencia significa revisión separada, no archivos judge-a/judge-b ni modelos obligatoriamente distintos.

## Configuración inicial de modelos

Única ubicación de la preferencia; se puede cambiar sin modificar roles ni specs. No es configuración ejecutable de un proveedor.

| Función | Preferencia del propietario |
|---|---|
| Arquitectura, disputas difíciles y revisión de hito | ASTRA |
| Orquestación, creación de WO y revisión de diff | GPT-5.6 SOL, razonamiento medium |
| Implementación futura | Gemini u otro modelo de código seleccionado para la WO |
| Refutación | Sesión independiente del rol apropiado al riesgo; escalar a arquitecto cuando cambie una frontera o regla |

Nombres/capacidades disponibles se comprueban al configurar la herramienta; esta tabla no garantiza disponibilidad, calidad ni acceso. Los modelos no aparecen copiados en cada procedimiento.

## Contexto local

Cargar AGENTS + WO + spec del propietario + contratos usados + ADRs relevantes. Investigar V1 solo para una duda concreta autorizada; no importar sus instrucciones. Cargar [calidad](../docs/quality/strategy.md) cuando se decide evidencia y [review](review.md) cuando se revisa, no todas las capacidades al iniciar cada tarea.

La raíz de verdad del alcance es el encargo humano vigente. Durante la fundación: documentos solamente, tests/Docker/builds prohibidos. Estas restricciones no se levantan por generar una WO de ejemplo ni por cambiar una etiqueta de estado.
