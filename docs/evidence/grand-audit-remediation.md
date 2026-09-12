# Grand audit — remediación documental F01–F07

Corte:2026-09-12. Autor de correcciones, **no reviewer independiente del candidato**. Estado de cada hallazgo: FIXED_PENDING_INDEPENDENT_REVIEW. Alcance autorizado: solo Markdown, fuentes oficiales, estática, commits/push y un PR abierto; ninguna implementación, test, build, Docker, WO, dato real, proveedor, envío operativo o merge.

## Baseline e identidad

Auditoría original: **REQUEST CHANGES — DOCUMENTARY/ARCHITECTURAL DEFECTS FOUND**, sobre main post-PR7 `114275e7567ea2ace203e76e18426554ecc42a7e`, tree `c69d08ffb9d0cf50497d53c3894692f29979d993`. F01/F02 P1; F03/F04/F05 P2; F06/F07 P3; ningún P0 ni fundamento para reescribir arquitectura. A3/B16/C13/D6 era propuesta del grand audit, distinta de A0 histórico del freeze.

Al recibir remediación: checkout limpio `e7e43fbdec3b84a3af14310d555cfd4b4198f949`, mismo tree `c69d08ffb9d0cf50497d53c3894692f29979d993`; main local estaba en1708659. Fetch y fast-forward seguro a114275e; rama nueva única `docs/grand-audit-remediation`. PR7 ya fusionado; no se modifica ni reabre. El informe original de conversación no se había guardado como archivo del repositorio: este registro conserva hallazgos, no reconstruye retrospectivamente todo el audit. Evidencia histórica preexistente intacta; su aceptación no se reasigna al candidato.

## Trazabilidad por hallazgo

