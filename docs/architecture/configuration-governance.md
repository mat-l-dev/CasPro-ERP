# Configuración, activación e impacto

[Plantillas y automatizaciones tipadas](automation.md) reutilizan este protocolo por dueño/familia: template, regla, calendario, mandato y AIRequestTemplate tienen revisiones/efectos distintos; no activación conjunta por guardar una plantilla. Accounting usa accounting.policy.prepare/approve con delegación administrativa para template/regla/equivalence mapping/POL-26 de su función. ImpactManifest incluye drafts editados, ocurrencias consumidas, mandatos, fuente/corte, versiones de modelo/prompt/evaluación y presupuesto; activar no recalcula historia ni renueva permiso vencido. Centro de automatización es router de descriptores y runs, no settings dump ni Rule DSL.

Propuesta del amendment según [review](../review.md). El Centro de Configuración y Administración es una superficie de consulta y entrada a comandos de los dueños de [boundaries](boundaries.md), no un módulo empresarial nuevo. [Roles](roles-delegation.md) gobierna WHO; cada política tipada del dueño gobierna WHEN/HOW. El [registro TILMUX](../product/company-policy-register.md) indexa contratos/versiones, no ejecuta reglas. Fundamento [GOV-S03/S07/S11/S14–17](../research/governance-authorization-benchmark.md).

## Catálogo de superficies y autoridad

ConfigurationDescriptor publicado por dueño: ID de familia, nombre, propósito, tipos de scope soportados, schema/versión, comandos públicos de consultar/preparar/validar/aprobar/activar, recursos de permiso, política referenciada, efectos admitidos, vistas de historial/evidencia y consumidores conocidos. Es contrato estático registrado en entrega, no tabla que permita subir endpoints/scripts/SQL desde UI. Descriptor no contiene valores ni secretos. Centro obtiene DTOs autorizados y entrega intención al caso de uso del dueño/coordinador; dueño no llama al Centro ni lee modelos ajenos. No JSON dump settings[key], reglas evaluadas como texto o approval workflow universal.

Cambiar configuración empresarial exige conjunción de (a) mandato administrativo R-CONFIG con familia/verbos/scope explícitos **o** ConfigDelegation vigente emitida por tal autoridad y (b) capability de política/maestro del dueño. Rol de dominio por sí solo no habilita configuración. R-CONFIG tiene verbos administrativos pero no obtiene aprobación contable/tributaria por ellos. Una delegación a contador puede suministrar verbos `configuration.prepare/approve/activate` solo para la familia Accounting y exige además `accounting.policy.prepare/approve`; ninguna entrega `accounting.post` ni `treasury.money.confirm`. Delegar no exige que el administrador tenga permiso para ejecutar la operación económica; sí techo administrativo para esa familia. Precios y requisitos de sitio son valores de dueño, gobernados igual.

Vocabulario finito de verbos de política: preparar/validar/consultar/aprobar/activar/sustituir, materializados por descriptor para Access, Organization, Catalog, Sales, Procurement, Inventory, Treasury, Accounting, Tax, Documents, Corporate, Integrations u Operations. No prefijo comodín: asignación enumera familia y verbos, verificando contrato registrado. `configuration.activate` no sustituye permiso de dominio. Cambiar facultades, SoD o el propio protocolo se valida contra autoridad **anterior vigente**, nunca con la revisión propuesta que concedería su aprobación. Piso de seguridad/retención legal/último admin no es configurable por un rol empresarial.

## Capacidades tipadas de política

Esta tabla completa el catálogo de roles: solo la plantilla nombrada incluye las capabilities exactas de su columna. Son permisos de **política**, además del mandato administrativo por familia; nunca permisos de pago/posting/despacho. Consultar requiere `configuration.view` o lectura autorizada de la política del dueño. Validar usa prepare más las lecturas de impacto; activar exige approve del dueño más `configuration.activate`; sustituir sigue prepare/approve/activate. La aprobación interna puede admitir E conforme SOD-08, también en roles cuyo deber operativo no admite autoaprobación. No concede facultad profesional.

