# SP2 — Escenarios de aceptación futuros

No son tests escritos o ejecutados. Propietarios de comportamiento: [alcance](../flows/first-operational-circuit.md), [negocio](../flows/sales-stock-treasury.md), [CPE/Documents](../flows/cpe-document-delivery.md), [integraciones](../flows/jumpseller-external-work.md) y [matriz](../cross-cutting/command-matrix.md). Cada escenario usa sus comandos/guardas; los [perfiles](../../history/work-orders-sp2.md) seleccionan evidencia por propiedad, sin repetir suites por nombres de módulos.

Fixtures sintéticas: entidades A/B, miembros/principales distintos, moneda PEN salvo indicación, documentos/IDs/cuentas ficticios identificados como tales. Las pruebas aplican HP1–HP3 según su estado vigente y políticas sintéticas explícitas para los parámetros todavía pendientes de HP2–HP5; un fixture no aprueba esos parámetros ni acredita una regla fiscal. Proveedor simulado con respuestas de contrato para pruebas ordinarias; cuentas/efectos reales solo en una validación futura expresamente autorizada, nunca LOCAL/CI. Las carreras usan conexiones separadas y barreras controladas, verificando también auditoría/eventos/intenciones persistidas.

## Circuito completo y propuesta

| ID | Given | When | Then |
|---|---|---|---|
| SP2-AC-001 | SKU/Party/mapping/cuenta válidos, P=2/N=0, política sintética completa, pedido de 1 unidad/100 y ningún dinero | C02/C03/C04, aceptar C14, proponer/confirmar 100 C16/C17 y aplicar C18, preparar/entregar C19/C20; CPE externo/artefactos C30–C33, C34/C35/C07/C08/C09 | Una venta/T, una reserva consumida, P=1, un cobro/aplicación, CPE vinculado sin emisión CasPro y una primera entrega documental; sin segundo descuento ni llamada externa bajo lock |
| SP2-AC-002 | Webhook válido de pedido nuevo | C02 recibe; C03 refresca y C04 selecciona observación | Receipt/caso durables; UNDECIDED, sin venta/reserva/cobro; READY no significa aceptado |
| SP2-AC-003 | Mismo pedido recibido dos veces con diferentes recepciones | Procesar ambos y dos C14 concurrentes con distintas claves | Un caso/venta/objetivo y reserva única; segundo devuelve aceptación existente o conflicto de términos, nunca duplica |
| SP2-AC-004 | Propuesta no aceptada, nueva lectura cambia líneas/dirección | C04 selecciona generación vigente | Revisión/snapshot de propuesta nuevos, anterior conservado; validar de nuevo; no deltas sobre líneas adivinadas |
| SP2-AC-005 | Venta aceptada de 1 unidad; update pide 2 | C04 | REVIEW_REQUIRED; no aumentar venta/R/L. Demanda extra observada no se cuenta dos veces y bloquea ejecución incompatible |
| SP2-AC-006 | Pedido CANCELED observado por lectura fresca | Llega webhook antiguo Pending | No READY ni reactivación por arribo; refrescar/reconciliar; sin aceptación automática |
| SP2-AC-007 | Generación GET 8 y después 9 | Responde primero 9 y después 8 | 8 se conserva tardía sin sustituir selección ni freshness de 9 |
| SP2-AC-008 | Webhook se pierde y existe pedido remoto no conocido | C03 completa barrido paginado | Descubre pedido/caso; misma identidad que una recepción posterior, sin segunda venta |
| SP2-AC-009 | Scan falla en página intermedia | C03 termina con error | PARTIAL_SCAN; no avanzar checkpoint completo ni aumentar stock por ausencia aparente de pedidos |
| SP2-AC-010 | SKU UNLINKED/AMBIGUOUS/MISSING_REMOTE o unidad incompatible | C04/C14 | BLOCKED con motivo específico; no adivinar por nombre ni reservar parcialmente |
| SP2-AC-011 | Dos líneas del mismo SKU, cantidades 1 y 2 | Aceptar | Demanda total 3, evidencia de ambas líneas preservada; no deduplicar por SKU |
| SP2-AC-012 | Total/desglose no coincide con la interpretación aprobada | C14; luego C15 REVISE_PROPOSAL con evidencia/política y C04 reevalúa | Primero TOTAL_MISMATCH y rollback íntegro; después solo propuesta explicada/revisada puede ser READY, original externo intacto. Una nueva observación material invalida conformidad; no tolerancia inventada |
| SP2-AC-013 | Firma falsa o ruta conexión A con body/identidad de B | C02 | Rechazo sin negocio; no seleccionar entidad desde payload; auditoría técnica acotada |
| SP2-AC-014 | Body con firma válida, header event/triggered-at alterado o repetido | C02/C04 | Header no firmado no cancela ni paga; lectura seleccionada decide propuesta |
| SP2-AC-015 | Secuencia de snapshots A→B→A, hash A ya conocido | Llega nueva observación de A y se reconcilia | No se pierde por dedupe eterna de hash; generación vigente seleccionada, sin duplicar compromiso |

