# Originales, firmas, formularios, sitio cliente y reclamaciones

Propuesta del amendment; [review](../../review.md) controla fase. Documents posee bytes/metadatos/entrega, Sales el acto comercial/paquete cliente/reclamación, Corporate poderes/custodia legal aplicable. [Normativa](../../research/normative/operational-completeness.md) distingue ley, reglamento y requisito del cliente. No CompliancePlatform ni nuevo WorkflowEngine.

## Originales y derivados

DocumentVersion identifica entidad, clase/owner/public ID, revisión, procedencia (generado/recibido/scan firmado), hash/algoritmo, tamaño, MIME detectado, objeto privado/key/version, estado STAGED/QUARANTINED/AVAILABLE/REJECTED/MISSING, fechas/autor y retención/legal hold. PostgreSQL conserva metadatos, no adjuntos binarios/base64. Original subido o firmado es inmutable; OCR, thumbnail, PDF comprimido/redactado/preview son derivados con hash/tamaño propios, relación, propósito, generador/versión y parámetros. PDF generado puede optimizarse antes de sellar original; escaneo firmado recibido no se sustituye para ahorrar espacio.

Upload con límite de aplicación y bucket/plan, tamaño total/cuota por entidad, MIME/sniffing/extensión coherentes, antivirus/parser aislado con CPU/memoria/tiempo/páginas acotados, bloqueo de contenido activo/macros/zip bombs. STAGED/QUARANTINED nunca usable para aprobación/firma/descarga general. Persistencia de bytes fuera de TX seguida de finalización con hash/metadata y audit; fallo deja staging rastreable para reconciliación, no prueba empresarial AVAILABLE sin objeto.

Acceso requiere permiso al hecho/versión y audiencia, no UUID; descarga privada/proxy o URL breve ligada a propósito. URL ya entregada tiene ventana de exposición que B10/C10/C11 deben evaluar; no prometer revocación inmediata de bytes descargados. Preview seguro sin ejecución ni contenido externo; export restringido/redactado conserva relación, no se llama original. Dedupe dentro de entidad/clase/política puede compartir objeto immutable con referencias/retenciones independientes; no búsqueda por hash que revele otra entidad. Dedupe no fusiona dos documentos comerciales iguales.

Inventario de objetos↔metadata, huérfanos/quarantines con edad y causa, cuota/tamaño/crecimiento y alerta responsable. Purga requiere vencimiento por clase, ausencia de hold/referencias activas y aprobación; no TTL genérico del storage que borre evidencia. Backup DB y objetos se versionan/coordinan por manifiesto/corte, claves aparte, verificación de hash/faltantes y restore aislado con efectos externos desactivados. B13/C10 exigen ensayo posterior; backup de Supabase DB no acredita objetos.

PhysicalCustody por versión/material: original/copia, sede/archivo/armario/caja/carpeta/folio, custodio y estado IN_CUSTODY/ON_LOAN/MISSING/TRANSFERRED/DISPOSED, ingreso/préstamo/prestatario/autorización/vencimiento/devolución/transferencia y evidencia. Localizador privado; perder original no borra scan ni afirmar equivalencia jurídica. Disposición física y digital tienen políticas/evidencia independientes y legal hold.

## Firma y aceptación

SignatureEnvelope para versión/hash exactos, propósito/acto dueño, firmantes/identidad/rol/facultades snapshot, orden si necesario y provider-neutral reference. Tres métodos: **WET_SIGNATURE_SCAN**, **ELECTRONIC_ACCEPTANCE**, **DIGITAL_SIGNATURE_IOFE**. PNG/sello visual no prueba criptográfica; consentimiento no IOFE puede tener valor probatorio según acto/ley, no se presenta automáticamente como IOFE.

Por firma digital guardar bytes firmados originales, hash de entrada/salida, proveedor/ID, certificado emisor/serie/sujeto/validez/cadena, algoritmo, fecha declarada de firma, timestamp confiable si existe, verificación a fecha, CRL/OCSP/evidencia y resultado VALID/INVALID/REVOKED/UNKNOWN con motivo. Certificado expirado hoy no invalida automáticamente una firma pasada con tiempo/evidencia suficientes; sin tiempo fiable no inventar validez histórica. Validez técnica≠poder del firmante≠aceptación comercial.

Estados PREPARED→REQUESTED→PARTIALLY_SIGNED→SIGNED→VERIFIED; DECLINED/EXPIRED/CANCELLED/UNCERTAIN separados. Envío/callback aplican intención durable/epoch/B12; timeout consulta por ID antes de reenviar. Callback antiguo se registra sin reactivar versión sustituida. Cambiar contenido invalida envelope pendiente y requiere otra aceptación; versión firmada permanece. No elegir proveedor real ni enviar documento en esta misión.

## Formularios y paquete del sitio

TemplateRevision Documents: clase/owner, idioma, campos permitidos/obligatorios, numeración por entidad/serie, versión efectiva/aprobador, audiencia y texto aprobado. RenderManifest congela fuente/revisiones/valores/template/formato/hash, actor y fecha. Reimpresión conserva número/revisión y se distingue de reemisión; corrección nueva versión no borra firmado. Formularios: packing list, hoja despacho, constancia entrega/POD, aceptación, instalación, commissioning, demostración, transferencia, conteo y visita. Son evidencia comercial/control interno salvo tipo legal explícito; no se denominan CPE/GRE. Documents recibe valores del coordinador y no consulta modelos Sales/Inventory.

