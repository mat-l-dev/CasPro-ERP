# Workflow mínimo

Mecanismo de coordinación, no otra fuente de reglas empresariales. Autoridad: [roles](README.md). Evidencia: [calidad](../docs/quality/strategy.md).

| Etapa | Entrada y trabajo | Salida / condición de avance |
|---|---|---|
| 1. Orientar | Objetivo, spec local y alcance vigente; explorar únicamente incertidumbres relevantes | Hechos, preguntas y evidencia que cambia decisión |
| 2. Decidir/especificar | Investigar fuente primaria si corresponde; propuesta con alternativas y consecuencias | Spec/ADR revisable; aprobación empresarial donde haga falta |
| 3. Encargar | Preparación autorizada, spec aceptada, contratos y riesgos | WO con límites, non-goals y Validation Profile; no lista masiva de tareas |
| 4. Aplicar | Trabajo dentro del modo autorizado; implementar exige fase habilitada y WO regenerada autorizada | Diff mínimo; ejecución autorizada de evidencia; candidato identificado |
| 5. Verificar/aceptar | Candidato exacto, contrato y evidencia disponible | Aceptado/rechazado/condicionado con motivo; refutación según riesgo |
| 6. Sincronizar/cerrar | Impactos reales de lo aceptado | Fuentes afectadas coherentes y evidencia archivada por candidato; registro operativo solo tras despliegue real |

Explorar, research, proposal, spec y design son capacidades dentro de las dos primeras etapas, no cinco bibliotecas duplicadas. Sync/status/archive son parte del cierre, no ceremonias obligatorias para un cambio pequeño.

Implementar no otorga autorización para commit/push, despliegue, gasto, envío externo o borrado. Si el encargo ya los autoriza, no pedir permiso repetido. Si un cambio altera materialmente una política o frontera, detener esa parte y presentar la decisión concreta; continuar lo independiente.

La WO declara si se permite ejecución. En modo estático, el resultado se limita a evidencia de lectura; REQUIRES LATER VALIDATION para lo dinámico. No aplicar un procedimiento de tests por la mera presencia de su skill.

Al revisar un candidato se aplica el contrato de equivalencia e invalidación de [calidad](../docs/quality/strategy.md) y se añade el contraejemplo necesario. Este protocolo no mantiene otra definición de reutilización ni permite inferirla del nombre de una tarea o módulo.

Archive significa conservar la decisión/evidencia del trabajo de CasPro conforme a su política, no acceder o modificar legacy de Wbpro. No borrar historia empresarial ni reescribir una aprobación anterior.

## Entrega por candidato

Antes de editar: identificar rama/base/head y cambios existentes; no normalizar trabajo ajeno. Crear rama del alcance autorizado. Comprobar la fase en [review](../docs/review.md) y el encargo; para implementación, exigir además WO regenerada explícitamente autorizada y respetar sus límites conforme al [protocolo](README.md#autoridad-y-autorización). Si la preparación de WOs no está autorizada, limitarse al análisis de alcance permitido, sin producir una WO.

Commit/push/PR cuando el encargo los cubra. El PR nombra base/head/tree y claims/evidencia pendientes; no se fusiona por auto-PASS ni porque «se ve bien». Reviewer separado evalúa el candidato sin modificarlo; el autor corrige y entrega nuevo delta para revisión. Merge requiere aceptación del candidato aplicable y autorización del propietario; si ya existen ambas, proceder sin reconfirmación ceremonial. Publicar identidad del merge y evaluar equivalencia conforme QA.

Un hallazgo en docs se registra con fuentes/owner/impacto; no arreglarlo dentro de una skill ni cambiar semántica silenciosamente. Continuar lo independiente permitido. No cerrar gates con una simulación ni convertir falta de evidencia en fallo demostrado de runtime.
