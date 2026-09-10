# Calidad por riesgo, alcance y evidencia

Contrato de [ADR-009](../decisions/adr-009-quality.md). **Esta fase no ejecuta tests ni construye un runner.** Solo se realiza revisión estática de los documentos nuevos. Toda evidencia de software descrita aquí está pendiente.

## Categorías ortogonales

| Categoría | Propósito / qué prueba | Qué no prueba | Coste relativo y activación |
|---|---|---|---|
| STATIC | Sintaxis, tipos, imports, secretos, dependencias, contratos localizables | Reglas financieras ni concurrencia correcta | Bajo/medio; archivos y fronteras afectados; escaneos globales según riesgo |
| UNIT | Política/cálculo puro con ejemplos | PostgreSQL, HTTP o persistencia | Bajo; sin inicializar Django, DB, filesystem o red cuando no son parte de la propiedad |
| PROPERTY | Invariante sobre valores/secuencias generadas | Garantía universal ni semántica real de DB si el modelo es puro | Variable; dinero, reparto, stock y máquinas con propiedad clara |
| INTEGRATION | Servicio, modelo y restricciones reales | Contrato del proveedor en producción | Medio; PostgreSQL real, escenarios pequeños |
| CONTRACT | Acuerdos entre módulos/adaptadores, tipos, versiones y errores | Estado actual de un proveedor sin prueba externa | Bajo/medio; cambios de frontera o dependencia |
| TRANSACTIONAL | Intercalación controlada, rollback, deduplicación y recuperación | Todas las planificaciones posibles o todo fallo de infraestructura | Alto; cambios de recursos, locks o transiciones críticas |
| BROWSER | Tareas humanas, teclado, foco y recorridos de alto valor | Exhaustividad de cada regla de dominio | Alto; pocas tareas críticas o cambio UI transversal |
| MIGRATION | Instalación vacía, actualización desde release anterior y datos representativos | Restore completo de servicios/objetos externos | Alto; cambio de schema/datos y release candidato |
| NON-FUNCTIONAL | Carga representativa, límites, latencia, recuperación y controles de seguridad | Cumplimiento empresarial automático | Alto/variable; cambio de riesgo, revisión periódica o incidente |

Categoría de ejecución y etiqueta de propiedad son distintas. Un test de DB no se vuelve unitario por llamarse unit. Un caso puede cubrir varias propiedades, pero se ejecuta una vez por configuración requerida. Fixtures y configuración de pytest se organizan para que UNIT no arranque Django por importación global de conftest.

## Validation Profile de la Work Order

Cada WO declara categorías, módulos/contratos afectados, invariantes, casos mínimos, entorno/roles, evidencia esperada y exclusiones justificadas. Ejemplos conceptuales, no comandos ejecutables:

| Cambio | Perfil mínimo razonable |
|---|---|
| Reparto puro | STATIC + UNIT + PROPERTY:proration |
| Aplicación de cobros | STATIC + UNIT + INTEGRATION:Treasury + TRANSACTIONAL:shared-money + PROPERTY:conservation |
| Política RLS | STATIC + INTEGRATION:runtime-role + CONTRACT:all-entrypoints + TRANSACTIONAL:connection-reuse |
| Foco de un diálogo | STATIC:UI + BROWSER:keyboard-task; no suite financiera por defecto |
| Migración | STATIC + MIGRATION:clean/upgrade + integración afectada |
| Documento fundacional | Revisión de enlaces, referencias y coherencia; no tests de aplicación |

El orquestador calcula la unión de casos necesarios; deduplica por identidad de caso + parametrización/configuración + fixture y datos + variantes requeridas, incluidas semillas cuando formen parte de la garantía. No fusiona matrices distintas ni concatena perfiles superpuestos. La dependencia relevante incluye consumidores y configuración compartida; una incertidumbre sobre el alcance impide asumir equivalencia.

## Niveles de ejecución futuros

| Nivel | Evidencia esperada |
|---|---|
| Developer feedback | Perfil focalizado; prueba roja cuando se cambia comportamiento; sin suite global automática |
| Pull Request | Unión de perfiles de las WO, controles globales de seguridad/fronteras y revisión del diff |
| Main | Registrar evidencia que satisfaga el contrato de equivalencia del candidato integrado; un cambio de árbol necesita evaluación de impacto, no solo un cambio de etiqueta PR→main |
| Release candidate | Suite completa ordinaria una vez con JUnit, cobertura y tiempos; perfiles de migración/seguridad necesarios no cubiertos; prueba del mismo artefacto desplegable |
| Scheduled deep validation | Propiedades ampliadas, dependencias, datos grandes y casos adversariales seleccionados; sin reintentos que oculten fallos |
| Recovery drill | Restore aislado, verificación DB+blobs+roles, conciliación y medición RPO/RTO |

El pipeline completo no incluye por defecto cada benchmark, navegador soportado o proveedor real. El release manifiesta qué matriz es obligatoria y qué evidencia se reutiliza. Si dos entornos son parte de la garantía, ejecutar ambos es evidencia distinta; no es duplicación ceremonial.

## Reutilización verificable

Este apartado es la fuente del contrato de equivalencia; ADR-009, operación y protocolo IA lo referencian. Reutilizar significa que un resultado anterior sigue acreditando una afirmación concreta del candidato actual, no trasladar una etiqueta verde.

