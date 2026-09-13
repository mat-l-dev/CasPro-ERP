# Propietarios y dependencias

Contrato arquitectónico de [ADR-001](../decisions/adr-001-modularity.md). La flecha A → B significa que A puede importar y llamar la API pública de B; no autoriza leer sus modelos.

## Mapa de módulos

| Módulo | Posee | Puede depender/llamar | Debe evitar |
|---|---|---|---|
| Workspace, agrupación provisional | Subáreas Identity, Organization y Access delimitadas abajo | Audit; infraestructura de autenticación | Módulos operativos; convertir el perfil empresarial en datos globales |
| Audit | Rastro técnico/empresarial mínimo de quién hizo qué | Primitivas compartidas | Cualquier llamada de negocio de retorno |
| Documents | Archivo privado, versiones, procedencia, disponibilidad, entrega documental y ciclo de trámite DataSubjectRequest según la frontera de privacidad abajo | Workspace, Audit; puertos de objetos/email conectados por composición | Decidir fundamento legal de solicitudes, estados legales del CPE, deuda o entrega física; importar Sales/Procurement o SDKs de proveedores en el dominio |
| Operations, capacidad técnica existente | Registro y ciclo operativo PrivacyIncidentCase; operación/recuperación según delivery, sin apropiarse de hechos de negocio | Workspace, Audit, Documents para evidencia; puertos de infraestructura por composición | Decidir finalidad/base jurídica, modificar hechos de otros dueños o convertir al coordinador superior en dueño de datos; no exige un paquete nuevo |
| Parties | Contrapartes por entidad, roles cliente/proveedor, identidad vigente | Workspace, Audit, Documents | Apropiar saldos o tratar persona igual a usuario |
| Catalog | Bienes/SKU, unidades, especificaciones y precios comerciales versionados | Workspace, Audit; Documents para referencias de evidencia del amendment profesional | Existencias y costes de stock |
| Marketing, pequeño dueño propuesto post-freeze | Organización y contenido comercial, aprobación de uso, campaña/marca/copy y planificación/observación de publicación según mapa siguiente | Workspace/Access, Audit, Catalog y Documents por APIs; transporte futuro por composición superior | Apropiar bytes/custodia, producto/precio/stock, autoridad jurídica o HTTP/SDK; crear Communications/Media con estado duplicado |
| Inventory | Almacenes/ubicaciones, movimientos, coste operativo, seriales, reservas y stock publicable | Catalog, Workspace, Audit, Documents | Importar Sales/Procurement, decidir si un cliente pagó o registrar VNR/deterioro contable |
| Procurement | Compromisos de compra, obligaciones y expediente CPE recibido de proveedor, con sus ajustes comerciales | Parties, Catalog, Workspace, Audit, Documents | Escribir existencias o dinero |
| Sales | Pedidos, progreso comercial, expediente CPE de venta y ajustes comerciales | Parties, Catalog, Workspace, Audit, Documents | Consultar/escribir Treasury o Inventory directamente |
| Treasury | Cuentas, movimientos, objetivos de liquidación, aplicaciones/reversiones y conciliación | Parties, Workspace, Audit, Documents | Leer modelos comerciales o generar asientos |
| Accounting | Plan aplicado, políticas contables versionadas, asientos y cierres futuros | Workspace, Audit, Documents; contrato de hechos económicos | Llamar/escribir módulos operativos |
| Tax | Perfiles, fuentes/reglas fiscales verificadas, conciliación y expedientes futuros | Accounting, Workspace, Audit, Documents; contrato de hechos | Alterar hechos operativos o emitir/presentar CPE a SUNAT en el alcance inicial |
| Corporate capability | Socios/tenencias, acuerdos, poderes, contratos, relaciones y financiamientos; frontera lógica separada | Organization/Parties/Documents/Audit por contratos; publica hechos a Treasury/Accounting/Tax | Crear ahora una app `legal`, mover dinero, asentar o concluir impuestos/control por una etiqueta |

