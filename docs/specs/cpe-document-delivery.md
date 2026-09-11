# SP2 — CPE externo, archivo y entrega documental

Propietarios: Sales conserva CPE de venta/vínculo comercial; Documents conserva archivo, disponibilidad, política e intención de entrega. Adaptadores SUNAT/Resend ejecutan consultas/envíos concretos fuera de transacción. No nuevo Document Vault ni plataforma CRM/email. Estas son las fuentes locales de estados; [CM0](command-matrix.md#cm0) completa fichas, [integraciones](integrations.md) posee jobs y protocolo externo. HP4/HP5 de [alcance](first-operational-circuit.md) delimitan decisiones de política.

## Identificar, adquirir, vincular y verificar

Baseline: operador prepara contexto de venta en CasPro, emite fuera por SOL/u otra vía autorizada, registra identidad/evidencia de esa emisión, importa artefactos disponibles y registra verificación oficial cuando aplique. CasPro no emite, presenta ni tiene botón para enviar CPE a SUNAT. La [revisión RCP](../research/tax-current-review.md) exige separar oportunidad de emisión, otorgamiento, pago y despacho: un diagrama que muestre CPE después de dispatch no prescribe ese orden legal. Conformidad del medio de pago/anticipo puede generar obligación antes de que Treasury confirme o Sales acepte internamente. Preservar observación y fecha externa; la demora de captura no desplaza el nacimiento legal.

La identidad externa de CPE es `(RUC emisor, tipo, serie, número)`, bajo entidad propietaria; conservar valores recibidos y normalización de contrato, sin colisiones por quitar ceros/formatos arbitrariamente. Para el CPE de esta venta: emisor corresponde a Organization acreditada, fecha/moneda/importes/componentes compatibles con el expediente, identidad del adquirente compatible cuando exista/se exija y evidencia que lo relaciona con esa venta. Una identidad externa conocida no se asigna a dos ventas por error.

**Corrección Astra de cardinalidad:** una venta puede tener varios CPE por anticipos, liquidación y notas; cada CPE mantiene identidad única y vínculo a una sola venta en el alcance inicial. No se confunde multiplicidad legítima con ambigüedad: AMBIGUOUS indica correspondencia no resuelta. Un CPE que agrupe varias ventas queda registrado sin aplicación automática, fuera de este contrato hasta ampliación explícita. No se parte artificialmente una operación para evitar identificación del adquirente.

El expediente de emisión puede existir antes de la venta aceptada: se vincula provisionalmente al caso externo identificado o queda UNLINKED con evidencia y actor. C30 no exige inventar aceptación/reserva para registrar un documento real. La aceptación C14 no adopta automáticamente esos CPE; C33 confirma su correspondencia con la venta y conserva el antecedente.

## Asignaciones documentales de anticipos y correcciones

Sales conserva por versión de vínculo: identidad CPE, finalidad ADVANCE/SETTLEMENT/SALE/CREDIT_NOTE/DEBIT_NOTE, líneas originales, moneda, importes brutos/base/impuestos, porción atribuida a líneas/episodios comerciales y referencias a anticipos deducidos o documento modificado. Los nombres son roles internos, no códigos SUNAT inventados. Se requiere desglose fuente, no inferencia por total. La selección aprobada debe explicar `importe nuevo documentado = operación documentada − anticipos deducidos`, sin sumar de nuevo un anticipo que el documento final ya descuenta.

Guardas de C33: misma entidad/emisor/moneda y adquirente compatible; una porción fuente no se asigna dos veces; importes asignados no exceden el documento/episodio neto; toda nota identifica documento modificado y motivo real. Un anticipo aplicado documentalmente no confirma dinero, liquida Treasury ni reconoce ingreso Accounting. CPE emitido por toda la operación puede cubrir documentalmente el total con varios cobros; la multiplicidad se permite cuando hay documentos reales, no se exige emitir uno nuevo por cada registro de Treasury.

C33 publica una revisión de conciliación con importes por CPE, deducciones, notas, diferencia explicada/no explicada y obligaciones de emisión/otorgamiento pendientes. Una corrección o cambio de asignación invalida esa revisión y las aprobaciones de entrega afectadas. Retraer vínculo conserva CPE/bytes; anulación tributaria requiere evidencia externa. Una nota de crédito no devuelve stock ni dinero y no reduce el compromiso comercial sin C15.

Antes de C20, el operador ve la lista completa de CPE/obligaciones y evidencia de traslado aplicable; se revalida cumplimiento HP4 del acto, nunca un booleano de “hay expediente”. C17 conserva el cobro real aunque haya incumplimiento documental: el hecho durable permite abrir pendiente urgente, con fecha original, sin ocultar dinero ni declarar cumplimiento retrospectivo. Si el origen/operación aún es desconocido, se conserva esa incertidumbre y Tax evalúa el trigger cuando se identifique.

Lecturas: dossier por venta con anticipos/liquidación/notas y drill-through a cobro/evidencia; lista de CPE no vinculados; obligaciones vencidas por causa/fecha; vista individual de cada entrega documental. La unicidad de primera entrega sigue siendo **por CPE/finalidad**, por lo que enviar un CPE no marca enviados los restantes. C33 no envía documentos ni cambia aprobación de otra identidad sin explicar el impacto.

Aceptación adicional obligatoria: cobros40+60 para venta100 no habilitan despacho con40; CPE anticipo40 y liquidación con deducción40 suman100 de cobertura documental, no140; CPE único100 con dos cobros sigue siendo válido si corresponde a emisión real/política; dos identidades legítimas no son AMBIGUOUS; nota posterior conserva original y no refund automático; CPE previo a aceptación se registra sin reserva/venta ficticia; reenviar CPE-A no envía CPE-B; falta de guía exigible bloquea nuevo despacho, no captura del hecho monetario ocurrido.

Si el CPE contiene referencia de pedido/venta, se contrasta. Si no la contiene, el operador debe aportar contexto de emisión trazable y corroborar identidad/desglose contra la venta, registrando selección/atestación y evidencia; CasPro no afirma que SUNAT certificó esa relación. Solo «mismo monto + hora», destinatario de email coincidente o nombres parecidos → AMBIGUOUS, no LINKED. Un comprador sin identidad fiscal solo se admite conforme HP4 y con otra evidencia suficiente de correspondencia, nunca documento ficticio.

| Dimensión Sales | Estados y significado |
|---|---|
| Necesidad | POLICY_UNKNOWN / REQUIRED / NOT_REQUIRED según HP4; no se deduce de tener un archivo |
| Emisión externa | NOT_OBSERVED / OBSERVED: identidad, fuente y registro del operador; no orden de emisión |
| Vínculo | UNLINKED / LINKED / MISMATCH / AMBIGUOUS / RETRACTED, con revisión e historia |
| Verificación | NOT_CHECKED / PENDING / MATCH_REPORTED / NEGATIVE_REPORTED / UNAVAILABLE / CONFLICT; resultado/fuente/fecha e inputs consultados |
| Adquisición/disponibilidad | NONE/PARTIAL/REQUIRED_AVAILABLE derivados de versiones en Documents; ACQUIRED no significa original auténtico o CPE válido |
| Entregabilidad | Documents calcula DELIVERABLE o razones de bloqueo usando política, vínculo/verificación y artefactos; no es estado legal de Sales |

| Transición | Comando / guarda / corrección |
|---|---|
| NOT_OBSERVED → OBSERVED | C30 registra identidad/fuente explícitas; cambiar identidad usada crea corrección/retractación, no sobrescritura |
| UNLINKED/MISMATCH/AMBIGUOUS → LINKED | C33, evidencia compatible y elección inequívoca, raíz Sales vigente; falta de dato mantiene bloqueo |
| NOT_CHECKED/UNAVAILABLE → PENDING → resultado | C33 solicita consulta o registra evidencia oficial manual; C08 conserva respuesta y versión; un error de red no da NEGATIVE ni MATCH |
| LINKED → RETRACTED/MISMATCH | C30/C33 con evidencia/motivo/capacidad de corrección; invalida entregabilidad/aprobación correspondiente, conserva CPE/archivos anteriores |

VERIFIED técnico: el manual oficial de Consulta Integrada describe POST `validarcomprobante`, con RUC del consultante en ruta y del emisor en datos, tipo/serie/número/fecha/importe; success indica ejecución de consulta, no por sí solo aceptación del CPE. El código estadoCp 1 informa aceptado, 0 no informado y 2 anulado; otros valores/desconocidos requieren interpretación aplicable, no se convierten en éxito [S23](../decisions/sources.md). Guardar códigos/raw acotado y observaciones, sin inventar estado fiscal universal.

La verificación se vincula al conjunto exacto de inputs y fecha. Si cambian, resultado previo deja de acreditar esa identidad/vínculo. El servicio no demuestra por sí solo autenticidad de los bytes ni que la venta sea la correcta. Sin cuenta/capacidad habilitada, baseline manual: consulta oficial realizada externamente y evidencia referenciada por operador; UNAVAILABLE permanece visible si no hay verificación exigida. No simular navegador SOL ni enumeración/descarga masiva; capacidad automática de adquisición PENDING VALIDATION.

## Documents: bytes, versiones y relaciones

Documento/evidencia es raíz lógica por entidad, finalidad y hecho(s) compatibles; artifact es contenido concreto, versionado sin sobrescribir original. Puede haber varios PDF/XML asociados al mismo CPE, pero la selección de versiones entregables es explícita. No todo término requiere tabla; sí identidad/ownership/relaciones verificables en PostgreSQL y bytes privados en object storage.

| Procedencia | Alcance |
|---|---|
| ORIGINAL_EXTERNAL | Bytes adquiridos como original de fuente externa identificada; conserva procedencia/evidencia, no certifica autenticidad por declaración o hash |
| GENERATED_REPRESENTATION | PDF/XML u otra representación producida por CasPro, con fuentes/parámetros/versión; nunca reemplaza requisito de XML original |
| EXTERNAL_COPY | Copia, escaneo/captura o impresión aportada como representación externa; necesaria para no etiquetar una captura del operador como original del emisor |

Metadata: entidad/ID, tipo declarado/detectado, tamaño, hash/algoritmo, origen/actor/instante, clave/versión privada de objeto, versión lógica, relación al hecho, política/clase de retención y estado de disponibilidad. Parsing XML produce datos derivados con hash/parserversion, conserva bytes originales y deshabilita DTD/entidades externas/red/expansión no acotada. PDF no ejecuta scripts ni se entrega a visor arbitrario. Formatos/límites/analizador deben elegirse y validarse antes de habilitar upload; lo desconocido queda en cuarentena.

| FROM → TO | Comando / propiedad |
|---|---|
| Sin versión → STAGED/QUARANTINED | C31 crea intención/identidad; carga privada fuera de transacción; no es AVAILABLE por responder object storage |
| QUARANTINED → AVAILABLE / REJECTED | C32 comprueba bytes/hash/tipo/límites/seguridad y procedencia con resultado de análisis de esa versión |
| AVAILABLE → MISSING / QUARANTINED | C32 registra ausencia/integridad rota con motivo; invalida selección entregable, sin fabricar objeto sustituto |
| MISSING → AVAILABLE | C32 solo tras restaurar misma versión/hash y verificar; una representación nueva no satisface identidad antigua |

Object key/version de contenido disponible es inmutable bajo roles ordinarios; el resultado de análisis se liga a esos bytes. DB y objeto no son transacción única: carga huérfana se reconcilia, metadata sin blob no queda disponible. Plazos de retención HP5: no purga de original referenciado, aprobación/entrega o protección idempotente por caducar una URL. Previews temporales sí tienen limpieza acotada; no se convierten automáticamente en evidencia permanente.

C38 proporciona preview PDF privado o descarga: autorización vigente del documento/hecho y contexto antes de conceder proxy/URL breve; cache por versión/entidad con permisos actuales, nunca URL permanente como permiso. Una revocación impide nueva concesión; una URL ya emitida conserva su ventana técnica limitada, a definir antes de activación. Si se exige revocación inmediata, usar proxy reautorizado. No acceso público de clientes por URL de bucket; email entrega adjuntos, no habilita portal de clientes.

Informe: PREVIEW_TEMPORARY o PERSISTED_SNAPSHOT por C26. Snapshot generado registra tipo, parámetros relevantes, corte, versión de cálculo/contrato, actor, origen GENERATED_REPRESENTATION y hash; contenido/coste incompleto explícito. El render se hace fuera de transacción operacional larga con dataset consistente. Snapshots pertenecen a Documents, cálculo al dueño de datos.

## Intención, aprobación y modo de entrega

Modos y HOLD se aplican por entidad/finalidad documental. MANUAL crea solicitud explícita; AUTO_WITH_APPROVAL prepara y espera C35; AUTO permite ejecución sin aprobación individual únicamente con política completa aprobada; DISABLED impide todo nuevo dispatch, incluso manual/reenvío. AUTO_WITH_APPROVAL es el modo operativo inicial. Registrar política no la habilita sin capacidad/validaciones pertinentes.

La preparación automática tiene consumidor concreto: cambios relevantes del vínculo CPE, disponibilidad del artefacto o política solicitan reevaluación durable de entrega por CPE/finalidad, deduplicada por revisión. El coordinador de ese caso materializa los contratos de Sales/Documents y ejecuta C34 bajo mandato Documents; no añade Documents → Sales. Un dossier ya preparado se reevalúa con sus insumos seleccionados: no crea otro original ni reemplaza automáticamente contenido aprobado. Si falta insumo, conserva DRAFT/razones; completar requisitos habilita READY/aprobación pendiente según modo. C39 cambia selección explícitamente y también solicita reevaluación en modos automáticos. Una fuente sin cambio no encadena reevaluaciones infinitas.

Finalidad inicial: entrega de CPE de venta al cliente. Primera intención única para `(entidad, CPE, finalidad)`, protegida aun con claves distintas, cambios de destinatario/versiones o restauración. El dossier de Documents no se duplica para eludirla. Intención original cancelada/bloqueada permanece identificada; no borrar para recrear otra. Reenvío es intención nueva por C37 ligada al original y mismo CPE.

| Dimensión Documents | Valores / contrato |
|---|---|
| Preparación | DRAFT / READY / CANCELED; READY reúne insumos, no acredita envío |
| Aprobación | NOT_REQUIRED / PENDING / APPROVED / INVALIDATED; modo/política decide necesidad; C35 registra autor/instante/fingerprint |
| HOLD | Bloqueo de dossier/finalidad o intención con motivo/actor; efectivo si cualquiera está activo. Intención nueva hereda bloqueo del dossier, no lo elude |
| Ejecución/resultado | Derivado de autorizaciones, attempts y observaciones: NOT_SENT / IN_PROGRESS / PROVIDER_ACCEPTED / UNKNOWN / REJECTED_KNOWN y resultado de entrega abajo. No copiar enum job como otra máquina empresarial |

Entregabilidad exige CPE inequívocamente vinculado, verificación requerida por HP4 vigente para esos inputs, todos los artefactos requeridos AVAILABLE con procedencia admisible, destinatario válido/autorizado, finalidad/política completa y capacidades actuales. Ningún modo permite omitir esos requisitos. Para primera entrega, además no hay entrega previa conocida externa/interna ni otra original en curso/ambigua. Historia insuficiente bloquea automatismo hasta resolución explícita con evidencia; no se interpreta DB vacía como «nunca enviado» después de restore.

La aprobación fija: entidad/CPE y revisión relevante del vínculo/desglose, destinatario solicitado y efectivo (TO/CC/BCC), versiones/hashes de artifacts, remitente autorizado, asunto/cuerpo/contenido relevante, finalidad, modo/versión de política, configuración de entorno pertinente, actor/mandato y excepción de segregación si aplica. Fingerprint canónico de esos insumos; no copiar perfil Party entero. Cambio relevante invalida la aprobación aunque un booleano APPROVED antiguo siga almacenado como historia. Cambiar Party por sí solo no cambia el snapshot aprobado; aplicar una corrección relevante sí lo hace.

Antes de C07 se materializan adjuntos/render necesarios fuera de DB bajo autorización, verificando hash/tamaño/versión. En la fase corta final se releen mandato/permisos, vínculo, política, HOLD, disponibilidad y fingerprint; se confirma intento/dispatch antes de HTTP. No recuperar un documento mutable durante el envío y llamarlo aprobado. HOLD confirmado antes de autorización impide dispatch; después del punto de autorización puede haber llamada en vuelo que no se cancela mágicamente, queda evidencia de carrera y resultado a conciliar. El mismo límite aplica a revocación durante un efecto ya autorizado.

| Transición de decisión | Comando / guarda / fallo / corrección |
|---|---|
| Sin original → DRAFT y aprobación PENDING según modo | C34, unicidad CPE/finalidad; faltantes conservan DRAFT/razones, no envío |
| DRAFT → READY | C34/C39 reevalúan insumos; cambios después de aprobación producen INVALIDATED |
| PENDING/INVALIDATED → APPROVED | C35 contra fingerprint vigente; autor único exige excepción; no aprueba datos aún incompletos |
| READY + permiso/aprobación válida → solicitud de dispatch | C34/C35 según modo, trabajo durable; C07 reautoriza al ejecutar |
| HOLD ausente → activo / activo → liberado | C36 o bloqueo automático por ambigüedad; liberación explícita con capacidad/motivo, no por callback o cambio de modo |
| Original/reenviado conocido → nuevo reenvío DRAFT | C37, nuevo propósito de reenvío y clave; respeta HOLD, política/entorno/aprobación; CPE no cambia |

Una intención preparada que cambió antes de dispatch se puede volver a presentar: en MANUAL, C34 REQUEST_MANUAL_DISPATCH referencia esa intención y revisión con autorización de envío nueva; en AUTO_WITH_APPROVAL, C35 aprueba la revisión nueva; AUTO reevalúa el mandato de política. Se conserva la identidad empresarial original o de reenvío, sin otro original ni otro intento mientras exista uno en vuelo/UNKNOWN. C39 por sí solo nunca solicita dispatch.

## Resend: resultado e incertidumbre

Retry mantiene intención, clave, destinatario y contenido exactos; solo se habilita tras prueba de no ejecución o resolución reconciliada compatible. Timeout o proceso caído después de registrar dispatch → UNKNOWN/HOLD y consulta/revisión antes de repetir; no retry ciego dentro ni fuera de las 24 h del proveedor. Vencida esa ventana, la unicidad local sigue viva; si no puede determinarse el resultado, no fabricar otro original ni despejar HOLD por tiempo transcurrido.

ID externo conocido permite consultar proveedor; desconocido no habilita búsqueda por email+hora como prueba de identidad. Un callback temprano queda pendiente hasta asociación por resultado o evidencia inequívoca de proveedor, incluyendo correlación opaca de la intención cuando el contrato la soporte; no por coincidencia de asunto. Reenvío tras cambiar destinatario es nueva intención y aprobación, no retry con payload distinto. Fallo/bounce no invalida CPE ni venta.

Callbacks se autentican/deduplican en C02/C09; su fuente acredita al menos una vez y orden no garantizado [S24](../decisions/sources.md). Documents conserva conjunto de observaciones por external ID/attempt, no overwrites por último arribo. Derivación local inicial:

| Observaciones compatibles | Resultado presentado / consecuencia |
|---|---|
| API aceptó / sent, sin resultado de destino | PROVIDER_ACCEPTED / pendiente de entrega; no prueba lectura |
| delivery_delayed sin resultado definitivo | DELAYED; no reenviar como original nuevo |
| delivered | DELIVERY_REPORTED: servidor destinatario aceptó; no lectura ni aceptación fiscal [S27](../decisions/sources.md) |
| bounced o suppressed | NON_DELIVERY_REPORTED y pendiente de revisar destinatario/política; HOLD para nuevo envío a esa dirección |
| failed sin delivered contradictorio | FAILURE_REPORTED; revisar causa, no retry por webhook aislado |
| delivered y bounced/failed incompatibles para el mismo intento/destinatario | CONFLICT/HOLD, ambas evidencias conservadas y consulta autorizada; no elegir la fecha más reciente como verdad universal |
| sent/delayed tardío después de resultado más concluyente | Conservar observación sin degradar resultado; no nuevo job de envío |

opened/clicked no se usan como garantía de lectura humana ni tracking CRM. Eventos desconocidos se conservan acotados y requieren revisión de contrato si afectan resultado. Observaciones de otra conexión no se asocian aunque email_id coincida.

## Entorno y destinatario efectivo

LOCAL/CI: adaptador de captura local sin SDK/credenciales/transporte Resend real; incluso fixture con destinatario «de prueba» no sale a red. STAGING captura por defecto. Activación excepcional de envío STAGING requiere configuración completa y allowlist segura; todas las direcciones TO/CC/BCC se sustituyen antes de congelar/aprobar, y el adaptador vuelve a validar las efectivas. Una dirección no permitida, copia olvidada o entorno desconocido produce ENVIRONMENT_BLOCKED. Registrar solicitado vs efectivo y modo CAPTURE/SEND; un capture no es aceptación del proveedor ni evidencia de entrega real.

PRODUCTION usa destinatario empresarial permitido por política. Ningún modo/reenvío elude la guardia de entorno. Cambio de allowlist/remitente/configuración relevante invalida payload/aprobación pendientes y obliga a preparar nuevamente; jamás cambiar solo el transporte manteniendo aprobación del contenido anterior. La configuración de restore empieza con efectos desactivados. Gate EMAIL-ENV debe demostrar estas negativas antes de habilitar proveedor; no enviar email real en LOCAL/CI para probarlo.

## Fichas documentales (CM0)

<a id="c30"></a>
### C30 — Registrar identidad de CPE externo

- **OWNER / PURPOSE:** Sales; registrar expectativa/emisión observada o retractar identidad errónea, sin emitir CPE.
- **INPUT / READS:** venta/revisión si existe, caso externo identificado si procede, identidad externa, finalidad, fecha/moneda/importes/adquirente presentes, evidencia/contexto de emisión, acción y motivo; entidad emisora acreditada y candidatos/vínculos existentes. Sin venta/caso mantiene UNLINKED.
- **LOCKS / LOCK ORDER:** I → E si caso previo → S si venta → C; creación por identidad natural protegida en I y UNIQUE; misma identidad no crea otra raíz aunque cambie la venta propuesta. No bloquear filas inexistentes.
- **WRITES / PRE / POST:** expediente y emisión OBSERVED o vínculo RETRACTED con revisión; identidad/contexto explícitos; no declaración de validez por guardar datos. Corrección conserva anterior y bloquea entregabilidad/aprobación derivadas.
- **IDEMPOTENCY / RETRY / FAILURES:** D; CM0; CPE_IDENTITY_CONFLICT/ISSUER_MISMATCH/INSUFFICIENT_LINK_EVIDENCE. Identidad ya usada no se edita en sitio.
- **EVENTS / AUDIT:** ExternalCpeRecorded/CpeLinkRetracted, actor/evidencia/revisiones; no CpeIssuedByCasPro.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; emisión fuera del sistema. Rectificación referenciada y nueva revisión por capacidad sales.correct_cpe.

<a id="c31"></a>
### C31 — Adquirir artefacto privado

- **OWNER / PURPOSE:** Documents; adquirir original/copia o representación generada con procedencia explícita.
- **INPUT / READS:** contexto, raíz documental/finalidad, tipo/procedencia/origen, archivo y metadatos declarados, retención; permisos/relación empresarial y política de límites.
- **LOCKS / LOCK ORDER:** I → D → J para preparar metadata; soltar antes de cargar objetos. No FK/vínculo a recurso ajeno sin contrato de pertenencia validado.
- **WRITES / PRE / POST:** STAGED/QUARANTINED y trabajo de verificar esa versión; nunca AVAILABLE solo por upload. Original no sobrescrito; representación generada registra parámetros/versión fuente.
- **IDEMPOTENCY / RETRY / FAILURES:** D por adquisición, hash no fusiona autorización entre entidades; CM0; UNSAFE_TYPE/LIMIT_EXCEEDED/WRONG_OWNER/STORAGE_UNAVAILABLE.
- **EVENTS / AUDIT:** ArtifactAcquisitionStarted con actor/procedencia; disponibilidad posterior C32.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** bytes privados fuera de transacción; carga huérfana reconciliada. Nueva versión corrige, no reetiquetar reconstrucción XML como original.

<a id="c32"></a>
### C32 — Verificar disponibilidad/integridad de versión

- **OWNER / PURPOSE:** Documents; decidir si los bytes concretos pueden usarse, no su validez tributaria.
- **INPUT / READS:** versión/clave/hash esperados, resultado de análisis de contenido/seguridad y lectura de objeto; estado/procedencia/política actuales.
- **LOCKS / LOCK ORDER:** I → D → J en registro final; verificación de objeto fuera de DB, resultado ligado a clave/versión inmutable.
- **WRITES / PRE / POST:** AVAILABLE solo si coincidencia/seguridad y límites acreditados; REJECTED/MISSING/QUARANTINED por fallo; invalidación de entregabilidad de esa versión. No marcar disponible una versión nueva en lugar de original faltante.
- **IDEMPOTENCY / RETRY / FAILURES:** D o identidad versión+análisis; CM0; HASH_MISMATCH/OBJECT_MISSING/UNSAFE_CONTENT/STALE_ANALYSIS. Repetir análisis no duplica versiones.
- **EVENTS / AUDIT:** ArtifactAvailable/ArtifactUnavailable con evidencia técnica; auditoría de transición de disponibilidad.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** lectura/análisis/restore de objetos en fase separada; nueva verificación de mismos bytes puede recuperar disponibilidad; nueva representación conserva identidad distinta.

<a id="c33"></a>
### C33 — Vincular CPE y registrar/solicitar verificación

- **OWNER / PURPOSE:** coordinador Sales/Documents; Sales decide correspondencia y resultado CPE, Documents vincula artefactos compatibles.
- **INPUT / READS:** venta, conjunto de CPE/artefactos/revisiones afectados, asignaciones documentales/anticipos/notas, evidencia de correspondencia y resultado oficial manual o solicitud de consulta; emisor/adquirente/identidad/desglose y política HP4. Se descubren todos los documentos que limitan las asignaciones antes de bloquearlos.
- **LOCKS / LOCK ORDER:** I → S → C → D → J; plan completo de versiones antes de tomar locks.
- **WRITES / PRE / POST:** LINKED solo si correspondencia inequívoca, pertenencia y límites de asignación; revisión de conciliación documental con referencias exactas. Resultado de verificación ligado a inputs exactos o PENDING + job de lectura. Mismatch/ambigüedad conserva bloqueo y evidencia, nunca heurística monto/hora. Aplicaciones documentales y nuevas revisiones se confirman juntas; no cambio Treasury/GL.
- **IDEMPOTENCY / RETRY / FAILURES:** D; CM0; CPE_MISMATCH/CPE_AMBIGUOUS/POLICY_UNRESOLVED/CAPABILITY_UNVERIFIED; red caída queda UNAVAILABLE, no verificado. Retraer/corregir un vínculo exige además sales.correct_cpe.
- **EVENTS / AUDIT:** CpeLinked/CpeVerificationRecorded/Requested, fuente, actor y contenido de consulta referenciado; aprobación posterior consume revisión relevante.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno en transacción; consulta por C07/C08 posterior o evidencia manual. Retraer/corregir vínculo con historia; no modificar bytes para hacerlos coincidir.

<a id="c34"></a>
### C34 — Preparar original o solicitar dispatch manual

- **OWNER / PURPOSE:** Documents en coordinador con lecturas verificadas de Sales; PREPARE_ORIGINAL crea la única intención original; REQUEST_MANUAL_DISPATCH solicita envío de una intención original/reenvío ya preparada, sin crear otra.
- **INPUT / READS:** acción, entidad/CPE/finalidad o intención preparada/revisión, versiones seleccionadas, destinatario solicitado, contenido/remitente, modo/política y solicitud explícita de dispatch MANUAL si corresponde; vínculo, evidencia de entrega previa, permisos/configuración de entorno y HOLD del dossier.
- **LOCKS / LOCK ORDER:** I → S → C → D → N → J; C/D existentes serializan creación; UNIQUE de primera CPE/finalidad aunque claves de request difieran.
- **WRITES / PRE / POST:** intención DRAFT/READY y aprobación requerida; destinatario efectivo seguro resuelto, fingerprint de insumos; faltantes quedan pendientes, nunca dispatch. MANUAL crea trabajo únicamente con solicitud explícita y capacidad documents.send del solicitante; preparar por sí solo no lo envía. AUTO usa mandato vigente de política; AUTO_WITH_APPROVAL crea trabajo tras C35. C07 exige mandato documents.send en todos los modos.
- **IDEMPOTENCY / RETRY / FAILURES:** D por acción + unicidad natural de original y dispatch vigente de intención/revisión; CM0; ORIGINAL_ALREADY_EXISTS/PRIOR_DELIVERY_UNKNOWN/RECIPIENT_MISSING/ARTIFACT_REQUIRED/HOLD. Original existente no se recrea con otro dossier/recipient; solicitar dispatch no modifica payload ya despachado ni evita un resultado incierto.
- **EVENTS / AUDIT:** DocumentDeliveryPrepared, actor/propósito/huella y bloqueos; no EmailSent.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; render/obtención de bytes se prepara aparte; C39 corrige antes de dispatch, C37 es reenvío explícito.

<a id="c35"></a>
### C35 — Aprobar entrega preparada

- **OWNER / PURPOSE:** Documents; decisión humana sobre insumos concretos.
- **INPUT / READS:** intención/revisión/fingerprint y actor; insumos actuales, política/entorno, permisos, HOLD, excepción de segregación y entregabilidad.
- **LOCKS / LOCK ORDER:** I → S → C → D → N → J; mismo plan que posterior C07 para esas guardas.
- **WRITES / PRE / POST:** PENDING/INVALIDATED → APPROVED con fingerprint/autor/instante/excepción; mismos insumos vistos y completos, capacidad vigente; intención de enviar durable se registra en ese commit.
- **IDEMPOTENCY / RETRY / FAILURES:** D; CM0; APPROVAL_STALE/SEGREGATION_REQUIRED/NOT_DELIVERABLE/HOLD/ENVIRONMENT_BLOCKED. Nunca aprueba nueva revisión sin presentarla al operador.
- **EVENTS / AUDIT:** DocumentDeliveryApproved, versiones/destinatarios usados y excepción; no simular segundo aprobador.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; C36 HOLD o cambio relevante invalida autorización futura; C07 revalida, no confía en el checkbox.

<a id="c36"></a>
### C36 — Cambiar política o HOLD

- **OWNER / PURPOSE:** Documents; SET_MODE/SET_POLICY exige documents.manage_policy; PLACE_HOLD/CANCEL_UNSENT, documents.hold; RELEASE_HOLD, documents.release_hold. CANCEL_UNSENT es una decisión de bloqueo definitivo de esa intención aún no despachada, no borrado.
- **INPUT / READS:** dossier/finalidad/intención, revisión, modo/política o motivo/evidencia de resolución; estado, dispatch/resultado y permisos.
- **LOCKS / LOCK ORDER:** I → D (política y dossier ordenados) → N → J; no tocar venta/dinero desde un bloqueo documental.
- **WRITES / PRE / POST:** política versionada o HOLD persistido/liberado; liberar requiere causa resuelta y capacidad. CANCEL_UNSENT solo antes de dispatch y conserva identidad original. DISABLED/HOLD impiden futuro dispatch; no eliminan callback ni resultado en vuelo.
- **IDEMPOTENCY / RETRY / FAILURES:** V para modo/HOLD con revisión; D cancelación/resolución; CM0; OUTCOME_UNKNOWN/HOLD_CAUSE_UNRESOLVED/ALREADY_DISPATCHED.
- **EVENTS / AUDIT:** DocumentPolicyChanged/DeliveryHeld/HoldReleased/UnsentDeliveryCanceled, actor/motivo; cambio de modo no levanta HOLD ni revive aprobaciones invalidadas.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; nueva decisión explícita, sin promesa de retirar correo aceptado remotamente.

<a id="c37"></a>
### C37 — Solicitar reenvío explícito

- **OWNER / PURPOSE:** Documents; nueva intención ligada al original, no CPE nuevo.
- **INPUT / READS:** CPE/original, destinatario/contenido/artefactos elegidos, razón y clave nueva; resultado anterior conocido/reconciliado, política, permiso y HOLD efectivo.
- **LOCKS / LOCK ORDER:** I → S → C → D → N → J; original consultado bajo el mismo dossier y nueva intención por identidad única.
- **WRITES / PRE / POST:** intención RESEND nueva y aprobación según modo; CPE inalterado. UNKNOWN previo no se resuelve creando reenvío; insumos completos y hold liberado con evidencia. Dispatch MANUAL exige solicitud explícita y documents.send además de documents.resend; la creación y aprobación automática siguen las mismas guardas de C34/C35.
- **IDEMPOTENCY / RETRY / FAILURES:** D; CM0; ORIGINAL_OUTCOME_UNKNOWN/HOLD/RECIPIENT_INVALID/NOT_DELIVERABLE; doble click con misma clave devuelve mismo reenvío.
- **EVENTS / AUDIT:** DocumentResendRequested con razón/actor/original y destinatario efectivo; aprobación posterior cuando proceda.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; C07 futuro ejecuta; corrección antes de dispatch C39, luego otra intención explícita si procede.

<a id="c38"></a>
### C38 — Autorizar preview o descarga

- **OWNER / PURPOSE:** Documents; leer versión privada con permisos actuales.
- **INPUT / READS:** entidad/actor, documento/versión/finalidad; permisos del hecho vinculado, disponibilidad y política de acceso/URL.
- **LOCKS / LOCK ORDER:** D solo en fase corta si se emite concesión; lectura materializada bajo contexto, nunca lock durante streaming/render.
- **WRITES / PRE / POST:** concesión breve o respuesta de proxy y auditoría de acceso; sin permiso no revela existencia; bytes corresponden a versión autorizada. Preview generado temporal no crea snapshot permanente.
- **IDEMPOTENCY / RETRY / FAILURES:** R, sin clave empresarial; reautorizar cada solicitud; AUTH_DENIED/ARTIFACT_UNAVAILABLE/URL_EXPIRED, nunca fallback público.
- **EVENTS / AUDIT:** DocumentAccessed con actor/propósito, sin payload sensible en logs; no hecho económico.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** lectura privada fuera de DB; revocación/expiración según mecanismo validado; cache no evita reautorización.

<a id="c39"></a>
### C39 — Corregir insumos de intención no despachada

- **OWNER / PURPOSE:** Documents; preparar revisión visible y anular aprobación materialmente obsoleta.
- **INPUT / READS:** intención/revisión, campos permitidos de recipient/artifacts/contenido, motivo; vínculo/política/dossier/estado actual y configuración de entorno.
- **LOCKS / LOCK ORDER:** I → S → C → D → N → J si solicita reevaluación; C07 usa mismas raíces antes de registrar dispatch.
- **WRITES / PRE / POST:** nueva revisión/fingerprint con solicitado/efectivo; aprobación previa INVALIDATED; READY solo con entregabilidad. Ningún attempt despachado puede cambiar payload/clave en sitio.
- **IDEMPOTENCY / RETRY / FAILURES:** V; CM0; ALREADY_DISPATCHED/REVISION_CONFLICT/ARTIFACT_MISMATCH. Si C07 ganó la carrera, corregir requiere C37 tras resultado resuelto.
- **EVENTS / AUDIT:** DocumentDeliveryInputsChanged/ApprovalInvalidated, diferencias relevantes y autor.
- **EXTERNAL I/O / REVERSAL/CORRECTION:** ninguno; aprobar otra vez C35; recuperar un valor anterior sigue siendo nueva revisión, no restaura aprobación automáticamente.