| Dimensión | Condición necesaria para reutilizar | Qué impide reutilizar |
|---|---|---|
| Afirmación | Mismo contrato, propiedad y criterios de aceptación | Cambio semántico de la spec o descubrimiento de un contraejemplo que el caso no detecta |
| Candidato e insumos | Identidad de archivos relevantes, incluidos nuevos/no versionados, código, tests, fixtures/datos, runner, locks, configuración y assets/artefactos aplicables | Cambio relevante, insumo no identificado o dependencia cuyo impacto se desconoce; HEAD por sí solo es insuficiente |
| Entorno | Misma configuración o equivalencia explícitamente justificada para la afirmación: runtime/librerías, PostgreSQL, schema/migraciones, políticas, grants/roles efectivos, extensiones, aislamiento/conexión y demás parámetros usados | Coincidir solo en nombre de entorno/rol; cambio no evaluado de DB, permisos, dependencias, proveedor o datos externos |
| Selección | Casos, parámetros, variantes, datos y semillas requeridos identificados y cubiertos | Caso requerido ausente, nueva matriz, muestreo requerido distinto o selección incompleta |
| Resultado y procedencia | Ejecución completa identificada, resultado satisfactorio, artefactos íntegros y origen revisable | Fallo, omisión requerida, flakiness ocultada por retry, artefacto perdido/no confiable o evidencia externa cuya vigencia ya no es válida |

La equivalencia se decide por afirmación: una prueba pura no necesita coincidir en datos de proveedor que no consume; una garantía RLS sí depende de políticas y permisos efectivos. Diferencias de entorno que no estén justificadas bloquean reutilización. No hay caducidad temporal universal para evidencia determinista; las comprobaciones de estado externo sí declaran su vigencia.

Mientras no exista un mecanismo validado de dependencias, la reutilización automática exige identidad completa del candidato y sus condiciones; el mecanismo de selección parcial entre candidatos distintos permanece PROVISIONAL. Una excepción editorial manual requiere comprobar y registrar que el cambio no altera contrato ni insumo ejecutable, con revisión explícita. No se autoriza reutilización parcial automática porque «ese módulo no cambió».

Para aceptar en el futuro una selección parcial se necesita un manifiesto de dependencias transitivas e insumos por afirmación y demostrar que cambios adversariales en configuración compartida, permisos, fixtures, consumidores y runner invalidan los resultados afectados. Lo desconocido exige nueva evidencia del alcance potencialmente afectado, sin repetir todo por rutina.

Un PR→main con contenido e insumos equivalentes conserva evidencia; un merge que cambia ese contenido se evalúa como nuevo candidato. Una edición de spec que cambia comportamiento invalida la evidencia correspondiente aunque no cambie código. El resultado antiguo no se borra: se conserva como histórico y deja de acreditar el candidato nuevo. Un consumidor o test ausente nunca figura PASSED o NOT_APPLICABLE si era requisito.

## Diseño de pruebas

- Hypothesis para conservación, particiones/redondeo y secuencias receive/apply/refund/reverse/retry. El modelo de referencia se deriva de la spec, no copia el algoritmo productivo. Conservar ejemplos reducidos de fallos [S15](../decisions/sources.md).
- PostgreSQL real para locks, RLS, constraints e idempotencia. Pruebas con rol runtime distinto al propietario de migraciones. SQLite y mocks no prueban esas propiedades.
- Concurrencia con conexiones independientes y puntos controlados de lectura/espera/commit. Comprobar recursos persistidos, agregados y trazas; demostrar que la prueba detecta una inversión relevante. Repetición sirve para diagnóstico, no sustituye el diseño de la carrera.
- Factories/builders locales de datos mínimos. Una prueba de precio no crea compra/recepción; un recorrido integral sí puede usar esa cadena.
- DB de pruebas aislada por ejecución/worker. Reutilización local posible con huella de schema y reconstrucción explícita; clean-install y upgrade conservan bases limpias dedicadas. Nunca crear/dropear bases mediante un nombre inferido del entorno productivo.
- Playwright en recorridos de alto valor. Trazas/imágenes retenidas al fallar, con datos sintéticos [S17](../decisions/sources.md). Evaluación manual de accesibilidad donde la automatización no basta.

## Coste, flakiness y observación

Instrumentar colección, creación/migración de DB, setup/call/teardown, consultas y esperas relevantes; anotar CPU/RAM/OS/versión de DB/worker count y volumen. Medir primero un baseline reproducible, luego fijar budgets. No se proponen segundos arbitrarios en esta fundación.

Una ejecución produce múltiples informes; coverage es diagnóstico, sin porcentaje universal de aprobación. Un fallo original seguido de retry exitoso sigue siendo fallo/flaky, con propietario y tratamiento visible. Los retries diagnósticos se etiquetan y no convierten la certificación en verde.

Los verificadores mecánicos comprueban estructura e inventario, no intentan interpretar algoritmos financieros completos. Cambiar archivos no debe dejar operaciones fuera de su inventario. Cambios en el runner o en las propias pruebas exigen revisar que sigue detectando el contraejemplo, evitando que la IA haga pasar un fallo quitando la aserción.

DoD proporcional: comportamiento + evidencia requerida + revisión por riesgo + impacto documental/migratorio/de seguridad resuelto. Una categoría inaplicable lleva razón breve; no se fabrica trabajo para rellenar casillas.
