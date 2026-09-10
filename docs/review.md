# Revisión y condición de avance

Fecha: 2026-09-10. **Gate 1: CLOSED, PASS documental. Foundation Amendment: PASS documental.** Este archivo es la fuente del estado global; cada ADR conserva la autoridad sobre sus alcances. Esos cierres no acreditan software construido, desplegado o production-ready ni sustituyen aprobaciones empresariales. SUPERPROMPT 2 fue autorizado por un mandato posterior y se registra al final; los cierres anteriores no fueron por sí mismos su autorización.

## Refutación del diseño

| Contraejemplo | Corrección incorporada al diseño | Riesgo que queda |
|---|---|---|
| Una reventa legítima viola la unicidad vitalicia del serial; toda devolución repone stock | Invariantes por dirección, movimiento original, remanente y ciclo; retorno de cliente entra y devolución a proveedor sale | Guardas de reventa y valoración de salida a proveedor requieren especificación/validación de dominio |
| El CPE de proveedor acaba en Sales o Documents | Sales posee su expediente de venta; Procurement el recibido; Documents conserva evidencia y disponibilidad técnica | Tratamientos fiscales/contables y contratos de verificación pendientes |
| Caída de proceso pierde progreso o hace de workflows un dueño empresarial | Progreso en el caso del módulo dueño; registros técnicos durables con productor/solicitante y consumidor identificados | Esquema/backend y recuperación se validan al primer caso; no engine genérico |
| Workspace convierte perfiles empresariales en datos globales | Identity/Organization/Access delimitados; directorio mínimo y datos protegidos separados; agrupación provisional | Recorridos administrativos y evidencia de acceso pendientes |
| Una tabla nueva sin RLS o una política permisiva evade la defensa | Condiciones de inventario, permisos efectivos y detección adversarial de regresiones | RLS PROVISIONAL; evidencia PENDING VALIDATION, sin protección frente a proceso/admin comprometido |
| El orden monetario seleccionado no contempla claves ni raíces inexistentes | La lista pasa a hipótesis local; matriz común derivada de comandos, intenciones y creación | Concurrencia/rollback/retry necesitan evidencia ejecutable posterior |
| Una operación reversible duplica cobros; una lectura exige clave innecesaria | Clasificación por efecto de repetición; garantía natural o deduplicación durable según el caso | Retención, solicitudes en curso y ámbito exacto por intención pendientes |
| Decimal con precisión 38 se interpreta como exactitud demostrada | Principios exactos separados de parámetros provisionales y rangos por justificar | Extremos, acumulaciones, residuos y pérdida de precisión requieren evidencia |
| Un resultado de QA acredita código/roles/fixtures distintos | Contrato único de equivalencia e invalidación; reutilización parcial automática condicionada | Manifiesto transitivo y detección de cambios relevantes pendientes de validación |
| Un ADR acepta por arrastre sus detalles; Gemini carga todos los roles | Tabla autoritativa por alcance en cada ADR; índice sin copia de estados; carga de Gemini condicional | Eficacia real de contexto/herramientas se revisa en la primera WO autorizada |
| No HTTP bajo lock pero se pierde el envío, o restore repite el efecto externo | Intención durable separada del hecho, consumidor deduplicado y restore con efectos desactivados | Backend, replay y drill pendientes; no exactly-once externo |
| Migrar Supabase significa mover solo un dump | DB, objetos, secretos, roles y servicios externos requieren inventarios y recuperación separados | Proveedor/cuenta/capacidades no provisionados |

## Riesgos arquitectónicos abiertos

