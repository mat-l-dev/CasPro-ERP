# Revisión y condición de avance

Fecha: 2026-09-10. Alcance: correcciones documentales de Gate 1 en CasPro. **Veredicto: PASS. Gate 1: CLOSED, exclusivamente documental.** Este archivo es la fuente del estado global del gate; cada ADR conserva la autoridad sobre sus alcances. Nada de esta entrega acredita software construido, desplegado o production-ready ni aprueba decisiones empresariales. SUPERPROMPT 2 no se inicia ni queda autorizado por este cierre.

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

Todas figuran PENDING HUMAN DECISION. Los ADRs distinguen principios aceptados y mecanismos provisionales; estos últimos conservan incertidumbre técnica, que no se traslada al propietario como si fuera una decisión empresarial.

| ID | Decisión | Recomendación / qué condiciona |
|---|---|---|
| H1 | Primer uso empresarial, bienes/servicios y nivel de contabilidad interna exigible desde ese uso | Empezar por un circuito pequeño completo; no habilitar ventas por tener pantallas si falta el cierre requerido |
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

## SUPERPROMPT 2: siguiente fase propuesta

Después de revisión humana, resolver H1 y las políticas que bloqueen el circuito elegido; especificar Workspace/Parties/Catalog mínimos y un recorrido comercial completo con dinero, stock, evidencia y correcciones. Precisar estados, contratos entre propietarios, límites monetarios/temporales y matriz de locks; mantener Accounting/Tax separados y validar normativa antes de fijar tratamientos.

Diseñar casos de aceptación y Validation Profiles, ordenar riesgos habilitantes y preparar solo las primeras WO pequeñas revisables. No especificar todos los módulos exhaustivamente por rutina, no generar una cola masiva y no iniciar implementación, infraestructura o pruebas salvo autorización expresa en esa fase.