## Maestros, acceso y carga

| ID | Given | When | Then |
|---|---|---|---|
| SP2-AC-016 | Dos personas comparten email | Resolver Party por C11 | No fusión automática; selección/evidencia explícitas |
| SP2-AC-017 | Invitado sin customer ID ni identidad fiscal | Crear/resolver propuesta | Referencia restringida a pedido y datos declarados; no documento ficticio; HP4 decide identidad exigible |
| SP2-AC-018 | Venta aceptada con contacto/dirección snapshot | Editar Party | Venta/artefactos/aprobación no se reescriben desde maestro; corrección comercial explícita si se solicita |
| SP2-AC-019 | Dos mappings del mismo external product/variant hacia SKU distintas | C12 concurrente | Conflicto/único vínculo válido, no selección por última escritura |
| SP2-AC-020 | No email, o dirección de envío incompleta | C14 y luego C34 | Email ausente queda pendiente documental; dirección incompleta bloquea aceptación de envío; no completar con datos del operador |
| SP2-AC-021 | CSV/XLSX válido con altas/cambios/duplicados/conflictos | C24 | Preview clasificado, hash/revisiones/parser; ninguna existencia o maestro confirmado por upload |
| SP2-AC-022 | Una fila inválida dentro de lote confirmado | C25 | Ninguna nueva fila de ese lote aplicada; otros lotes previos identificados conservan su resultado, sin fingir atomicidad de archivo entero |
| SP2-AC-023 | Maestro/política/permisos cambian tras preview | C25 | PREVIEW_STALE/AUTH_DENIED, no aplicar cambios distintos de los revisados |
| SP2-AC-024 | Lote de apertura confirmado | Repetir con misma clave o reimportar filas con nuevo lote | No duplicar P/coste; identidad de procedencia de fila protege además de clave de lote |
| SP2-AC-025 | XLSX con fórmulas/macros/enlaces externos, CSV exportado con celdas maliciosas | Preparar/importar/exportar | No ejecutar ni usar fórmula cacheada como verdad; rechazar campo requerido con fórmula; exportación neutralizada |
| SP2-AC-026 | Usuario A conoce UUID/external ID de B | Leer, buscar, abrir preview o ejecutar comando | Denegación sin filtración de existencia, snippets o conteos; ninguna escritura cruzada |
| SP2-AC-027 | Actor autenticado sin contexto/capacidad o staff sin concesión | C14/C17/C20/C35/C38 | Denegar; staff no suple permiso económico |
| SP2-AC-028 | Conexión DB usada para A | Commit/rollback/error/savepoint, luego B y luego sin contexto | Sin datos cruzados ni contexto persistente; lectura ORM materializada dentro de transacción |
| SP2-AC-029 | Rol runtime real, dos entidades y referencias padre/hijo | SQL/ORM sin filtro, INSERT/UPDATE/DELETE/bulk/referencia cruzada | RLS/grants/pertenencia efectivos; no demostrarlo con rol owner de migración |
| SP2-AC-030 | Tabla nueva sin protección, policy permisiva o BYPASS/owner indebido introducidos deliberadamente | Evaluar gate de aislamiento | El candidato falla; verificador no acepta por detectar solo columna tenant/policy cualquiera |
| SP2-AC-031 | Revocada la membresía/autoridad que sustenta el mandato del job después de prepararlo | C07 reconstruye contexto | No efecto nuevo; aprobación antigua no presta permisos eternamente |
| SP2-AC-032 | Bootstrap/selección/admin Workspace | Operador selecciona entidad o revoca miembro | Solo directorio mínimo/membresías propias fuera de contexto; perfil/establecimientos protegidos y cambio administrativo auditado |