- RLS + Django + roles administrados puede fallar por configuración, consulta perezosa o contexto de conexión. Requiere una validación habilitante antes de negocio sensible.
- El orden monetario de bloqueos necesita comprobarse con topologías cambiantes y creación simultánea de raíces; la coherencia de texto no demuestra ausencia de deadlocks.
- La sincronización entre obligación comercial y objetivo de liquidación exige un único workflow; permitir escrituras directas reintroduciría dos saldos autoritativos.
- Workspace, representación durable y selección parcial de evidencia necesitan concretarse sin introducir ciclos, motores genéricos o excepciones de acceso implícitas.
- Django 6.1 implica actualizar de forma planificada y verificar dependencias; no heredar compatibilidad de V1.
- App/DB en proveedores distintos añade conectividad, egress y responsabilidad compartida; región común no garantiza latencia aceptable.
- Continuar en un proyecto nuevo cuesta revalidar capacidades. El repositorio vacío facilita el diseño, no demuestra ahorro frente a refactorizar V1.

## Decisiones realmente humanas

Conservan pendientes humanos en los alcances indicados; el amendment concretó parte de H1 y SUPERPROMPT 2 eligió el circuito B2C. Las cinco políticas del circuito se precisan únicamente en [HP1–HP5](specs/first-operational-circuit.md). Los ADRs distinguen principios aceptados y mecanismos provisionales; estos últimos conservan incertidumbre técnica, que no se traslada al propietario como si fuera una decisión empresarial.

| ID | Decisión | Recomendación / qué condiciona |
|---|---|---|
| H1 | Políticas empresariales exigibles al primer uso; circuito seleccionado por SUPERPROMPT 2 | Venta B2C por Jumpseller, Treasury, entrega física, CPE externo y Documents/Resend quedan especificados. HP1–HP5 delimitan decisiones productivas pendientes; margen básico no sustituye Accounting |
| H2 | Presupuesto de hosting, almacenamiento, soporte y región/condiciones de tratamiento de datos | Managed inicialmente; candidato Render+Supabase, sin contratación en esta fase |
| H3 | RPO, RTO y retención empresarial/regulatoria | Decidir pérdida/interrupción tolerable antes de seleccionar plan de backups y continuidad |
| H4 | Excepción de segregación y acciones que requieren aprobación adicional | Mostrar autoaprobación; no simular dos personas; limitar devoluciones/elevaciones/cierres conforme al riesgo aceptado |
| H5 | Validación contable/tributaria/contractual aplicable y hechos empresariales acreditados | Profesional/propietario confirma lo de su competencia; no adoptar conclusiones dudosas de V1 como regla |

La identidad visual de marca puede definirse después; una UI neutral accesible permite avanzar. No se transfiere al propietario elegir frameworks, locks o nombres de archivos.

## Validaciones técnicas posteriores, no ejecutadas

1. Resolver compatibilidad real Python/Django/driver/tipos/QA y fijar locks.
2. Demostrar RLS/roles/entrypoints/queries sin filtro y referencias cruzadas.
3. Demostrar conservación monetaria, reversión, parcialidades y carreras diseñadas.
4. Probar CSP/HTMX/accesibilidad y flujo de teclado con datos representativos.
5. Demostrar instalación/upgrade/restore con DB+blobs+roles y efectos externos desactivados.
6. Obtener baseline desglosado y probar deduplicación del plan de evidencia antes de fijar budgets.

Todas son REQUIRES LATER VALIDATION. No son una orden para ejecutarlas ahora ni en SUPERPROMPT 2 sin autorización expresa.

## Cobertura del encargo

| Pregunta fundacional | Fuente que la responde |
|---|---|
| Producto, usuario inicial y non-goals | [Producto](product/charter.md) |
| Dominios, propiedad y cardinalidad | [Modelo](domain/model.md) y [fronteras](architecture/boundaries.md) |
| Stack, alternativas y portabilidad | [Tecnología](architecture/technology.md) y [ADRs](decisions/index.md) |
| Dinero, cantidades, fechas, estados e identidad | [Datos](architecture/data.md) e [invariantes](domain/invariants.md) |
| Autenticación, autorización y multiempresa | [Acceso](architecture/tenancy-access.md) |
| Concurrencia, idempotencia y reversión | [Transacciones](architecture/transactions.md) |
| Integraciones, async, Accounting y Tax | [Integraciones](architecture/integrations.md) y mapa de propietarios |
| UI, diseño visual, grids y reporting | [UI](architecture/ui.md) y estrategia de datos |
| QA y evidencia sin duplicación | [Calidad](quality/strategy.md) |
| Seguridad y fallos | [Threat model](security/threat-model.md) |
| Entrega, migración, operación y recuperación | [Delivery](operations/delivery.md) |
| Cinco verdades y documentación local | [Índice](index.md) |
| Roles IA, autoridad, revisión y WO | [Protocolo](../.ai/README.md) |
| Extracción y coste de V1 | [Política](v1-reference/policy.md) |

