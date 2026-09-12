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

Tailwind no garantiza diseño ni accesibilidad. Los componentes semánticos y tokens viven en un lugar canónico; templates de módulo los consumen. No permitir que cada agente invente otra variante de inputs/tablas mediante clases arbitrarias. Node 24 LTS/npm será herramienta de build, no runtime de servidor; assets fijados y locales, sin CDN en ejecución [S11](../research/technical-sources.md).

## Propiedad del estado

Servidor: reglas empresariales, cantidades/dinero confirmados, capacidades, estados persistentes y errores finales. Navegador: foco, selección temporal, paneles abiertos, filtro aún no aplicado y solicitud en curso. La UI no puede inventar payment_confirmed ni autorizar por ocultar un botón.

Las operaciones críticas tienen formularios semánticos y fallback de envío completo donde sea práctico. HTMX mejora búsqueda, paginación y fragmentos; mismas capacidades/CSRF y contrato en requests completas y parciales. Errores conservan valores, explican causa y llevan al primer campo inválido; cambios parciales anuncian resultado sin perder foco.

CSP sin unsafe-eval; scripts propios externos, no ejecución de scripts introducidos por fragmentos. Selección: HTMX con allowEval/allowScriptTags desactivados, mismo origen y caché de historial deshabilitada en páginas sensibles; evitar atributos que dependan de eval [S12](../research/technical-sources.md). Si Alpine demuestra utilidad, evaluar su build CSP con sus límites, no relajar CSP para incorporarlo [S13](../research/technical-sources.md).

## Sistema visual para los primeros recorridos

La tabla orienta contratos visuales comunes; no ordena construir todas las piezas antes de los módulos. Cada componente se implementará al tener un consumidor autorizado, conservando el vocabulario compartido.

| Capa | Contrato de diseño |
|---|---|
| Foundations | Tipografía legible, cifras tabulares, escala pequeña de espacios, densidad compacta/cómoda, roles semánticos de color, radio/sombra discretos y foco visible |
| Componentes | Botón/input/select/fecha/dinero, badge, menú, diálogo/drawer, tabs, paginación y tabla; estados disabled/loading/error consistentes |
| Componentes empresariales | Selector de entidad, contraparte y SKU; importe+moneda; estado comercial/fiscal/financiero separado; timeline de evidencia |
| Layouts | App shell, sidebar, encabezado, cola de trabajo, formulario, detalle y master/detail |

La dirección visual admite `LIGHT`, `DARK` y `SYSTEM`, mediante tokens semánticos con variantes y contraste medido. `SYSTEM` es la preferencia inicial, sigue el dispositivo y una elección explícita del usuario prevalece. No se fija todavía branding; los colores comunican semántica acompañada de texto/icono, nunca como único indicador. La influencia de Apple se limita a claridad, jerarquía, consistencia, respuesta inmediata y respeto de preferencias; no se copian componentes, assets ni una apariencia de macOS.

Desktop-first, densidad útil y navegación predecible; responsive sin sacrificar tareas de teclado. Cada usuario puede elegir densidad compacta/cómoda sin cambiar significado. Búsqueda, filtros, orden, columnas y vistas guardadas conservan solo parámetros autorizados; una URL representa estado de consulta no sensible. Acciones masivas muestran selección e impacto y tienen semántica de fallo por fila/lote. Evitar cards decorativas y animaciones sin función.

