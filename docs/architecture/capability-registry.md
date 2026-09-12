# Registro exacto de capabilities

Dueño: Access para identidad y elegibilidad; cada dominio conserva semántica, aprobación y comando. Complementa [roles y delegación](roles-delegation.md), [configuración](configuration-governance.md) y [CM0](../specs/cross-cutting/command-matrix.md). Corrección F01/F02 propuesta, pendiente de revisión independiente; ningún grant real ni implementación.

## Resolución y alcance

Cada fila registra un ID literal. El permiso efectivo requiere ID registrado, RoleAssignment vigente o principal técnico expresamente mandatado, scope de ese mismo ID, entidad/contexto válidos, revisión/epoch actual, todas las conjunciones y guardas del comando. Concesiones del mismo ID pueden unir recursos autorizados; nunca se combina scope de una acción con capability de otra. La intersección entre permisos participantes limita el comando completo. ID desconocido, wildcard, alias retirado o scope vacío deniega. Un nuevo ID o ampliación de RoleTemplate requiere diff, aprobación y nueva concesión explícita; una revisión restrictiva contrae inmediatamente grants efectivos y descendientes conforme A5. No expansión automática, ni combinación de roles que borre SoD.

OPERATIVOS significa únicamente las plantillas R-MASTER, R-SALES, R-SALES-APPROVE, R-CREDIT, R-REQUEST, R-BUYER, R-PURCHASE-APPROVE, R-WAREHOUSE, R-INVENTORY-CONTROL, R-TREASURY, R-TREASURY-APPROVE, R-ACCOUNTING, R-ACCOUNTING-CONTROL, R-TAX, R-RECORDS, R-CORPORATE y R-SITE, siempre dentro de sus objetos. Elegible no significa concedido. R-PLATFORM no obtiene negocio por administrar infraestructura. El texto negativo «sin access.manage» o «no GL sin accounting.post» nunca añade elegibilidad a ese rol.

Las fichas referenciadas son consumidores del permiso de comando; las duties de preparación/aprobación descritas aquí tienen consumidor explícito en la fase indicada. Una aprobación es evidencia de actor, capability, scope, objeto, monto/destino, revisión y vigencia, no un booleano intercambiable. El ejecutor conserva la capability final; si es el mismo actor debe reunir ambas y SoD. Cuando separe maker/checker, el checker aporta la duty, el ejecutor la acción final; no exige convertir al maker en checker. Las tablas de responsabilidades especializan las fichas, no crean rutas participantes alternativas. Tax: TX5 usa tax.external.record; X05 conserva tax.record_filing y X08 tax.reconcile, con sus propios contratos y estados; no presentan ni pagan por esa responsabilidad.

## Principales técnicos cerrados

| Principal documental | IDs elegibles | Límite que debe probarse antes de conceder |
|---|---|---|
| T-INBOUND | integration.receive | Solo conexión/entidad y C02 autenticado; ningún comando económico |
| T-INTEGRATION | integration.process | C04/C09, intención ya autorizada y revalidada; no checker, post ni dinero |
| T-RECONCILE | integration.reconcile | C03/C05 por conexión y mandato de publicación; DTO mínimo de disponibilidad autorizado por Inventory, sin lectura humana del almacén |
| T-SHADOW | shadow.interpret, shadow.post, shadow.correct | Solo cápsula/run y ledger experimental; ningún ID oficial ni rol humano |
| T-CONFIG | configuration.activate | Solo CG4 sobre aprobación/digest/familia/vigencia, nunca preparar/aprobar ni cambiar política fuera del mandato |
| T-RULE | accounting.post | Excepción explícita RULE_AUTO_EXECUTE OFF: mandato de regla determinística/revisión/fuentes y aprobación A03; distinto del modelo, proveedor y shadow |

Ningún otro ID de este registro es concedible a principal técnico por analogía. Los workers de render/export/comparación ejecutan la intención acotada del humano y revalidan sus permisos/audiencia al consumir y entregar; no reciben un rol humano ni permiso de lectura general propio. La copia de cápsula ocurre por el puerto de lectura autorizado antes de entregarla al executor aislado. Mandato técnico no es «permiso equivalente» que permita omitir el ID exacto registrado. Nuevos servicios requieren registrar consumidor y techo antes de su entrega.

## Catálogo activo

Scope es un techo tipado, nunca ENTITY_ALL por defecto. Las lecturas conservan restricciones por finalidad; export, descarga y relectura tras restore revalidan. Las capacidades policy/configuration exigen permiso del dueño AND delegación administrativa de familia, ImpactManifest/revisión y SoD según CG1–5. El consumidor enlazado conserva todos los demás requisitos. Para privacy, únicamente las personas nombradas bajo [ciclo de datos](../security/personal-data-lifecycle.md) son elegibles, sin agregar roles nuevos.

