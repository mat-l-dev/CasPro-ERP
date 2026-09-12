# Auditoría de vigencia del sistema de agentes CasPro

Corte: **2026-09-12**. Evaluación y corrección documental del autor; **PENDING INDEPENDENT REVIEW**. El encargo permite merge de PR #8, nueva rama, auditoría, correcciones, commit/push y un nuevo PR abierto. No permite WOs, código, tests de aplicación, builds, Docker, migraciones ni merge del nuevo PR. [Review](../review.md) conserva la fase global.

## A–B. Secuencia y baseline

PR #8 se verificó OPEN, no merged, limpio y MERGEABLE sobre `cf41b741ede9061e4b6b3a57e83be233eea1ba02`, tree `49096b080ad241f5c3d8d7e7f559e321f8cb01c1`. Frente al candidato semántico aceptado `25bea3199f5f2271f06315e5e49a1567c0ea235b`, tree `e732b0668ccc976f56d49f07d230f9caf437d54a`, solo difería docs/review.md por sincronización de aceptación. Main seguía en `114275e7567ea2ace203e76e18426554ecc42a7e`.

El propietario autorizó expresamente «haz el merge y lo del prompt». Se fusionó [PR #8](https://github.com/mat-l-dev/CasPro-ERP/pull/8) mediante merge commit, con control del HEAD esperado, a las **2026-09-12T22:10:23Z**.

- Main/origin-main inicial de esta auditoría: **574937c2f811562948318d7ebde5e9f95b815056**.
- Tree: **49096b080ad241f5c3d8d7e7f559e321f8cb01c1**; idéntico al cierre de estado integrado.
- Working tree limpio antes de crear **docs/agent-system-freshness-audit**.
- La rama anterior se conserva; no era necesario eliminarla para este encargo.
- Autor distinto del futuro reviewer de aceptación; no se simula revisión independiente ni delegación.

## C. Inventario y primera pasada antes de editar

Inventario por filesystem, incluyendo ocultos: **19 archivos** de instrucciones, enumerados uno por fila abajo. Raíz: AGENTS, CLAUDE, GEMINI, README. .ai: cinco archivos. .agents: directorio skills con diez directorios caspro y un SKILL.md en cada uno; sin auxiliares. No se asumió que la lista conocida fuera completa.

No existen superficies de proyecto .claude, .gemini, .codex, .github, .cursor, .windsurf o .vscode, archivos Copilot, MCP, hooks, comandos adicionales ni AGENTS.override.md/nested agent files. La búsqueda cubrió nombres de instrucciones/prompts/configuración en archivos del repositorio fuera de history/legacy; metadatos Git, instalaciones personales, secretos y repositorios externos no se trataron como instrucciones versionadas CasPro. No se crearon adapters por simetría.

Primera pasada: se leyeron íntegramente los 19 archivos y se completaron inventario, matriz, contraste oficial y hallazgos **antes de modificar instrucciones**. La matriz se conservó en memoria de trabajo antes de la primera edición; esta publicación posterior no representa hallazgos retrospectivos inventados. Validación inicial: **150 referencias locales incluyendo 2 imports; 24 fragmentos; 10 cabeceras YAML/nombres/catálogos coherentes; 0 fallos**.

### Matriz del baseline

CURRENT? califica adecuación de routing, no antigüedad. Parcial no significa arquitectura inválida. UPDATE agrega rutas precisas; KEEP_WITH_CLARIFICATION cambia solo el enlace de investigación de los adapters. Las fechas/procedencias históricas no se reetiquetan como actuales.

| FILE | PURPOSE | AUTHORITY LEVEL | CONSUMER | ROUTES TO | LAST RELEVANT ASSUMPTION | CURRENT? | MISSING CONTRACT? | STALE? | CONTRADICTORY? | TOO BROAD? | TOO NARROW? | DUPLICATES? | PROVIDER-SPECIFIC? | RESEARCH? | ACTION |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| AGENTS.md | Router universal | Router subordinado | Todo agente | review → catálogo/protocolo → dueño | Freeze y lectura progresiva | Parcial | Rutas capability/privacidad/IA | No | No | No | Sí: triggers transversales | No | No | No | UPDATE |
| CLAUDE.md | Adaptador de import/lectura textual | Adaptador de harness | Claude Code | AGENTS + catálogo + research histórico | Import único; .claude/skills nativo | Sí | Seguimiento actual de tooling | No: conducta VERIFIED_CURRENT | No | No | No | No | Claude | Sí P03–05 | KEEP_WITH_CLARIFICATION |
| GEMINI.md | Adaptador de import/discovery | Adaptador de harness | Gemini CLI | AGENTS + catálogo + research histórico | Alias .agents; list/reload; fallback | Sí | Seguimiento actual de tooling | No: conducta VERIFIED_CURRENT | No | No | No | No | Gemini | Sí P06–08 | KEEP_WITH_CLARIFICATION |
| README.md | Presentar proyecto y entrada | Resumen no normativo | Persona/agente nuevo | review/index/AGENTS/history | Documentación sin runtime autorizado | Sí | No | No | No | No | No | No | No | No | KEEP |
| .ai/README.md | Autoridad y trabajo compartido | Protocolo subordinado | Todo agente | ADR011/review/QA/gates | Roles/WO/permiso; IA de desarrollo | Parcial | IDs exactos; privacidad; separar IA | No | No | No | Sí: rutas | Repite breve límite de skills a propósito | No | No | UPDATE |
| .ai/workflow.md | Ciclo de entrega | Protocolo subordinado | Autor/reviewer/orquestador | review/QA/protocolo | Autor→review→merge autorizado | Parcial | Sincronización aceptada y cleanup explícitos | No | No | No | Sí: cierre | No | No | No | UPDATE |
| .ai/review.md | Rúbrica proporcional | Protocolo subordinado | Reviewer separado | QA/spec/candidato | Perfiles/equivalencia/independencia | Parcial | Ownership/IDs/fuente factual/STOP explícitos | No | No | No | Sí: checks durables | No | No | No | UPDATE |
| .ai/work-order.md | Plantilla no ejecutable | Plantilla subordinada | Preparador/implementador/reviewer | review/protocolo/spec/gates | Campos obligatorios cuando aplique ambiguos | Parcial | Núcleo + triggers capacidades/privacidad/efectos | No | No | No | Sí: selección condicional | No | No | No | UPDATE |
| .ai/skills.md | Selección y compatibilidad | Catálogo subordinado | Todo agente | 10 skills/canónicos/adapters | Taxonomía de diez anterior a nuevos contratos | Parcial | Privacidad/AI/shadow/Case Flow/mirror | No: C/G/T vigente | No | No | Sí: descubrimiento de tareas | No | C/G/T | Sí P01–08 | UPDATE |
| .agents/skills/caspro-architecture/SKILL.md | Amendment/ownership | Skill: router, no ley | Agente de architecture | Boundaries/ADR/spec | Fronteras antes de privacy fact closure | Parcial | privacy ownership/config/capability/Case Flow | No | No | No | Sí: rutas condicionadas | No | Compartida C/G; textual T | No | UPDATE |
| .agents/skills/caspro-accounting/SKILL.md | Ledger/cierre/reporting | Skill: router, no ley | Agente de accounting | Accounting/M07/NPIF/goldens | Posting manual/ledger oficial | Parcial | templates/automatización/AI→draft/shadow | No | No | No | Sí: rutas condicionadas | No | Compartida C/G; textual T | No | UPDATE |
| .agents/skills/caspro-compliance/SKILL.md | Tax/Corporate/aplicabilidad | Skill: router, no ley | Agente de compliance | Tax/M09/Corporate/M06 | Actos y expedientes fiscales generales | Parcial | filing mirror/privacidad/IA por propósito | No | No | No | Sí: rutas condicionadas | No | Compartida C/G; textual T | No | UPDATE |
| .agents/skills/caspro-economic-flow/SKILL.md | Flujos stock/dinero | Skill: router, no ley | Agente de economic-flow | Dueño/CM0/hechos/spec | SP2 y núcleo económico | Parcial | B2B crédito/construcción y financiación/terceros | No | No | No | Sí: rutas condicionadas | No | Compartida C/G; textual T | No | UPDATE |
| .agents/skills/caspro-external-effects/SKILL.md | Transporte/proveedor | Skill: router, no ley | Agente de external-effects | Integraciones/flow/CM0 | CPE/correo/Jumpseller | Parcial | AIService/proveedor y privacidad del envío | No | No | No | Sí: rutas condicionadas | No | Compartida C/G; textual T | No | UPDATE |
| .agents/skills/caspro-normative-research/SKILL.md | Vigencia/procedencia | Skill: router, no ley | Agente de normative-research | Registro/fuente oficial/dueño | Fecha/alcance/RTF/PCGE | Parcial | Conflicto oficial/versión distribuida/efectividad | No | No | No | Sí: rutas condicionadas | No | Compartida C/G; textual T | No | UPDATE |
| .agents/skills/caspro-platform/SKILL.md | Acceso/seguridad/restore/maestros | Skill: router, no ley | Agente de platform | M01–02/access/threat/delivery | RLS/restauración base | Parcial | registro/config/privacidad/restore sin reexposición | No | No | No | Sí: rutas condicionadas | No | Compartida C/G; textual T | No | UPDATE |
| .agents/skills/caspro-review/SKILL.md | Evaluación independiente | Skill: router, no ley | Agente de review | Rúbrica/QA/diff/spec | Claims/equivalencia por riesgo | Parcial | IDs/ownership y diferencia factual/semántica | No | No | No | Sí: rutas condicionadas | No | Compartida C/G; textual T | No | UPDATE |
| .agents/skills/caspro-ui/SKILL.md | Apariencia/interacción | Skill: router, no ley | Agente de ui | UI/spec/QA | Atajo de navegación requiere solo UI | Parcial | Case Flow/disclosure/preview vs download | No | Atajo de búsqueda sensible requiere más que UI | No | Sí: rutas condicionadas | No | Compartida C/G; textual T | No | UPDATE |
| .agents/skills/caspro-work-order/SKILL.md | Preparación de WO | Skill: router, no ley | Agente de work-order | Plantilla/programa/spec/QA | Campos y perfil del alcance | Parcial | Núcleo/triggers modernos/watch items | No | No | No | Sí: rutas condicionadas | No | Compartida C/G; textual T | No | UPDATE |

## Dependencias canónicas contrastadas

Lectura dirigida a las secciones que deciden routing/autoridad, no reapertura de la auditoría empresarial.

| Fuentes | Contraste de instrucciones |
|---|---|
| [Review](../review.md), [índice](../index.md) | Fase única, mapa de autoridad, aceptación exacta y estado de merge |
| [Boundaries](../architecture/boundaries.md) | Propiedad de los cinco hechos privacy; Operations técnico, coordinación sin hechos paralelos |
| [Registro de capabilities](../architecture/capability-registry.md), [roles](../architecture/roles-delegation.md), [configuración](../architecture/configuration-governance.md) | ID literal, scopes/conjunciones, principales cerrados, descriptor/política y autoridad administrativa |
| [Privacidad](../security/personal-data-lifecycle.md), [threat model](../security/threat-model.md) | Lectura/export/AI, custodia frente a aprobación, restricciones y barrera de restore |
| [AIService](../architecture/ai-assistance.md), [Accounting templates/shadow](../accounting/templates-automation-shadow.md) | ProviderAdapter, proveedor inicial elegido por propietario, AI→draft, aislamiento oficial/shadow |
| [Case Flow](../specs/cross-cutting/case-flow-preview.md) | Owner de presentación, lectura parcial, disclosure previo a layout, preview/download y stale |
| [External Tax Filing Mirror](../specs/flows/external-tax-filing-mirror.md) | Dueño Tax, preparado/presentado/eficaz/liquidado separados, evidencia Documents, dinero Treasury |
| [Gaps](../roadmap/decisions-gaps.md), [programa](../roadmap/program.md), [specs](../specs/index.md) | A/B/C/D, construcción confirmada frente a activación, secuencia documental y WO |
| [QA](../quality/strategy.md), [ADR-011](../decisions/adr-011-ai.md), [ADR-012](../decisions/adr-012-global-documentation-freeze.md) | Reutilización por afirmación/candidato, roles/modelos, freeze y autorización independiente |

Salvo review y los índices, estas fuentes no se editan. Los índices solo enlazan el seguimiento y remiten aceptación a review; no trasladan contratos. Las etiquetas de propuesta en fuentes históricas/contextuales no se convierten por esta auditoría en una reapertura de arquitectura.

## D. Tooling y adapters

[Memo de currentness](../research/agent-tooling-currentness.md): diez fuentes oficiales P01–P10 consultadas hoy, con discovery, precedencia, skills, trust, límites y consecuencias. Codex: AGENTS/skills/configuración; Claude: memoria/skills/seguridad/subagentes; Gemini: GEMINI/skills/trusted folders. Las URLs de developers.openai.com redirigieron a learn.chatgpt.com; se registra el destino oficial. No se usó el corte previo como sustituto de verificar.

C/G/T queda **VERIFIED_CURRENT documentalmente**: Codex y Gemini documentan el directorio compartido; Claude conserva lectura textual/import único y no promete comando nativo CasPro. Es distinción de compatibilidad, no permiso ni prueba funcional. No se encontró CLI codex en PATH; la metadata de la sesión sí expone las diez skills. No se ejecutaron clientes Claude/Gemini, subagentes, instalaciones o cambios de trust.

## Hallazgos y correcciones confirmadas

| ID / severidad inicial | Evidencia/contraejemplo del baseline | Corrección aplicada / resultado del autor |
|---|---|---|
| AS01 HIGH | Permisos remitían a acceso/CM0 pero faltaba una ruta explícita al registro exacto; privacidad dependía de navegación indirecta | AGENTS/protocolo/catálogo y skills afectadas enlazan registro, ownership y ciclo. Resuelto como routing; ningún ID o dueño creado |
| AS02 HIGH | Faltaban triggers explícitos de shadow, filing mirror y Case Flow; UI decía que un atajo de búsqueda requería solo UI | Skills/catálogo añaden ramas acotadas; búsqueda que revela datos exige contrato de lectura. B2B/financiación enlazan contratos existentes. Resuelto |
| AS03 MEDIUM | Preferencias de desarrollo no decían expresamente que eran distintas de AIService runtime | Separación explícita y enlace en protocolo; sin copiar proveedor/modelo/precios ni cambiar selección. Resuelto |
| AS04 MEDIUM | Flujo no detallaba aceptación→sincronización→merge y cleanup; rúbrica no tenía STOP explícito ni contraste factual separado | Secuencia durable, candidato exacto, corrección/re-review proporcional, ownership/IDs/fuentes y STOP. Resultados históricos conservados. Resuelto |
| AS05 HIGH | Plantilla llamaba a todo «obligatorio cuando aplique», sin núcleo ni triggers de hechos/capabilities/privacidad | Núcleo obligatorio, secciones por riesgo y paquete de reviewer/watch items. Además se aclara que legacy no obtiene la excepción READ-ONLY de Wbpro. Resuelto; no WO generada |
| AS06 MEDIUM | Norma y fecha se distinguían, pero no el conflicto entre fuentes oficiales/distribución/página orientativa | Procedimiento de conciliación y seis clases de fecha; sin fijar versión PLAME ni tasa en skill. Resuelto |
| AS07 MEDIUM | Protocolo protegía frente a PDFs/webhooks/tools genéricamente, sin señalar salidas de modelo ni evidencia pegada | Regla común explícita para XML/uploads/proveedores/modelos y prompts históricos; no repetida en diez skills. Resuelto |
| AS08 LOW | Enlaces de compatibilidad actuales llevaban al expediente del 2026-09-11 | Nuevo memo de consulta, adapters/catálogo enlazados; informe anterior intacto. Resuelto, sin cambio de conducta proveedor |
| AS09 BLOCKER | Tras el merge autorizado, review seguía diciendo PR8 OPEN y pendiente de merge | Solo estado/índices: merge real identificado, nueva misión documental y review pendiente. Resuelto. Es frescura de fase, no un nuevo bloqueador de diseño A |
| AS10 INFO | Jerarquía, diez nombres únicos, imports mínimos y no permisos por skill ya eran coherentes | Se conservan; no skill adicional, copia de proveedor o rediseño |

No se atribuye a AS01–AS09 fallo demostrado de runtime. Son defectos/clarificaciones de instrucciones. No hubo preguntas empresariales irreducibles.

## E–M. Veredictos por superficie y skill

| Superficie | Veredicto del autor tras corrección |
|---|---|
| AGENTS.md | Router compacto con entradas condicionales para ID exacto, privacidad y runtime AI; no manual de negocio |
| CLAUDE.md | KEEP_WITH_CLARIFICATION: import/lectura textual íntegros; enlace actual |
| GEMINI.md | KEEP_WITH_CLARIFICATION: alias/list/reload/fallback íntegros; enlace actual |
| .ai/README.md | Autoridad preservada; fuentes no confiables, rutas por trigger y separación de IA explícitas |
| workflow | Ciclo completo sin PR transitorio, autoaceptación ni merge implícito |
| review rubric | Review proporcional del diff/candidato; propiedad/IDs/fuente material; PASS/REQUEST CHANGES/STOP |
| WO template | Núcleo + ocho triggers, salida de reviewer; usable sin generar WO |
| skill catalog | Diez filas y diez archivos, sin duplicados/huérfanos; modos modernos descubribles |

Cada SKILL.md fue leído íntegro. La matriz inicial responde trigger, rutas, supuesto, faltante, anchura y duplicación. Esta matriz complementaria registra qué contratos se activan en cada skill; «cond.» significa solo si la tarea cruza esa frontera, nunca lectura obligatoria en toda tarea.

| Skill | Capability registry | Privacidad | Desarrollo/runtime AI | Vigencia normativa | Case Flow | Filing Mirror | Shadow | Contexto excluido por defecto / veredicto |
|---|---|---|---|---|---|---|---|---|
| architecture | Permiso/comando | Ownership/ciclo | Protocolo/ADR si cambia frontera | Solo afirmación mutable | Si proyección | Solo frontera Tax | Solo frontera AI | No todos ADR/history; UPDATE coherente |
| accounting | Acción/principal AI/regla | Datos/prompt | AIService y proveedor | PCGE/marco por pregunta | Solo consumidor | Solo frontera Tax real | Ruta explícita aislamiento/comparación | No dinero operativo ni research total; UPDATE coherente |
| compliance | Actor/comando/aprobación | Aplicabilidad legal | IA Perú por finalidad | Registro y memo por período | Solo consumidor | Ruta explícita Tax | No: accounting salvo aplicabilidad | No transporte ni todos dominios; UPDATE coherente |
| economic-flow | Actor/comando | Cond. por protocolo/objeto | Observación/candidato | Solo regla fiscal discutida | Solo vista del hecho | No salvo obligación afectada | No | Una rama, no todo circuito; UPDATE coherente |
| external-effects | Principal/efecto | Datos que salen/retención | AIService/transporte | Norma solo si decide validez | No salvo entrega/lectura | No salvo transporte documental | Solo transporte de cápsula por contrato | No ledger/Tax completo; UPDATE coherente |
| normative-research | Solo si propuesta altera autorización, protocolo | Norma por finalidad | Aplicabilidad, no elegir coding agent | Ruta principal; fuentes discrepantes | No | Si versión/plazo/formulario | Solo aplicabilidad IA | No toda normativa ni research rutinario; UPDATE coherente |
| platform | Ruta explícita roles/configuración | Técnica y restore | Aislamiento proveedor | Compliance si interpretación | Cond. entrypoint/disclosure | No salvo entrada/dato | Cond. aislamiento | No M01/M02 para toda cuestión privacy; UPDATE coherente |
| review | Delta afectado | Delta afectado | Según claim | Fuente externa material | Si delta | Si delta | Si delta | No todo ERP ni lectura de todos playbooks; UPDATE coherente |
| ui | Lectura/preview/download/export | Dato sensible | No para CSS; dueño si AI UI | No para presentación fija | Ruta explícita | Si superficie Tax | Si superficie Accounting | CSS: solo UI/artefacto; UPDATE coherente |
| work-order | Trigger de actor/comando | Trigger de datos/restore | Trigger de proveedor | Trigger profesional | Solo alcance WO | Solo alcance WO | Solo alcance WO | No WOs históricas ni todos campos opcionales; UPDATE coherente |

Preguntas comunes de las 20 solicitadas: enlaces resuelven y se revisó concepto (Q5); no alias obsoleto/estado transitorio ni confusión de rol como permiso (Q6–8); cada frontera actual se cubre arriba (Q9–15); Wbpro READ-ONLY y exclusiones permanecen por router/protocolo sin lecturas de legado (Q16). No skill demasiado amplia que requiera división; sí rutas estrechas corregidas, sin duplicación material (Q17–19). El camino por secciones permite trabajar sin releer el repo (Q20). Contexto ajeno se excluye en cada fila (Q3); no se crean roles/capabilities de producto en estas respuestas.

## N–T. Taxonomía, contexto y autoridad

**N. No se necesita skill nueva.** Privacidad técnica cabe en platform, aplicabilidad legal en compliance, ownership en architecture; acceso/configuración en platform; automatización contable en accounting, transporte en external-effects; Documents se selecciona por resultado. Separarlas crearía duplicación y lectura de contexto sin otro dueño. No skills de modelo ni módulos Privacy/Communications/Reporting.

**O. Desarrollo ≠ runtime.** Astra/Sol/implementadores y Claude/Gemini/Codex son recursos del trabajo de desarrollo; AIService/ProviderAdapter y selección inicial DeepSeek API/V4.1-Flash pertenecen al contrato del producto. Solo se enlaza ese contrato: no se reelige proveedor, coding agent ni permisos oficiales/shadow.

**P–Q. Permisos y privacidad.** El registro exacto se activa por roles/comandos/principales/configuración, no por cada CSS. Propiedad del ciclo, ejecución, custodia, coordinación y autoridad legal siguen en boundaries/privacy. La conjunción privacy.context.prepare se enlaza a su sección canónica sin reescribirla. Las rutas cubren restricciones en lecturas/exports/IA y restore con lecturas normales OFF; no hay eliminación automática de historia.

**R. Vigencia.** No se rehizo investigación tributaria/legal ni se cambió F01–F07. Se mejoró cómo verificar cuando la tarea lo exige: fuente primaria, edición/publicación/efectividad, discrepancia oficial, límite de acceso y validación profesional. El antecedente PLAME enseña a separar resolución/distribución/página orientativa; no copiar su versión a un playbook.

**S. Contexto.** Base compartida una vez: AGENTS + sección de estado vigente + protocolo + selección de catálogo. Añadir una skill y fuentes por tarea. Los conteos siguientes son estimaciones de documentos con secciones seleccionadas, incluyendo esos cuatro base; no tokens medidos ni obligación de cargar archivos completos. QA/research se añaden por evidencia o vigencia, no automáticamente.

| Tarea | Camino después de base | Estimación habitual |
|---|---|---|
| Amendment de arquitectura | architecture → boundaries/ADR pertinente → spec → gates | 8–10 documentos/secciones |
| Implementación Accounting futura autorizada | accounting + WO vigente → Accounting/M07/sección NPIF → gates/QA; shadow solo en ese modo | 10–12 |
| Research Tax | normative-research → registro → Tax/memo del período → fuente oficial concreta; profesional/gates según impacto | 8–10 locales + fuentes pertinentes |
| Seguridad/privacidad | platform → privacy/boundaries → sección exacta de registro; delivery solo restore | 8–10 |
| UI | ui → contrato UI/artefacto; Case Flow/permisos solo si contenido | 6 visual; 8–10 sensible |
| Integración | external-effects → integración/flow → comando/dueño/gates; proveedor actual por pregunta | 9–11 |
| Review | review → rúbrica/QA → diff/spec/gates; fuente material por claim | 9–11 |
| Generación WO futura | work-order → plantilla → tarjeta/spec/dueño/gates/QA → triggers aplicables | 10–12 |

No hay carga automática de 40 archivos, history, diez skills, research/evidence completos ni superprompts. El texto total aumenta de **6.536 a 8.124 palabras** por rutas faltantes; es todo el inventario, no contexto de cada tarea. AGENTS queda en **23 líneas/3.014 bytes** y los adapters en **10 líneas** cada uno; ninguna skill supera 35 líneas. El protocolo queda en 54 líneas y la plantilla en 46. Medición por espacios/líneas, no tokenizer; límite de 32KiB de Codex no se confunde con todo contexto leído.

**T. Autoridad/inyección.** Jerarquía preservada: sistema/harness → alcance autorizado → fuentes canónicas → WO autorizada cuando aplique → instrucciones/playbooks → herramientas. Un cliente puede cargar texto después de otro sin convertirlo en permiso. Regla común frente a PDFs/XML/uploads/README externos/payloads/modelos/contratos como evidencia y history. La tarea directa del propietario conserva su autoridad; la instrucción incrustada en datos no la hereda. No hooks, cambios de trust ni permisos del host. Autoría y aceptación separadas.

## U. Términos y fechas

Búsqueda en los 19 archivos actuales, evaluando contexto de cada hit:
- Cero IDs retirados accounting.journal.prepare, accounting.period.reopen, accounting.report.approve e integrations.connection.manage; cero A3 y referencias transitorias PR7/PR8.
- Wbpro aparece como referencia restringida; no ERP vigente, eliminación/recreación de CasPro ni implementación copiada.
- No elección runtime pendiente ni DeepSeek como coding agent; menciones Astra/Sol en preferencias de desarrollo son válidas.
- No Operations universal ni creación de Communications/Reporting; reporting en Accounting es función, no módulo inventado.
- No D universalmente opcional ni crédito B2B opcional por inferencia; nueva ruta apunta a construcción/activación en fuente existente.
- PAID remoto no confirma dinero; emisión/presentación SUNAT no autorizadas; selección física FIFO no redefine valoración; shadow no obtiene posting oficial.
- No versiones PLAME/tasas IGV/IPM hardcodeadas en instrucciones. Se enlazan registros/memos del período.

No había fechas ISO en los 19 archivos del baseline que exigieran renovación. Clasificación de dependencias: corte del expediente agent-system-research **HISTORICAL_CUTOFF + RESEARCH_CUTOFF**, conservado; fecha review **CURRENT_STATUS_DATE**; «PR8 OPEN» después del merge era **STALE_CURRENTNESS_CLAIM** corregida; fechas de ADR/candidatos **HISTORICAL_CUTOFF**; efectividad de normas/versiones **VERSION_EFFECTIVE_DATE** si la tarea las usa. No se encontró IRRELEVANT_DATE que justificara editar. Fecha vieja no demuestra invalidez.

## V / AA. Validación estática

- Instrucciones: **216 referencias locales (214 enlaces + 2 imports), 40 fragmentos, 0 rutas/anchors fallidos**; AGENTS/CLAUDE/GEMINI resueltos. Imports verificados como rutas, no activación ejecutada.
- Diez SKILL.md, nombres únicos y carpeta=name; catálogo↔filesystem exacto, sin huérfanos ni skills no documentadas.
- YAML validado como los diez mappings reales de dos escalares: name simple y description entre comillas, delimitadores y ausencia de claves duplicadas. No se afirma validar extensiones YAML que estos archivos no usan.
- Cero aliases retirados/transitorios en instrucciones; todos los IDs literales actuales del routing contrastados con registro.
- Semántica de enlaces revisada por dueño/acción, incluyendo privacy.context.prepare, shadow aislado, Case Flow, filing mirror y gobierno de crédito.
- diff --check sin errores; diff limitado a instrucciones, este informe/memo, estado e índices. Contratos de arquitectura/negocio, gates y evidencia histórica conservados.
- Comprobación ampliada a instrucciones, informe, memo y cuatro archivos de estado/índice: **428 referencias locales incluyendo 2 imports, 45 fragmentos, 0 fallos**, sobre 25 archivos (24 cambiados más README conservado). Conteo de filas primarias: **B16/C13/D6**; registro intacto. No nuevo bloqueador semántico A. La extracción de IDs excluye destinos de enlaces y nombres de archivos: los routers enlazan el catálogo, sin copiar IDs nuevos ni aliases.
- No tests/builds/Docker/Python/SQL/migraciones ni aplicaciones/proveedores reales. No revisión independiente ni ejecución de tres clientes atribuida a estas comprobaciones.

## W–Z. Delta y conservación

**Archivos actualizados:** 18 del inventario: AGENTS, CLAUDE, GEMINI, los cinco .ai y los diez SKILL.md. Los adapters solo cambian enlace. Además docs/review.md (fase/merge real), docs/index.md y docs/evidence/index.md (ruta actual y estado histórico), docs/research/index.md (descubrimiento del memo). **22 existentes actualizados**.

**KEEP:** README.md íntegro. Se dejan intactos todos los contratos canónicos del cuadro de dependencias salvo review/index, todo el registro de gates, investigación normativa y evidencia histórica (incluido agent-system-research.md y grand-audit-remediation.md). No cambio por fecha antigua. Ningún archivo deprecated/deleted, skill nueva, copia, wrapper o configuración añadida.

**ADD_NEW_FILE:** este informe y [agent-tooling-currentness.md](../research/agent-tooling-currentness.md). Informe = evidencia del candidato; memo = procedencia oficial mutable, sin duplicar historia ni verdad empresarial. Total previsto: **24 Markdown**.

## AB–AC. Pendientes y preparación para WOs

**AGENT SYSTEM READY FOR WO REGENERATION? YES WITH NON-BLOCKING WATCH ITEMS**, como evaluación documental del autor. **Regeneración todavía NO autorizada**: requiere review independiente favorable, aceptación/merge del nuevo PR y encargo de preparación según review. No se produjo WO candidata.

| Watch item | Responsable / trigger | Límite |
|---|---|---|
| Versión/discovery/contexto real de cada cliente | Mantenedor del host, antes de usarlo en una WO ejecutable o tras cambio de versión | Fuentes verificadas no equivalen a ensayo del host; no permisos por alias |
| Metadata de muchas skills externas | Orquestador, si el cliente avisa truncación/omite skill | Usar catálogo y lectura permitida; no cargar todo ni configurar bypass |
| Cambios externos de proveedor/norma | Dueño/research, ante claim material o trigger de vigencia | Revalidar alcance concreto, preservar evidencia anterior |

Hallazgos BLOCKER/HIGH pendientes de corrección del autor: **0**. AS09 era estado de instrucciones, no nuevo A de arquitectura. **A0 / B16 / C13 / D6** preservado; B/C/D abiertos; validaciones profesionales y runtime siguen pendientes.

## AD–AI. Entrega y veredicto

Un commit coherente de auditoría/refresh en la rama indicada; el cuerpo del PR y la respuesta final identificarán el HEAD/tree resultante después de materializar este informe, evitando un hash autorreferencial. Baseline y alcance quedan fijados arriba; el nuevo PR debe permanecer OPEN. Preguntas al propietario: **0**.

**PASS — AGENT SYSTEM REFRESH READY FOR INDEPENDENT REVIEW**

**IMPLEMENTATION: NOT AUTHORIZED.** No merge del nuevo PR ni regeneración de WOs en esta misión.