ClientSiteProfile Sales por entidad/Party cliente/sitio-unidad y actividad (visita, demo, entrega, instalación; soporte futuro por trigger). RequirementProfileRevision contiene autoridad LAW/REGULATION/MINE_POLICY/VENDOR_QUALIFICATION/INTERNAL, fuente/cláusula/template, effective dates, applicability expression acotada (actividad/persona/equipo/vehículo/tarea), required/optional y quién decide; no DSL jurídica. Una exigencia particular no se convierte en campo obligatorio global.

RequirementInstance: perfil, sujeto específico (empresa/persona/equipo/vehículo/tarea), sitio/visita, requerido/no aplicable con razón, responsable, DocumentVersion, fecha/expiración, estado MISSING/PREPARED/SUBMITTED/ACCEPTED/REJECTED/EXPIRED/WAIVED, evidencia de envío/respuesta/aceptación y excepción con autoridad/validez. Waiver del cliente no deroga ley. Se admiten formularios propios del cliente junto al normativo, conservando campos y revisión.

Pack SITE_VISIT/DEMONSTRATION/INSTALLATION selecciona personas/equipos/vehículos/tareas/fechas y requisitos aplicables; export/print snapshot y manifiesto, excluye datos personales innecesarios. Salud: aptitud/limitaciones de acceso pertinentes, no diagnóstico por defecto; acceso especial, no search global ni PDF comercial. Documentos de otra persona/modelo/serie no satisfacen requisito aunque nombre coincida.

ReadyForSubmission requiere evidencia disponible, versiones/personas/modelos correctos y revisión interna; ReadyForVisit requiere aceptación externa cuando exigible y vigencias que cubran fecha/turno. Cambio de fecha, persona, equipo, tarea o norma/perfil vuelve a evaluar. Vencimiento antes de visita revoca readiness aunque paquete ya se imprimió; muestra hoja de faltantes/caducados. PETAR solo para supuesto de alto riesgo; exige permiso real del responsable del sitio por turno. CasPro nunca transforma su READY en autorización de trabajo; supervisor externo puede denegar entrada.

## Libro de Reclamaciones

Sales posee ClaimCase: entidad/establecimiento/canal/libro/serie y Hoja única, consumidor/contacto/canal autorizado y representante cuando corresponda, fecha/hora/zona recepción, bien/servicio objeto (incluida instalación), pedido/venta/producto opcionales, importe, relato/pedido, reclamo vs queja, adjuntos, responsable y base legal/calendario efectivos. Falta de orden CasPro no impide recepción. Intake físico/virtual produce copia/conserva hoja y procedencia; duplicado de sincronización liga caso, no borra reclamo legítimo repetido.

RECEIVED→ASSIGNED→UNDER_REVIEW→RESPONSE_APPROVED→RESPONDED→CLOSED, con resolución/seguimiento; plazo y entrega son dimensiones independientes. Deadline15 días hábiles calculado con calendario legal versionado/fecha de recepción, sin prórroga silenciosa; alertas internas antes de vencer y OVERDUE persistente si se venció. Profesional C06 valida regla/canal/adecuación2026; no usar proyecto reglamentario como norma. Respuesta aprobada sin prueba de entrega no marca RESPONDED; intento fallido conserva fecha/reintento autorizado y vencimiento original. Cerrar tarde no borra incumplimiento.

Acceso ecommerce puede exponerse en Jumpseller mediante integración separada C11/B12, con entrega durable de intake/copia y fallback accesible; no depende de tener login ERP ni habilita portal general. CasPro prepara y registra respuestas solo por mandato de envío real; no se envían en esta misión. Reclamo no abre automáticamente garantía/RMA ni refund; solución económica entra por comandos de Sales/Treasury/Inventory existentes y queda ligada al caso.

## Comandos y control de corrección

| ID / capacidad | Precondiciones y efecto | Fallo/corrección |
|---|---|---|
| DR1 finalizar original / documents.ingest | Hash/tamaño/inspección/cuota, versión/owner autorizados; finalize metadata+audit CM0 | Objeto faltante/hostil queda quarantined/missing; nunca AVAILABLE ficticio |
| DR2 derivar/render / documents.render | Snapshot/plantilla aprobados, límite/capacidad y manifest | Nuevo objeto/hash relacionado; firma original intacta; derivado fallido no sustituye |
| DR3 prestar/verificar original / documents.custody.manage | Custodio/ubicación/versión y actor, lock registro custodia | Movimiento/prueba; MISSING inicia búsqueda/responsable, sin «encontrado» automático |
| DR4 solicitar/verificar firma / documents.sign.prepare/verify | Hash/firmantes/facultades/public contract y política del acto, intención/epoch | Resultado técnico separado y callback idempotente; UNKNOWN bloquea uso que exige VALID |
| SP1 preparar/validar pack / sales.site.prepare/approve | Perfil/visita/sujetos/documentos exactos, revisión/fechas/autoridades | Snapshot/faltantes; cambio de entrada invalida readiness; no crea permiso minero |
| LR1 registrar/responder / sales.claims.intake/respond | Número dedupe por origen, datos mínimos y deadline; aprobación/responsable/entrega autorizada | Caso/copia/audit/intención durable; fallo envío deja pendiente; corrección append-only |

Los permisos/locks por raíz y finalización idempotente usan CM0; operaciones costosas/externas fuera de TX. B02/B09/B10/B12/B13 cubren fuga/hostilidad/replay/restauración; C06/C10/C11/C13 antes del acto real. Este diseño no acredita firma válida, ingreso minero, cumplimiento de plazo ni restore ejecutado.
