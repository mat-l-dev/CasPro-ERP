# ADR-012 — Especificar M01–M09 antes de implementar

Fecha: 2026-09-11. Mandato: handoff Astra y autorización posterior del propietario para completar el programa documental. Sustituye únicamente la secuencia anterior que podía cerrar M00 y comenzar M01 mientras el resto permanecía en arquitectura.

| Alcance | Estado | Evidencia/condición |
|---|---|---|
| Separar documentación, skills y entrega | ACCEPTED por instrucción directa del propietario | Deep specs M01–M09 preceden al GLOBAL DOCUMENTATION FREEZE |
| No implementar CasPro en esta fase | ACCEPTED / obligatorio | No código funcional, tests CasPro, builds, Docker, migraciones, despliegues ni activación de integraciones |
| Auditoría externa pcge-peru | Autorización acotada ya ejecutada | Se reutiliza evidencia de la auditoría; no repetir pruebas sin motivo concreto nuevo. Nunca extiende permiso a Wbpro/CasPro |
| Aceptación global del candidato | Revisión independiente obligatoria | Estado vigente únicamente en [review](../review.md); editar documentación no equivale a aceptación |
| Derivar skills | Condicionado a aceptación del freeze | Investigación dedicada posterior con necesidad repetitiva demostrada; no derivación en esta misión |

Cuatro roadmaps independientes comparten hitos: producto expresa resultados; documentación completa decisiones/contratos; skills guían trabajo repetible después de freeze; entrega implementa incrementos mediante WO autorizada. Una dependencia de entrega M05→M07 no retrasa el análisis de Accounting hasta tener compras implementadas. Los contratos de hechos y casos sintéticos deben existir primero.

M01–M09 se especifican ahora de extremo a extremo, incluidos apertura, hechos económicos preservados desde los primeros hitos, servicios comprados, financiación, ajustes, EEFF y Tax. M10 conserva conceptos y triggers concretos; una capability necesaria para el primer paquete financiero no se esconde allí por comodidad.

La validación profesional del mutuo se programa en documentación, **antes del primer financiamiento**, aunque su implementación física sea M06. No es requisito para vender si no se activa financiación; tampoco se permite que un desembolso real espere una investigación prometida para M06.

## Condición de freeze

Para cada hito: dueño y fuente local; decisiones/provisionalidades; entradas/salidas; estados y comandos; invariantes; recursos/atomicidad/concurrencia; correcciones/replay; acceso/evidencia; UX; casos y perfil de validación; dependencias; alcance autorizado/prohibido; criterios de salida/escalación. Amendment de cierre 2026-09-11 por encargo del propietario: [gaps](../roadmap/decisions-gaps.md) distingue A diseño, B validación de implementación, C activación real y D evolución con trigger. Solo A impide presentar diseño resuelto; B debe declarar hipótesis/ensayo/pase/fallo, C función/momento y D trigger. Aceptación independiente permanece obligatoria. Una política real distinta de la superficie especificada requiere amendment, no un parámetro inventado para evitar A.

El freeze identifica commit/árbol exacto, fuentes/fechas, decisiones aceptadas, pendientes compatibles y revisión independiente por riesgo. Un candidato de IA puede quedar SPECIFIED; no obtiene FROZEN por autoevaluación. Tras aceptación, cambios de comportamiento usan amendment con análisis de impacto, versión y casos afectados; ninguna skill puede alterar una norma o política.

El estado global vive en [review](../review.md); el [programa](../roadmap/program.md) y las [deep specs](../specs/deep-spec-index.md) dirigen lectura local. Las WOs SP2 requieren regeneración después del freeze y de la investigación de skills, además de autorización explícita. La entrega podrá ser incremental; no requiere construir de una vez todos los módulos ni ejecutar categorías QA sin consumidor.
