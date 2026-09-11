# Frontend, sistema visual y UX

Selección de [ADR-004](../decisions/adr-004-ui.md): Django SSR + Tailwind CSS 4 compilado + HTMX 2 donde reduzca trabajo + JavaScript nativo pequeño. Alpine no es dependencia inicial. Ningún componente ni configuración de build se implementa en esta fase.

## Alternativas y límites

| Opción | Juicio para CasPro |
|---|---|
| Templates + CSS propio + JS | ACCEPTABLE: mínima herramienta, pero requiere sostener un vocabulario visual propio y evitar variaciones generadas por IA |
| SSR + Tailwind + HTMX | GOOD: formularios/validación del servidor, navegación parcial y composición visual común; se acepta build de assets |
| Añadir Alpine por defecto | QUESTIONABLE: duplica responsabilidad de interacción sin consumidor demostrado; su build estándar exige facilidades incompatibles con CSP estricta |
| Django API + React SPA | QUESTIONABLE inicialmente: dos capas de estado, serialización, auth y validación para un ERP principalmente documental |
| Isla React/otro framework | ACCEPTABLE si una pantalla necesita edición/virtualización que no se pueda resolver de forma mantenible con HTML; contrato y bundle aislados |

Tailwind no garantiza diseño ni accesibilidad. Los componentes semánticos y tokens viven en un lugar canónico; templates de módulo los consumen. No permitir que cada agente invente otra variante de inputs/tablas mediante clases arbitrarias. Node 24 LTS/npm será herramienta de build, no runtime de servidor; assets fijados y locales, sin CDN en ejecución [S11](../decisions/sources.md).

## Propiedad del estado

Servidor: reglas empresariales, cantidades/dinero confirmados, capacidades, estados persistentes y errores finales. Navegador: foco, selección temporal, paneles abiertos, filtro aún no aplicado y solicitud en curso. La UI no puede inventar payment_confirmed ni autorizar por ocultar un botón.

Las operaciones críticas tienen formularios semánticos y fallback de envío completo donde sea práctico. HTMX mejora búsqueda, paginación y fragmentos; mismas capacidades/CSRF y contrato en requests completas y parciales. Errores conservan valores, explican causa y llevan al primer campo inválido; cambios parciales anuncian resultado sin perder foco.

CSP sin unsafe-eval; scripts propios externos, no ejecución de scripts introducidos por fragmentos. Selección: HTMX con allowEval/allowScriptTags desactivados, mismo origen y caché de historial deshabilitada en páginas sensibles; evitar atributos que dependan de eval [S12](../decisions/sources.md). Si Alpine demuestra utilidad, evaluar su build CSP con sus límites, no relajar CSP para incorporarlo [S13](../decisions/sources.md).

## Sistema visual para los primeros recorridos

La tabla orienta contratos visuales comunes; no ordena construir todas las piezas antes de los módulos. Cada componente se implementará al tener un consumidor autorizado, conservando el vocabulario compartido.

| Capa | Contrato de diseño |
|---|---|
| Foundations | Tipografía legible, cifras tabulares, escala pequeña de espacios, densidad compacta/cómoda, roles semánticos de color, radio/sombra discretos y foco visible |
| Componentes | Botón/input/select/fecha/dinero, badge, menú, diálogo/drawer, tabs, paginación y tabla; estados disabled/loading/error consistentes |
| Componentes empresariales | Selector de entidad, contraparte y SKU; importe+moneda; estado comercial/fiscal/financiero separado; timeline de evidencia |
| Layouts | App shell, sidebar, encabezado, cola de trabajo, formulario, detalle y master/detail |

La dirección visual admite `LIGHT`, `DARK` y `SYSTEM`, mediante tokens semánticos con variantes y contraste medido. `SYSTEM` sigue la preferencia del dispositivo y una elección explícita del usuario prevalece. No se fija todavía branding; los colores comunican semántica acompañada de texto/icono, nunca como único indicador. La influencia de Apple se limita a claridad, jerarquía, consistencia, respuesta inmediata y respeto de preferencias; no se copian componentes, assets ni una apariencia de macOS.

