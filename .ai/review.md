# Rúbrica única de revisión y refutación

Cada revisor recibe el contrato, candidato identificado y evidencia. Evalúa el cambio, no si coincide con la explicación del implementador.

| Perfil por riesgo | Pregunta decisiva | Evidencia apropiada |
|---|---|---|
| Lectura/UI/accesibilidad | ¿La tarea es comprensible y operable con teclado, estados y errores coherentes? | Diff, tarea representativa y evidencia UI según alcance |
| Integridad/fiabilidad | ¿Qué contraejemplo crea o pierde dinero/stock, mezcla entidad o viola una transición? | Propiedad independiente, carrera, rollback y lectura de constraints |
| Seguridad | ¿Quién puede forzar el efecto y qué frontera puede eludir? | Amenaza aplicable, permisos, entradas adversariales y configuración |
| Resiliencia/operación | ¿Qué queda tras caer el proceso, proveedor o DB, y cómo se recupera? | Estado durable, idempotencia, migración/restore y manifiesto |
| Arquitectura/contexto | ¿La regla sigue local a su propietario y el consumidor depende solo del contrato? | Grafo, firmas, fuentes canónicas y coste de comprender el cambio |

Seleccionar perfiles según la WO, no seis revisores por commit. Cambio CSS pequeño no dispara auditoría monetaria; Treasury activa integridad/fiabilidad y evidencia transaccional; despliegue activa seguridad/resiliencia/operación.

## Refuter para alto riesgo

Intentar invalidar una conclusión mediante un escenario específico: mismo dinero en dos obligaciones; refund simultáneo con entrega; consulta sin filtro; mensaje repetido; restore que reenvía una orden; evidencia de otro candidato. Declarar supuestos y propiedad rota. Distinguir fallo demostrado, secuencia plausible estática y validación pendiente.

Un riesgo conocido puede seguir bloqueando aceptación. No esconderlo por estar documentado. No elevar hallazgos por antigüedad de una fuente sin comprobar su vigencia/aplicación.

## Veredicto

Entregar conclusión, evidencia, impacto y cambio requerido. Aceptar solo el alcance demostrado. Una decisión técnica de arquitectura no aprueba normativa ni hechos empresariales. Una revisión estática no certifica ejecución. Si se requieren dos jueces, usar sesiones independientes de esta misma rúbrica y resolver discrepancias por evidencia/contrato, no votación automática.

## Separación y salida del reviewer

Entradas: encargo/WO, base/head/tree e insumos relevantes, diff y afirmaciones/evidencia del autor. Reviewer trabaja en contexto separado, en lectura, y no corrige el candidato durante su evaluación. Si edita, pasa a ser autor de esa corrección y otro reviewer evalúa el nuevo delta. No auto-PASS seguido de merge.

Evaluar por separado cumplimiento de spec, corrección de código cuando exista, invariantes, seguridad, suficiencia/equivalencia de evidencia, scope creep y claims sobre gates. No repetir pruebas costosas sin cambio relevante, incertidumbre o contraejemplo que lo justifique; [Quality](../docs/quality/strategy.md#reutilización-verificable) conserva el contrato, no este documento.

Leer el diff real entre base y candidato; comprobar HEAD/tree e insumos al iniciar y cerrar. Un informe del autor o PASS anterior es evidencia contextual, no prueba del candidato actual. Por frontera afectada: contrastar dueño del hecho/ciclo con [boundaries](../docs/architecture/boundaries.md), distinguiendo custodia/ejecución/coordinación/autoridad legal; contrastar IDs y conjunciones con [registro exacto](../docs/architecture/capability-registry.md), y privacidad con su [contrato](../docs/security/personal-data-lifecycle.md). Un enlace que resuelve debe además acreditar el concepto citado.

Separar hallazgo factual de hallazgo arquitectónico: una fuente oficial puede estar desactualizada aunque el diseño sea coherente. Verificar fuente primaria vigente cuando la afirmación externa sea material; diferenciar fecha histórica, consulta y vigencia. Preservar evidencia antigua y registrar discrepancia/limitación, sin cambiar su corte ni exigir research ajeno al delta. Cada hallazgo declara severidad, archivo/afirmación, evidencia, impacto y corrección mínima; una ambigüedad pequeña de ownership puede ser material. Re-revisión proporcional cubre corrección y dependencias afectadas, sin reabrir por rutina lo aceptado.

Salida: identidad, alcance evaluado, fuentes, hallazgos con archivo/impacto/requisito, evidencia ejecutada/reutilizada/pendiente, gates no cerrados y veredicto. PASS acepta solo alcance demostrado; REQUEST CHANGES requiere un delta correctivo concreto; STOP retiene evaluación/efecto por candidato inesperado, autoridad insuficiente o fuente indispensable inaccesible, indicando requisito y parte independiente posible. Los resultados históricos PASS WITH CHANGES/FAIL conservan su alcance, no se reetiquetan. Un candidato sin revisión separada sigue PENDING INDEPENDENT REVIEW. Ningún veredicto autoriza producción o merge por sí mismo.
