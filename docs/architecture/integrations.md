# Integraciones, eventos y trabajo durable

Contrato de [ADR-008](../decisions/adr-008-integrations.md). No hay integraciones ni workers implementados.

## Frontera externa

Los adaptadores viven fuera de Sales, Treasury y Procurement. Traducen HTTP/archivos del proveedor a valores conocidos; no deciden deuda, stock o tratamientos fiscales. La composición conecta adaptadores concretos con puertos explícitos; no registro global reemplazable durante una request.

| Integración | Primer uso conceptual | Condición de activación |
|---|---|---|
| SUNAT | Preparación, consulta y conciliación de evidencia | Fuente normativa y contrato técnico vigente; ningún envío/presentación automática inicial |
| Jumpseller | Entrada de pedidos y conciliación de estados | Un pedido externo es propuesta, no orden de despachar; firma/cuenta/duplicados/stock deben especificarse |
| Bancos | Importar extractos y registrar evidencia de movimientos | Conciliar no ordena transferir; pago externo automático fuera de alcance |
| Email | Avisos sin datos sensibles innecesarios | Fallo de notificación no invalida una transacción económica confirmada |
| Storage | Evidencia privada y exportaciones temporales | Adaptador de objetos, autorización al descargar y recuperación de blobs |

Cada conexión declara proveedor/cuenta, entidad local vinculada, secreto externo a Git, URL permitida, timeouts de conexión/lectura, tamaño máximo, política de retry, identidad externa y traducción de errores. No aceptar una URL arbitraria recibida en webhook ni elegir entidad a partir del cuerpo sin verificar su conexión.

Webhooks: autenticar según contrato oficial, verificar antigüedad/replay cuando el proveedor lo permita, persistir recepción durable y responder pronto; duplicados se reconocen sin repetir el efecto. Falta de versión/orden fiable obliga a reconciliar con la fuente; no suponer entrega ordenada.

## Tres clases de evento

| Clase | Qué representa | Propiedad |
|---|---|---|
| Hecho de dominio/económico | Algo confirmado y necesario para consumidores o explicación empresarial | Lo produce su dueño en la misma transacción del hecho |
| Mensaje de integración | Representación para un contrato externo | Versión y datos mínimos; no es automáticamente un hecho aceptado |
| Registro outbox/job | Intención durable de entregar/procesar un trabajo | Estado operativo y política de recuperación; no nueva regla de negocio |

El evento lleva ID, entidad, tipo/versión, raíz/revisión, fecha empresarial, instante de registro, correlación/causación y datos suficientes sin PII indiscriminada. Accounting consume hechos versionados y registra el ID consumido junto con el asiento en su transacción; no conoce modelos operativos ni publica asientos desde Sales. Tax separa su interpretación. Consumir un evento no prueba que la política contable/tributaria sea correcta.

## Síncrono primero; durable cuando haya consumidor

Dinero y stock locales se resuelven dentro de una transacción corta. Consultar proveedores, enviar correos o producir reportes largos sucede fuera de esa transacción. Para un efecto que deba sobrevivir al proceso, el cambio y su intención quedan en DB antes del commit; on_commit solo puede despertar un consumidor, nunca ser el único registro del trabajo.

Al activar trabajo durable, una cola/outbox PostgreSQL y un proceso worker simple son el candidato PROVISIONAL, sin broker inicial. El backend y su representación requieren un consumidor concreto y evidencia de caída/reanudación antes de aceptarse. Contrato de referencia: claim corto con exclusión, lease/vence, token de intento, contador/fecha de próximo intento, límite/backoff, resultado y dead-letter con replay autorizado. El worker no mantiene un lock DB durante HTTP. Un resultado de lease antiguo no puede sobrescribir al intento vigente.

La entrega es al menos una vez. La unicidad del ID procesado y el efecto de DB se confirman juntos. Frente a un proveedor, una lease no evita duplicación de un efecto externo: se exige clave idempotente del proveedor o conciliación antes de reenviar. Resultado ambiguo de dinero/documento irreversible → revisión/consulta de estado, no retry ciego.

No se adopta Celery, Redis, RabbitMQ, Kafka ni SQS inicialmente. Se reconsidera si volumen, scheduling, topología o operación lo justifican. Django Tasks ofrece API/plumbing; no aporta por sí solo el worker productivo [S10](../decisions/sources.md). Su backend se evaluará cuando exista trabajo concreto, evitando implementar un framework general de colas.

## Dónde persiste la coordinación que debe sobrevivir

| Estado necesario | Propietario y persistencia conceptual |
|---|---|
| Progreso empresarial para reanudar | En PostgreSQL, en el caso del módulo dueño: Sales o Procurement cuando exista una devolución comercial. Una intención que solo afecta Treasury permanece allí; no crea un expediente comercial artificial. Conserva sus decisiones y referencias a hechos de otros propietarios, sin copiar sus saldos ni sustituirlos por flags |
| Hecho físico, monetario o documental | En su módulo propietario. Documents persiste archivo/disponibilidad; Sales y Procurement conservan sus respectivos expedientes CPE |
| Entrega de un hecho producido / tarea solicitada | Registro técnico durable en PostgreSQL bajo responsabilidad del productor/solicitante; contiene identidad de intención, destino, intento y resultado técnico. El backend es infraestructura reemplazable, no dueño del hecho |
| Procesamiento de un consumidor | El consumidor persiste su recepción/deduplicación junto con su efecto; por ejemplo Accounting con el asiento. Un acuse de entrega del productor no demuestra ese efecto |

Si el progreso se deriva íntegramente de hechos persistidos, se reconstruye por referencias y no se almacena otra máquina de estados. Si hay una decisión empresarial indispensable no derivable, la especificación la asigna al caso del módulo dueño antes de implementarla. Workflows ejecuta coordinación sin tablas propias de hechos ni progreso empresarial en memoria como única copia.

Tablas, campos, esquema técnico compartido o por módulo y backend exacto permanecen PROVISIONAL hasta el primer caso durable; esta asignación de responsabilidad no crea un workflow engine ni un nuevo módulo. Su aceptación requiere demostrar recuperación tras commit/caída, deduplicación y ausencia de divergencia con los propietarios. Si todo cabe en una transacción local, no se introduce seguimiento durable adicional.

## Fallos que el contrato debe admitir

Commit correcto + proceso muerto antes de publicar; duplicado; mensaje fuera de orden; respuesta tardía; credencial vencida; proveedor caído; timeout con efecto externo ya ejecutado; objeto subido con metadatos no confirmados; metadatos existentes con blob ausente.

Documents tratará DB y objetos como recursos no atómicos: carga temporal/cuarentena, confirmación de disponibilidad, reconciliación de huérfanos y política de limpieza. Una descarga usa autorización actual y enlace breve o proxy autenticado; URL opaca permanente no es permiso.

REQUIRES LATER VALIDATION: esquemas/payloads reales, autenticación del proveedor, replay, leasing y caída de proceso, contratos de storage y restauración DB+blobs. No se verificó ninguna cuenta externa en esta fase.