Objetivo WCAG 2.2 AA: etiquetas y errores asociados, teclado completo, foco visible/no oculto, contraste, reflow, objetivos de al menos 24×24 CSS px o espaciado equivalente y autenticación accesible. No afirmar conformidad hasta evaluación manual y automatizada [S14](../research/technical-sources.md). Tailwind 4 requiere navegadores modernos; la matriz inicial usa versiones soportadas de Chromium/Firefox y Safari cuando corresponda, respetando los mínimos oficiales [S11](../research/technical-sources.md). Referencias: [WCAG 2.2](https://www.w3.org/TR/WCAG22/), [Apple color/dark appearances](https://developer.apple.com/design/human-interface-guidelines/color) y [teclados](https://developer.apple.com/design/human-interface-guidelines/keyboards).

## Teclado y seguridad de acciones

### Iconos, emojis y tokens

Selección de diseño candidata: Lucide SVG, una sola familia de trazo/tamaño y nombres semánticos internos; servir solo el subconjunto usado como assets locales. La [licencia oficial](https://lucide.dev/license) es ISC y conserva avisos MIT para iconos derivados de Feather: mantener ambos avisos aplicables en la distribución. No usar SF Symbols ni assets propietarios Apple. Un icono decorativo es oculto al lector de pantalla; un botón solo con icono tiene nombre accesible visible mediante ayuda, sin depender exclusivamente del tooltip.

Emojis ocasionales y profesionales acompañan texto en navegación/ayuda o identificación de una sección (p.ej. 📦 Inventario, 📎 Evidencia). No reemplazan estado, importe, error ni acción; no llenan cada fila o botón. Evitar dependencia del color/glifo de un sistema, y comprobar lectura/contraste en LIGHT/DARK/SYSTEM. Imprimir/exportar mantiene significado textual aun sin glifo.

Tokens obligatorios: fondo/superficie/texto primario-secundario/borde/foco/selección y estados success/warning/danger/info; tipografía y números tabulares; escala de espacio, objetivo interactivo y densidad; movimiento normal/reduced. Cada tema mapea roles, no invierte colores mecánicamente. Target WCAG AA con zoom/reflow, foco no tapado por panel fijo y errores anunciados; valores cromáticos finales se eligen y miden al construir componentes, no se declaran accesibles por nombre.

### Registro de atajos y foco

Registro único por acción: ID, combinación configurable, alcance global/página/dialog/modal/tabla, etiqueta/ayuda, prioridad, condición de disponibilidad y manejo de conflicto. Paleta y búsqueda tienen botón visible; proponer Ctrl/Cmd+K solo tras probar conflictos del navegador/lector. Escape cierra el panel superior y devuelve foco a su invocador, sin descartar un formulario sucio sin aviso. Dentro de edición de texto no capturar letras, flechas o atajos nativos globalmente. Atajos de una tecla se pueden desactivar/remapear y no están activos mientras se escribe.

Tabla de lectura usa HTML table con enlaces/botones y Tab normal. Solo una tabla realmente interactiva adopta [patrón grid WAI-ARIA](https://www.w3.org/WAI/ARIA/apg/patterns/grid/) y su contrato completo de foco/celdas; añadir role=grid no crea navegación accesible. Selección, paginación y edición son estados distintos. Tras filtro/swap restaurar foco a control estable, anunciar número de resultados y conservar selección solo si las filas siguen válidas. Ayuda muestra atajos disponibles en ese contexto.

Todo recorrido frecuente debe completarse con teclado y foco predecible. Se respetan atajos del navegador/sistema; los atajos CasPro se limitan a navegación, búsqueda y comandos frecuentes, se muestran junto a la acción y pueden descubrirse desde ayuda. Una sola tecla no confirma despacho, pago, ajuste, cierre, CPE, email o borrado. El atajo puede abrir/preparar el formulario; la misma revisión, permiso, idempotencia y confirmación semántica del control visible siguen aplicando. Los cambios HTMX restauran foco por identidad y anuncian resultados.

## Tablas, edición y cifras

HTML semántico con paginación/filtrado de servidor es el estándar. No elegir grid avanzada sin tareas reales de edición en bloque, clipboard, navegación celular, columnas configurables o virtualización. Un dataset grande no obliga por sí solo a virtualizar en navegador: primero paginar y medir.

Si aparece ese caso, comparar candidatos con su licencia, coste, accesibilidad, CSP y prueba de tarea representativa. No hay biblioteca de grid seleccionada hoy.

Los importes llegan como texto decimal y moneda; presentación del servidor y entrada localizada inequívoca. No usar parseFloat/Number como fuente de cálculos empresariales. Feedback provisional no confirma dinero y se reconcilia con el servidor.

## Operación del primer período

Bandeja única de pendientes/excepciones como lectura de los dueños: pedido sin correspondencia, discrepancia de stock/pago del canal, CPE sin vínculo/artefacto, aprobación de entrega o bounce. Cada entrada muestra entidad, origen, antigüedad, motivo y siguiente acción autorizada; resolverla invoca al dueño, no cambia flags de un workflow engine. WARNING informa y permite las acciones válidas; BLOCKING identifica la acción impedida y qué debe resolverse, sin bloquear indiscriminadamente todo el ERP. HOLD documental sigue el [contrato de entrega](integrations.md).

Búsqueda global reúne solo recursos permitidos de la entidad activa mediante consultas públicas de cada propietario. Incluye permisos en resultados, extractos, conteos, sugerencias y cachés; sin contexto no busca en todas las entidades. Abrir un resultado vuelve a autorizar. No requiere motor externo ni Customer de CRM. Preview PDF autorizado, CSV/Excel validate → preview → confirm y cifras de coste/margen usan el [contrato de datos](data.md); ajustes muestran motivo, impacto y auditoría antes de confirmar.

El detalle documental usa panel dividido cuando mejora la tarea: lista/relaciones a un lado, preview PDF/XML/metadata al otro, con alternativa de página completa y descarga autorizada. El document flow muestra relaciones reales y estados de sus dueños —por ejemplo PO→recepción→CPE→pago→posting— y permite drill-down; no almacena una segunda secuencia empresarial ni decide qué paso “completó” el caso.

## Navegación y continuidad

Shell con entidad activa y entorno inequívocos; almacén, cuenta, moneda o período aparecen en la tarea donde condicionan datos/acciones, sin un período global oculto. Agrupación inicial: Mi trabajo; Operaciones (Ventas, Compras, Inventario, Tesorería); Control (Contabilidad, Tributación, Societario); Compartido (Documentos, Maestros). Búsqueda, ayuda, preferencias y administración accesible son utilidades. Los grupos organizan navegación, no cambian dueños ni publican módulos sin implementar. Etiquetas en español y alias de búsqueda; orden estable y favoritos personales separados.

Lista → detalle → relación → regreso conserva consulta, fila/foco, desplazamiento y pestaña cuando siguen autorizados. Breadcrumb describe jerarquía; historial describe visitas. URL directa y pestaña nueva son rutas válidas. La continuidad guarda parámetros seguros y vuelve a autorizar datos: no PII en URL/localStorage ni restauración de HTML sensible desde historial. Revocación descarta contenido protegido y selección inválida, mostrando un contexto permitido; conservar un formulario nunca prevalece sobre acceso revocado.

Usar lista/detalle, comparación y preview según tarea. Máximo habitual de dos paneles simultáneos es dirección de diseño, no límite empresarial; disponer de recorrido secuencial/página completa en pantallas estrechas y para tecnología asistiva. Redimensionar tiene alternativa de teclado. Preview es lectura; editar es una acción explícita. No introducir una pila ilimitada de drawers ni panel IA permanente.

## Composición de tareas y evidencia

Detalle muestra identidad, contraparte/fecha/moneda pertinentes, estados de cada dueño y siguiente acción permitida. Resumen, líneas, relacionados y actividad tienen propósitos distintos; una excepción bloqueante se anuncia fuera de una pestaña oculta. Timeline narra eventos; Document Flow proyecta relaciones tipadas, direccionales y N:M con cantidades/importes si existen, evidencia, autoridad y estado del dueño. No convierte PO→recepción→CPE→pago en una secuencia obligatoria. Distinguir sugerido/confirmado, ofrecer lista completa además del grafo y no sumar dos veces un documento por aparecer en dos ramas. Abrir otra relación permite volver al ancla. Ocultar nodos/conteos restringidos; describir solo el alcance visible sin revelar que existe un expediente privado.

Original PDF/XML, texto extraído y datos sugeridos se distinguen. No invertir colores del original ni presentarlo como documento accesible por tener OCR. Mostrar versión/origen y diferenciar ilegible, análisis pendiente y formato no soportado. LIGHT/DARK/SYSTEM cambian chrome y componentes; impresión tiene presentación legible propia. Preferencias visuales nunca cambian precisión empresarial, aprobaciones ni contexto. Crear un maestro desde selector devuelve su identidad al borrador conservado; posibles duplicados exigen resolución del dueño, sin merge automático.

Conciliación bancaria compara extracto y candidatos con cuenta, moneda, corte y totales de cada conjunto; mantiene filas estables mientras hay foco. El grupo preparado explica signos, asignaciones, remanentes y diferencia; una sugerencia expone evidencia, no una confianza numérica sin calibrar. Retirar candidato no desconcilia una relación confirmada. [T04–T06](../specs/milestones/treasury-corporate-deep.md) gobiernan confirmación/corrección y [preparar/ejecutar](transactions.md#preparar-y-ejecutar) gobierna su activación. Ante timeout: «Resultado por verificar», consulta de la intención original y sin botón de retry económico ciego.

Cierre muestra estado Accounting del período separado del progreso de tareas, dependencias, responsable/evidencia existentes y su revisión. Tarea completada no cierra período; faltante conduce al dueño y no crea “forzar cierre”. EEFF muestran entidad/libro/marco, período/comparativo, moneda/unidad/escala, corte y versión. El drill-through conserva monto y alcance original: contribución → miembros; fórmula → operandos; narrativa → evidencia. No inventa asientos para toda celda. Totales de detalle y diferencias de alcance se explican; cambiar filtros crea otra vista. Un paquete histórico no se recalcula al abrirlo; exportación conserva su contexto y versión conforme a [reporting](../specs/acceptance/reporting-goldens.md).

## Selección, errores y pendientes

Tablas distinguen lectura operativa, edición de borrador, análisis y comparación. Identidad y columnas críticas permanecen reconocibles; cantidades muestran unidad e importes moneda. Foco no equivale a selección. Selección de página, filas elegidas y todos los resultados son modos explícitos; totales de página/filtro/selección/entidad no se intercambian. Una acción masiva revisa impacto y cambios de entradas invalidan su preparación; muestra éxito/fallo/resultado incierto por unidad conforme a la atomicidad del dueño. No promete Undo para hechos que exigen reversión. Vistas personales no crean permiso para compartir ni filtros ocultos.

Estado empresarial, interacción, gravedad y frescura son ejes diferentes. UNKNOWN, cero y no aplicable tienen representaciones distintas. Error explica qué objeto, qué ocurrió, qué efecto se conoce y siguiente acción segura; error de campo más resumen accesible, conflicto compara revisiones sin sobrescribir, resultado incierto permanece visible. Toast solo para feedback no crítico. Las sugerencias de IA siguen [AI](ai-assistance.md) y no confirman decisiones.

Inbox agrupa por entidad + dueño + objeto + causa vigente; no una tarea por cada callback. El dueño publica si bloquea una acción, gravedad, fecha límite cuando exista, antigüedad y acción autorizada; orden inicial gravedad y luego antigüedad, con identidad como desempate. Asignación exige responsable válido y capacidad del dueño; lectura/seguimiento/posposición no resuelven la causa. Resolver consulta el estado autoritativo y retira la excepción solo si cesó. Escalar enlaza la causa al responsable autorizado; no inventa SLA, vencimientos legales ni un motor de aprobaciones. El cambio de prioridad local no libera HOLD.

## Límites de validación visual

Delta de navegación del [amendment aceptado](../evidence/b2b-financing-amendment.md): ancla [venta B2B](../specs/flows/b2b-commercial-dossier.md) con cliente, cotización/OC opcionales, revisiones/diferencias/aceptación, términos de pago, reservas/parciales, CPE, entrega documental, cobros/aplicaciones y conciliación. Ancla [financiación](../specs/flows/financing-events-statements.md) con contrato/adendas, desembolsos, pagos por cuenta, reembolsos, principal devuelto, estados mensuales y evidencia/audit. Mostrar naturaleza y remanentes, fecha del hecho/registro/firma y nivel de evidencia de entrega externa; «enviado» no se muestra como «recibido». Lista navegable y Document Flow son proyecciones con permisos/cortes, sin dueño de hechos nuevo ni diseño pixel-perfect. Ninguna suma del estado mensual autoriza compensar obligaciones.

El [memo de reconciliación](../evidence/ux-reconciliation.md) registra procedencia y disposición del blueprint; este documento conserva la autoridad UX. Estructura, estados, continuidad, semántica, seguridad y accesibilidad son contratos de diseño revisables ahora. Hexadecimales, anchos, tamaños exactos, duraciones, densidad de 32/40/44 px y combinaciones concretas de atajos son candidatos de prototipo, no requisitos congelados.

Diálogo modal solo cuando el contenido exterior es inerte: foco inicial en contenido pertinente o acción menos destructiva, Tab contenido, Escape seguro y devolución al invocador o siguiente paso lógico. Evitar que Enter que abrió la revisión active también confirmar. WCAG 2.2 AA 2.4.11 exige foco no **enteramente** oculto; hacerlo completamente visible es objetivo adicional, no atribuirlo a ese mínimo. El grosor de un anillo no acredita conformidad. Reflow aplica al shell y formularios; la excepción de una tabla que necesita dos dimensiones no exime a la página completa. Ver [W3C modal](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/), [foco](https://www.w3.org/WAI/WCAG22/Understanding/focus-not-obscured-minimum.html) y [reflow](https://www.w3.org/WAI/WCAG22/Understanding/reflow.html).

REQUIRES LATER VALIDATION: tareas representativas, teclado/lector, foco tras swaps, reflow/zoom/temas, CSRF/CSP, compatibilidad, doble submit/retry y revocación. Contrato y ensayo se separan en [gates de implementación](../roadmap/decisions-gaps.md); no se construyó ni evaluó una UI ejecutable en esta fase.