## Stock, reservas y entrega

| ID | Given | When | Then |
|---|---|---|---|
| SP2-AC-033 | P=5/N=1/R=0 y propuesta 3 | C14 | R=3, A=1, P=5; aceptación íntegra, no salida física |
| SP2-AC-034 | P=1/N=0 y dos propuestas de 1 | Dos C14 intercalados | Solo una acepta; STOCK_INSUFFICIENT en otra; invariante N+R≤P y auditoría coherentes |
| SP2-AC-035 | Reserva 3, no consumida | Cancelar 1 por C15 dos veces | Liberar exactamente 1; R=2, P igual; no segunda liberación por duplicado |
| SP2-AC-036 | Reserva 3, cobertura completa | Preparar/entregar 1 por C19/C20 | P−1/R−1, entrega parcial y asignación agotada; restantes conservados; misma preparación no se confirma dos veces |
| SP2-AC-037 | Dos preparaciones compiten por mismo serial/remanente | C19 concurrentes | Una asignación válida; no dos preparaciones de la misma unidad |
| SP2-AC-038 | Preparación READY | C15 cancela antes de C20 o C20 confirma antes | Primer orden invalida preparación/libera solo pendiente; segundo conserva entrega y cancela solo remanente, sin borrar stock consumido |
| SP2-AC-039 | P=4/N=0/R=3 | Ajuste negativo 2 o daño de 2 por C13 | RESERVATION_CONFLICT; no robar reserva ni hacer A negativo; resolver negocio antes |
| SP2-AC-040 | P/N/R/X/B del ejemplo de Inventory | Aceptar demanda X y luego despachar | Q no vuelve a descontar cantidades al convertir X→R ni al consumir R/P |
| SP2-AC-041 | Stock objetivo y remoto iguales, llega eco de publicación | C02/C03/C05 | Observación/no-op; ningún movimiento local o loop de publicación |
| SP2-AC-042 | Plan versión 4 y stock/caso cambió a 5 antes de dispatch | C07 | SUPERSEDED; no publicar versión 4 |
| SP2-AC-043 | PUT versión 4 en vuelo, aparece versión 5 | Responde 4 tarde | No marca versión 5 sincronizada; resultado retenido y reconciliación pendiente |
| SP2-AC-044 | Inbox atrasado/scan parcial/X ambiguo | C05 intenta aumentar stock | BLOCKING; no interpretar faltante como demanda cero |
| SP2-AC-045 | GET stock=5, checkout baja remoto a 3 antes de PUT=4 | Intentar publicación positiva sin protocolo probado/ventana | Bloqueada por gate STOCK-PUBLISH; la spec no considera PUT=4 «reducción segura» ni afirma fence remoto por lease |
| SP2-AC-046 | SKU retirado con reserva válida anterior | Confirmar entrega/retorno o intentar nueva aceptación/apertura | Ejecutar/corregir compromiso previo permitido por guardas; compromiso/apertura nueva rechazados |
| SP2-AC-047 | Salida original 3 con coste total 10 y retornos parciales | C21 retorna 1+1+1 | Reparto conserva 10 y residuo exacto; cuarta unidad rechazada, no recalcular desde unitario redondeado |
| SP2-AC-048 | Venta→retorno→reventa legítima del mismo serial | Registrar nueva devolución contra segunda salida | Ciclo nuevo válido; duplicar retorno contra la misma salida inválido; no unicidad vitalicia de venta |
| SP2-AC-049 | Retorno autorizado recibido; luego se acredita error de captura | C21 RECEIVE_RETURN y CORRECT_RETURN | Entrada no vendible sin refund/CPE automático; compensación solo hasta retorno neto con unidades/ciclo disponibles, coste conservado y ambas mitades corregidas. No retirar unidades revendidas/reservadas; C13 exige revisión para habilitar reventa |
| SP2-AC-050 | Caída al guardar audit/evento de entrega | C20 | Rollback de Sales, P/R/costes/seriales y trabajo durable; rechazo auditado fuera si DB permite |

## Dinero y correcciones