| Familia / dueño | Prepare: capability y rol | Approve: capability y rol |
|---|---|---|
| Seguridad técnica / Identity | identity.security.policy.prepare / R-PLATFORM | identity.security.policy.approve / R-PLATFORM |
| Roles/delegación/SoD / Access | access.policy.prepare / R-ACCESS | access.policy.approve / R-ACCESS |
| Gobierno del cambio / dueño del protocolo administrativo Access | configuration.governance.prepare / R-CONFIG | configuration.governance.approve / R-CONFIG |
| Organización/maestros / Organization y Parties por descriptor separado | organization.policy.prepare, parties.policy.prepare / R-MASTER | organization.policy.approve, parties.policy.approve / R-MASTER |
| Catálogo/precios / Catalog | catalog.policy.prepare / R-MASTER | catalog.policy.approve / R-SALES-APPROVE |
| Comercial/crédito/sitio / Sales, subfamilias con scopes independientes | sales.policy.prepare / R-SALES, R-CREDIT o R-SITE solo en su subfamilia | sales.policy.approve / R-SALES-APPROVE; R-SITE solo requisitos de sitio |
| Compras/importación / Procurement | procurement.policy.prepare / R-BUYER | procurement.policy.approve / R-PURCHASE-APPROVE |
| Inventario/almacenes / Inventory | inventory.policy.prepare / R-INVENTORY-CONTROL | inventory.policy.approve / R-INVENTORY-CONTROL |
| Dinero/instrumentos/fondos / Treasury | treasury.policy.prepare / R-TREASURY | treasury.policy.approve / R-TREASURY-APPROVE |
| Manual/cierre/reporting / Accounting | accounting.policy.prepare / R-ACCOUNTING | accounting.policy.approve / R-ACCOUNTING-CONTROL |
| Fiscal / Tax | tax.policy.prepare / R-TAX | tax.policy.approve / R-TAX |
| Custodia/retención/plantillas/firma / Documents | documents.policy.prepare / R-RECORDS | documents.policy.approve / R-RECORDS, con autoridad del acto y aval profesional cuando corresponda |
| Registros societarios / Corporate | corporate.policy.prepare / R-CORPORATE | corporate.policy.approve / R-CORPORATE |
| Conexiones / Integrations | integrations.policy.prepare / R-PLATFORM | integrations.policy.approve / R-PLATFORM más aprobación empresarial del efecto |
| Continuidad/operación / Operations | operations.policy.prepare / R-PLATFORM | operations.policy.approve / R-PLATFORM por mandato operacional |
| MARKETING_CONTENT / Marketing, nuevo amendment pendiente | marketing.policy.prepare / R-MARKETING | marketing.policy.approve / R-MARKETING-APPROVE |