Desktop-first, densidad útil y navegación predecible; responsive sin sacrificar tareas de teclado. Cada usuario puede elegir densidad compacta/cómoda sin cambiar significado. Búsqueda, filtros, orden, columnas y vistas guardadas conservan solo parámetros autorizados; una URL representa estado de consulta no sensible. Acciones masivas muestran selección e impacto y tienen semántica de fallo por fila/lote. Evitar cards decorativas y animaciones sin función.

Objetivo WCAG 2.2 AA: etiquetas y errores asociados, teclado completo, foco visible/no oculto, contraste, reflow, objetivos de al menos 24×24 CSS px o espaciado equivalente y autenticación accesible. No afirmar conformidad hasta evaluación manual y automatizada [S14](../decisions/sources.md). Tailwind 4 requiere navegadores modernos; la matriz inicial usa versiones soportadas de Chromium/Firefox y Safari cuando corresponda, respetando los mínimos oficiales [S11](../decisions/sources.md). Referencias: [WCAG 2.2](https://www.w3.org/TR/WCAG22/), [Apple color/dark appearances](https://developer.apple.com/design/human-interface-guidelines/color) y [teclados](https://developer.apple.com/design/human-interface-guidelines/keyboards).

## Teclado y seguridad de acciones

Todo recorrido frecuente debe completarse con teclado y foco predecible. Se respetan atajos del navegador/sistema; los atajos CasPro se limitan a navegación, búsqueda y comandos frecuentes, se muestran junto a la acción y pueden descubrirse desde ayuda. Una sola tecla no confirma despacho, pago, ajuste, cierre, CPE, email o borrado. El atajo puede abrir/preparar el formulario; la misma revisión, permiso, idempotencia y confirmación semántica del control visible siguen aplicando. Los cambios HTMX restauran foco por identidad y anuncian resultados.

## Tablas, edición y cifras

HTML semántico con paginación/filtrado de servidor es el estándar. No elegir grid avanzada sin tareas reales de edición en bloque, clipboard, navegación celular, columnas configurables o virtualización. Un dataset grande no obliga por sí solo a virtualizar en navegador: primero paginar y medir.

Si aparece ese caso, comparar candidatos con su licencia, coste, accesibilidad, CSP y prueba de tarea representativa. No hay biblioteca de grid seleccionada hoy.

Los importes llegan como texto decimal y moneda; presentación del servidor y entrada localizada inequívoca. No usar parseFloat/Number como fuente de cálculos empresariales. Feedback provisional no confirma dinero y se reconcilia con el servidor.

## Operación del primer período

Bandeja única de pendientes/excepciones como lectura de los dueños: pedido sin correspondencia, discrepancia de stock/pago del canal, CPE sin vínculo/artefacto, aprobación de entrega o bounce. Cada entrada muestra entidad, origen, antigüedad, motivo y siguiente acción autorizada; resolverla invoca al dueño, no cambia flags de un workflow engine. WARNING informa y permite las acciones válidas; BLOCKING identifica la acción impedida y qué debe resolverse, sin bloquear indiscriminadamente todo el ERP. HOLD documental sigue el [contrato de entrega](integrations.md).

Búsqueda global reúne solo recursos permitidos de la entidad activa mediante consultas públicas de cada propietario. Incluye permisos en resultados, extractos, conteos, sugerencias y cachés; sin contexto no busca en todas las entidades. Abrir un resultado vuelve a autorizar. No requiere motor externo ni Customer de CRM. Preview PDF autorizado, CSV/Excel validate → preview → confirm y cifras de coste/margen usan el [contrato de datos](data.md); ajustes muestran motivo, impacto y auditoría antes de confirmar.

El detalle documental usa panel dividido cuando mejora la tarea: lista/relaciones a un lado, preview PDF/XML/metadata al otro, con alternativa de página completa y descarga autorizada. El document flow muestra relaciones reales y estados de sus dueños —por ejemplo PO→recepción→CPE→pago→posting— y permite drill-down; no almacena una segunda secuencia empresarial ni decide qué paso “completó” el caso.

REQUIRES LATER VALIDATION: navegación por teclado, foco tras swaps, CSRF/errores, CSP, compatibilidad de build, doble submit/retry y tareas densas con datos representativos. No se construyó UI durante la fundación.