| ID | Given | When | Then |
|---|---|---|---|
| SP2-AC-051 | Jumpseller PAID y ningún cobro Treasury | C04 y preparar entrega | Observación no crea N/A; confirmar entrega sin cobertura falla |
| SP2-AC-052 | Propuesta de cobro con evidencia HP2 válida | C17 por 100, C18 aplica 100 a L=100 | N=100/A=100/U=0, objetivo liquidado; referencia/cuenta/actor conservados |
| SP2-AC-053 | L=100 y cobro/aplicación de 40 | C18 y C20 con política sintética prepago completo | Parcial visible; COVERAGE_INSUFFICIENT sin salida física |
| SP2-AC-054 | L=100 y cobro de 130 | Aplicar 100 o intentar 130 | Primera deja U=30; segunda rechaza exceso; no ingreso adicional |
| SP2-AC-055 | Cobro USD, objetivo PEN | C18 | WRONG_CURRENCY, sin conversión/suma automática |
| SP2-AC-056 | Referencia bancaria ya confirmada | C17 con otra clave/propuesta | DUPLICATE_RECEIPT_REFERENCE, no segundo movimiento |
| SP2-AC-057 | Un cobro 100 y dos objetivos 80 | C18 concurrentes por 80 | No A(r)=160; uno falla o aplica solo importe explícito válido, sin prorrateo inventado |
| SP2-AC-058 | Objetivo 100 y dos cobros de 80 | Aplicaciones concurrentes | No A(o)>100; excedente de cobro sigue U o petición rechazada |
| SP2-AC-059 | Cobro 100 aplicado 80 y refund probado de 50 | C22 con plan de des-aplicar 30 | N=50/A=50/U=0, referencias/corrección y cobertura actualizadas; no CPE/retorno físico automático |
| SP2-AC-060 | Refund descubre aplicaciones; otra C18 crea una nueva antes de locks completos | C22 | Redescubrir S/T/R y validar plan; no refund con conjunto antiguo |
| SP2-AC-061 | Entrega compite con refund de su cobertura | C20/C22 en ambos órdenes | Refund primero impide entrega sin cobertura; entrega primero conserva hecho y refund deja déficit visible/bloqueo de nueva entrega |
| SP2-AC-062 | Cancelación reduce L de 200 a 100 con A=200 | C15 con des-aplicación explícita de 100 | L/T/A=100, U aumenta 100, reserva remanente liberada; no transferencia automática |
| SP2-AC-063 | Cobro capturado erróneamente, sin devolución bancaria real | C22 CAPTURE_CORRECTION | Tipo/motivo distintos de REFUND_EXTERNAL, original conservado, sin afirmar transferencia externa |
| SP2-AC-064 | Cuenta cerrada o moneda/propietario incompatibles | C17 o modificación C23 | No nuevo cobro ni cambio de moneda/entidad de cuenta usada; corrección histórica sigue guardas |
| SP2-AC-065 | Clave D repetida con diferente importe | C17/C18/C22 | IDEMPOTENCY_CONFLICT; no segundo efecto ni retorno de datos a actor revocado |

## CPE, bytes y documentos

| ID | Given | When | Then |
|---|---|---|---|
| SP2-AC-066 | CPE externo único, emisor/adquirente/desglose/evidencia compatibles | C30/C31/C32/C33 con verificación oficial exigida | LINKED y resultado ligado a inputs; artifacts disponibles por versión; ningún emisor SUNAT construido |
| SP2-AC-067 | CPE de otro emisor, comprador incompatible o importe distinto | C33 | MISMATCH, sin entregabilidad ni modificación de XML para coincidir |
| SP2-AC-068 | Dos CPE candidatos o solo mismo monto/hora | C33 | AMBIGUOUS; operador debe aportar evidencia de correspondencia, no selección automática |
| SP2-AC-069 | No hay API de adquisición habilitada | Operador importa archivos/registra consulta oficial manual | Puede seguir baseline según HP4; no asumir enumeración SOL ni pedir credenciales privadas en docs |
| SP2-AC-070 | Consulta HTTP exitosa con success/código negativo o desconocido | C08/C33 | No marcar MATCH por 200; conservar código/observaciones, diferenciar UNAVAILABLE y negativo |
| SP2-AC-071 | Se cambia identidad/importe de consulta después de resultado | Revalidar vínculo/aprobación | Resultado anterior no acredita nuevos inputs; aprobación relevante invalidada |
| SP2-AC-072 | XML original y XML reconstruido contienen mismos datos | Importar ambos o falta original requerido | Versiones/procedencia distintas; reconstruido no satisface original ni se renombra para pasarlo |
| SP2-AC-073 | Captura/escaneo aportado por operador | C31 | EXTERNAL_COPY, no ORIGINAL_EXTERNAL del emisor por ser un archivo externo |
| SP2-AC-074 | Metadata confirmada, blob ausente/hash diferente | C32/C34/C38 | MISSING/QUARANTINED, bloqueo de uso; no preview/email con otra versión sustituta |
| SP2-AC-075 | XML con DTD/entidad externa, PDF activo o tamaño excesivo | C31/C32 | Sin red/ejecución, cuarentena/rechazo según límites; no disponible por extensión .xml/.pdf |
| SP2-AC-076 | Usuario autorizado A / usuario ajeno o revocado | C38, URL caducada y cache de preview | Acceso privado a versión autorizada; denegación de nuevo acceso/URL caducada; cache no filtra datos |
| SP2-AC-077 | Reporte temporal vs snapshot persistido | C26 | Temporal no crea expediente permanente; snapshot lleva tipo/parámetros/corte/cálculo/actor/hash/procedencia |
| SP2-AC-078 | Venta/retorno con coste desconocido o impuestos no separables | Calcular margen | UNKNOWN/INCOMPLETE o base claramente identificada, nunca coste cero/utilidad neta/asiento o tratamiento fiscal inventado |