Todas las APIs de negocio usan el [contrato de acceso](tenancy-access.md). Audit recibe metadatos explícitos y no consulta Workspace, evitando el ciclo autorización ↔ auditoría.

Workspace es una agrupación PROVISIONAL según ADR-001: compartir el alta administrativa puede favorecer contexto local, pero no demuestra un único dominio ni una única política de acceso. No exige tres aplicaciones Django ni habilita una fusión indiscriminada de datos.

| Subárea | Propiedad y límite |
|---|---|
| Identity | Usuarios y principales de sistema; autenticación, sesiones y recuperación mediante su infraestructura. No decide membresía empresarial |
| Organization | Identidad y ciclo administrativo de entidades/establecimientos. Directorio global mínimo para selección; perfil empresarial y establecimientos bajo acceso por entidad. No posee contrapartes, almacenes, dinero ni tratamientos fiscales |
| Access | Membresías, capacidades, concesiones por recurso, contexto autorizado y ciclo de DataRestriction. Combina identidad y organización; ejecuta restricciones de acceso, sin decidir fundamento legal ni redefinir las reglas del recurso operativo |

Access consulta los contratos internos de Identity y Organization; estas subáreas no llaman Access para decidir sus propias reglas de dominio. La autorización de una actuación administrativa se coordina en la entrada correspondiente. Una concesión sobre un almacén conserva su referencia; Inventory verifica su pertenencia y sus guardas. No se añade una dependencia Workspace → Inventory.

Antes de aceptar la agrupación deben especificarse alta, selección de entidad, revocación y administración de establecimientos, con visibilidad de cada dato y sin ciclos entre subáreas. Su comportamiento de acceso requerirá evidencia ejecutable posterior. Si la agrupación dificulta esos contratos, se revisa ADR-001; no se crean paquetes adicionales de forma preventiva.

Corporate tiene frontera lógica propia y consume Organization/Parties por contratos; no añade una consulta inversa desde Organization. Su empaquetado físico se concreta al entregar la WO M06 sin cambiar esa dirección. No se crea un duodécimo paquete ahora. El [contrato Corporate](../corporate/architecture.md) y M06 delimitan actos/financiación, con mutuo todavía no validado.

Configuration no es un módulo universal: secretos/settings pertenecen a config; precios a Catalog; perfiles tributarios a Tax; políticas comerciales a su propietario. No se crea un almacén global de claves arbitrarias ni un DSL. Los datos con vigencia tienen esquema y consumidor identificados.

La [enmienda de configuración](configuration-governance.md) añade Centro como proyección/router superior: consume descriptores/DTOs y llama comandos completos del dueño, que nunca depende del Centro. Access posee concesiones/mandatos y protocolo administrativo; cada dominio posee payload/revisión/guardas/activación de su política. El [registro TILMUX](../product/company-policy-register.md) solo indexa esas referencias. Impacto cruza propietarios mediante lecturas autorizadas/coordinadores; Audit recibe valores explícitos sin consultas de retorno. No nuevo módulo de verdad empresarial ni ciclo hacia Access desde guardas del recurso.

## Propiedad de hechos de privacidad