## Evidencia y cierre correctivo de Gate 1

Antecedente: la revisión inicial examinó 38 archivos, 151 enlaces y la coincidencia entonces existente de 11 estados ADR/índice. Gate 1 refutó su suficiencia para promoción canónica y produjo PASS WITH CHANGES. Ese resultado histórico no acredita las correcciones posteriores ni la ejecución de software.

La corrección actual conserva los archivos existentes y cruza invariantes, ownership, acceso, coordinación, idempotencia, datos y QA. El intento adversarial posterior se resume en la tabla anterior: las restricciones equivocadas se sustituyen y los mecanismos sin evidencia conservan su condición provisional. No se sustituye incertidumbre por una regla inventada.

Resultado del recorrido estático: 174 enlaces internos comprobados sin destinos rotos, 11 ADRs con estados por alcance y 20 registros de fuentes con referencias reconocidas. El índice no conserva otra columna de estados. Permanecen 38 archivos Markdown: 28 modificados, ninguno añadido o eliminado. La referencia externa preexistente a V1 quedó fuera de lectura y de esta comprobación.

La revisión de consistencia no identificó contradicciones residuales dentro del alcance corregido. La segunda refutación también consideró un refund que solo afecta Treasury: su progreso permanece allí, sin exigir un expediente Sales artificial. Se conservan explícitamente los límites de prueba estática y los mecanismos pendientes; no se valida concurrencia, RLS, precisión ni recuperación ejecutables.

La afirmación «CasPro Foundation is ready to become canonical» se acepta como referencia de los contratos de diseño y de sus límites/provisionalidades, tras corregir los hallazgos y revisar su consistencia. Se rechaza si se interpreta como aceptación de todos los mecanismos, aptitud productiva o autorización para iniciar SUPERPROMPT 2. El cierre de este gate es documental y no levanta los pendientes técnicos o humanos.

No se ejecutan tests, builds, Docker, bases de datos ni verificadores de V1. No se crean archivos funcionales, modelos, migraciones o infraestructura; Wbpro no se consulta ni modifica durante esta corrección.

## Nuevo ERP frente a refactorización

La fundación es técnicamente defendible como diseño de CasPro. No demuestra que reescribir todo Wbpro sea más barato o necesario: los hallazgos anteriores no hacían irrecuperable su base. La recomendación técnica sigue siendo transferencia/refactorización selectiva antes que reconstrucción indiscriminada de todas las capacidades.

CasPro puede ser el nuevo destino autorizado por el propietario, manteniendo Wbpro intacto. La elección de ese destino no obliga a copiar su arquitectura ni a desechar toda pieza útil. No recomendaría iniciar una reescritura integral por el solo hecho de haber creado esta fundación; primero especificar un circuito y comparar coste/riesgo de portar cada familia bajo el contrato nuevo.

## Foundation Amendment posterior a Gate 1 — 2026-09-10