| ID exacto | Elegibilidad humana o técnica | Scope mínimo | Consumidor / significado y conjunción |
|---|---|---|---|
| access.admin.delegate | R-ACCESS | Entidad/instalación, asignación/ancestros; A5 | Contrato local del dueño para admin / delegate. [Consumidor](roles-delegation.md) |
| access.manage | R-ACCESS | Entidad/instalación, asignación/ancestros; A5 | Contrato local del dueño para manage. [Consumidor](../specs/flows/first-operational-circuit.md) |
| access.policy.approve | R-ACCESS | Entidad/instalación, asignación/ancestros; A5 | Contrato local del dueño para policy / approve. [Consumidor](roles-delegation.md) |
| access.policy.prepare | R-ACCESS | Entidad/instalación, asignación/ancestros; A5 | Contrato local del dueño para policy / prepare. [Consumidor](roles-delegation.md) |
| access.role.approve | R-ACCESS | Entidad/instalación, asignación/ancestros; A5 | Contrato local del dueño para role / approve. [Consumidor](roles-delegation.md) |
| access.role.prepare | R-ACCESS | Entidad/instalación, asignación/ancestros; A5 | Contrato local del dueño para role / prepare. [Consumidor](roles-delegation.md) |
| access.sessions.revoke | R-ACCESS | Entidad/instalación, asignación/ancestros; A5 | Contrato local del dueño para sessions / revoke. [Consumidor](roles-delegation.md) |
| access.view | R-ACCESS, R-AUDIT | Entidad/instalación, asignación/ancestros; A5 | Consultar concesiones/roles de entidad autorizada; no credenciales. [Consumidor](roles-delegation.md) |
| accounting.adjust | R-ACCOUNTING-CONTROL | Entidad/libro/período/propuesta | Contrato local del dueño para adjust. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.ai.accept_draft | R-ACCOUNTING | Entidad/libro/período/propuesta | Aceptar candidato a A02 Draft; AND accounting.prepare; no post. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.ai.request | R-ACCOUNTING | Entidad/libro/período/propuesta | Solicitar candidato minimizado; AND accounting.view/fuentes, propósito y budget. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.approve_reports | R-ACCOUNTING-CONTROL | Entidad/libro/período/propuesta | Contrato local del dueño para approve_reports. [Consumidor](../specs/acceptance/reporting-goldens.md) |
| accounting.close | R-ACCOUNTING-CONTROL | Entidad/libro/período/propuesta | Contrato local del dueño para close. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.close.approve | R-ACCOUNTING-CONTROL | Entidad/libro/período/propuesta | Autorizar corte/checklist A07; cierre además accounting.close. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.close.prepare | R-ACCOUNTING | Entidad/libro/período/propuesta | Preparar checklist/manifiesto A07; no bloquear período. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.configure | R-ACCOUNTING-CONTROL | Entidad/libro/período/propuesta | Contrato local del dueño para configure. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.export | R-ACCOUNTING-CONTROL | Entidad/libro/período/propuesta | Exportar informe autorizado R1/R2; AND accounting.report o accounting.view según dataset. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.journal.approve | R-ACCOUNTING-CONTROL | Entidad/libro/período/propuesta | Autorizar propuesta/revisión A03 humana o mandato determinístico acotado con policy/delegación según A03; ejecutor además accounting.post. T-RULE no recibe esta duty. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.measure | R-ACCOUNTING | Entidad/libro/período/propuesta | Contrato local del dueño para measure. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.policy.approve | R-ACCOUNTING-CONTROL | Entidad/libro/período/propuesta | Contrato local del dueño para policy / approve. [Consumidor](../specs/flows/financial-accounts-instruments.md) |
| accounting.policy.prepare | R-ACCOUNTING | Entidad/libro/período/propuesta | Contrato local del dueño para policy / prepare. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.post | R-ACCOUNTING-CONTROL; T-RULE solo mandato determinístico | Entidad/libro/período/propuesta | Contrato local del dueño para post. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.prepare | R-ACCOUNTING | Entidad/libro/período/propuesta | Contrato local del dueño para prepare. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.reconcile | R-ACCOUNTING | Entidad/libro/período/propuesta | Conciliar auxiliares/GL antes de A07; lectura/observaciones, no ajuste automático. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.reopen | R-ACCOUNTING-CONTROL | Entidad/libro/período/propuesta | Contrato local del dueño para reopen. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.report | R-ACCOUNTING | Entidad/libro/período/propuesta | Contrato local del dueño para report. [Consumidor](../specs/acceptance/reporting-goldens.md) |
| accounting.reverse | R-ACCOUNTING-CONTROL | Entidad/libro/período/propuesta | Contrato local del dueño para reverse. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.shadow.review | R-ACCOUNTING-CONTROL | Entidad/libro/período/propuesta | Revisar diferencias/labels; AND accounting.shadow.view; no firma oficial. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.shadow.run | R-ACCOUNTING | Entidad/libro/período/propuesta | Encargar run; AND accounting.shadow.view y fuentes; no poder técnico shadow. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.shadow.view | R-ACCOUNTING, R-ACCOUNTING-CONTROL, R-AUDIT | Entidad/libro/período/propuesta | Consultar comparación sellada; AND accounting.view y fuentes. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.template.use | R-ACCOUNTING | Entidad/libro/período/propuesta | Aplicar plantilla aprobada a propuesta; AND accounting.prepare. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.transition | R-ACCOUNTING-CONTROL | Entidad/libro/período/propuesta | Contrato local del dueño para transition. [Consumidor](../specs/milestones/accounting-deep.md) |
| accounting.view | R-ACCOUNTING, R-ACCOUNTING-CONTROL, R-AUDIT | Entidad/libro/período/propuesta | Contrato local del dueño para view. [Consumidor](../specs/milestones/accounting-deep.md) |
| audit.export | R-AUDIT | Entidad/dominio/período del encargo | Contrato local del dueño para export. [Consumidor](../architecture/transactions.md) |
| audit.view | R-AUDIT | Entidad/dominio/período del encargo | Contrato local del dueño para view. [Consumidor](../architecture/transactions.md) |
| automation.simulate | R-ACCOUNTING | Entidad/familia/run | Simulación Accounting; AND accounting.policy.prepare y lectura de inputs; sin efectos. [Consumidor](automation.md) |
| automation.view | OPERATIVOS, R-AUDIT; R-CONFIG/R-PLATFORM solo metadata | Entidad/familia/run | Consultar runs de familia; AND lectura de fuentes para contenido. [Consumidor](automation.md) |
| case_flow.export | R-RECORDS, R-AUDIT; OPERATIVOS por concesión de caso | Entidad/caso/objetos visibles | Exportar dossier; AND case_flow.view y export de cada sección. [Consumidor](../specs/cross-cutting/case-flow-preview.md) |
| case_flow.view | OPERATIVOS, R-AUDIT | Entidad/caso/objetos visibles | Consulta DTO filtrado; AND lectura de cada dueño antes de layout. [Consumidor](../specs/cross-cutting/case-flow-preview.md) |
| catalog.manage | R-MASTER | Entidad/catálogo/SKU/precio | Contrato local del dueño para manage. [Consumidor](../specs/flows/catalog-sites-warehouses.md) |
| catalog.map | R-MASTER | Entidad/catálogo/SKU/precio | Contrato local del dueño para map. [Consumidor](../specs/flows/first-operational-circuit.md) |
| catalog.policy.approve | R-SALES-APPROVE | Entidad/catálogo/SKU/precio | Contrato local del dueño para policy / approve. [Consumidor](../specs/flows/catalog-sites-warehouses.md) |
| catalog.policy.prepare | R-MASTER | Entidad/catálogo/SKU/precio | Contrato local del dueño para policy / prepare. [Consumidor](../specs/flows/catalog-sites-warehouses.md) |
| catalog.price.approve | R-SALES-APPROVE | Entidad/catálogo/SKU/precio | Autorizar revisión de precio para Catalog; AND configuración delegada y manifest; no aprobar venta. [Consumidor](../specs/flows/catalog-sites-warehouses.md) |
| catalog.price.prepare | R-MASTER | Entidad/catálogo/SKU/precio | Preparar revisión de precio comercial; no aprobarla ni cambiar venta comprometida. [Consumidor](../specs/flows/catalog-sites-warehouses.md) |
| configuration.activate | R-CONFIG; T-CONFIG solo mandato CG4 | Entidad + familia + recurso/revisión | Contrato local del dueño para activate. [Consumidor](configuration-governance.md) |
| configuration.approve | R-CONFIG | Entidad + familia + recurso/revisión | Contrato local del dueño para approve. [Consumidor](configuration-governance.md) |
| configuration.delegate | R-CONFIG | Entidad + familia + recurso/revisión | Conceder/revocar ConfigDelegation mediante RA2/RA3, AND access.admin.delegate o access.manage según acción y techo administrativo de familia. CG5 cancela/sustituye política, no emite delegaciones. [Consumidor](configuration-governance.md) |
| configuration.governance.approve | R-CONFIG | Entidad + familia + recurso/revisión | Contrato local del dueño para governance / approve. [Consumidor](configuration-governance.md) |
| configuration.governance.prepare | R-CONFIG | Entidad + familia + recurso/revisión | Contrato local del dueño para governance / prepare. [Consumidor](configuration-governance.md) |
| configuration.prepare | R-CONFIG | Entidad + familia + recurso/revisión | Contrato local del dueño para prepare. [Consumidor](configuration-governance.md) |
| configuration.view | R-CONFIG, R-AUDIT | Entidad + familia + recurso/revisión | Contrato local del dueño para view. [Consumidor](configuration-governance.md) |
| corporate.approve_financing | R-CORPORATE | Entidad/relación/expediente | Contrato local del dueño para approve_financing. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| corporate.finance.document | R-CORPORATE | Entidad/relación/expediente | Contrato local del dueño para finance / document. [Consumidor](../specs/flows/financial-accounts-instruments.md) |
| corporate.policy.approve | R-CORPORATE | Entidad/relación/expediente | Contrato local del dueño para policy / approve. [Consumidor](../specs/flows/financing-events-statements.md) |
| corporate.policy.prepare | R-CORPORATE | Entidad/relación/expediente | Contrato local del dueño para policy / prepare. [Consumidor](../specs/flows/financing-events-statements.md) |
| corporate.prepare_beneficial_owner | R-CORPORATE | Entidad/relación/expediente | Contrato local del dueño para prepare_beneficial_owner. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| corporate.record | R-CORPORATE | Entidad/relación/expediente | Contrato local del dueño para record. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| corporate.record_capitalization | R-CORPORATE | Entidad/relación/expediente | Contrato local del dueño para record_capitalization. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| corporate.records.approve | R-CORPORATE | Entidad/relación/expediente | Autorizar revisión de acto/estado; confirmar mediante corporate.record con facultades/SoD. [Consumidor](../specs/flows/financing-events-statements.md) |
| corporate.records.prepare | R-CORPORATE | Entidad/relación/expediente | Preparar acto/estado de financiación; no confirmar acto ni dinero. [Consumidor](../specs/flows/financing-events-statements.md) |
| corporate.view | R-CORPORATE | Entidad/relación/expediente | Contrato local del dueño para view. [Consumidor](../specs/flows/financing-events-statements.md) |
| documents.approve_delivery | R-RECORDS | Entidad/clase/objeto/revisión/audiencia | Contrato local del dueño para approve_delivery. [Consumidor](../specs/flows/first-operational-circuit.md) |
| documents.custody.manage | R-RECORDS | Entidad/clase/objeto/revisión/audiencia | Contrato local del dueño para custody / manage. [Consumidor](../specs/flows/records-signatures-site-packs.md) |
| documents.download | R-RECORDS; OPERATIVOS, R-AUDIT por mandato documental | Entidad/clase/objeto/revisión/audiencia | Descargar versión; AND documents.view, audiencia y restricción. [Consumidor](../specs/cross-cutting/case-flow-preview.md) |
| documents.hold | R-RECORDS | Entidad/clase/objeto/revisión/audiencia | Contrato local del dueño para hold. [Consumidor](../specs/flows/cpe-document-delivery.md) |
| documents.ingest | OPERATIVOS | Entidad/clase/objeto/revisión/audiencia | Contrato local del dueño para ingest. [Consumidor](../specs/flows/records-signatures-site-packs.md) |
| documents.manage_policy | R-RECORDS | Entidad/clase/objeto/revisión/audiencia | Contrato local del dueño para manage_policy. [Consumidor](../specs/flows/cpe-document-delivery.md) |
| documents.policy.approve | R-RECORDS | Entidad/clase/objeto/revisión/audiencia | Contrato local del dueño para policy / approve. [Consumidor](../specs/flows/records-signatures-site-packs.md) |
| documents.policy.prepare | R-RECORDS | Entidad/clase/objeto/revisión/audiencia | Contrato local del dueño para policy / prepare. [Consumidor](../specs/flows/records-signatures-site-packs.md) |
| documents.prepare_delivery | R-RECORDS | Entidad/clase/objeto/revisión/audiencia | Contrato local del dueño para prepare_delivery. [Consumidor](../specs/flows/first-operational-circuit.md) |
| documents.preview | OPERATIVOS, R-AUDIT | Entidad/clase/objeto/revisión/audiencia | Render de vista; AND documents.view, sin original por tener preview. [Consumidor](../specs/cross-cutting/case-flow-preview.md) |
| documents.record_external_delivery | R-RECORDS | Entidad/clase/objeto/revisión/audiencia | Contrato local del dueño para record_external_delivery. [Consumidor](../specs/flows/cpe-document-delivery.md) |
| documents.release_hold | R-RECORDS | Entidad/clase/objeto/revisión/audiencia | Contrato local del dueño para release_hold. [Consumidor](../specs/flows/cpe-document-delivery.md) |
| documents.render | R-RECORDS | Entidad/clase/objeto/revisión/audiencia | Contrato local del dueño para render. [Consumidor](../specs/acceptance/reporting-goldens.md) |
| documents.resend | R-RECORDS | Entidad/clase/objeto/revisión/audiencia | Contrato local del dueño para resend. [Consumidor](../specs/flows/cpe-document-delivery.md) |
| documents.retention.prepare | R-RECORDS | Entidad/clase/objeto/revisión/audiencia | Preparar propuesta por clase/legal hold; AND documents.policy.prepare y delegación. [Consumidor](../specs/flows/records-signatures-site-packs.md) |
| documents.send | R-RECORDS | Entidad/clase/objeto/revisión/audiencia | Contrato local del dueño para send. [Consumidor](../specs/acceptance/operational-scenarios.md) |
| documents.sign.prepare | R-RECORDS | Entidad/clase/objeto/revisión/audiencia | Contrato local del dueño para sign / prepare. [Consumidor](../specs/flows/records-signatures-site-packs.md) |
| documents.sign.verify | R-RECORDS | Entidad/clase/objeto/revisión/audiencia | DR4 verificar evidencia técnica de firma; no aprobar acto ni facultades. [Consumidor](../specs/flows/records-signatures-site-packs.md) |
| documents.upload | R-RECORDS | Entidad/clase/objeto/revisión/audiencia | Contrato local del dueño para upload. [Consumidor](../specs/flows/first-operational-circuit.md) |
| documents.verify_artifact | R-RECORDS | Entidad/clase/objeto/revisión/audiencia | Contrato local del dueño para verify_artifact. [Consumidor](../specs/flows/first-operational-circuit.md) |
| documents.view | OPERATIVOS; R-AUDIT por mandato | Entidad/clase/objeto/revisión/audiencia | Contrato local del dueño para view. [Consumidor](../specs/cross-cutting/case-flow-preview.md) |
| identity.security.manage | R-PLATFORM | Identidad/instalación nombrada; sin entidad implícita | Administrar factor/recuperación/seguridad técnica; revocación exige RA3; no membresía. [Consumidor](roles-delegation.md) |
| identity.security.policy.approve | R-PLATFORM | Identidad/instalación nombrada; sin entidad implícita | Contrato local del dueño para security / policy / approve. [Consumidor](roles-delegation.md) |
| identity.security.policy.prepare | R-PLATFORM | Identidad/instalación nombrada; sin entidad implícita | Contrato local del dueño para security / policy / prepare. [Consumidor](roles-delegation.md) |
| identity.user.manage | R-ACCESS | Identidad/instalación nombrada; sin entidad implícita | Preparar identidad verificada previa a asignación RA2; la concesión requiere access.manage; no crea membresía por alta. [Consumidor](roles-delegation.md) |
| imports.confirm | R-MASTER; R-BUYER/R-INVENTORY-CONTROL/R-TREASURY/R-ACCOUNTING/R-TAX por concesión de lote | Entidad/lote/participantes autorizados | C25 confirma lote; AND cada permiso de efecto/aprobación del dueño; atomicidad de ficha. [Consumidor](../specs/flows/first-operational-circuit.md) |
| imports.prepare | R-MASTER; R-BUYER/R-INVENTORY-CONTROL/R-TREASURY/R-ACCOUNTING/R-TAX por concesión de lote | Entidad/lote/participantes autorizados | C24 preview de lote; AND lecturas de participantes, parsing y revisiones. [Consumidor](../specs/flows/first-operational-circuit.md) |
| integration.manage_connection | R-PLATFORM | Entidad/conexión/operación/epoch | Contrato local del dueño para manage_connection. [Consumidor](../specs/flows/first-operational-circuit.md) |
| integration.process | T-INTEGRATION | Entidad/conexión/operación/epoch | C04/C09 procesamiento técnico mandatado; no heredar autoridad humana. [Consumidor](../specs/flows/jumpseller-external-work.md) |
| integration.receive | T-INBOUND | Entidad/conexión/operación/epoch | C02 recepción autenticada por conexión; no aceptar pedido ni crear dinero. [Consumidor](../specs/flows/first-operational-circuit.md) |
| integration.reconcile | R-PLATFORM; T-RECONCILE solo mandato programado | Entidad/conexión/operación/epoch | C03/C05 consulta/plan de sincronización, sin aceptación de negocio; AND inventory.view solo para actor humano que consulte disponibilidad. [Consumidor](../specs/flows/first-operational-circuit.md) |
| integration.replay | R-PLATFORM | Entidad/conexión/operación/epoch | C10 autoriza replay del alcance técnico, no aprobación de efectos económicos; revalidar resultado incierto. [Consumidor](../specs/flows/first-operational-circuit.md) |
| integrations.mandate.prepare | R-PLATFORM | Entidad/conexión/familia | Preparar mandato por conexión/efecto/destinatario; aprobación del dueño y Access vigente antes de ejecutar. [Consumidor](configuration-governance.md) |
| integrations.policy.approve | R-PLATFORM | Entidad/conexión/familia | Contrato local del dueño para policy / approve. [Consumidor](configuration-governance.md) |
| integrations.policy.prepare | R-PLATFORM | Entidad/conexión/familia | Contrato local del dueño para policy / prepare. [Consumidor](configuration-governance.md) |
| inventory.adjust | R-INVENTORY-CONTROL | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para adjust. [Consumidor](../specs/flows/first-operational-circuit.md) |
| inventory.adjust.approve | R-INVENTORY-CONTROL | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para adjust / approve. [Consumidor](../specs/flows/catalog-sites-warehouses.md) |
| inventory.approve_count | R-INVENTORY-CONTROL | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para approve_count. [Consumidor](../specs/milestones/inventory-deep.md) |
| inventory.confirm_delivery | R-WAREHOUSE | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para confirm_delivery. [Consumidor](../specs/flows/first-operational-circuit.md) |
| inventory.count | R-WAREHOUSE | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para count. [Consumidor](../specs/milestones/inventory-deep.md) |
| inventory.count.approve | R-INVENTORY-CONTROL | Entidad/WAREHOUSE_SET; pool completo al valorar | Autorizar resultado/diferencia INV04; confirmar además inventory.approve_count. [Consumidor](../specs/milestones/inventory-deep.md) |
| inventory.count.capture | R-WAREHOUSE | Entidad/WAREHOUSE_SET; pool completo al valorar | Capturar medición dentro del conteo autorizado INV04; no aprobar diferencia. [Consumidor](../specs/milestones/inventory-deep.md) |
| inventory.dispatch | R-WAREHOUSE | Entidad/WAREHOUSE_SET; pool completo al valorar | Deber físico del despacho C15; AND inventory.confirm_delivery y sales.confirm_delivery en coordinador. [Consumidor](../specs/milestones/inventory-deep.md) |
| inventory.dispatch_supplier_return | R-WAREHOUSE | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para dispatch_supplier_return. [Consumidor](../specs/milestones/inventory-deep.md) |
| inventory.inspect | R-WAREHOUSE | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para inspect. [Consumidor](../specs/milestones/inventory-deep.md) |
| inventory.opening | R-INVENTORY-CONTROL | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para opening. [Consumidor](../specs/flows/first-operational-circuit.md) |
| inventory.policy.approve | R-INVENTORY-CONTROL | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para policy / approve. [Consumidor](../specs/milestones/inventory-deep.md) |
| inventory.policy.prepare | R-INVENTORY-CONTROL | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para policy / prepare. [Consumidor](../specs/milestones/inventory-deep.md) |
| inventory.prepare | R-WAREHOUSE | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para prepare. [Consumidor](../specs/flows/first-operational-circuit.md) |
| inventory.receive | R-WAREHOUSE | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para receive. [Consumidor](../specs/milestones/procurement-deep.md) |
| inventory.receive_return | R-WAREHOUSE | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para receive_return. [Consumidor](../specs/flows/first-operational-circuit.md) |
| inventory.transfer | R-INVENTORY-CONTROL | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para transfer. [Consumidor](../specs/milestones/inventory-deep.md) |
| inventory.transfer.approve | R-INVENTORY-CONTROL | Entidad/WAREHOUSE_SET; pool completo al valorar | Autorizar revisión/cantidades del traslado TR1/TR2; despacho/recepción conservan sus comandos. [Consumidor](../specs/milestones/inventory-deep.md) |
| inventory.transfer.correct | R-INVENTORY-CONTROL | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para transfer / correct. [Consumidor](../specs/flows/catalog-sites-warehouses.md) |
| inventory.transfer.dispatch | R-WAREHOUSE | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para transfer / dispatch. [Consumidor](../specs/flows/catalog-sites-warehouses.md) |
| inventory.transfer.prepare | R-WAREHOUSE | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para transfer / prepare. [Consumidor](../specs/flows/catalog-sites-warehouses.md) |
| inventory.transfer.receive | R-WAREHOUSE | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para transfer / receive. [Consumidor](../specs/flows/catalog-sites-warehouses.md) |
| inventory.value | R-INVENTORY-CONTROL | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para value. [Consumidor](../specs/milestones/inventory-deep.md) |
| inventory.value.approve | R-INVENTORY-CONTROL | Entidad/WAREHOUSE_SET; pool completo al valorar | Autorizar propuesta de valoración INV03; publicar además inventory.value y autoridad sobre pool completo. [Consumidor](../specs/milestones/inventory-deep.md) |
| inventory.view | R-WAREHOUSE, R-INVENTORY-CONTROL, R-AUDIT | Entidad/WAREHOUSE_SET; pool completo al valorar | Contrato local del dueño para view. [Consumidor](../specs/milestones/inventory-deep.md) |
| operations.config.manage | R-PLATFORM | Instalación/entorno/mandato | Administrar settings operativos identificados; política de continuidad requiere CG y delegación. [Consumidor](../operations/delivery.md) |
| operations.policy.approve | R-PLATFORM | Instalación/entorno/mandato | Contrato local del dueño para policy / approve. [Consumidor](../operations/delivery.md) |
| operations.policy.prepare | R-PLATFORM | Instalación/entorno/mandato | Contrato local del dueño para policy / prepare. [Consumidor](../operations/delivery.md) |
| operations.restore.execute | R-PLATFORM | Instalación/entorno/mandato | Ejecutar restore bajo mandato operacional; acceso y efectos OFF hasta conciliación y aprobación. [Consumidor](../operations/delivery.md) |
| operations.restore.prepare | R-PLATFORM | Instalación/entorno/mandato | Preparar plan/manifiesto de restore aislado; no ejecutar ni habilitar efectos. [Consumidor](../operations/delivery.md) |
| organization.manage | R-MASTER | Entidad/sede nombrada | Contrato local del dueño para manage. [Consumidor](../specs/flows/first-operational-circuit.md) |
| organization.policy.approve | R-MASTER | Entidad/sede nombrada | Contrato local del dueño para policy / approve. [Consumidor](../specs/milestones/runtime-masters.md) |
| organization.policy.prepare | R-MASTER | Entidad/sede nombrada | Contrato local del dueño para policy / prepare. [Consumidor](../specs/milestones/runtime-masters.md) |
| organization.site.manage | R-MASTER | Entidad/sede nombrada | Contrato local del dueño para site / manage. [Consumidor](../specs/milestones/runtime-masters.md) |
| parties.manage | R-MASTER | Entidad/contraparte/caso | Contrato local del dueño para manage. [Consumidor](../specs/flows/first-operational-circuit.md) |
| parties.policy.approve | R-MASTER | Entidad/contraparte/caso | Contrato local del dueño para policy / approve. [Consumidor](../specs/milestones/runtime-masters.md) |
| parties.policy.prepare | R-MASTER | Entidad/contraparte/caso | Contrato local del dueño para policy / prepare. [Consumidor](../specs/milestones/runtime-masters.md) |
| policy.register.view | Roles con lectura autorizada de la política; R-AUDIT por mandato | Entidad/fila/familia autorizada | Consultar solo filas de política cuyos permisos de dominio se poseen. [Consumidor](../product/company-policy-register.md) |
| privacy.context.approve | R-CORPORATE con mandato de responsable legal | Entidad/finalidad/caso/sujeto/objeto/categoría/plan | Aprobar contexto con aval competente; AND aprobación de finalidad del dueño y administración configurada. [Consumidor](../security/personal-data-lifecycle.md) |
| privacy.context.prepare | Rol del dueño de finalidad; R-RECORDS por delegación documental | Entidad/finalidad/caso/sujeto/objeto/categoría/plan | Preparar ProcessingContext; no aprobar base jurídica ni habilitar tratamiento. [Consumidor](../security/personal-data-lifecycle.md) |
| privacy.decision.approve | R-CORPORATE con mandato del responsable del tratamiento | Entidad/finalidad/caso/sujeto/objeto/categoría/plan | Aprobar decisión motivada/plan por objeto y finalidad con dueño/aval legal; no alterar economía ni autoeliminar hold. [Consumidor](../security/personal-data-lifecycle.md) |
| privacy.execute | R-ACCESS para restricciones; R-RECORDS para artefactos; R-MASTER para atributos, por plan | Entidad/finalidad/caso/sujeto/objeto/categoría/plan | Aplicar paso autorizado; AND capability del dueño y plan aprobado/revisión vigente; no borrado económico ni ejecución general. [Consumidor](../security/personal-data-lifecycle.md) |
| privacy.incident.manage | R-PLATFORM por mandato de respuesta; R-RECORDS por mandato de recepción | Entidad/finalidad/caso/sujeto/objeto/categoría/plan | Registrar/contener incidente; decisión de notificar del responsable acreditado mediante privacy.decision.approve. [Consumidor](../security/personal-data-lifecycle.md) |
| privacy.request.manage | R-RECORDS por mandato de atención | Entidad/finalidad/caso/sujeto/objeto/categoría/plan | Recibir/verificar identidad, tramitar y preparar respuesta; no decidir supresión ni extender plazo discrecionalmente. [Consumidor](../security/personal-data-lifecycle.md) |
| privacy.view | R-RECORDS/R-CORPORATE por caso; R-ACCESS/R-PLATFORM solo metadata necesaria | Entidad/finalidad/caso/sujeto/objeto/categoría/plan | Consultar expediente de privacidad; AND permiso de fuente si contiene datos; sin lectura médica por rol. [Consumidor](../security/personal-data-lifecycle.md) |
| procurement.accept_service | R-BUYER | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para accept_service. [Consumidor](../specs/milestones/procurement-deep.md) |
| procurement.approve | R-PURCHASE-APPROVE | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para approve. [Consumidor](../specs/milestones/procurement-deep.md) |
| procurement.approve_advance | R-PURCHASE-APPROVE | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para approve_advance. [Consumidor](../specs/milestones/procurement-deep.md) |
| procurement.approve_direct | R-PURCHASE-APPROVE | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para approve_direct. [Consumidor](../specs/milestones/procurement-deep.md) |
| procurement.award.approve | R-PURCHASE-APPROVE | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para award / approve. [Consumidor](../specs/flows/sourcing-imports.md) |
| procurement.close | R-PURCHASE-APPROVE | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para close. [Consumidor](../specs/milestones/procurement-deep.md) |
| procurement.cost.allocate | R-BUYER | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para cost / allocate. [Consumidor](../specs/flows/sourcing-imports.md) |
| procurement.direct.approve | R-PURCHASE-APPROVE | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para direct / approve. [Consumidor](../specs/flows/sourcing-imports.md) |
| procurement.import.approve | R-PURCHASE-APPROVE | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para import / approve. [Consumidor](../specs/flows/sourcing-imports.md) |
| procurement.import.record | R-BUYER | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para import / record. [Consumidor](../specs/flows/sourcing-imports.md) |
| procurement.match | R-BUYER | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para match. [Consumidor](../specs/milestones/procurement-deep.md) |
| procurement.order.approve | R-PURCHASE-APPROVE | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Aprobar PO consumida por P02; publicación además procurement.approve. [Consumidor](../specs/milestones/procurement-deep.md) |
| procurement.order.prepare | R-BUYER | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Preparar PO dentro de P01; confirmar requiere procurement.prepare y revisión autorizada. [Consumidor](../specs/milestones/procurement-deep.md) |
| procurement.payability.approve | R-PURCHASE-APPROVE | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Autorizar liberación de obligación P05; comando además procurement.release_payability. [Consumidor](../specs/milestones/procurement-deep.md) |
| procurement.policy.approve | R-PURCHASE-APPROVE | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para policy / approve. [Consumidor](../specs/milestones/procurement-deep.md) |
| procurement.policy.prepare | R-BUYER | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para policy / prepare. [Consumidor](../specs/milestones/procurement-deep.md) |
| procurement.prepare | R-BUYER | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para prepare. [Consumidor](../specs/milestones/procurement-deep.md) |
| procurement.receive | R-WAREHOUSE | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para receive. [Consumidor](../specs/milestones/procurement-deep.md) |
| procurement.record_document | R-BUYER | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para record_document. [Consumidor](../specs/milestones/procurement-deep.md) |
| procurement.release_payability | R-PURCHASE-APPROVE | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para release_payability. [Consumidor](../specs/milestones/procurement-deep.md) |
| procurement.rent.confirm | R-PURCHASE-APPROVE | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para rent / confirm. [Consumidor](../specs/flows/financial-accounts-instruments.md) |
| procurement.requisition.prepare | R-REQUEST | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Preparar necesidad propia para PC1; no autorizar ni crear PO. [Consumidor](../specs/milestones/procurement-deep.md) |
| procurement.requisition.submit | R-REQUEST | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Remitir necesidad propia a PC1; no autoaprobar. [Consumidor](../specs/milestones/procurement-deep.md) |
| procurement.return | R-PURCHASE-APPROVE | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para return. [Consumidor](../specs/milestones/inventory-deep.md) |
| procurement.service.confirm | R-BUYER | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Autorizar conformidad de servicio P03; registrar además procurement.accept_service, sin stock. [Consumidor](../specs/milestones/procurement-deep.md) |
| procurement.sourcing.approve | R-PURCHASE-APPROVE | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para sourcing / approve. [Consumidor](../specs/flows/sourcing-imports.md) |
| procurement.sourcing.prepare | R-BUYER | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para sourcing / prepare. [Consumidor](../specs/flows/sourcing-imports.md) |
| procurement.view | R-REQUEST, R-BUYER, R-PURCHASE-APPROVE, R-AUDIT | Entidad/sitio/compra; OWN_DRAFTS en solicitud | Contrato local del dueño para view. [Consumidor](../specs/milestones/procurement-deep.md) |
| reports.snapshot | OPERATIVOS, R-AUDIT por concesión de informe | Entidad/informe/corte/fuentes autorizadas | C26 congela resultado autorizado; AND reports.view, y permisos export de dueños al exportar. [Consumidor](../specs/flows/first-operational-circuit.md) |
| reports.view | OPERATIVOS, R-AUDIT por concesión de informe | Entidad/informe/corte/fuentes autorizadas | C26 consulta definida; AND lecturas de fuentes, no export implícito. [Consumidor](../specs/flows/first-operational-circuit.md) |
| sales.accept_external_order | R-SALES | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para accept_external_order. [Consumidor](../specs/flows/first-operational-circuit.md) |
| sales.accept_return | R-SALES | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para accept_return. [Consumidor](../specs/flows/first-operational-circuit.md) |
| sales.claims.intake | R-SALES | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para claims / intake. [Consumidor](../specs/flows/records-signatures-site-packs.md) |
| sales.claims.respond | R-SALES-APPROVE | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | LR1: aprobar respuesta/revisión al reclamo, con responsable/plazo/canal; envío mediante Documents y mandato separado. [Consumidor](../specs/flows/records-signatures-site-packs.md) |
| sales.collections.manage | R-CREDIT | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Registrar gestión/promesa de cobranza ligada al objetivo; no dinero ni reestructuración aprobada. [Consumidor](../specs/flows/professional-sales.md) |
| sales.confirm_delivery | R-SALES | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para confirm_delivery. [Consumidor](../specs/flows/first-operational-circuit.md) |
| sales.contract.approve | R-SALES-APPROVE | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para contract / approve. [Consumidor](../specs/flows/professional-sales.md) |
| sales.correct | R-SALES-APPROVE | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para correct. [Consumidor](../specs/flows/first-operational-circuit.md) |
| sales.correct_cpe | R-SALES-APPROVE | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para correct_cpe. [Consumidor](../specs/flows/cpe-document-delivery.md) |
| sales.credit.approve | R-SALES-APPROVE | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para credit / approve. [Consumidor](../specs/flows/professional-sales.md) |
| sales.credit.prepare | R-CREDIT | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Preparar límite/condiciones CR1 sin aumentar exposición. [Consumidor](../specs/flows/professional-sales.md) |
| sales.credit.review_exposure | R-CREDIT | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Revisar exposición/cálculo/aging CR1; no aprobar límite ni cobrar. [Consumidor](../specs/flows/professional-sales.md) |
| sales.discount.approve | R-SALES-APPROVE | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Autorizar descuento/margen por objeto/revisión antes de QS1/QS4; no editar precio libre. [Consumidor](../specs/flows/professional-sales.md) |
| sales.dispatch.authorize | R-SALES-APPROVE | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para dispatch / authorize. [Consumidor](../specs/flows/professional-sales.md) |
| sales.fulfillment.confirm | R-SALES | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para fulfillment / confirm. [Consumidor](../specs/flows/professional-sales.md) |
| sales.order.accept | R-SALES | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para order / accept. [Consumidor](../specs/flows/professional-sales.md) |
| sales.policy.approve | R-SALES-APPROVE, R-SITE | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para policy / approve. [Consumidor](../specs/flows/professional-sales.md) |
| sales.policy.prepare | R-SALES, R-CREDIT, R-SITE | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para policy / prepare. [Consumidor](../specs/flows/professional-sales.md) |
| sales.prepare_delivery | R-SALES | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para prepare_delivery. [Consumidor](../specs/flows/first-operational-circuit.md) |
| sales.quote.accept | R-SALES | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para quote / accept. [Consumidor](../specs/flows/professional-sales.md) |
| sales.quote.approve | R-SALES-APPROVE | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Autorizar revisión QS1; emitir además sales.quote.issue. [Consumidor](../specs/flows/professional-sales.md) |
| sales.quote.issue | R-SALES | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para quote / issue. [Consumidor](../specs/flows/professional-sales.md) |
| sales.quote.prepare | R-SALES | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Preparar revisión de cotización previa a QS1; sin emisión ni compromiso. [Consumidor](../specs/flows/professional-sales.md) |
| sales.refund.approve | R-SALES-APPROVE | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Autorizar causa/importe comercial C18; Treasury conserva aprobación monetaria y comando refund. [Consumidor](../specs/flows/professional-sales.md) |
| sales.refund.prepare | R-SALES | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Preparar solicitud comercial C16/C18, sin salida de dinero. [Consumidor](../specs/flows/professional-sales.md) |
| sales.register_cpe | R-SALES | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para register_cpe. [Consumidor](../specs/flows/first-operational-circuit.md) |
| sales.return | R-SALES | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para return. [Consumidor](../specs/milestones/inventory-deep.md) |
| sales.site.approve | R-SITE | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | SP1: aprobar revisión de pack/readiness dentro de sitio/sujetos; no autorizar PETAR ni emitir aptitud médica. [Consumidor](../specs/flows/records-signatures-site-packs.md) |
| sales.site.prepare | R-SITE | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para site / prepare. [Consumidor](../specs/flows/records-signatures-site-packs.md) |
| sales.site.requirements.manage | R-SITE | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para site / requirements / manage. [Consumidor](../specs/flows/records-signatures-site-packs.md) |
| sales.site.view | R-SITE, R-AUDIT | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Consultar requisitos/paquete del sitio autorizado; no información médica por defecto. [Consumidor](../specs/flows/professional-sales.md) |
| sales.verify_cpe | R-SALES | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para verify_cpe. [Consumidor](../specs/flows/first-operational-circuit.md) |
| sales.view | R-SALES, R-SALES-APPROVE, R-CREDIT, R-AUDIT | Entidad/CLIENT_SET/SITE_SET/ASSIGNED_CASES | Contrato local del dueño para view. [Consumidor](../specs/flows/professional-sales.md) |
| shadow.correct | T-SHADOW | Entidad/run/cápsula, solo DB experimental | Reversa/nueva revisión experimental; no overwrite. [Consumidor](../accounting/templates-automation-shadow.md) |
| shadow.interpret | T-SHADOW | Entidad/run/cápsula, solo DB experimental | Interpretar cápsula sellada; sin core ni etiquetas oficiales previas. [Consumidor](../accounting/templates-automation-shadow.md) |
| shadow.post | T-SHADOW | Entidad/run/cápsula, solo DB experimental | Postear únicamente ledger experimental validado; nunca ledger oficial. [Consumidor](../accounting/templates-automation-shadow.md) |
| support.reference.read | OPERATIVOS | Objeto de soporte del caso autorizado | Lectura mínima ID/nombre/UOM/estado del objeto necesario; no expediente completo. [Consumidor](roles-delegation.md) |
| tax.approve | R-TAX | Entidad/obligación/período/filing | Contrato local del dueño para approve. [Consumidor](../specs/milestones/tax-deep.md) |
| tax.configure | R-TAX | Entidad/obligación/período/filing | Contrato local del dueño para configure. [Consumidor](../specs/milestones/tax-deep.md) |
| tax.correct | R-TAX | Entidad/obligación/período/filing | Contrato local del dueño para correct. [Consumidor](../specs/flows/external-tax-filing-mirror.md) |
| tax.export | R-TAX | Entidad/obligación/período/filing | Contrato local del dueño para export. [Consumidor](../specs/flows/external-tax-filing-mirror.md) |
| tax.external.record | R-TAX | Entidad/obligación/período/filing | TX5: registrar filing externo/captura y vínculo de liquidación con evidencia; sin dinero ni envío. X05 usa tax.record_filing en su ruta, no alias. [Consumidor](../specs/flows/tax-workspace-books.md) |
| tax.policy.approve | R-TAX | Entidad/obligación/período/filing | Contrato local del dueño para policy / approve. [Consumidor](../specs/milestones/tax-deep.md) |
| tax.policy.prepare | R-TAX | Entidad/obligación/período/filing | Contrato local del dueño para policy / prepare. [Consumidor](../specs/milestones/tax-deep.md) |
| tax.prepare | R-TAX | Entidad/obligación/período/filing | Contrato local del dueño para prepare. [Consumidor](../specs/flows/external-tax-filing-mirror.md) |
| tax.prepare_payment | R-TAX | Entidad/obligación/período/filing | Contrato local del dueño para prepare_payment. [Consumidor](../specs/milestones/tax-deep.md) |
| tax.prepare_registers | R-TAX | Entidad/obligación/período/filing | Contrato local del dueño para prepare_registers. [Consumidor](../specs/milestones/tax-deep.md) |
| tax.profile.approve | R-TAX | Entidad/obligación/período/filing | TX1: evaluar/aprobar obligación y aplicabilidad por perfil/período/fuente. X01 activar configuración conserva tax.configure AND autoridad administrativa. [Consumidor](../specs/flows/tax-workspace-books.md) |
| tax.reconcile | R-TAX | Entidad/obligación/período/filing | Contrato local del dueño para reconcile. [Consumidor](../specs/flows/external-tax-filing-mirror.md) |
| tax.record_filing | R-TAX | Entidad/obligación/período/filing | Contrato local del dueño para record_filing. [Consumidor](../specs/flows/external-tax-filing-mirror.md) |
| tax.review | R-TAX | Entidad/obligación/período/filing | Mirror: verificar captura/evidencia y revisar discrepancia; sin declarar verificado lo incompleto ni aceptar propuesta por silencio. TX4 conserva tax.export para exportar. [Consumidor](../specs/flows/external-tax-filing-mirror.md) |
| tax.view | R-TAX, R-AUDIT | Entidad/obligación/período/filing | Contrato local del dueño para view. [Consumidor](../specs/flows/external-tax-filing-mirror.md) |
| treasury.application.confirm | R-TREASURY-APPROVE | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Autorizar distribución para C13/T03; aplicar además treasury.apply. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.application.prepare | R-TREASURY | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Preparar distribución N:M para C13/T03; sin consumir residual. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.apply | R-TREASURY-APPROVE | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para apply. [Consumidor](../specs/flows/first-operational-circuit.md) |
| treasury.bank_destination.approve | R-TREASURY-APPROVE | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Autorizar destino con evidencia independiente; invalida aprobaciones de pago de revisión anterior. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.bank_destination.prepare | R-TREASURY | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Preparar nueva revisión de destino; no validar su autenticidad ni usarla aprobada. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.close_statement | R-TREASURY-APPROVE | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para close_statement. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.confirm_payment | R-TREASURY-APPROVE | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para confirm_payment. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.confirm_receipt | R-TREASURY-APPROVE | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para confirm_receipt. [Consumidor](../specs/flows/first-operational-circuit.md) |
| treasury.confirm_transfer | R-TREASURY-APPROVE | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para confirm_transfer. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.correct | R-TREASURY-APPROVE | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para correct. [Consumidor](../specs/flows/first-operational-circuit.md) |
| treasury.expense.approve | R-TREASURY-APPROVE | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para expense / approve. [Consumidor](../specs/flows/financial-accounts-instruments.md) |
| treasury.finance.confirm | R-TREASURY-APPROVE | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para finance / confirm. [Consumidor](../specs/flows/financial-accounts-instruments.md) |
| treasury.finance.prepare | R-TREASURY | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Preparar disposición/amortización FI2; no crear movimiento. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.import_statement | R-TREASURY | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para import_statement. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.manage_account | R-TREASURY-APPROVE | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para manage_account. [Consumidor](../specs/flows/first-operational-circuit.md) |
| treasury.money.confirm | R-TREASURY-APPROVE | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para money / confirm. [Consumidor](../specs/flows/professional-sales.md) |
| treasury.money.prepare | R-TREASURY | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Preparar evidencia de ocurrencia, sin confirmarla; T02/C12 según dirección. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.payment.approve | R-TREASURY-APPROVE | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Autorizar destino/importe/revisión de pago T02; confirmar además treasury.confirm_payment. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.payment.prepare | R-TREASURY | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Preparar propuesta P06/T02; registrar con treasury.propose_payment, no pago. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.petty.manage | R-TREASURY-APPROVE | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para petty / manage. [Consumidor](../specs/flows/financial-accounts-instruments.md) |
| treasury.petty.prepare | R-TREASURY | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Preparar anticipo/rendición FI3/FI4; no reconocer gasto ni transferir. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.policy.approve | R-TREASURY-APPROVE | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para policy / approve. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.policy.prepare | R-TREASURY | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para policy / prepare. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.prepare_financing | R-TREASURY | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para prepare_financing. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.propose_payment | R-TREASURY | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para propose_payment. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.propose_receipt | R-TREASURY | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para propose_receipt. [Consumidor](../specs/flows/first-operational-circuit.md) |
| treasury.reconcile | R-TREASURY | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para reconcile. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.refund | R-TREASURY-APPROVE | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para refund. [Consumidor](../specs/flows/first-operational-circuit.md) |
| treasury.refund.approve | R-TREASURY-APPROVE | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Autorizar salida monetaria C18/T04; AND aprobación comercial cuando corresponde y treasury.refund. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.unreconcile | R-TREASURY-APPROVE | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para unreconcile. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |
| treasury.view | R-TREASURY, R-TREASURY-APPROVE, R-ACCOUNTING, R-AUDIT | Entidad/ACCOUNT_SET/moneda/instrumento/objetivo | Contrato local del dueño para view. [Consumidor](../specs/milestones/treasury-corporate-deep.md) |

## Retirados sin alias runtime

| Identificador anterior | Único ID canónico | Motivo |
|---|---|---|
| integrations.connection.manage | integration.manage_connection | Misma responsabilidad; no había consumidor distinto documentado. Reemplazo editorial explícito, no doble concesión. |
| accounting.journal.prepare | accounting.prepare | Misma responsabilidad; no había consumidor distinto documentado. Reemplazo editorial explícito, no doble concesión. |
| accounting.period.reopen | accounting.reopen | Misma responsabilidad; no había consumidor distinto documentado. Reemplazo editorial explícito, no doble concesión. |
| accounting.report.approve | accounting.approve_reports | Misma responsabilidad; no había consumidor distinto documentado. Reemplazo editorial explícito, no doble concesión. |

No existe migración de grants ejecutada. Si se encontraran datos/configuraciones reales con nombres antiguos, su conversión exige inventario, revisión de scope/SoD, aprobación y validación B02/C13 en otra misión; no fallback permisivo. Las menciones históricas o de esta tabla de retirada no son entradas activas. Las formas abreviadas de prosa se leen solo contra el ID completo de este registro; nunca se envían barras a un guard.