Este mapa posee la asignación canónica de los cinco registros del [ciclo de datos personales](../security/personal-data-lifecycle.md#contexto-y-dueños). Poseer significa persistir identidad, revisiones, estado/transiciones y resultado del registro mediante el contrato público del dueño; custodiar un artefacto, ejecutar un paso o coordinar participantes no transfiere esa propiedad. No hay módulo Privacy ni super-rol.

| Hecho persistente | Único dueño del registro y su ciclo | Autoridad y ejecución que no adquiere |
|---|---|---|
| PersonalDataPurpose | Dominio de finalidad identificado por owner/familia del ConfigurationDescriptor estático registrado; cada finalidad tiene un único dueño y referencia estable | Define necesidad/uso de su proceso con autoridad empresarial acreditada; no obtiene potestad legal ni datos de otros dominios |
| ProcessingContext | El mismo dominio dueño del PersonalDataPurpose referenciado; conserva revisiones y referencias de aprobación | La aprobación jurídica viene del responsable del tratamiento acreditado, con asesoramiento competente; Documents custodia la evidencia |
| DataRestriction | Access; conserva alcance, causa/decisión referenciada, vigencia, revisión y levantamiento | Ejecuta y hace exigible restricción de acceso; cada dueño aplica los pasos sobre sus propios datos/derivados. No decide supresión legal ni borra historia económica |
| DataSubjectRequest | Documents; posee el expediente y ciclo de atención, plazos, decisiones recibidas por referencia, pasos/constancias y cierre del trámite | Registrar una decisión aprobada no la emite jurídicamente. El responsable del tratamiento decide, el dominio evalúa sus hechos y cada dueño ejecuta el plan autorizado |
| PrivacyIncidentCase | Operations como capacidad técnica; posee el registro y ciclo operativo del incidente, evaluación documentada, decisiones recibidas por referencia y cierre operativo | Organiza contención/seguimiento y recuperación; el responsable del tratamiento decide la obligación de notificar. Documents custodia comunicaciones/evidencias, Access restringe y cada dominio corrige sus datos |

La coordinación transversal de atención, incidente o restore compone contratos por encima de los dueños; no posee ninguno de estos cinco registros ni un estado paralelo. Operations no se usa aquí como nombre de ese coordinador: su registro operativo se distingue de la composición de pasos. El progreso de solicitud queda en Documents, el de incidente en Operations y cada resultado de ejecución en su dueño. Restore conserva la barrera de privacidad y las aprobaciones operacionales ya especificadas, sin reasignar hechos al recuperar copias.

Documents recibe evaluaciones/decisiones y resultados como valores/referencias versionadas verificadas por la entrada/coordinación, sin llamadas de retorno a dominios/Operations; Access recibe la decisión referenciada sin consultar modelos del dominio. Operations consume evidencia por Documents; Documents no importa Operations. Corporate coordina la validación de facultades/asesoramiento por sus contratos existentes; ni esa coordinación ni R-CORPORATE sustituyen la autoridad real del responsable del tratamiento o le transfieren los cinco registros. Las decisiones legales recibidas se registran con autor, fundamento y evidencia en el expediente correspondiente, no se derivan de su custodio. Se conservan el grafo acíclico, la custodia Documents, las restricciones Access y los gates profesionales/de activación.

## Flujos que cruzan propietarios

<a id="marketing-content"></a>
### Marketing Content — ownership del nuevo amendment

**PENDING INDEPENDENT REVIEW**, posterior al alcance aceptado de PR #10. [Spec única](../specs/flows/marketing-content-media-library.md) posee ciclos/comandos. Se elige un pequeño dueño lógico Marketing con Documents y adaptadores por composición; no app Django ni plataforma Marketing materializada.

| Registro / ciclo persistente | Único dueño | Responsabilidad separada |
|---|---|---|
| MarketingFolder/árbol, MarketingTag/asignaciones y carpeta primaria del activo | Marketing | Access posee grants/restricciones; carpeta no concede permisos ni es ruta física |
| MarketingAsset / MarketingAssetRevision / UsageRightsRevision y aprobación/retiro/archivo | Marketing | Documents posee DocumentVersion, disponibilidad/hash/objeto/derivados y custodia; no aprobación de uso Marketing |
| MarketingCampaign y sus vínculos revisables; BrandKit / BrandKitRevision; MarketingCopy / CopyRevision | Marketing | Catalog conserva SKU/kit/especificaciones/precio; Documents evidencia y representaciones, sin copiar ciclo editorial |
| PublicationPlan / revisiones; PublicationRecord / correcciones y futura intención de publicación empresarial | Marketing | Integrations posee transporte/job/attempt/observación técnica; Documents solo custodia evidencia, no DeliveryIntent CPE duplicado |
| PersonalDataPurpose / ProcessingContext de familia estática MARKETING_CONTENT | Marketing | Mismos cinco dueños transversales de privacidad: Access DataRestriction; Documents DataSubjectRequest; Operations PrivacyIncidentCase |

Marketing es autoridad empresarial de finalidad/uso, **no autoridad jurídica por software**. Responsable del tratamiento/facultado y profesional competente validan fundamento/licencia/uso real; Corporate coordina acreditación cuando corresponda. Access ejecuta restricciones, cada dueño aplica sus pasos, Documents conserva evidencia y Operations coordina incidente/restore. El coordinador superior no posee estados paralelos. Referencias de custodia se registran mediante Documents en la misma TX del vínculo Marketing, sin consultas Documents→Marketing ni Catalog→Marketing; transporte se conecta por puertos/valores verificados. Este delta no reasigna ningún hecho previo.

### Coordinación económica y documental existente

Delta del [amendment B2B/financiación aceptado](../evidence/b2b-financing-amendment.md): Sales incorpora cotizaciones y OCs **del cliente** con significado comercial; Procurement conserva OCs **al proveedor**. [B2B](../specs/flows/b2b-commercial-dossier.md) usa los contratos existentes de stock/dinero. Para [pago por cuenta de empresa](../specs/flows/financing-events-statements.md), coordinador compone Corporate (pago externo/naturaleza/derecho), Procurement (obligación) y Treasury (liquidación por tercero sin caja propia y posterior reembolso). No añade dependencias inversas entre módulos. Corporate posee estado de financiación derivado; Documents snapshot y evidencia. [C40](../specs/flows/cpe-document-delivery.md#c40) registra historia externa sin adaptar el dominio a Resend.

| Coordinador | Participantes | Hecho coordinado |
|---|---|---|
| Recepción de compra | Procurement + Inventory | Recepción contra compromiso y progreso, en una transacción |
| Registro de obligación | Sales/Procurement + Treasury | Publicar objetivo de liquidación con referencia y versión comercial |
| Entrega | Sales + Treasury + Inventory | Elegibilidad comercial, dinero vigente si procede y salida física |
| Devolución de cliente / a proveedor | Sales o Procurement + Inventory + Treasury, según el caso | Dirección física y monetaria explícitas; retorno, ajuste comercial y refund son pasos relacionados, no equivalentes automáticos |
| Adquirir y vincular/verificar CPE externo | Sales o Procurement + Documents; Tax cuando se requiera interpretación fiscal | El dueño comercial conserva su expediente y vínculo verificado; Documents conserva artefactos y decide disponibilidad/entregabilidad documental, sin emitir ni determinar validez legal |
| Aceptar pedido de canal / reservar / publicar disponibilidad | Sales + Parties + Catalog + Inventory, según la actuación | Sales conserva pedido y referencia externa; Parties resuelve contraparte; Inventory aplica compromiso y calcula disponibilidad; publicación mediante adaptador externo |

Los coordinadores están por encima de los módulos. Ningún módulo los importa ni los llama. Tienen autoridad transaccional, no propiedad de datos. Los adaptadores externos tampoco los invocan como efecto oculto: una entrada autenticada entrega un mensaje traducido al caso de uso correspondiente.

Si una coordinación continúa después del commit, el progreso empresarial queda en su dueño y la entrega/reintento de tareas en registros técnicos durables con responsable explícito; [integraciones](integrations.md) define esa separación. Workflows no adquiere tablas de hechos ni un estado empresarial universal.

Documents sigue siendo el propietario existente del archivo y de las intenciones de entrega documental; no se crea Document Vault ni un módulo de mensajería. El coordinador proporciona referencias/revisiones verificadas del CPE y el destinatario autorizado mediante contratos de valores; Documents no consulta hacia Sales, Procurement o Parties. El flujo completo revalida esos insumos antes de despachar, sin invertir dependencias. Sales y el adaptador SUNAT no llaman a Resend. La bandeja de pendientes reúne lecturas de propietarios; no adquiere sus decisiones ni hechos.

El contrato distingue comandos completos y operaciones participantes de un workflow. Web, imports y workers solo invocan comandos completos; las operaciones participantes se publican exclusivamente para coordinadores identificados y exigen su frontera transaccional. No existe un segundo comando público que permita devolver dinero, cambiar un objetivo comercial o despachar omitiendo a los otros propietarios necesarios. Cada participante conserva la validación de pertenencia y sus guardas; la composición restringe llamadores y el plan común determina los locks. Esta disciplina dentro de un proceso requiere revisión/verificación posterior: una marca de contexto no constituye aislamiento frente a código malicioso.

Treasury conserva una proyección versionada del importe liquidable, no una segunda factura. Modificarla exige el flujo coordinado de su dueño comercial. Si no puede sincronizarse, la operación económica no confirma; nunca continúa usando un límite desactualizado. Sales concreta esa obligación en SP2 y Procurement en [M05](../specs/milestones/procurement-deep.md). Accounting consume ambos hechos mediante su [arquitectura propia](../accounting/architecture.md).

## Contratos y persistencia

- APIs públicas: valores tipados, IDs públicos, revisiones y errores de negocio estables. No QuerySets, managers ni modelos Django hacia consumidores.
- Read/command separados por función; una lectura no confirma negocio. Las lecturas sensibles pueden registrar acceso explícitamente.
- Las políticas puras no importan Django. No se fuerza a sacar del ORM una restricción que depende de PostgreSQL.
- Relaciones dentro del módulo: FKs normales. Entre módulos: solo identidad pública estable, contrato explícito y protección de pertenencia; puede haber FK a esa clave publicada si aporta integridad. No navegar relaciones privadas ni cascadas entre propietarios.
- La integridad referencial y el grafo de llamadas son vistas distintas. No declarar ausencia de acoplamiento porque no haya import directo.
- Las escrituras de stock/dinero solo entran por los casos de uso definidos. Los permisos de DB restringen operaciones destructivas sobre historia; los verificadores de código no son una frontera contra código malicioso en el mismo proceso.

La matriz anterior es acíclica: Audit → primitivas; Workspace → Audit; soporte → Workspace/Audit; operación → soporte; Accounting → soporte/hechos; Tax → Accounting/soporte. Los flujos superiores consumen estos contratos. Los eventos no crean llamadas de retorno.

## Ownership del amendment profesional propuesto

[Specs profesionales](../specs/index.md#amendment-profesional-propuesto) extienden los mismos dueños: Organization sede; Catalog perfiles/kits; Inventory almacén/tránsito/serial/costo; Sales cotización/contrato comercial/instalación/exposición/reclamación/paquete de sitio; Procurement necesidad/RFQ/adjudicación/importación y obligación de renta; Treasury instrumento/custodia de dinero; Accounting mapping cuenta financiera→GL y medición; Corporate facultades/tenencia/contrato de alquiler; Documents original/derivado/firma/custodia física; Tax obligación/FX fiscal/libros.

La referencia Catalog→Documents para evidencia técnica es extensión explícita acíclica; Documents no vuelve a Catalog. Políticas de aplicabilidad o facultades entre dueños se transfieren como valores/revisiones mediante coordinador superior, sin añadir Sales→Corporate/Tax, Organization→Corporate ni Treasury→Sales. La raíz H27 protege exposición en coordinadores que además aplican dinero. Buscar/drill-down agrega lecturas autorizadas, no crea módulo Graph ni una base de hechos compartida. Maker/checker es decisión acotada del dueño, no motor universal.
