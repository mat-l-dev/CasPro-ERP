# Governance, roles, configuration and policies — informe A–AF

Expediente del autor, corte 2026-09-12. Amendment semántico acotado solicitado por el propietario; no barrido de producto ni aceptación independiente. Contratos en arquitectura/producto/accounting; este informe conserva la justificación, cobertura y límites del candidato. Estado autoritativo: [review](../review.md).

## A. Baseline

Verificado antes de editar: main == origin/main `17086593d28c2619fba6cca6827fd998525bb158`; tree `e24e999a3de4541c2a398b9372bf41591f9df634`; working tree limpio y ramas local/remota solo main. Rama creada `docs/governance-roles-configuration-policies`. Se conservan freeze, IA, agentes/skills, B2B/financiación y completitud profesional aceptados. A0/B16/C13/D6. IMPLEMENTATION NOT AUTHORIZED. Los expedientes anteriores no se reescriben.

## B. Benchmark externo

[GOV-S01–17 y GOV-N01/N02](../research/governance-authorization-benchmark.md) registran edición/fecha/fuente/aplicación/límite. SAP: business roles/catálogos/restricciones y actividades de customizing; Dynamics: duty/privilege/permission, scope, SoD y feature separada de permiso; NetSuite: permisos/restricciones, roles personalizables, contexto de rol y niveles de preferencia; Odoo19 soportado: ACL aditivas y reglas por grupo/global; OWASP/NIST: mínimo privilegio, autorización de servidor, cambio/impacto y recuperación. No se ejecutó tenant ni se copiaron jerarquías, Full, sudo, habilitación automática o permisos globales. SAP dinámico/Odoo apertura limitada se documentan expresamente.

## C. Gaps actuales y delta propuesto

| Fuente baseline / gap concreto | Nuevo contrato / razón | Conservado |
|---|---|---|
| tenancy-access: capabilities sin catálogo profesional exacto | roles-delegation: 21 plantillas por duties y matriz explícita | Access dueño; is_staff no negocio |
| Composición/alcance multirol poco explícitos | Unión por capability y recurso; no producto cartesiano | Entidad/recurso y guardas obligatorias |
| Administración/delegación/última ruta insuficientemente detalladas | Mandatos/techo/vigencia, A5, ancla y recuperación fuera de banda | Bootstrap cerrado; no superweb |
| Maker/checker remitido genéricamente a madurez | SoD desde M01/operación; excepción por objeto y revisión al crecer | Una persona nunca dos revisores |
| Configuration correctamente rechazada como módulo universal, UX faltante | Centro por descriptores/DTOs y comandos de dueño | Sin settings dump/DSL/propiedad duplicada |
| Cambios críticos sin contrato común de impacto/effectivity | CG1–5, manifest, clasificación de efecto y locks M25 | Hechos/versiones/CM0 y jobs del dueño |
| Políticas dispersas, estructura vs valores confundibles | POL-01–26, índice completo y readiness por hito | Dueños y gates existentes |
| NPIF catálogo representable sin manual empresarial futuro | Manual AC-01–23, decisiones A/E/S y expedientes PD-AC01–08 | Promedio uniforme/FIFO físico; validación C01–03 |
| Crédito/COD unidos en estado por trigger | Crédito requerido por nuevo mandato; COD separado | Modelo CreditPolicyRevision/H27 y prepago inicial |
| Perfil de mina extensible sin prueba explícita del nombre desconocido | Afirmación config-only para semántica existente y contraejemplo de nueva autoridad | LAW/REGULATION/MINE_POLICY/VENDOR_QUALIFICATION/INTERNAL |

## D. Modelo exacto de roles