## Entrega documental y Resend

| ID | Given | When | Then |
|---|---|---|---|
| SP2-AC-079 | AUTO_WITH_APPROVAL y todos los requisitos | Cambia vínculo/disponibilidad; consumidor durable ejecuta C34 sin C35, luego aprobar | Una preparación automática deduplicada; antes no dispatch, después una intención durable elegible revalidada por C07. Caída antes de reevaluar no pierde preparación ni crea otro original |
| SP2-AC-080 | Aprobación vigente, cambia recipient/artifact/subject/política relevante | C39/C33/C36 y C07 | APPROVAL_STALE/INVALIDATED; no enviar contenido distinto; requiere nueva aprobación |
| SP2-AC-081 | HOLD en dossier y otro intento de reenvío | C37 o cambiar modo a MANUAL/AUTO | HOLD sigue efectivo; nueva intención/mode no lo elude |
| SP2-AC-082 | DISABLED, política incompleta o preparador MANUAL sin documents.send | C34/C35/C07 manual/auto | Sin dispatch, bloqueo explícito; preparar no concede permiso de enviar. Corregir una intención no despachada requiere C34 REQUEST_MANUAL_DISPATCH autorizado o C35 según modo, sin otro original |
| SP2-AC-083 | Dos C34 con claves distintas/doble click | Concurrencia | Una primera intención por entidad/CPE/finalidad; no dos originales por recipient/versión diferente |
| SP2-AC-084 | C35 y C39 concurrentes | Aprobar/cambiar en ambos órdenes | Aprobación se liga a inputs que existían bajo locks; cambio posterior invalida; no mezcla |
| SP2-AC-085 | Dispatch autorizado y HTTP timeout, proveedor pudo aceptar | C08/lease vence | UNKNOWN/HOLD; no retry ciego ni lease nueva que reenvíe automáticamente |
| SP2-AC-086 | Fallo demostrado antes del efecto, retry autorizado | C07 posterior | Misma intención/clave/payload; no cambiar recipient bajo etiqueta RETRY |
| SP2-AC-087 | Resultado desconocido y han pasado más de 24 h | Intentar nuevo envío | Unicidad local persiste; HOLD/reconciliación, no otra primera entrega por vencer dedupe proveedor |
| SP2-AC-088 | Original conocido y reenvío explícito autorizado | C37 con nueva clave, C35 si procede | Nueva intención relacionada/mismo CPE, controles completos; doble click de reenvío con misma clave no duplica |
| SP2-AC-089 | delivered, luego sent/delayed tardío | C09 | No degradar a pendiente ni generar reenvío; delivered no acredita lectura humana |
| SP2-AC-090 | bounced/failed/suppressed | C09 | Pendiente de entrega/HOLD correspondiente, CPE y venta inalterados; no refund |
| SP2-AC-091 | delivered y bounced incompatibles para intento/destinatario | C09 | CONFLICT con ambas observaciones y conciliación; no elegir último arribo |
| SP2-AC-092 | Callback duplicado firmado, o svix-id repetido con body diferente | C02/C09 | Primero deduplicado sin efecto adicional; segundo conflicto de integridad, no sobrescritura |
| SP2-AC-093 | Callback válido llega antes de guardar email_id | C09, después C08/conciliación | Receipt pendiente conservado y asociación inequívoca posterior; no vincular por email/asunto |
| SP2-AC-094 | LOCAL/CI, credencial inyectada accidentalmente, cualquier modo | Intentar transporte real | ENVIRONMENT_BLOCKED/captura local; cero red Resend y cero correo real |
| SP2-AC-095 | STAGING captura por defecto; luego envío habilitado con TO seguro pero CC/BCC reales | Preparar/aprobar/despachar | Captura por defecto; en envío, todas las direcciones efectivas seguras o rechazo; ninguna copia al cliente real |
| SP2-AC-096 | STAGING allowlist/remitente cambia tras aprobación | C07 | Invalidar y reaprobar nuevo efectivo; no cambiar transporte a escondidas |
| SP2-AC-097 | Preparador=aprobador sin excepción de segregación | C35 | SEGREGATION_REQUIRED; con excepción sintética vigente, registrar misma persona y motivo, no dos revisores falsos |
| SP2-AC-098 | HOLD se confirma antes o después del punto de autorización de C07 | Intercalar | Antes impide dispatch; después conserva límite de cancelación/carrera y resultado a conciliar; no promesa falsa de retractar correo |
| SP2-AC-099 | Primera entrega conocida por vía externa o historial restaurado insuficiente | C34/AUTO | No nuevo original automático; registrar evidencia/resolver incertidumbre antes de permitir actuación |