Mandato: incorporar necesidades reales del primer período, sin reabrir Gate 1. Antes de editar se comprobó árbol limpio, rama main con seguimiento origin/main, [remoto CasPro-ERP](https://github.com/mat-l-dev/CasPro-ERP.git) y HEAD 586bdfdad789b30d548d8159a9acaaf5bd098603, idéntico al main anunciado por el remoto. No se reescribió historia ni se hizo commit/push.

Cambian el alcance ecommerce/correo, la entrega documental de Documents y las necesidades operativas iniciales. El [producto](product/charter.md) delimita el alcance y [ADR-008](decisions/adr-008-integrations.md) conserva la autoridad de sus decisiones: proveedores iniciales elegidos, mecanismos pendientes. Las otras decisiones de Gate 1 no se reauditan.

| Contradicción o contraejemplo del amendment | Resolución documental |
|---|---|
| Ecommerce diferido, prohibición indiscriminada de escrituras externas y README sin remoto | Jumpseller/correo incluidos expresamente; CasPro no emite/presenta/envía CPE a SUNAT; README distingue generación y publicación |
| Documents tiene prohibido decidir «entrega», o vuelve a poseer el CPE | Entrega documental diferenciada de entrega física/estado legal; referencias verificadas vía coordinador, sin llamadas Documents → Sales/Procurement/Parties |
| Pedido importado y despacho descuentan dos veces; webhook eco repite publicación | Reserva y movimiento separados, objetivo versionado y reconciliación; frescura incierta bloquea incremento; carreras externas aún requieren validación |
| Consulta SUNAT se interpreta como descarga total SOL, o XML reconstruido sustituye original | Capacidad de consulta acotada, adquisición masiva no verificada e importación del operador; procedencia/representación explícita |
| Reenvío, timeout, callback tardío o restore producen otro original o invalidan la venta | Intención/propósito y destinatario fijados, HOLD, deduplicación local, conciliación y restauración sin efectos; resultado del correo separado del CPE/venta |

Revisión estática del cambio: referencias locales afectadas resueltas, fuentes S21–S25 identificadas y diff limitado a 13 archivos Markdown existentes, sin altas/bajas. No se encontraron contradicciones residuales en el alcance modificado; no se valida comportamiento ejecutable. El proveedor de objetos, políticas concretas de stock/artefactos/retención/margen y mecanismos/cuentas de integración siguen provisionales; los pendientes humanos no resueltos permanecen arriba. La documentación pública de Jumpseller tiene cifras de retries inconsistentes, por lo que no se fija esa garantía.

**Foundation Amendment: PASS documental.** La fundación queda lista para especificación en SUPERPROMPT 2 cuando el propietario la autorice; ese paso deberá concretar los pendientes del circuito, sin darlos por resueltos ni habilitar operación real. Gate 1 permanece CLOSED. No se inicia SUPERPROMPT 2, no se ejecutan tests/Docker/builds, no se implementa software ni se consulta/modifica Wbpro.

## SUPERPROMPT 2 — especificación del circuito, 2026-09-10

Mandato posterior explícito: especificar y publicar la rama documental; no implementar ni ejecutar WOs. Preflight: árbol limpio, main/HEAD/origin/main idénticos tras fetch en `e89f344fc76cc70092962764e626f48ef80b6e90`, remoto CasPro ya publicado, sin archivos ajenos. Se creó `spec/superprompt-2-first-operational-circuit` desde ese origin/main; no se reescribe historia ni se trabaja directamente sobre main.

La [spec de entrada](specs/first-operational-circuit.md) distribuye siete archivos por contexto: alcance/maestros/operación, negocio, CPE/Documents, integración, matriz de comandos, aceptación y WOs/perfiles. No se crean nuevos módulos, ADRs, motores de workflow, identidad Customer duplicada ni código. Los documentos fundacionales afectados solo actualizan enlaces, estado de fase y pendientes ya concretados; Gate 1 no se reaudita.

| Refutación del primer circuito | Respuesta incorporada y límite |
|---|---|
| Dos webhooks/dos reservas duplican venta o consumen el mismo stock | Caso por conexión+pedido, aceptación explícita íntegra, unicidades y raíces compartidas; concurrencia real pendiente |
| Propuesta discrepante queda bloqueada sin corrección posible | C15 revisa términos con evidencia, conserva observación y C04 reevalúa; nueva observación material invalida conformidad |
| PAID crea dinero, cierre de cuenta compite con confirmación o refund evade cobertura | Treasury confirma evidencia, F entra en orden común, S/T/R protegen aplicación/refund/entrega; no transferencia ni dinero desde webhook |
| Retorno se confunde con refund o corrección de retorno duplica reventa | Dirección/original/ciclo/coste y corrección referenciada con tope/unidades disponibles; pasos físicos, comerciales, fiscales y monetarios separados |
| PUT absoluto considerado reducción repone stock consumido por checkout concurrente | Gate STOCK-PUBLISH; publicación positiva desatendida bloqueada hasta protocolo probado, ventana controlada explícita para baseline. No fence remoto ni cero sobreventa inventados |
| Preparar en MANUAL envía sin capacidad o corrección obliga a crear segundo original | Solicitud de dispatch y documents.send explícitos, revisión de intención existente, unicidad original, C39/C35 y revalidación antes de I/O |
| Preparación automática se pierde o Documents llama Sales directamente | Reevaluación durable por caso mediante coordinador, insumos verificados; no nuevo dueño empresarial ni framework genérico |
| CPE equivocado/XML reconstruido pasa o aprobación cambia de destinatario | Correspondencia documentada, procedencia original/representación/copia, fingerprint y permisos actuales; política HP4 pendiente, no tratamiento fiscal inventado |
| Staging filtra CC/BCC, timeout/lease/restore repite original | Guardia de entorno sobre todos los destinatarios, UNKNOWN/HOLD y conciliación, registro antes de I/O, efectos desactivados al restaurar |
| WO necesita inventar evidencia o seis WOs aparentan terminar el ERP | Seis encargos PREPARED con perfiles/recortes/gates; UNIT aislado y RLS habilitante en WO-SP2-02. No atribuir a evidencia parcial un escenario completo |

Contradicción externa conservada: documentación oficial Jumpseller discrepa sobre momento de descuento de stock y calendario de retries; [S21/S26](decisions/sources.md). El contrato bloquea la activación dependiente hasta comprobar la tienda/flujo real. No se trasladan esas afirmaciones a invariantes internas. SUNAT solo acredita la consulta documentada de un CPE identificado, no descarga total SOL; el baseline manual sigue disponible según política.

**SUPERPROMPT 2: PASS documental.** Se revisaron las fichas, transiciones, permisos, orden común y contraejemplos del circuito; no se identificaron contradicciones internas residuales en este alcance. Comprobaciones estáticas: 17 archivos Markdown (7 nuevos y 10 existentes), 218 referencias locales resueltas, incluidas 49 a anchors explícitos; 37 fichas completas y coincidentes con la matriz; 110 escenarios y seis WOs sin IDs duplicados, referencias a fuentes reconocidas entre S01–S28. El grafo de 11 módulos permanece acíclico, sin nuevas dependencias empresariales; no hay archivos vacíos, patrones de secretos detectados o cambios fuera de la lista autorizada. Diff completo revisado y comprobación de whitespace sin errores; son comprobaciones documentales, no pruebas de aplicación.

No se ejecutaron tests de aplicación, Docker, builds, CI ni infraestructura; tampoco se consultó Wbpro/legacy ni cuentas privadas o se enviaron correos. La revisión del diseño no demuestra locks, RLS, precisión, recuperación ni semántica de proveedores ejecutables. Workspace/RLS, mecanismos de concurrencia y durabilidad, rangos numéricos y activación de proveedores conservan sus condiciones provisionales; HP1–HP5 condicionan operación, no la preparación independiente de WO-SP2-01.

La preparación siguiente está delimitada por [WO-SP2-01](specs/work-orders.md#wo-sp2-01): runtime/calidad mínima identificables para poder demostrar después aislamiento. Las seis WOs permanecen sin ejecutar y requieren autorización nueva; no SUPERPROMPT 3 ni operación real por cerrar esta especificación.
