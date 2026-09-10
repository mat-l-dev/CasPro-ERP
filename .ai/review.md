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