[Modelo](../architecture/roles-delegation.md#modelo-y-composición): usuario→membership→asignación/revisión de rol→capability+scope→comando; PolicyRevision gobierna condiciones empresariales. Roles planos, versionados; custom solo subconjuntos explícitos del catálogo, sin herencia/wildcard/DSL. Modificar plantilla no amplía asignaciones ya aprobadas.

## E. Catálogo estándar

[Catálogo canónico de 21 roles](../architecture/roles-delegation.md#catálogo-estándar-y-matriz-de-capacidades), con nombre exacto/ID/duty/scopes/autoridad/MFA/self/clase. Cuatro responsabilidades administrativas se distinguen de operación: plataforma, acceso, configuración y aprobación del dominio. Ventas y compras separan preparador/aprobador; inventario separa operación/control; contabilidad prepara/controla; registros/sitio y auditoría conservan fronteras. Ningún Employee ni rol por puesto transitorio.

## F. Matriz rol/capability

El catálogo anterior, su matriz de capabilities existentes y la [matriz exacta de políticas por familia](../architecture/configuration-governance.md#capacidades-tipadas-de-política) enumeran permisos y roles. Se cotejaron identificadores publicados en las tablas de specs para no perder un comando al introducir nombres profesionales. Lectura, preparación, aprobación, export y administración no se heredan. RoleRevision no elimina capabilities existentes de confirmación. SystemPrincipal solo posee mandato técnico tipado; no entra en las 21 plantillas humanas.

## G. Scope y restricciones

Tupla de grant por entidad/capability/recurso/vigencia/mandato. ENTITY explícito o conjuntos tipados SITE/WAREHOUSE/ACCOUNT/CLIENT, casos asignados o borradores propios solo cuando el dueño lo define. Vacío/desconocido deniega. Nueva entidad no hereda políticas/grants como aprobados. Scope de conjunto no incorpora almacén futuro; ENTITY sí lo incluye deliberadamente para esa misma capability y preview lo advierte.

## H. Composición de varios roles

Unión de scopes **de la misma acción**: receive W1+W2 permite ambos, no otra entidad ni dispatch ausente. Sales.view entidad+sales.quote.prepare sitioX mantiene escritura X. Aprobar crédito/exportar/configurar exigen grants propios. Suspensión, vigencia, piso de seguridad, guardas y gates no se anulan por otro rol. Casos08–12 y41 refutan ampliaciones.

## I. Administración y delegación

[AdminDelegation/ConfigDelegation](../architecture/roles-delegation.md#delegación-y-último-administrador): grantor/beneficiario reales, mandato/techo, scope/familias/verbos, razón, evidencia, aprobación y effective_from/to. Subdelegación OFF por defecto; como máximo un nivel adicional si expresa. Concesión temporal liga descendientes; asignación permanente ordinaria no caduca por salida del otorgante. Configuración exige administrador/delegado y permiso del dueño; autoridad administrativa no confirma dinero.

## J. Lockout y recuperación

Ruta ancla no expirante por instalación/entidad, MFA y recuperación acreditados; toda pérdida de ruta, no solo borrado de rol, aplica guarda. A5 evita doble revocación concurrente. Compromiso confirmado permite suspensión por incidente fuera de banda y bloqueo web temporal; mandato de un uso, custodia independiente, re-enrolamiento y audit durable. No dos identidades falsas ni bootstrap reabierto. B02/B13 quedan pendientes de ejecución real.

## K. SoD

[SOD-01–11](../architecture/roles-delegation.md#segregación-acotada-y-arranque): banco/pago, compra/aprobación, recepción/pago, crédito, asiento/cierre, refund, concesión admin, configuración, inventario, independencia y autoridad externa. DYNAMIC permite asignación combinada pero no acto propio sin excepción; REVIEW advierte concentración; HARD no admite eludir autoridad/piso/independencia. Analizar combinación completa al asignar y al actuar.

## L. Arranque con una persona

Propietario recibe solo roles/grants expresos necesarios por incremento; no boolean mágico. SELF_APPROVAL_EXCEPTION registra persona, objeto/duties, monto/moneda/scope, motivo, aceptación del riesgo, vigencia, compensación y evidencia en cada acto. Revisión elegida cada90 días y al incorporar checker real; retirar/resolver excepción antes de activar nueva separación. Política real pendiente implica HOLD, no permiso tácito.

## M. Taxonomía de configuración

[14 clases](../architecture/configuration-governance.md#taxonomía-scope-y-precedencia) cubren plataforma, seguridad, organización, comercial/precios, compras, inventario, tesorería, contabilidad, fiscal, documentos, sitio, integración, activación y preferencias. Secretos no son valores empresariales; banco/almacén son maestros. Cada clase especifica dueño, scopes, override, fechas, aprobación/audit, efecto y consumidores.

## N. Centro de Configuración

Proyección/control de entrada por APIs del dueño; descriptores estáticos registrados, no endpoints/scripts configurables. Catálogo/búsqueda autorizados, entidad/scope, actual/próximo y readiness; detalle Actual/Propuesta/Impacto/Aprobación/Historial/Evidencia. Centro no posee payload ni estados del dominio y ningún dueño lo importa de vuelta. UX conceptual enlazada en UI, sin implementación.

## O. Precedencia

Por familia, nunca cascada universal: piso de seguridad restringe; contabilidad/fiscal no override personal/sitio; almacén gobierna manejo/publicación, no método uniforme; límite específico no amplía techo salvo override tipado permitido; USER elige preferencias visuales sobre defaults, no políticas. Resolver devuelve fuente/revisión/regla o HOLD por ausencia/conflicto. LAW/REGULATION y legal hold aplicables prevalecen sobre waiver/retención local.

## P. Ciclo de política

DRAFT→VALIDATED→APPROVED→SCHEDULED→EFFECTIVE→SUPERSEDED; CANCELLED antes de efecto. Contenido editado invalida manifest/aprobación. Activación inmediata conserva guardas; activación programada vencida y no comprobada bloquea consumidor con POLICY_ACTIVATION_PENDING. Rollback crea revisión nueva, no borra historia. Fechas, timezone y período se distinguen del momento de registro.

## Q. ImpactManifest

[Contrato](../architecture/configuration-governance.md#manifiesto-de-impacto-y-concurrencia): old/new, fuente/schema/revisión, efectiva, dominios/consumidores, corte/IDs/hash de abiertos/previews/jobs/intents, reconciliación/reposting/migración, retroactividad/reversibilidad, gates/evidencia/autoridades/digest. Seis clases de efecto desde preferencia hasta cambio retroactivo prohibido. Locks I0/A5/K10/M25/H27/S/O30 y posteriores existentes; snapshot modificado rechaza. No HTTP con transacción abierta ni efecto incierto reintentado a ciegas.

## R. Registro de políticas

[TILMUX POLICY REGISTER](../product/company-policy-register.md): todas las entradas tienen identidad, nombre, owner, propósito/scope, estado/versión/fechas, base, autoridad/aprobador, typed-policy/params, excepciones/evidencia, consumidores/gate/revisión. Estado real pendiente explícito, no campos vacíos interpretados como valores activos. Registro es índice, no motor.

## S. Inventario completo

26 agrupaciones: acceso; delegación/recuperación; SoD; configuración; maestros; cotización/precio/descuento/margen; contratos/instalación; crédito/cobranzas/COD; reclamo/devolución/refund; procurement/RFQ/directa; proveedor/banco; inventario/almacén/traslado; conteo/costo; Treasury/pagos; tarjetas; préstamos/financiación; caja chica; manual; cierre/EEFF; Tax; archivo/retención/firma; continuidad; integración; importación; Corporate/sitio; IA si se activa. No 39 documentos separados por cada función.

## T. Readiness contable

[Manual AC-01–23](../accounting/tilmux-policy-manual.md): reglas normativamente determinadas y elecciones aceptadas preservadas; ocho expedientes concretos para marco/apertura, inventarios, ingresos/anticipos, cartera, PPE, contratos/FX, juicios/cierre, presentación/notas. Promedio uniforme/FIFO físico, cuatro EEFF/EFE directo; sin tasa de guía, IAS8/NIIF16/NIIF15 o fiscalidad trasplantada por defecto. Elegibilidad real no presumida. C01–03/C08 conservan validación profesional.

## U. Readiness empresarial

[Matriz por hito](../product/company-policy-register.md#readiness-de-políticas): estructura Access/config/continuidad M01; maestros M02; inventario/costo/dinero M03; comercial M04/B2B; crédito en su incremento requerido; compras/importación M05; Treasury/instrumentos M06; manual/cierre M07; EEFF M08; Tax salidas M09, obligaciones antes del hecho dependiente. Valores reales no bloquean hitos no relacionados.

## V. ASTRA-RESOLVED DECISIONS

La delegación amplia de diseño del propietario ya se ejerció; estas decisiones no se devuelven como preguntas. A/E/S son las clases definidas en el registro; OWNER-DELEGATED DECISION significa decisión de diseño por delegación, no aprobación de un dato real desconocido.

| Decisión | Rationale / fuente | Reversibilidad / condición de activación |
|---|---|---|
| AD-01 21 roles planos por duties, sin jerarquía arbitraria / E | GOV-S01/04/09 y Access; cubre responsabilidades sin rol por título | Nueva RoleRevision explícita, reasignación/preview; B02/C13 |
| AD-02 Unión por capability y scope, sin READ→WRITE/APPROVE/EXPORT / E | GOV-S05/08/12/14; elimina ampliación cartesiana | Cambiar semántica exige amendment, no setting; B02/B03 |
| AD-03 Separar plataforma, acceso, configuración y autoridad del dominio / E | GOV-S04/07/14; poseer credencial/admin no aprueba negocio | Mandatos pueden reasignarse con revisión; B02/C13 |
| AD-04 Subdelegación OFF y un nivel adicional máximo si expresa / S | Mínimo privilegio GOV-S14, tamaño CasPro; evita cadenas opacas | Nueva revisión/preview dentro del modelo; C13 |
| AD-05 MFA humano, step-up ligado a intención de5 minutos para crítico / S | GOV-S15; ventana elegida aquí, no norma del proveedor | Ventana solo por revisión de seguridad sin bajar piso; B01/B02/C10/C13 |
| AD-06 Última ruta ancla y recuperación fuera de banda de un uso / E/S | GOV-S17 + M01; resiste pérdida/compromiso sin cuenta oculta | Cambio operacional ensayado; ancla no se retira sin reemplazo; B13/C10 |
| AD-07 SoD dinámica y excepción honesta por objeto; revisión90 días/al crecer / E/S | GOV-S06/16 y realidad startup autorizada | Excepción caduca/se retira; historia intacta; política real/compensación C04/C13 |
| AD-08 Centro router y políticas tipadas por dueño / E | Boundaries, GOV-S03/11/16; UX central sin propiedad universal | Añadir descriptor válido; significado nuevo requiere spec; B01/B02 |
| AD-09 Lifecycle/manifest/seis efectos, historia inmutable / E/S | CM0 y GOV-S16; previene Save reinterpretando todo | Rollback mediante revisión nueva; B03/B10/B13 |
| AD-10 Sin política/alcance/evidencia necesaria: HOLD; no defaults monetarios inventados / S | Contratos CasPro, mínimo privilegio | Valores aprobados sustituyen ausencia, no hechos; gates del dueño |
| AD-11 Registro en26 grupos y readiness por último hito responsable / E | Ownership + fuentes ERP; evita dependencia M01 de todos los valores | Índice extensible sin nuevo motor; políticas antes de su hecho real |
| AD-12 Preservar promedio uniforme/FIFO físico y cuatro EEFF/EFE directo / E, OWNER-DELEGATED DECISION ya aceptada | NPIF/catálogo y review; no reabrir método ni pedir nombres al owner | Método/pool exige amendment/transición, no override; C01/C03/C08 |
| AD-13 B2B crédito obligatorio, inicialmente OFF; COD separado / autoridad del encargo + S | Mandato actual cambia prioridad, modelo previo aceptado | OFF reversible tras POL-08/permisos/pruebas/D03; deuda histórica no desaparece |
| AD-14 Requisito minero con nombre nuevo y semántica existente = configuración/maestro / E | ClientSiteProfile aceptado; no rama por nombre | Nueva revisión conserva fuente/plantilla/visitas; semántica nueva requiere spec |
| AD-15 IA/integraciones con mandato técnico, nunca rol humano / E/S | ADR-011/CM0/GOV-S14; ejecutar entrega no ser aprobador | Revocación/epoch y UNKNOWN; D01/B12/B16/C11 según efecto |
| AD-16 Sin retención validada/hold resuelto no purga automática / A/S | Contrato HP5/C10; ley no es preferencia del usuario | Política legalmente validada y autorización de destrucción, no simple fecha pasada |

## W. OWNER DECISIONS REQUIRED

**Ninguna pregunta inmediata necesaria para cerrar esta propuesta.** [OD-01–05](../product/company-policy-register.md#owner-decisions-required) agrupan titulares/custodia, riesgo comercial, límites de compra/pago, hechos maestros/cuentas y continuidad/retención adicional. Cada una tiene pregunta, por qué investigación no decide, recomendación, A/B/consecuencias, deferibilidad y default delegado. No se inventan personas, montos ni hechos; la activación correspondiente espera. Los ocho expedientes profesionales son aplicación a hechos/estimaciones, no preguntas de ley al propietario.

## X. Corrección de roadmap B2B crédito

Charter/program/capabilities/gaps/review/Sales/CM0 distinguen **REQUIRED TO IMPLEMENT** de activación inicial DISABLED y D03. Incremento posterior B2B+Treasury base/exposición, salida futura con capability y pruebas; no “quizá construir M10”. No cambia CreditPolicyRevision/H27 ni activa operación. COD no fue confirmado requerido por evidencia previa suministrada: no inferencia por asociación. No nuevo gate.

## Y. Escalabilidad minera

Caso de aceptación: documento de nombre desconocido para empresa/persona/equipo/vehículo/tarea, con campos tipados existentes, fuente/aplicabilidad/template/vigencia/evidencia/estado. Resultado de diseño: configuración/maestros, sin migración/código. Cambiar formato/version por mina no altera otras minas; waiver solo fuente cliente. Nuevo workflow, potestad o efecto económico exige spec: extensibilidad no equivale a zero-code universal. Es resultado de inspección contractual, no prueba de UI ejecutada.

## Z. Escalabilidad

Clasificación del cambio concreto dentro de contratos conocidos; la segunda alternativa marca la frontera. CONFIGURATION ONLY conserva semántica y autorización; NEW POLICY REVISION incluye ciclo de cambio, no edición libre.

| Área | Variación prevista / clasificación | Frontera y motivo |
|---|---|---|
| Roles/usuarios | Asignar plantilla/subconjunto/scope conocido: CONFIGURATION ONLY | Nuevo permiso de negocio: NEW SPEC REQUIRED + CODE CHANGE EXPECTED; no crear poder con texto |
| Sedes | Alta/estado/dirección por entidad: MASTER DATA ONLY | Nueva entidad/autoridad legal no hereda aprobación; expansión de contrato requiere spec |
| Almacenes | Alta con capacidades conocidas: MASTER DATA ONLY; manejo/publicación: NEW POLICY REVISION | No stock por alta, no nuevo grant implícito; nuevo tipo de custodia exige spec |
| Atributos de producto | Atributo de tipo admitido/unidad/validación: MASTER DATA ONLY | Cálculo/relación ejecutable nuevos: NEW SPEC REQUIRED + CODE CHANGE EXPECTED |
| Tipos documentales | Clase con custodia/evidencia conocida: MASTER DATA ONLY | Nuevo efecto legal/fiscal/autorización no nace del nombre: NEW SPEC REQUIRED |
| Templates | TemplateRevision con slots admitidos: CONFIGURATION ONLY | Campo con fuente nueva/cálculo no disponible: NEW SPEC REQUIRED; script arbitrario prohibido |
| Proveedor de firma | Nueva conexión a adapter ya soportado: CONFIGURATION ONLY | Protocolo/verificación diferentes: NEW ADAPTER + CODE CHANGE EXPECTED y validación legal/técnica |
| Proveedor de email | Cambiar conexión soportada: CONFIGURATION ONLY | Proveedor nuevo: NEW ADAPTER + CODE CHANGE EXPECTED; no reescribir Sales |
| Política de ventas | Límites/vigencia/cláusulas dentro de contrato: NEW POLICY REVISION | Nuevo modelo de venta o servicio independiente: NEW SPEC REQUIRED |
| Política de crédito | Límite/plazo/eligibilidad/holds/feature: NEW POLICY REVISION | Nueva medición de riesgo/compromiso no representada: NEW SPEC REQUIRED; OFF no omite entrega requerida |
| Política de compras | Bandas/tolerancias/aprobadores/criterios existentes: NEW POLICY REVISION | Workflow/efecto no definido: NEW SPEC REQUIRED, no motor universal |
| Evaluación de proveedor | Criterios/pesos/tipos de evidencia ya previstos: NEW POLICY REVISION; perfil: MASTER DATA ONLY | Algoritmo/potestad nueva: NEW SPEC REQUIRED + CODE CHANGE EXPECTED |
| Cuentas financieras | Alta de tipo admitido por entidad/moneda: MASTER DATA ONLY | Nuevo instrumento con efectos distintos: NEW SPEC REQUIRED |
| Bancos | Identidad/cuenta: MASTER DATA ONLY | Nuevo layout/API bancario: NEW ADAPTER + CODE CHANGE EXPECTED; no promesa API por alta |
| Tarjetas | Contrato/cupo/ciclo/titular conocido: MASTER DATA ONLY + NEW POLICY REVISION | Producto/cálculo financiero no representado: NEW SPEC REQUIRED |
| Préstamos | Acuerdo/cronograma dentro de modelo: MASTER DATA ONLY + NEW POLICY REVISION | Nuevo tratamiento económico/fiscal: NEW SPEC REQUIRED; C06 no se salta |
| Obligaciones Tax | Perfil/período de obligación tipada ya soportada: NEW POLICY REVISION | Nueva obligación/base/layout: NEW SPEC REQUIRED + CODE CHANGE EXPECTED; fuente profesional primero |
| FX fuentes/propósitos | Selección de fuente/propósito admitido: NEW POLICY REVISION | Nuevo protocolo: NEW ADAPTER; nueva base de conversión: NEW SPEC REQUIRED |
| Mina/sitio | Requisito/template conocido por fuente: NEW POLICY REVISION + MASTER DATA ONLY | Autoridad/sujeto/efecto nuevo: NEW SPEC REQUIRED; no regla legal universal por nombre |
| Políticas contables | Elección/estimación tipada validada: NEW POLICY REVISION | Marco/método/pool/regla no prevista: NEW SPEC REQUIRED + CODE CHANGE EXPECTED; no recálculo histórico automático |
| Conexiones de integración | Instancia soportada/mandato/entorno: CONFIGURATION ONLY | Protocolo/evento distinto: NEW ADAPTER, o NEW SPEC REQUIRED si cambia hecho/autoridad |

## AA. Casos adversariales documentales

48 casos examinados por lectura contra contratos; **PASS documental de cobertura**, no tests de CasPro ejecutados. RA = roles/delegación; CG = configuración; PR = registro; AC = manual. Resultado esperado es criterio para evidencia futura B/C pertinente. Los casos01–40 corresponden en orden a los40 requeridos por el encargo.

| Caso | Estímulo / contrato | Resultado esperado y razón verificable |
|---|---|---|
| 01 | Propietario concentra todos los roles / RA startup | Asignaciones expresas, solo funciones entregadas; acto propio conserva SELF_APPROVAL_EXCEPTION, no dos personas |
| 02 | Personal futuro recibe almacén / RA catálogo | R-WAREHOUSE+W1 no concede pago/precio/admin ni otro almacén |
| 03 | Contador lee dinero / RA catálogo | treasury.view autorizado; access.manage ausente, deniega modificación de acceso |
| 04 | R-CONFIG intenta pago / CG autoridad | configuration.activate no treasury.money.confirm; denegado |
| 05 | Aprobador de pago intenta concederse admin / RA mandato | Sin mandato delegable access no puede elevarse; tener dinero no administra roles |
| 06 | Último admin retira su acceso / RA última ruta | Guarda A5 rechaza si no hay reemplazo habilitado verificado |
| 07 | Último admin comprometido / RA incidente | Suspensión fuera de banda, web bloqueada y recuperación auditada de un uso; no retener cuenta comprometida |
| 08 | Rol nuevo expande scope / RA composición | Preview muestra unión por cada capability/ENTITY futuro; rechazo sin revisión/aprobación |
| 09 | W1+W2 con solapamiento / RA composición | Unión idempotente, sin doble efecto ni permiso sobre W3 |
| 10 | Leer entidad+preparar cotización soloX / RA composición | Lectura amplia; preparación soloX; no uso del scope de lectura para escritura |
| 11 | Revocar durante operación / RA revocación | Operación ordinaria corta ya autorizada puede terminar; efecto privilegiado revalida A5; siguientes deniegan |
| 12 | Rol cambiado después de preview / RA/CG | Confirmación revalida epoch/mandato/revisión, no usa foto previa como autoridad |
| 13 | Worker recibe rol humano / RA principal | Tipo incompatible rechaza; solo mandato técnico de propósito/efecto aprobado |
| 14 | Descuento cambia mañana / CG fechas | Vieja revisión hoy; nueva desde activación válida; cotización aceptada preservada, previews abiertos se revalidan según efecto |
| 15 | Límite baja bajo exposición / CG crédito | HOLD nueva exposición y revalidar abiertos; no borrar factura ni fabricar cobro |
| 16 | Crédito construido pero global OFF / CG feature | Ningún ON por cliente ni rol lo supera; no despacho con nueva exposición |
| 17 | ON solo scope aprobado / CG feature | Conjunción global/cliente/moneda/política/permiso/gates; otros clientes siguen OFF |
| 18 | Política contable próximo ejercicio / CG/AC | Revisión SCHEDULED; período actual conserva fuente; fecha vencida sin validación retiene |
| 19 | Cambiar política después de cierre / AC/CG | No reinterpreta posting; ajuste/transición/reapertura autorizados según caso |
| 20 | Régimen fiscal cambia próximo período / CG Tax | Selección por obligación/período/hechos/fuente; no cambia cálculo del pasado ni por login |
| 21 | Editar revisión histórica / CG lifecycle | Rechazo; nueva revisión con old/new/motivo; sin DELETE de efectiva |
| 22 | Preferencia usuario cambia método contable / CG precedencia | Campo fuera de clase; deniega, no override por USER |
| 23 | Secreto en configuración ordinaria / CG audit | Campo no permitido rechaza/redacta antes de log; solo referencia al mecanismo secreto |
| 24 | Reducir retención con legal hold / CG Documents | Hold bloquea destrucción; nueva política no dispensa conservación |
| 25 | Nuevo documento minero nombre desconocido / sitio | Tipo/aplicabilidad existente: configurar revisión/maestro; sin migración/código |
| 26 | Otra mina usa versión distinta / sitio | TemplateRevision por sitio y vigencia, no reemplazo global ni invalidez automática de otra mina |
| 27 | Mina dispensa requisito que también es ley / sitio | Waiver afecta su fuente cliente; LAW/REGULATION aplicable sigue obligatorio |
| 28 | Nuevo almacén / CG maestros | Alta no crea stock ni se añade a WAREHOUSE_SET; ENTITY deliberado conserva su significado |
| 29 | Nuevo banco / matriz Z | Maestro si significado conocido; formato/API nuevo necesita adapter, no campo que finja integración |
| 30 | Nuevo email provider / CG Integrations | Adapter/contrato Documents; Sales conserva comando y negocio; C11/B12 antes de efecto |
| 31 | Cambia policy con job pendiente / CG epochs | Revisar mandato/revisión antes de ejecutar; UNKNOWN se concilia, no segundo envío |
| 32 | Confirmar preview config obsoleto / CG manifest | STALE_IMPACT y rollback; nuevo snapshot/aprobación necesarios |
| 33 | Cambio exige migración / CG efecto | MIGRATION_REQUIRED bloquea activar desde Save; spec y ejecución futura autorizadas |
| 34 | Cambio declara retroactividad sobre hechos / CG efecto | PROHIBITED_RETROACTIVE_CHANGE; corrección explícita del dueño, no edición masiva |
| 35 | Autoaprobación al inicio / RA SoD | Solo política/objeto/límite/fecha permitidos y rastro de misma persona; no excepción tácita |
| 36 | Mismo acto tras crecer personal / RA SoD | Resolver/retirar excepción afectada antes de activar checker; dos personas reales cuando política lo exige |
| 37 | Delegación con fecha fin / RA vigencia | Expira al autorizar, no necesita esperar scheduler; descendientes temporales limitados |
| 38 | Delegado vencido cambia config / CG/RA | Denegado aunque sesión válida y UI vieja; epoch/fecha actual |
| 39 | Dos admins cambian misma política / CG M25 | Serialización por familia/scope; segunda revisión/digest obsoletos rechazan, sin último-write-wins |
| 40 | Restore DB con configuración equivocada / CG/M01 | Efectos bloqueados hasta cotejar manifest/revisiones/secret refs; DB arrancada no PASS |
| 41 | Cap A/W1 + cap B/W2 / RA unión | Nunca autoriza A/W2 por mezclar scopes; prueba contra producto cartesiano |
| 42 | Dos admins se revocan a la vez / RA A5 | Última ruta serializada; segundo cambio que dejaría cero falla; audit y epoch atómicos |
| 43 | Política nueva se concede su propia aprobación / CG autoridad | Evaluar autoridad anterior/piso; borrador no puede aprobarse usando facultad propuesta |
| 44 | Activación programada retrasada y consumidor llega / CG resolver | POLICY_ACTIVATION_PENDING, no utilizar política vieja como si no hubiera vencido la programación |
| 45 | Admin configura Accounting sin capability del dueño / CG AND | Deniega; administrador más authority contable/profesional requerido, no OR |
| 46 | Nombre de formulario incorpora nueva potestad o efecto / sitio | Sale de semántica existente: NEW SPEC REQUIRED; no esconder workflow en atributo |
| 47 | Revocar ancestro temporal vs salir grantor permanente / RA mandato | Descendiente temporal pierde vigencia; asignación permanente aprobada no se borra por cese del otorgante |
| 48 | Fallo audit al conceder o activar / RA/CG atomicidad | Rollback de concesión/revisión/epoch/intención, ninguna aprobación parcial ni secreto en registro de fallo |

## AB. Roadmap y gates

No IDs nuevos ni gates cerrados: A0/B16/C13/D6. B01 compatibilidad de mecanismos; B02 roles/scopes/mandatos/MFA; B03 concurrencia A5/M25/H27; B09 UX centro; B10 preview/secretos; B13 recuperación/config. B04–08/B11–12/B16 se aplican al consumidor correspondiente, no se acreditan por este informe. C01/C03 manual/costo; C04 compras/SoD; C05 cuentas/dinero; C06–09 profesionales; C10 continuidad/retención; C13 personas/maestros/autoridades. D03 retiene activación del crédito requerido y triggers separados. [Programa](../roadmap/program.md) y [registro de gaps](../roadmap/decisions-gaps.md) poseen plazo/estado.

## AC. Archivos canónicos y delta

Seis archivos nuevos: [roles](../architecture/roles-delegation.md), [configuración](../architecture/configuration-governance.md), [registro](../product/company-policy-register.md), [manual](../accounting/tilmux-policy-manual.md), [research](../research/governance-authorization-benchmark.md) y este informe. Sin duplicar carpetas/módulos. Sincronización breve en review; architecture tenancy-access/boundaries/UI; product charter; roadmap program/capabilities/decisions-gaps; NPIF catálogo; runtime-masters; CM0/economic-facts; Sales y records/site; índices general/specs/research/evidence. Diff de la rama es inventario exacto; ningún código, WO ni evidencia histórica editada.

## AD. Commits y candidato

Primer commit de fuentes: `7c1ca7ce6edea2166ee33e6cdc7304f6f24a1e3a`, tree `1ff27e78ea0041f790eb30b2c82d8f2bf2b08fec`. Segundo commit reúne contratos/cobertura/sincronización sobre baseline A; identidad final commit/tree se publica en cuerpo del PR y entrega final. El propio archivo no intenta almacenar su hash autorreferente. `git log main..HEAD` identifica los commits de esta rama; la base de comparación es el baseline completo de A, no un branch móvil externo.

## AE. PR y revisión

PR contra main, rama `docs/governance-roles-configuration-policies`, título **Specify roles, configuration governance and company policies**. Debe permanecer **OPEN**, sin merge. Reviewer independiente evalúa candidato exacto y este delta semántico; se entregan fuentes/contratos/casos y validación estática. Aprobaciones reales y pruebas ejecutables siguen abiertas. URL/head/tree finales en entrega y cuerpo del PR.

## AF. Veredicto y límites

**PASS — GOVERNANCE / ROLES / CONFIGURATION / POLICIES AMENDMENT READY FOR INDEPENDENT REVIEW**, veredicto del autor. Cobertura documental: catálogo/matriz/scopes/delegación/SoD/recuperación, configuración/manifest/policies/readiness, crédito obligatorio, escalabilidad minera y48 casos; no bloqueador de diseño que requiera pregunta inmediata. Revisión independiente pendiente; no autoaceptación ni evidencia ejecutable.

Validación de entrega **PASS estático**: 24 archivos del alcance; 121 referencias locales/anclas añadidas o tocadas; 17 tablas nuevas coherentes; IDs únicos/contados de21 roles,26 políticas,23 temas contables,8 expedientes profesionales,5 decisiones futuras,48 casos y32 secciones A–AF. Cotejo de122 identificadores de capability de tablas de specs, sin faltantes en catálogo/matrices. B16/C13/D6 conservan exactamente sus IDs; A0 sin bloqueador nuevo identificado. Búsqueda acotada de modalidad/estado actual: sin crédito opcional/diferido M10 ni PR #6 esperando merge; expedientes históricos preservados. Revisión de dueños/consumidores/orden y `git diff --check` satisfactorias. No tests/builds/Docker, código, migraciones, WOs, datos privados ni runtime. **IMPLEMENTATION: NOT AUTHORIZED.** Próxima acción: revisión independiente de esta enmienda; merge y WOs solo en sus futuras misiones autorizadas.
