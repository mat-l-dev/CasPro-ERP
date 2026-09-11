# Propietarios y dependencias

Contrato arquitectónico de [ADR-001](../decisions/adr-001-modularity.md). La flecha A → B significa que A puede importar y llamar la API pública de B; no autoriza leer sus modelos.

## Mapa de módulos

| Módulo | Posee | Puede depender/llamar | Debe evitar |
|---|---|---|---|
| Workspace, agrupación provisional | Subáreas Identity, Organization y Access delimitadas abajo | Audit; infraestructura de autenticación | Módulos operativos; convertir el perfil empresarial en datos globales |
| Audit | Rastro técnico/empresarial mínimo de quién hizo qué | Primitivas compartidas | Cualquier llamada de negocio de retorno |
| Documents | Archivo privado, versiones, procedencia, disponibilidad y entrega documental | Workspace, Audit; puertos de objetos/email conectados por composición | Decidir estados legales del CPE, deuda o entrega física; importar Sales/Procurement o SDKs de proveedores en el dominio |
| Parties | Contrapartes por entidad, roles cliente/proveedor, identidad vigente | Workspace, Audit, Documents | Apropiar saldos o tratar persona igual a usuario |
| Catalog | Bienes/SKU, unidades, especificaciones y precios comerciales versionados | Workspace, Audit | Existencias y costes de stock |
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
| Access | Membresías, capacidades, concesiones por recurso y contexto autorizado. Combina identidad y organización; no redefine las reglas del recurso operativo |

Access consulta los contratos internos de Identity y Organization; estas subáreas no llaman Access para decidir sus propias reglas de dominio. La autorización de una actuación administrativa se coordina en la entrada correspondiente. Una concesión sobre un almacén conserva su referencia; Inventory verifica su pertenencia y sus guardas. No se añade una dependencia Workspace → Inventory.

Antes de aceptar la agrupación deben especificarse alta, selección de entidad, revocación y administración de establecimientos, con visibilidad de cada dato y sin ciclos entre subáreas. Su comportamiento de acceso requerirá evidencia ejecutable posterior. Si la agrupación dificulta esos contratos, se revisa ADR-001; no se crean paquetes adicionales de forma preventiva.

Corporate tiene frontera lógica propia y consume Organization/Parties por contratos; no añade una consulta inversa desde Organization. Su empaquetado físico se concreta al entregar la WO M06 sin cambiar esa dirección. No se crea un duodécimo paquete ahora. El [contrato Corporate](../corporate/architecture.md) y M06 delimitan actos/financiación, con mutuo todavía no validado.

Configuration no es un módulo universal: secretos/settings pertenecen a config; precios a Catalog; perfiles tributarios a Tax; políticas comerciales a su propietario. No se crea un almacén global de claves arbitrarias ni un DSL. Los datos con vigencia tienen esquema y consumidor identificados.

## Flujos que cruzan propietarios

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
