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

No se fija todavía paleta/branding; una apariencia neutral con contraste verificable basta para especificar comportamiento. Los colores comunican semántica acompañada de texto/icono, nunca como único indicador.

Desktop-first, densidad útil y navegación predecible; responsive sin sacrificar tareas de teclado. Búsqueda y filtros conservables, URL que representa estado de consulta no sensible, acciones masivas con selección visible y semántica de fallo por fila/lote. Evitar cards decorativas y animaciones sin función.

Objetivo WCAG 2.2 AA: etiquetas y errores asociados, teclado completo, foco no oculto, contraste, reflow, tamaño de objetivo y autenticación accesible. No afirmar conformidad hasta evaluación manual y automatizada [S14](../decisions/sources.md). Tailwind 4 requiere navegadores modernos; la matriz inicial usa versiones soportadas de Chromium/Firefox y Safari cuando corresponda, respetando los mínimos oficiales [S11](../decisions/sources.md).

## Tablas, edición y cifras

HTML semántico con paginación/filtrado de servidor es el estándar. No elegir grid avanzada sin tareas reales de edición en bloque, clipboard, navegación celular, columnas configurables o virtualización. Un dataset grande no obliga por sí solo a virtualizar en navegador: primero paginar y medir.

Si aparece ese caso, comparar candidatos con su licencia, coste, accesibilidad, CSP y prueba de tarea representativa. No hay biblioteca de grid seleccionada hoy.

Los importes llegan como texto decimal y moneda; presentación del servidor y entrada localizada inequívoca. No usar parseFloat/Number como fuente de cálculos empresariales. Feedback provisional no confirma dinero y se reconcilia con el servidor.

REQUIRES LATER VALIDATION: navegación por teclado, foco tras swaps, CSRF/errores, CSP, compatibilidad de build, doble submit/retry y tareas densas con datos representativos. No se construyó UI durante la fundación.