## Recuperación y evidencia

| ID | Given | When | Then |
|---|---|---|---|
| SP2-AC-100 | Commit de venta/objetivo/reserva/job correcto | Proceso cae antes de despertar worker | Trabajo durable sigue; on_commit perdido no pierde intención ni duplica hechos |
| SP2-AC-101 | DISPATCHED confirmado | Caída antes de HTTP o después de HTTP antes de C08 | UNKNOWN conservador salvo prueba de no envío; no deducir resultado de que falte external ID |
| SP2-AC-102 | Worker viejo con lease/token vencido y nuevo estado vigente | Llega resultado viejo | Conservar evidencia tardía, no sobrescribir fila/generación vigente; reconciliar |
| SP2-AC-103 | Shutdown con claims y dispatch en vuelo | Reiniciar | Claim sin dispatch recuperable; dispatch incierto retenido; ningún worker mantiene transacción durante espera |
| SP2-AC-104 | Backup anterior a email/stock ejecutado externamente | Restaurar DB/outbox y objetos | Efectos desactivados/epoch nuevo; reconciliar historia externa antes de reactivar, no asumir ausencia de entrega por DB antigua |
| SP2-AC-105 | Restore DB correcto pero blobs/versiones no coinciden | Validar dossier/descarga | Bloqueo disponibilidad/entrega, sin sustituto generado etiquetado original |
| SP2-AC-106 | Errores transitorios repetidos o rate limit/auth fallida | Worker agota política | Espera acotada/dead-letter o bloqueo credencial, sin retry infinito ni registro perdido |
| SP2-AC-107 | Fixture/rol/grants/parser/contrato/lock cambia tras evidencia QA | Evaluar reutilización | Invalidación por afirmación según QA; nombre de módulo/HEAD o PASS anterior no basta |
| SP2-AC-108 | Categoría UNIT seleccionada | Colección/ejecución futura | No inicializar Django/DB/red por conftest/plugin global; separación demostrada por guardia negativa |
| SP2-AC-109 | Bandeja muestra bloqueo de fuente | Resolver por comando del dueño o editar proyección | Solo el cambio fuente válido resuelve; no flag resolved que oculte condición real |
| SP2-AC-110 | Búsqueda por CPE/pedido externo con igual número en otra conexión/entidad | Consultar paginado | Resultado, conteos/snippets y navegación respetan contexto; no sumar ni revelar coincidencias ajenas |

## Refutación documental de esta entrega

La revisión final debe recorrer especialmente SP2-AC-003, 034, 045, 057–061, 068, 080–085, 094–096 y 100–105 contra las fichas/matriz, buscando un paso sin dueño/guarda/evidencia. Una secuencia plausible sin garantía queda como mecanismo pendiente y gate de activación; no se convierte en prueba pasada. El estado real de revisión y sus límites se registra en [review](../../review.md), sin reauditar Gate 1.