Descriptor estático MARKETING_CONTENT: usos/superficies editoriales, presets permitidos, requisitos de derechos y finalidades personales específicas; [contrato MC](../specs/flows/marketing-content-media-library.md#autorización-configuración-y-privacidad). Extiende explícitamente la lista finita de dueños anterior, sin familia wildcard ni grants automáticos. Cada P/contexto de Marketing referencia ese descriptor y conjuga privacy.context.prepare, marketing.policy.prepare y configuration.prepare para misma entidad/P/scope bajo A5/M25. Marketing posee revisiones/contextos; responsable acreditado decide fundamento. Cuotas/retención física/parser siguen Documents/Operations y restricciones Access. BrandKit/copy son contenido empresarial, no familia genérica que permita subir scripts. CG1–5 e ImpactManifest se aplican sin cambiar autoridad previa.

Los handlers CG1–5 se implementarán por el dueño con estos permisos; no son cinco endpoints universales que escriban sus tablas. Revisión de maestros ordinarios conserva sus comandos existentes y exige además la delegación administrativa correspondiente; introducir una regla nueva exige el contrato de política. Aprobar el gobierno de cambios/roles usa la revisión de autoridad anterior, guardas mínimas no configurables y SOD-07/08; un borrador no concede su propio permiso.

## Taxonomía, scope y precedencia

La precedencia se define por familia; nunca SYSTEM→ENTITY→SITE→WAREHOUSE→ROLE→USER para todos los valores. Scope omitido = error para dato empresarial requerido. EffectiveResolver devuelve valor **más fuente/scope/revisión/fecha/regla**; conflicto o dato ausente bloquea cálculo final. Excepción de cliente más específica solo donde Sales la define, nunca sobre escritura fiscal.

| Clase / dueño | Scopes y overrides permitidos | Vigencia / aprobación / audit / retrospectividad | Consumidor y regla de precedencia |
|---|---|---|---|
| Plataforma y secretos / Operations, Identity | SYSTEM/entorno; secretos en mecanismo externo aprobado, no DB empresarial | Despliegue/versionado; mandato técnico S; audit redactado; no reescribe negocio | Runtime toma referencia/version/hash no secreto; fallar si material no coincide. USER/ROLE no override |
| Seguridad y acceso / Access, Identity | SYSTEM fija piso; entidad restringe dentro del piso; grant por capability/recurso | Vigencias explícitas; aprobación S/SoD; audit; efecto sobre autorizaciones nuevas/privilegiadas | Intersección de restricciones obligatorias, unión por capability de concesiones; rol no baja MFA/último-admin |
| Organización / Organization | LEGAL_ENTITY/SITE, relación explícita | Maestro versionado, autoridad administrativa + organization.site.manage; sin borrado histórico | Nueva sede es maestro, no boolean; SITE no suplanta identidad legal |
| Política comercial / Sales; precios / Catalog | ENTITY; SITE o CLIENT solo si contrato tipado lo admite; moneda separada | Revisión/fechas, aprobación de dueño + delegación; audit; futura o revalida abiertos | Política global fija techo; excepción particular aprobada dentro del techo o override acotado permitido; no override USER/ROLE |
| Compras / Procurement | ENTITY/SITE/categoría contratados | Revisión, aprobador y audit; sourcing/directa/conformidad futura | Regla específica debe declarar qué hereda; si dos reglas igual prioridad aplican, conflicto y HOLD |
| Inventario / Inventory | ENTITY/pool para método; WAREHOUSE para manejo/publicación/conteo; SITE referencia | Revisión/efecto/approval; audit; sin traslado mágico ni recoste silencioso | Pool/método uniformes no override por almacén; elegibilidad almacén además respeta conexión y gates |
| Tesorería / Treasury | ENTITY/ACCOUNT_SET/fondo/instrumento/moneda | Revisión/approval S; audit; no modifica movimientos confirmados | Política cuenta puede restringir límites globales; no ampliar facultades por crear banco |
| Contabilidad / Accounting | ENTITY+libro+marco+período; nunca USER/SITE/ROLE | Efectividad aprobada, aval C01/C03; audit; ajustes/transición explícitos | Regla válida única por hecho/edición; ningún fallback a política de otra entidad |
| Fiscal / Tax | ENTITY+obligación+período+régimen/actividad | Fuente/fecha, validación C08 y aprobación; audit; período histórico intacto | Política de obligación seleccionada por hechos/regla, no preferencia ni fecha de login |
| Documentos / Documents; acto por dueño | ENTITY+clase/audiencia; ubicación física por SITE | Versionada, aprobación S para retención/firma; audit; hold prevalece sobre purga | Plazo legal aplicable/hold y mínimo aprobado no se reducen por override local; sin plazo validado no destruir |
| Requisitos de cliente / Sales | CLIENT_SITE+actividad+sujeto; fuente normativa separada | Revisión/evidencia/approval delegada; audit; revalida visitas abiertas | LAW/REGULATION obligatorios aplicables se acumulan; waiver cliente solo su MINE_POLICY/VENDOR_QUALIFICATION; INTERNAL no sustituye ley |
| Integración / Integrations con dueño del propósito | ENTITY+conexión+ambiente+propósito | Versionado/approval S/C11; audit sin credenciales; nuevos intentos | El ambiente limita efecto; la conexión no concede derecho sobre otro dueño; nuevo proveedor puede requerir adapter |
| Activación / dueño de capability | ENTITY y subset permitido explícito; entorno impone desactivación | Revisión/approval/gates/momento; audit; no reescribe hechos | Intersección de deploy compatible, feature habilitada, scope/permiso/política/gates; OFF global vence ON de cliente |
| Preferencia personal / UI, usuario | USER por entidad cuando pertinente; default SYSTEM; ROLE solo plantilla de vista opcional | Cambio inmediato/reversible; sin aprobación empresarial; audit mínimo si comparte | Valor USER explícito→default elegido de vista/rol→SYSTEM. Usuario elige una plantilla, varios roles no compiten por tema; no altera calendario fiscal/cálculos |

Nueva entidad no hereda políticas reales de otra como aprobadas: copiar produce borradores y manifiesto de procedencia. Alta de nuevo banco/almacén/cliente es maestro; el descriptor aplica la política ya conocida, no amplía automáticamente scope de grants enumerados.

## Ciclo de cambio y efectos

DomainPolicyRevision o revisión de maestro del dueño conserva ID natural, schema, entidad/scope, versión, old/new, motivo, fuente/evidencia, autor, aprobador, autoridad, valid_from/to, instante de registro, impacto y excepciones. Política actual inmutable; la interfaz crea DRAFT. Estados: DRAFT→VALIDATED→APPROVED→SCHEDULED→EFFECTIVE→SUPERSEDED; CANCELLED solo revisión no efectiva. Cambiar contenido vuelve a DRAFT e invalida aprobación/manifiesto. Activación inmediata recorre las mismas guardas sin omitir estados lógicos. Intervalos semiabiertos [from,to), zona declarada y UTC; no solapamiento por clave/scope/prioridad. No usar hora del navegador.

| Clase de efecto | Consecuencia permitida | Condición de salida |
|---|---|---|
| PREFERENCE_ONLY | Presentación personal sin cálculo/autoridad | Reversible; no afecta hechos |
| FUTURE_EFFECT_ONLY | Nuevos objetos/acciones desde fecha | Snapshots históricos permanecen |
| REVALIDATE_OPEN_OBJECTS | Previews/órdenes/visitas/mandatos abiertos se reevalúan | Antes del siguiente efecto dependiente, bloquear si revisión obsoleta |
| REBUILD_DERIVED_PROJECTION | Reconstruir vista no autoritativa con corte | Señalar desfase; nunca usar caché vieja para autorizar |
| MIGRATION_REQUIRED | Cambio excede contrato de dato/adapter | No activar desde Save; nueva spec/WO autorizada y validación posterior |
| PROHIBITED_RETROACTIVE_CHANGE | Intenta mutar hecho/posting/aprobación histórica | Rechazo; usar corrección/ajuste/transición del dueño |

Una revisión puede combinar efectos compatibles (futuro+revalidación+rebuild); son enumeraciones interpretadas por handler del dueño, no instrucciones ejecutables del usuario. Reposting no se dispara por configuración: manifiesto identifica ajuste/transición requerido y retiene activación hasta procedimiento autorizado; ninguna escritura masiva sobre todas las tablas. Rollback funcional crea una nueva revisión que restaura comportamiento admisible; historia y revisiones previas se conservan.

## Manifiesto de impacto y concurrencia

ImpactManifest sellado contiene entidad/familia/objeto, versión old/new y valores redactados, effective_from/timezone, motivo, actor, policy/source/schema, dominios/contratos consumidores y sus versiones, conjunto/corte/hash de objetos abiertos afectados, previews invalidados, jobs/intents y estado externo, reconciliación/reposting/migración requerida, efecto/retroactividad/reversibilidad, gates y evidencia, aprobadores/excepción SoD, fecha y digest. Cardinalidad grande se muestra paginada con total y snapshot; datos ocultos a un aprobador se agregan solo con permiso. Sin visibilidad suficiente, remitir a aprobador autorizado y bloquear aprobación incompleta; no revelar títulos/valores restringidos.

No basta un conteo estimado. Preparar impacto puede usar proyección para explorar; VALIDATED requiere fuentes/cortes completos o dependencia declarada NOT_READY. Antes de confirmar: descubrir todos los recursos, tomar locks comunes I0→A5 (autorización privilegiada)→K10 si conexión/publicación→M25 (policy/scope root y revisiones)→H27 si crédito→S/O30 y demás del dueño→D80/N90/J final. No holding DB durante HTTP o aprobación humana. Nuevas raíces de política usan creación bajo padre+UNIQUE y orden determinista. Un conjunto cambiado tras lock provoca rollback/redescubrimiento. Policy lock es por familia/scope, no mutex global de todas las operaciones.

Cada consumidor registra revisión de política al confirmar y revalida bajo raíz M25 pertinente. Activador toma bloqueo exclusivo; consumidor bloqueo compatible de lectura hasta su confirmación. Cambio de autorización/versión/objeto/conjunto desde preview genera STALE_IMPACT, rollback y nuevo manifiesto; no aprobar «lo que haya». Cambios de catálogo dinámico de consumidores requieren nuevo descriptor/spec, nunca consumidores desconocidos omitidos como cero. Flujos con K deben descubrirlo antes de M25; no adquirir K tras inventario.

EFFECTIVE es acto confirmado, no marca adelantada por fecha. Si una revisión SCHEDULED ya venció su fecha y no fue activada/verificada, resolver operación dependiente devuelve POLICY_ACTIVATION_PENDING; no continuar silenciosamente con política anterior. Activador revalida autorización/mandato aprobado, gates, contexto y digest a la fecha; si cambió, retiene y pide nueva revisión del impacto. Job posee mandato técnico temporal ligado a aprobación, no impersona al aprobador. Antes del envío externo se revalida epoch; intento ya enviado/UNKNOWN se concilia, no se duplica ni «desenvía». Restore con revisión/config/secret-reference incompatibles mantiene efectos bloqueados, aunque DB haya arrancado.

| Comando / clase | Capacidad y precondiciones | Efecto / compensación |
|---|---|---|
| CG1 preparar / V | configuration.prepare + permiso del dueño, delegación/familia/scope vigentes | DRAFT con razón/old/new; no cambia valor efectivo |
| CG2 validar impacto / D si conserva manifiesto | mismas lecturas autorizadas; cortes/contratos completos, schema válido | Manifest por revisión/intención; no aprobación; error deja borrador |
| CG3 aprobar/programar / V | configuration.approve + aprobación de política del dueño; S; SoD, evidencia/gates aplicables | APPROVED/SCHEDULED sobre digest exacto; no efecto económico |
| CG4 activar / D | configuration.activate + autoridad del dueño o mandato técnico de activación aprobado; orden anterior | Revisiones/epoch/audit/intenciones de invalidación atómicos; fallo no deja medio conjunto activo |
| CG5 cancelar/sustituir / V o D según efectos | autoridad actual, S si crítico, nueva evaluación | Cancela futura o crea nueva revisión; nunca DELETE de efectiva |

Audit crítico: actor real, acting roles/capabilities/grants y revisiones, entidad/recursos, old/new redactados, timestamp/effectivity, motivo, aprobación, excepción, manifiesto, correlación y fuente/evidencia. Fallo de audit revierte confirmación. Los secretos nunca entran al manifiesto, DB común o logs; clave almacenada solo mediante referencia opaca al mecanismo aprobado. Contenido sensible pegado en campo no permitido se rechaza/redacta antes de audit; no registrar payload fallido íntegro.

## Centro de Configuración y Administración

Identidad de permisos F01: emitir/revocar ConfigDelegation es concesión de Access por RA2/RA3; exige configuration.delegate sobre familia/techo AND access.admin.delegate o access.manage según acción, con aprobación/revisión/A5/SoD. CG5 conserva cancelación/sustitución de política. T-CONFIG solo puede consumir configuration.activate para CG4 bajo mandato aprobado/digest/epoch; no recibe rol humano ni capacidades de preparación/aprobación. [Registro exacto](capability-registry.md) conserva esta excepción técnica separada de los roles.

Navegación: Seguridad y acceso; Organización y maestros; Comercial y crédito; Compras e importación; Inventario; Tesorería; Contabilidad; Tributación; Documentos y sitio cliente; Integraciones; Operación y continuidad. Cada tarjeta muestra owner, entidad/scope, actual efectivo, próximo programado, readiness y acción disponible. Buscador por policy ID/nombre/dueño solo devuelve descriptores autorizados; la ausencia de permiso no filtra datos en totales.

Detalle: Actual / Propuesta / Impacto / Aprobación / Historial / Evidencia y gates. Comparación old/new, destinatarios afectados, vigencia, razón, responsable, profesional requerido y excepción visible. Editar crea borrador; botón primario cambia a Preparar, Solicitar aprobación o Activar según paso. Confirmación crítica expone qué cambiará y qué permanecerá histórico, reauth/SoD y revisión exacta. Teclado/foco/errores/preview siguen [UI](ui.md); no página de500 campos, checkbox de superadmin ni Edit sobre histórico. Read-only puede ver estado sin modificar. USER theme/locale está en Preferencias, separado de políticas.

## Crédito B2B y extensibilidad

**B2B CREDIT: CONFIRMED IMPLEMENTATION REQUIREMENT / REQUIRED TO IMPLEMENT, CONFIGURATION-CONTROLLED ACTIVATION.** Entrega acotada posterior a B2B y núcleo Treasury/exposición, antes de aceptar el incremento como completo; desactivación inicial segura no excusa omitir código en ese incremento futuro autorizado. Mantiene [CreditPolicyRevision](../specs/flows/professional-sales.md) y H27. Registro de activación expresa enabled, entidad/clientes/sitios elegibles, moneda, límite/plazo/vencimiento/aging/mora/holds/override/techo/expiración/evidencia y policy revision. OFF permite cobrar/conciliar deuda existente, bloquea nuevos compromisos/despachos que requieran crédito; cambios no extinguen deuda. Reducir límite por debajo de exposición crea HOLD a nueva exposición y reevalúa abiertos, no borra facturas ni inventa pago. Inicial prepago íntegro sigue por defecto hasta activación D03/C05/C13 y pruebas pertinentes. COD conserva diseño y decisión de activación futura; los mandatos aceptados previos no prueban que su implementación sea obligatoria. No se promueve COD por asociación.

Nuevo documento minero con significado ya previsto es RequirementProfileRevision/TemplateRevision y master data, sin migración ni rama de código por nombre. Sales conserva fuente/applicability tipada y LAW/REGULATION/MINE_POLICY/VENDOR_QUALIFICATION/INTERNAL; plantillas solo campos admitidos, no scripts. Dos minas pueden usar versiones distintas sin cambiar obligatoriedad global. Nueva potestad legal, cálculo, tipo de sujeto no representado o efecto económico exige spec/adapter/código según frontera. [Matriz de escalabilidad](../evidence/governance-roles-configuration-policies.md#z-escalabilidad) distingue estos casos, sin promesa zero-code universal.