| ID / original y causa | Corrección y archivos canónicos | Fuente, contraejemplo y criterio de cierre candidato | Gate restante / estado |
|---|---|---|---|
| F01 P1 — roles: conexión plural con ID diferente de C01; C24–26 pedían IDs sin elegibilidad; deberes nuevos coexistían con comandos sin mapa exacto | [Registro](../architecture/capability-registry.md), [roles](../architecture/roles-delegation.md), [configuración](../architecture/configuration-governance.md), [CM0](../specs/cross-cutting/command-matrix.md), [A02/A03/A07](../specs/milestones/accounting-deep.md), [policy register](../product/company-policy-register.md). Cuatro IDs consolidados, paths import/report/reconcile/replay, duties/confirmación separadas y excepciones técnicas explícitas | Baseline git114275e y consumidores locales, no analogía por nombre. C01 no reconoce antiguo ID; import no evade participantes, shadow no postea oficial. Cada ID tiene elegibilidad/scope/consumidor y conjunción; desconocido/wildcard deniega | B02/B03 y C13; runtime/grants no probados. FIXED_PENDING_INDEPENDENT_REVIEW |
| F02 P1 — threat-model cubría minimización, incidentes dinero/credenciales y salud sitio, sin rights/decision lifecycle ni reconciliación post-backup | [Ciclo mínimo](../security/personal-data-lifecycle.md), [amenazas](../security/threat-model.md), [delivery](../operations/delivery.md), siete IDs en registro. Finalidad/contexto/restricción/solicitud/incidente con dueño, transiciones, permisos, decisión y cierre | [Ley29733/DS016](../research/normative/privacy-current-review.md). Solicitud de supresión no borra ledger; backup antiguo no reexpone; notificación por supuestos, no48 universal. Diario posterior fuera del rollback y lectura normal OFF hasta manifiesto completo | B02/B10/B13/B15, C06/C10/C11/C13. Diseño completo candidato; política/producción no aprobadas. FIXED_PENDING_INDEPENDENT_REVIEW |
| F03 P2 — automation asignaba SiteForm a Operations, Email a Communications/Documents y Report a Reporting; contrato sitio daba requisito a Sales y representación a Documents | [Familias](../architecture/automation.md), [records/site packs](../specs/flows/records-signatures-site-packs.md): contenido/aplicabilidad del dueño, representación/version/render Documents, captura consumidor, entrega separada; plantilla contable sigue Accounting | Contratos de dominios existentes. Cambiar layout no decide requisito, fórmula fiscal, permiso de envío ni muta firmado. Los cinco ejemplos tienen responsabilidades inequívocas, sin módulo nuevo | Ensayos pertinentes B08/B10/B15 y política real C10/C13; FIXED_PENDING_INDEPENDENT_REVIEW |
| F04 P2 — riesgo de ingeniería/proveedor documentado sin evaluación específica Ley31814/DS115 por propósito | [IA canónica](../architecture/ai-assistance.md), [research y matriz](../research/normative/ai-peru-applicability.md): registro por finalidad con autoridad/inputs/outputs/personas/impacto, clasificación razonada, plazo y controls/gates | Fuentes oficiales del memo. Monto contable no implica alto riesgo automáticamente; click no sanea prohibición; público/privado y evaluación voluntaria distintos. DeepSeek inicial preservado | D01/B16/C06/C10/C11/C13 y C08 para Tax; fecha general expresada con fórmula legal, sector/tamaño reales pendientes. FIXED_PENDING_INDEPENDENT_REVIEW |
| F05 P2 — total18 correcto, omisión de transición de componentes2026–2029 | [Research](../research/normative/igv-ipm-transition.md), [Tax regla versionada](../specs/milestones/tax-deep.md): componentes solo para consumidor que los exige, por hecho/fecha legal/entidad/fuente; G1 intacto | SUNAT PDF art.17 y orientación actual. Contraste con HTML antiguo y lectura parcial Congreso explícitos. Misma base/total, split diferente al cruzar2027; corrección histórica conserva norma del hecho | B04/B08/B14 y C07/C08; sin cálculo runtime ni política real. FIXED_PENDING_INDEPENDENT_REVIEW |
| F06 P3 — DH4 CPE citaba N009, que es NIC21; enlace resolvía pero significado no | [Gaps DH4](../roadmap/decisions-gaps.md#dh4), registro normativo suplemento: N020/N023/N037 existentes | [Registro](../research/normative/normative-register.md), N020 CPE, N023 oportunidad y N037 evidencia CPE. NIC21 no se renumera; revisión de ocurrencias separa mención correctiva de uso incorrecto | C07/C08 aplicabilidad real; FIXED_PENDING_INDEPENDENT_REVIEW |
| F07 P3 — review decía actualizar PR7 OPEN; D generalizaba opcionalidad; ADR11 mezclaba tooling/runtime | [Review](../review.md), [gaps](../roadmap/decisions-gaps.md), [ADR11](../decisions/adr-011-ai.md): merge y mandato actual; D01/D03 mixtos; DeepSeek runtime seleccionado, tooling provisional | Git/main y aclaraciones explícitas del propietario. No convertir todo PROVISIONAL en ACCEPTED ni reescribir evidencia. Búsqueda histórica canónica no encontró afirmación CasPro eliminado/recreado que deba corregirse | Revisión independiente del candidato y gates intactos; FIXED_PENDING_INDEPENDENT_REVIEW |

## F01 — método y resultados

Barrido de todos los Markdown canónicos de architecture/specs/accounting/tax/corporate/domain/operations/security/product; no solo C01/import. Extracción de namespaces explícitos (access,identity,organization,parties,catalog,inventory,procurement,sales,treasury,accounting,tax,corporate,documents,integration,integrations,operations,configuration,automation,case_flow,shadow,ai,audit,imports,reports,support,policy,privacy), deduplicación literal, exclusión de extensiones .md, conciliación contra tablas de roles/políticas y consumidores. Expansión semántica de abreviaturas prepare/approve, intake/respond y view/snapshot; negaciones no cuentan como concesión. Revisión de significado tras barrido: no basta coincidencia de tokens o link válido.

| Conteo | Resultado y definición |
|---|---|
| Universo lexical baseline | 251 IDs distintos; incluye los4 posteriormente retirados; reports.snapshot estaba abreviado |
| Activos exactos finales | 255:251−4+1 explicitado+7 privacidad |
| Elegibles humanos | 250; plantillas/mandatos candidatos, cero asignaciones reales |
| Exclusivamente técnicos | 5: integration.receive, integration.process, shadow.interpret, shadow.post, shadow.correct |
| Compartidos con excepción técnica explícita | 3: integration.reconcile, accounting.post, configuration.activate; jamás herencia por rol humano |
| Elegibles técnicos totales | 8; seis clases de principal con techo documentado |
| IDs exactos en fichas/tablas de comando identificadas por ID | 134 en123 filas; se extrae capability de acción/columna de guardas, expandiendo abreviaturas contra catálogo |
| IDs literales referidos por specs, incluyendo prosa | 140; no es otro catálogo ni conteo de endpoints. Registro también cubre lecturas, duties y política fuera de esas tablas |
| Sin resolución / sin consumidor documentado / filas activas duplicadas | 0 / 0 / 0; revisión documental del autor, no ejecución de guards |

Retirados sin aliases runtime: integrations.connection.manage→integration.manage_connection; accounting.journal.prepare→accounting.prepare; accounting.period.reopen→accounting.reopen; accounting.report.approve→accounting.approve_reports. Quedan únicamente en tabla explícita de retirada y este historial. No se migraron grants ni se permite aceptar ambos nombres por fallback.

La elegibilidad de R-PLATFORM para conexión/reconcile/replay no le da inventory.view: C05 humano reúne además concesión del rol de Inventory para los mismos recursos. imports.confirm requiere permisos/decisiones de cada dueño; reports.snapshot añade view/fuentes/export. Tax TX5 y X05 no son alias; preservan captura histórica y registro de constancia respectivamente. ConfigDelegation usa RA2/RA3 con conjunción; CG5 cancela/sustituye política. T-CONFIG activa digest autorizado, sin aprobarlo. Estas distinciones fueron revisadas contra las fichas, además del conteo.

## Fuentes y límites de investigación

[Privacidad Perú](../research/normative/privacy-current-review.md), [IA Perú](../research/normative/ai-peru-applicability.md) e [IGV/IPM](../research/normative/igv-ipm-transition.md) son el registro acotado de URLs, artículos, publicación/vigencia, inferencias y límites. Fuente legal primaria leída: DS016 oficial Congreso y DS115 El Peruano; SUNAT PDF art.17 reproduce Ley32387 y transición, orientación confirma componentes. Ley31814 texto oficial indexado/objeto y autoridad corroborados por DS115; descarga íntegra Congreso falló. Ley32387 consolidada localizada/indexada pero descarga íntegra falló: no se atribuye lectura completa ni se funda el split en reproducción municipal. SUNAT HTML histórico discrepa por desactualización; se conserva como discrepancia, no norma actual. RM152/ENIA no se aplica como obligación pública universal a privados.

No se resolvieron hechos empresariales reales ni términos privados de proveedor. Activación exige revisión vigente de norma/sector/tamaño, responsable, categorías/finalidades, banco, custodios, encargados/país/DPA, plazos/hold y controles demostrados. Cero preguntas inmediatas al propietario.

## Recomputación A/B/C/D

**A0 / B16 / C13 / D6**, evaluación del autor pendiente de re-revisión. F01 tiene identidad/scope/elegibilidad/consumidores; F02 tiene dueños/estados/decisión/autorización/retención/restore; F03 tiene responsabilidades separadas. No se difiere ninguna de esas decisiones a pruebas. F04/F05 ahora disponen fuente/criterio/aplicabilidad/versión y salida segura; hechos reales se resuelven en gates existentes. F06/F07 no justifican A nuevo. Se contaron16 filas B01–B16,13 C01–C13 y6 D01–D06 en las tablas propietarias, no cada mención en suplementos.

[Extensión de criterios](../roadmap/decisions-gaps.md#recomputación-candidata-f01f07) precisa quién valida, evidencia/momento y respuesta segura. Ningún B/C/D cerrado; D01 construcción IA/shadow confirmada y D03 crédito requerido se distinguen de activación y funciones opcionales. No producción ni implementación autorizadas. Una revisión independiente puede refutar estos cierres: el autor no los presenta como aceptados.

## Rechecks adversariales

Evaluación **documental** del autor: cada fila inspecciona la regla/contraejemplo y su salida requerida. Los67 resultan coherentes en el candidato; no son67 tests ejecutados ni prueba de runtime. Las referencias agrupan el contrato propietario de cada caso.

| Nº | Caso | Resultado documental / comportamiento requerido | Contrato |
|---:|---|---|---|
| 1 | Conexión ID | COHERENTE: integration.manage_connection único; antiguo retirado, sin alias. | [Fuente](../architecture/capability-registry.md) |
| 2 | imports.prepare | COHERENTE: R-MASTER o concesión de lote a rol participante, AND lecturas. | [Fuente](../architecture/capability-registry.md) |
| 3 | imports.confirm | COHERENTE: Elegible no basta: exige efecto/aprobación de cada dueño C25. | [Fuente](../architecture/capability-registry.md) |
| 4 | reports.view | COHERENTE: Rol operativo/auditor por informe y fuentes autorizadas. | [Fuente](../architecture/capability-registry.md) |
| 5 | reports.snapshot | COHERENTE: ID completo; AND reports.view y export cuando salga de vista. | [Fuente](../architecture/capability-registry.md) |
| 6 | Accounting prepare | COHERENTE: accounting.prepare consolidado; aprobación y post siguen distintos. | [Fuente](../architecture/capability-registry.md) |
| 7 | Automatización | COHERENTE: 15 IDs previos resueltos; simulate exige política/fuentes; sin efecto. | [Fuente](../architecture/capability-registry.md) |
| 8 | Tax externo/conciliación | COHERENTE: TX5 external.record, X05 record_filing y X08 reconcile conservan consumidores distintos. | [Fuente](../architecture/capability-registry.md) |
| 9 | Configuración AND | COHERENTE: Dueño y administrador/delegación por misma familia; CG4 no checker técnico. | [Fuente](../architecture/capability-registry.md) |
| 10 | Shadow técnico | COHERENTE: Tres IDs solo T-SHADOW; ningún permiso oficial. | [Fuente](../architecture/capability-registry.md) |
| 11 | Contracción de privilegio | COHERENTE: A5/revisión restringe concesión y descendientes; no conserva expansión. | [Fuente](../architecture/capability-registry.md) |
| 12 | Roles y scopes | COHERENTE: Unión solo del mismo ID; permisos participantes sobre mismos recursos. | [Fuente](../architecture/capability-registry.md) |
| 13 | ID desconocido | COHERENTE: Denegación, sin aproximación por nombre. | [Fuente](../architecture/capability-registry.md) |
| 14 | Wildcard | COHERENTE: No es entrada del registro ni concesión válida. | [Fuente](../architecture/capability-registry.md) |
| 15 | Nuevo ID | COHERENTE: Diff/aprobación/concesión explícitos; no actualizar asignados automáticamente. | [Fuente](../architecture/capability-registry.md) |
| 16 | Acceso del titular | COHERENTE: Identidad proporcional, copia de lo propio, terceros redactados y respuesta trazada. | [Fuente](../security/personal-data-lifecycle.md) |
| 17 | Rectificación | COHERENTE: Revisión de atributo; evidencia inmutable por addendum/corrección del dueño. | [Fuente](../security/personal-data-lifecycle.md) |
| 18 | Supresión con retención fiscal | COHERENTE: Conservación motivada restringida; no cascada cliente→factura→ledger. | [Fuente](../security/personal-data-lifecycle.md) |
| 19 | Salud de sitio | COHERENTE: Estado/vencimiento mínimo; original médico con audiencia separada. | [Fuente](../security/personal-data-lifecycle.md) |
| 20 | Incidente bajo umbral | COHERENTE: Caso documentado art.35 y decisión motivada de no notificar. | [Fuente](../security/personal-data-lifecycle.md) |
| 21 | Incidente sobre umbral | COHERENTE: Evaluar art.34.1/34.3/34.5 por destinatario, conocimiento y plazo. | [Fuente](../security/personal-data-lifecycle.md) |
| 22 | Encargado conoce | COHERENTE: Aviso inmediato al responsable; no espera investigación final. | [Fuente](../security/personal-data-lifecycle.md) |
| 23 | Breach proveedor incompleto | COHERENTE: Incertidumbre explícita, evaluación/contención inicial, ampliación posterior sin reiniciar conocimiento. | [Fuente](../security/personal-data-lifecycle.md) |
| 24 | Legal hold | COHERENTE: No se levanta por petición/tarea; fundamento, alcance y revisión. | [Fuente](../security/personal-data-lifecycle.md) |
| 25 | Backup anterior restaurado | COHERENTE: Diario posterior fuera del rollback; lectura normal y efectos OFF hasta conciliación íntegra. | [Fuente](../security/personal-data-lifecycle.md) |
| 26 | Export tras revocación | COHERENTE: Revalidación al consumo/entrega y cancelación de salida pendiente. | [Fuente](../security/personal-data-lifecycle.md) |
| 27 | PII en auditoría | COHERENTE: Referencia mínima opaca, no payload sensible completo; retención diferenciada. | [Fuente](../security/personal-data-lifecycle.md) |
| 28 | Original conservado | COHERENTE: Original legal permanece restringido; ni preview ni descarga por retención. | [Fuente](../security/personal-data-lifecycle.md) |
| 29 | Finalidad desconocida | COHERENTE: HOLD a nuevos usos; recepción mínima restringida para tramitar/contener con fundamento. | [Fuente](../security/personal-data-lifecycle.md) |
| 30 | Historia anterior a CasPro | COHERENTE: Fuente/fecha originales; sin consentimiento retroactivo inventado. | [Fuente](../security/personal-data-lifecycle.md) |
| 31 | Sales aplica/Documents render | COHERENTE: Sales decide requisito y aplicabilidad; Documents versión/render. | [Fuente](../architecture/automation.md#familias-de-plantillas) |
| 32 | ReportTemplate | COHERENTE: Fórmulas/definición por dominio; layout no cambia mayor/impuesto. | [Fuente](../architecture/automation.md#familias-de-plantillas) |
| 33 | EmailTemplate | COHERENTE: Contenido/audiencia del acto; editar plantilla no autoriza envío. | [Fuente](../architecture/automation.md#familias-de-plantillas) |
| 34 | Revisión firmada | COHERENTE: No overwrite: nueva revisión conserva usos y originales. | [Fuente](../architecture/automation.md#familias-de-plantillas) |
| 35 | Operations en tabla | COHERENTE: Captura/superficie, sin nuevo dueño de requisito. | [Fuente](../architecture/automation.md#familias-de-plantillas) |
| 36 | Plantilla Accounting | COHERENTE: Semántica/revisión/aplicación en Accounting; no traslado a Documents. | [Fuente](../architecture/automation.md#familias-de-plantillas) |
| 37 | Documents no decide aplicabilidad | COHERENTE: Render requiere descriptor del dueño; no regla por formulario. | [Fuente](../architecture/automation.md#familias-de-plantillas) |
| 38 | Dominio no muta render histórico | COHERENTE: Solicita nueva representación; conserva artefacto previo. | [Fuente](../architecture/automation.md#familias-de-plantillas) |
| 39 | Sugerencia contable humana | COHERENTE: Riesgo jurídico candidato razonado; DRAFT y A03 separado, no calificación automática por dinero. | [Fuente](../research/normative/ai-peru-applicability.md) |
| 40 | Shadow | COHERENTE: Finalidad experimental evaluada; aislamiento no exime privacidad. | [Fuente](../research/normative/ai-peru-applicability.md) |
| 41 | Explicación Tax | COHERENTE: Solo explicación de cálculo/fuente; LATER/OFF conserva trigger. | [Fuente](../research/normative/ai-peru-applicability.md) |
| 42 | IA global OFF | COHERENTE: Cada finalidad necesita aprobación propia; ninguna fila activa proveedor. | [Fuente](../research/normative/ai-peru-applicability.md) |
| 43 | Propósito nuevo | COHERENTE: Nueva revisión/aplicabilidad/manifest y gates antes de nuevas solicitudes. | [Fuente](../research/normative/ai-peru-applicability.md) |
| 44 | Alias cambia modelo | COHERENTE: Identidad resuelta/versiones invalidan evaluación para nuevas solicitudes. | [Fuente](../research/normative/ai-peru-applicability.md) |
| 45 | Clasificación legal cambia | COHERENTE: Revisar fundamento/obligaciones/plazo; nueva revisión antes de activar. | [Fuente](../research/normative/ai-peru-applicability.md) |
| 46 | Sector público vs privado | COHERENTE: Arts.28–30/estándares públicos no son requisitos universales privados. | [Fuente](../research/normative/ai-peru-applicability.md) |
| 47 | Voluntario vs obligatorio | COHERENTE: Art.32 privado voluntario; si evalúa, conservar3 años; no certificación universal. | [Fuente](../research/normative/ai-peru-applicability.md) |
| 48 | Montos no bastan para alto riesgo | COHERENTE: Evaluar uso real, supuestos24 y residual; no etiqueta global. | [Fuente](../research/normative/ai-peru-applicability.md) |
| 49 | Click humano | COHERENTE: No sanea uso prohibido; capacidad real de detener/corregir y competencia. | [Fuente](../research/normative/ai-peru-applicability.md) |
| 50 | IGV/IPM2026 | COHERENTE: 15.5+2.5=18 en supuesto general; no14% inmediato. | [Fuente](../research/normative/igv-ipm-transition.md) |
| 51 | Frontera2027 | COHERENTE: Regla por fecha legal:15+3=18 desde2027-01-01. | [Fuente](../research/normative/igv-ipm-transition.md) |
| 52 | Frontera2028 | COHERENTE: 14.5+3.5=18 desde2028-01-01. | [Fuente](../research/normative/igv-ipm-transition.md) |
| 53 | Frontera2029 | COHERENTE: 14+4=18 desde2029-01-01, sujeto a norma posterior. | [Fuente](../research/normative/igv-ipm-transition.md) |
| 54 | Total igual/split distinto | COHERENTE: Persistir componentes cuando consumidor los demanda, no constantes globales. | [Fuente](../research/normative/igv-ipm-transition.md) |
| 55 | Importación desglosada | COHERENTE: Base/tributos/DAM y norma del hecho; no dividir total comercial arbitrariamente. | [Fuente](../research/normative/igv-ipm-transition.md) |
| 56 | Venta solo total | COHERENTE: Total autorizado18%; no agregar split innecesario a Sales. | [Fuente](../research/normative/igv-ipm-transition.md) |
| 57 | Corrección histórica | COHERENTE: Regla del hecho y nueva revisión/linaje, nunca tasa de hoy por fecha de corrección. | [Fuente](../research/normative/igv-ipm-transition.md) |
| 58 | Norma posterior | COHERENTE: Supersesión por efectividad; hueco/solapamiento/no conciliado retiene salida fiscal. | [Fuente](../research/normative/igv-ipm-transition.md) |
| 59 | G1 | COHERENTE: Fixture total18% y archivo sin cambio; no prueba de motor ejecutada. | [Fuente](../research/normative/igv-ipm-transition.md) |
| 60 | CPE | COHERENTE: DH4 enlaza N020/N023/N037 existentes. | [Fuente](../roadmap/decisions-gaps.md#recomputación-candidata-f01f07) |
| 61 | N009 | COHERENTE: Conserva NIC21; ninguna reasignación normativa. | [Fuente](../roadmap/decisions-gaps.md#recomputación-candidata-f01f07) |
| 62 | PR7 | COHERENTE: MERGED y baseline114275e; texto del encargo OPEN marcado histórico/superado. | [Fuente](../roadmap/decisions-gaps.md#recomputación-candidata-f01f07) |
| 63 | DeepSeek runtime | COHERENTE: Inicial seleccionado; activación y pruebas pendientes. | [Fuente](../roadmap/decisions-gaps.md#recomputación-candidata-f01f07) |
| 64 | IA de desarrollo | COHERENTE: Modelos/herramientas y recursos conservan PROVISIONAL según ADR11/.ai. | [Fuente](../roadmap/decisions-gaps.md#recomputación-candidata-f01f07) |
| 65 | D01 | COHERENTE: Construcción Accounting IA/shadow confirmada; activación por gates. | [Fuente](../roadmap/decisions-gaps.md#recomputación-candidata-f01f07) |
| 66 | D03 | COHERENTE: Crédito requerido inicialmente OFF; COD conserva trigger, no construcción obligatoria inferida. | [Fuente](../roadmap/decisions-gaps.md#recomputación-candidata-f01f07) |
| 67 | Wbpro/CasPro | COHERENTE: No inexactitud actual encontrada: Wbpro referencia, CasPro reemplazo; no CasPro borrado/recreado. | [Fuente](../roadmap/decisions-gaps.md#recomputación-candidata-f01f07) |

## Archivos y validación

- [architecture/ai-assistance.md](../architecture/ai-assistance.md)
- [architecture/automation.md](../architecture/automation.md)
- [architecture/capability-registry.md](../architecture/capability-registry.md)
- [architecture/configuration-governance.md](../architecture/configuration-governance.md)
- [architecture/roles-delegation.md](../architecture/roles-delegation.md)
- [decisions/adr-011-ai.md](../decisions/adr-011-ai.md)
- [evidence/grand-audit-remediation.md](../evidence/grand-audit-remediation.md)
- [evidence/index.md](../evidence/index.md)
- [index.md](../index.md)
- [operations/delivery.md](../operations/delivery.md)
- [product/company-policy-register.md](../product/company-policy-register.md)
- [research/index.md](../research/index.md)
- [research/normative/ai-peru-applicability.md](../research/normative/ai-peru-applicability.md)
- [research/normative/igv-ipm-transition.md](../research/normative/igv-ipm-transition.md)
- [research/normative/normative-register.md](../research/normative/normative-register.md)
- [research/normative/privacy-current-review.md](../research/normative/privacy-current-review.md)
- [review.md](../review.md)
- [roadmap/decisions-gaps.md](../roadmap/decisions-gaps.md)
- [security/personal-data-lifecycle.md](../security/personal-data-lifecycle.md)
- [security/threat-model.md](../security/threat-model.md)
- [specs/cross-cutting/command-matrix.md](../specs/cross-cutting/command-matrix.md)
- [specs/flows/records-signatures-site-packs.md](../specs/flows/records-signatures-site-packs.md)
- [specs/milestones/accounting-deep.md](../specs/milestones/accounting-deep.md)
- [specs/milestones/tax-deep.md](../specs/milestones/tax-deep.md)

Revisión estática: diff --check sin errores;778 enlaces locales y85 referencias con fragmento en24 archivos del delta, sin destino/anchor roto (incluido el anchor histórico Z. Escalabilidad leído por esa referencia concreta); sin anchors explícitos duplicados.255 filas activas únicas, cero sin elegibilidad/consumidor enlazado; cuatro retirados solo en sección de retiro dentro del corpus contractual. Barrido adicional de nombres punteados no encontró otro namespace de capability: rutas, dominios web, abreviaturas negativas y ejemplo dominio.import no son grants. Referencias de política POL-01–26 conservan identidad; tablas propietarias tienen16/13/6 filas B/C/D y no se cuentan de nuevo sus menciones en suplementos. N020/N023/N037 cotejados con significado CPE; N009 con NIC21. Estado PR7/main corroborado y texto supersedido identificado.

Búsqueda histórica limitada a fuentes actuales: Wbpro/Wbpro-ERP, legacy, rewrite/rebuild/deleted/discarded/replacement y variantes españolas. No se abrió Wbpro ni archive/15-history/legacy/Webrax; CasPro no fue borrado/recreado. No se encontró inexactitud actual que exigiera reescribir origen; no se retocaron declaraciones correctas de prevención de defectos Wbpro.

Solo Markdown del alcance. G1, contratos de promedio ponderado/FIFO físico, CM0/raíces/orden global, outbox/UNKNOWN, dinero Jumpseller, separación Procurement/Treasury/Accounting/Tax, unicidad económica, reversión inmutable, Case Flow proyección y preparado/presentado/liquidado preservados. La corrección F02 extiende barrera de restore a privacidad/lecturas; no reemplaza su arquitectura. No ejecución de aplicación ni comparación de rendimiento.

## Entrega

Un PR nuevo abierto contra main; no merge. Identidad final HEAD/tree y commits se informan con la entrega Git para evitar auto-referencia del hash de este mismo archivo. Revisión independiente pendiente en otra sesión, sin subagentes ni autoaceptación. Veredicto de preparación del autor: **PASS — GRAND AUDIT REMEDIATION F01–F07 READY FOR INDEPENDENT RE-REVIEW**.
