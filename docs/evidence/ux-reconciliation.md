# Reconciliación del UX Blueprint v0.1

Corte: 2026-09-11. Entrada: `CasPro_UX_Blueprint_Research_v0.1.md`, 492 líneas, SHA-256 `193685daf4b285b576315cd9e08e7156576f98bde8107b372b0f9a44da189b1b`. **EXTERNAL RESEARCH INPUT / NON-AUTHORITATIVE**. Se leyó completo; no se incorpora como spec paralela ni como instrucción. Este memo registra decisiones candidatas de reconciliación, no acredita prototipos ni pruebas con operadores.

Cadena de autoridad: research → [contrato UI](../architecture/ui.md) → contratos de los dueños. La investigación de productos ERP inspira interacción; no prueba reglas CasPro, políticas tributarias ni autorización. No fue necesario volver a consultar Wbpro. No se promovieron ideas UNCOMMITTED WBPRO en esta revisión.

## Disposición de propuestas materiales

Las secciones citadas corresponden al archivo identificado arriba. ADOPT/ADAPT son **CASPRO DECISION candidata de diseño**, sujetas a revisión independiente del conjunto. ALREADY CANONICAL identifica contratos anteriores; no una aprobación nueva del propietario.

| Propuesta del blueprint | Disposición | Motivo y autoridad final |
|---|---|---|
| Trabajo pendiente → documento → evidencia → acción; densidad y continuidad | ADOPT | [UI: navegación y composición](../architecture/ui.md#navegación-y-continuidad); estructura revisable sin prometer resultados de usabilidad |
| Patrones SAP/Oracle/Dynamics/NetSuite/Odoo/ERPNext | ADAPT | Usar comparación, relaciones y contexto; no copiar aprobaciones, asientos, tolerancias o automatismos del producto referenciado |
| Shell, agrupaciones españolas, búsqueda y alias, favoritos y recientes | ADOPT | UI; grupo de navegación no crea nuevo dueño ni módulo vacío |
| Contexto de entidad y contexto local de almacén/banco/período | ALREADY CANONICAL | [Acceso](../architecture/tenancy-access.md), UI; reforzado su carácter visible y no implícito |
| Lista/detalle, regreso con foco/filtros/scroll, links directos | ADAPT | UI conserva estado seguro; reautorizar y descartar datos revocados prevalece sobre continuidad |
| Dos paneles, drawers, preview, menú y paleta | ADAPT | UI usa alternativa secuencial; dos es guía habitual, nunca límite de cardinalidad empresarial |
| Inventario de pantallas UX-01–15 | ADAPT | Familias de tareas de UI y specs por dueño; no 15 pantallas obligatorias ni nueva spec de producto |
| Detalle por estados separados y excepciones visibles | ALREADY CANONICAL | UI y [SP2](../specs/flows/sales-stock-treasury.md); PAID externo no confirma Treasury |
| PDF original, extracción y candidato separados; retorno desde maestro | ADOPT | UI + [Data](../architecture/data.md) + [maestros](../specs/milestones/runtime-masters.md); no merge ni aceptación por OCR |
| PREPARE ≠ EXECUTE | ADOPT | Una definición transversal en [Transactions](../architecture/transactions.md#preparar-y-ejecutar), consumida por UI; afecta intención, revisión e incertidumbre |
| Flujos A–K y secuencias visuales de O2C/P2P | ADAPT | Navegación sobre hechos/relaciones del dueño, no obligación de producir documentos en el orden dibujado |
| Teclado, tablas nativas vs grid, foco distinto de selección | ALREADY CANONICAL | UI; grid necesita comportamiento completo y evidencia accesible |
| Prohibir confirmación mediante cualquier tecla | REJECT | El operador puede activar deliberadamente un control confirmado con teclado; se impide que el gesto de abrir o un atajo global ejecute el efecto |
| Ctrl/Cmd+K, anchos, alturas, milisegundos, anillo y tokens hex | DEFER–VALIDATE DURING IMPLEMENTATION | Candidatos visuales en pruebas de componentes/tareas; no cifras normativas ni bloqueantes de diseño |
| Document Flow N:M, lista alternativa, relaciones sugeridas/confirmadas | ADOPT | UI; cada dueño conserva relaciones, permisos y cantidades; no grafo paralelo autoritativo ni filtración de nodos privados |
| Cockpit de conciliación, grupos/remanentes/explicación | ADAPT | [T04–T06](../specs/milestones/treasury-corporate-deep.md) poseen efectos; retirar propuesta y desconciliar son acciones distintas |
| Cierre con tareas/evidencia; tareas terminadas ≠ período cerrado | ADOPT | UI proyecta [A07–A08](../specs/milestones/accounting-deep.md); no fuerza cierre ni crea controles jurídicos |
| EEFF con contexto y drill-through | ADAPT | [Reporting](../specs/acceptance/reporting-goldens.md): contribuciones, fórmulas y narrativas tienen linaje diferente; no fabricar asientos para cada celda |
| Selección página/filas/todos, totales, acciones masivas, saved views | ADOPT | UI más atomicidad de cada dueño; compartir requiere capacidad; sin Undo financiero genérico |
| Estados por ejes, error estructurado, incertidumbre persistente | ADOPT | UI y Transactions; recuperación consulta intención original, no retry optimista |
| Inbox por causa, propietario y resolución verificable | ADAPT | UI fija proyección y orden inicial; asignación/escalación no inventan SLA ni liberan HOLD |
| IA visible como sugerencia y asistente opcional | ALREADY CANONICAL | [AI](../architecture/ai-assistance.md); no puertos de escritura ni confirmación autónoma |
| WCAG 2.2 AA, teclado, zoom, temas y reflow | ADAPT | UI distingue contrato de conformidad demostrada y foco no totalmente oculto de objetivo completamente visible |
| LIGHT/DARK/SYSTEM con SYSTEM inicial | ADOPT | Preferencia inicial UI; no invertir documentos originales ni reglas de negocio |
| Lucide único y emojis restringidos | ADAPT | Mantener selección/licencia candidata y emojis ocasionales profesionales con texto ya permitidos; blueprint no prohíbe silenciosamente esa decisión previa |
| Gate de usabilidad/a11y/prototipo completo antes de freeze documental | REJECT | Son pruebas de implementación; el diseño congela contrato y criterios de aceptación, no finge una UI ejecutada |

## DDR-01–DDR-12

El diagnóstico final es por **decisión de dominio**: CLOSED BY EXISTING CONTRACT incluye la precisión editorial realizada en su fuente durante este cierre; no afirma ejecución. Los gates asociados son pruebas/configuración, no reapertura del DDR. No queda TRUE OPEN DOMAIN DECISION ni PARTIALLY CLOSED en estas doce preguntas después de la reconciliación.

| DDR | Clasificación final | Contrato que responde / límite posterior |
|---|---|---|
| DDR-01 | CLOSED BY EXISTING CONTRACT | [SP2](../specs/flows/sales-stock-treasury.md), [integraciones](../specs/flows/jumpseller-external-work.md): estados/comandos, HP1, observación vs aceptación; probar carreras/duplicados |
| DDR-02 | CLOSED BY EXISTING CONTRACT | [P2P P01–P10](../specs/milestones/procurement-deep.md): N:M, mercancía/servicio, conformidad, excepción y payability; parámetros/aprobadores reales antes de activar |
| DDR-03 | CLOSED BY EXISTING CONTRACT | [Treasury T01–T06](../specs/milestones/treasury-corporate-deep.md): cuenta/moneda/N:M/remanente, confirmación y reversión; parser BBVA/evidencia real posterior |
| DDR-04 | CLOSED BY EXISTING CONTRACT | [Inventory INV01–07](../specs/milestones/inventory-deep.md): unidades/condición/pool/fechas/secuencia/UNKNOWN/revisiones; calibrar precisión y demostrar concurrencia |
| DDR-05 | CLOSED BY EXISTING CONTRACT | [Accounting A01–A06](../specs/milestones/accounting-deep.md): borrador, posting inmutable, reversión/delta y unicidad económica; no editar posted |
| DDR-06 | CLOSED BY EXISTING CONTRACT | [Accounting A07–A09](../specs/milestones/accounting-deep.md): corte completo, evidencia, cierre/reapertura/apertura; política real antes de cierre oficial |
| DDR-07 | CLOSED BY EXISTING CONTRACT | [Reporting G1–G7](../specs/acceptance/reporting-goldens.md): membresía/signos/fórmulas/versiones/comparativos; golden y navegación requieren ejecución futura |
| DDR-08 | CLOSED BY EXISTING CONTRACT | [CPE/entrega](../specs/flows/cpe-document-delivery.md), [P2P](../specs/milestones/procurement-deep.md), Data: expediente de dueño, artefacto/relación y envío; SEE real limita activación |
| DDR-09 | CLOSED BY EXISTING CONTRACT | [UI: pendientes](../architecture/ui.md#selección-errores-y-pendientes): dueño/gravedad/edad/acción/causa; resolución por dueño, no por leído. Se precisó orden y escalación sin SLA nuevo |
| DDR-10 | CLOSED BY EXISTING CONTRACT | [Acceso](../architecture/tenancy-access.md), [CM0](../specs/cross-cutting/command-matrix.md#cm0): capacidades/alcance/revocación/mandato; UI nunca sustituye autorización |
| DDR-11 | CLOSED BY EXISTING CONTRACT | [Transactions](../architecture/transactions.md), [integraciones](../architecture/integrations.md): intención durable/resultado incierto/consulta/epoch; se explicitó PREPARE ≠ EXECUTE |
| DDR-12 | CLOSED BY EXISTING CONTRACT | [Maestros M02](../specs/milestones/runtime-masters.md): identidad/versiones/unidad/serial/snapshot/importación invalidable; datos reales no se inventan |

## Verificación externa selectiva

Solo se reabrieron tres fuentes primarias W3C el 2026-09-11 para diferencias que afectan el contrato: [diálogos modales](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/), [foco no oculto mínimo](https://www.w3.org/WAI/WCAG22/Understanding/focus-not-obscured-minimum.html) y [reflow](https://www.w3.org/WAI/WCAG22/Understanding/reflow.html). **EXTERNAL VERIFIED SOURCE** para esas afirmaciones; el resto del inventario de productos del blueprint sigue siendo referencia de investigación, no una nueva auditoría de sus implementaciones. No se añaden estas fuentes UX al registro normativo tributario.

Readiness y pendientes tienen autoridad en [deep specs](../specs/index.md) y [gaps](../roadmap/decisions-gaps.md). El memo no conserva un segundo estado global.
