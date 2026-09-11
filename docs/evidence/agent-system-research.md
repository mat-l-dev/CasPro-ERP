# Sistema de agentes y skills — investigación y expediente de revisión

Corte: 2026-09-11. Owner editorial: Architecture. Evidencia de investigación y evaluación del autor; no aprobación independiente, política empresarial ni prueba de ejecución CasPro. La autoridad global permanece en [review](../review.md). DOCUMENTATION OWNS TRUTH; SKILLS SELECT AND APPLY CONTEXT.

## A. Merge y baseline

[PR3](https://github.com/mat-l-dev/CasPro-ERP/pull/3) se verificó OPEN/MERGEABLE/CLEAN, branch `docs/final-information-architecture`, head `38d3057b53b9678647a12cbd6d42415404a235d0`, tree `174958f7e54a23a9247af1b0bb0d842e6827018e`, sin cambios locales ni commits desconocidos. Se fusionó con merge commit el 2026-09-11T21:56:10Z, sin squash/rebase.

Baseline main/origin-main: `70c9299e3e35c774789b8e1801d1583f99f04465`; tree `174958f7e54a23a9247af1b0bb0d842e6827018e`. Padres: `dbb1224d99f4dbdac61da25daf32f1fed872b4fa` y `38d3057b53b9678647a12cbd6d42415404a235d0`. La misión continúa en `ai/agent-system-and-skills`; el nuevo PR no se fusiona.

## B. Research externo oficial

Todas las páginas siguientes fueron abiertas y consultadas el 2026-09-11. Son documentación web mutable, sin edición de release fijada salvo indicación; la fecha de consulta no garantiza comportamiento de una instalación concreta. No se usan snippets, blogs ni preferencias de modelo como prueba de capacidades. No se investigaron otros harnesses, proveedores ERP o normas empresariales.

| ID / fuente oficial | Qué acredita | Límite / decisión CasPro derivada |
|---|---|---|
| O1 [Codex AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md) | Cadena global/proyecto hasta CWD; override antes de AGENTS, uno por directorio; archivos cercanos prevalecen; límite combinado configurable | Convención de proveedor, no jerarquía empresarial portable. Router breve en raíz; no overrides anidados |
| O2 [Build skills](https://learn.chatgpt.com/docs/build-skills) | SKILL.md con name/description; carga progresiva; discovery local `.agents/skills` desde CWD a raíz; nombres repetidos no se fusionan | Un namespace CasPro y contenido compartido. La metadata puede truncarse/omitirse por presupuesto; catálogo como fallback, sin afirmar discovery en esta sesión |
| O3 [Subagents](https://learn.chatgpt.com/docs/agent-configuration/subagents) | Workers especializados, configuración nativa TOML y herencia de permisos del padre/runtime | Rol no equivale a modelo ni sandbox universal. No crear configuración de agentes por proveedor sin necesidad; delegación acotada con contexto explícito |
| O4 [Approvals/security](https://learn.chatgpt.com/docs/agent-approvals-security), [permission profiles](https://learn.chatgpt.com/docs/permissions) | Permisos/sandbox son controles de herramienta; modos y perfiles dependen de configuración/host, incluidas diferencias Windows | Markdown no aplica aislamiento OS. No cambiar perfiles, permisos globales, credenciales o red en esta misión |
| C1 [Claude memory](https://code.claude.com/docs/en/memory) | CLAUDE.md jerárquico; imports @ relativos al archivo se cargan al inicio; instrucciones son contexto, no enforcement | Importar solo AGENTS; protocolo/skills bajo demanda. Imports extensos no ahorran contexto |
| C2 [Claude skills](https://code.claude.com/docs/en/skills) | `.claude/skills`, selección por descripción y slash; comandos antiguos siguen; extensiones de frontmatter propias; precedence por scope | `.agents/skills` no figura como discovery nativo. Adaptador textual explícito; sin copias, symlinks, wrappers por skill ni slash ficticio |
| C3 [Claude subagents](https://code.claude.com/docs/en/sub-agents) | Contexto separado, tools/permisos y skills precargables; no herencia de conversación | Entregar contrato/candidato al reviewer. No precargar todas las skills ni asumir que un worker recuerda permisos del encargo |
| C4 [Claude permissions](https://code.claude.com/docs/en/permissions) | Deny precede ask y allow; políticas managed y trust condicionan herramientas | No trasladar allowed-tools como autorización económica. Hooks se evaluaron, no se crean sin un control concreto que validar |
| G1 [Gemini context](https://geminicli.com/docs/cli/gemini-md/) | GEMINI.md global/workspace/JIT; imports @; `/memory show` y reload | Import pequeño a AGENTS, sin importar catálogo completo ni docs. Nombres/contexto dependen de configuración |
| G2 [Gemini skills](https://geminicli.com/docs/cli/using-agent-skills/), [discovery tutorial](https://geminicli.com/docs/cli/tutorials/skills-getting-started/) | Workspace `.gemini/skills` o alias `.agents/skills`; tiers y precedence; `/skills list`/reload; activation consent y workspace trust | Compartir `.agents/skills`; iniciar en raíz confiable y comprobar lista. No suprimir consentimiento ni asegurar comportamiento de toda versión |
| G3 [Gemini subagents](https://geminicli.com/docs/core/subagents/) | Definiciones Markdown en `.gemini/agents`, tools/model y políticas por subagente | Capability actual, no formato común con Codex; no configurar agentes persistentes ni remotos ahora |
| G4 [Gemini settings](https://geminicli.com/docs/cli/settings/), [policy engine](https://geminicli.com/docs/reference/policy-engine/) | Configuración user/workspace; allow/deny/ask_user y prioridades. Policy engine muestra actualización 2026-04-30 | Permisos externos al playbook. No generar JSON/TOML que conceda acceso; respetar configuración efectiva |
| S1 [Agent Skills specification](https://agentskills.io/specification) | Especificación pública del proyecto: SKILL.md, YAML name/description, nombres/rangos y recursos opcionales; referencia de validación | Estándar abierto publicado por Agent Skills, no estándar ISO ni garantía de discovery idéntico. Usar solo el subconjunto común name/description |

Las rutas antiguas de Codex redirigen actualmente a ChatGPT Learn; se citan los destinos oficiales leídos. Se descartó la página general Codex Security para sustentar permisos de sesión: describe otro producto. El research diferencia hechos documentados de decisiones de este diseño. Las convenciones de directorios, comandos, permisos y subagentes son específicas de cada proveedor; ninguna se eleva a estándar compartido.

## C. Auditoría del sistema existente

Lectura dirigida después del research: siete archivos de agentes/protocolo, índice por función, estado, calidad, ADR-011, boundaries, contrato de IA, charter, matriz de hitos y fuentes de los dueños seleccionados. Se consultaron encabezados para localizar secciones, no history ni toda la normativa por defecto.

| Elemento | Disposición | Razón |
|---|---|---|
| AGENTS.md | REFINE / ROUTER | Buen límite de autoridad; tabla por carpeta no resuelve familias de trabajo, prioridad de skills ni salida cuando falta autorización |
| CLAUDE.md | KEEP + REFINE / VENDOR ADAPTER | Import AGENTS correcto; falta declarar consumo textual de skills compartidas y sus límites nativos |
| GEMINI.md | REFINE / VENDOR ADAPTER | Enlace manual correcto; añadir import nativo mínimo, discovery/consent y fallback explícitos |
| .ai/README.md | REFINE / CANONICAL PROTOCOL | Conservar roles/modelos separados; aclarar autoridad, cargas, delegación y fase permitida |
| .ai/workflow.md | REFINE / CANONICAL PROTOCOL | Mantener ciclo y equivalencia QA; hacer explícitos branch/PR/reviewer/merge y acción bloqueada vs análisis posible |
| .ai/work-order.md | KEEP + REFINE / CANONICAL PROTOCOL | Ya evita duplicar reglas; añadir identidad de candidato, gates y condición de preparación futura. No producir WOs reales |
| .ai/review.md | KEEP + REFINE / CANONICAL PROTOCOL | Conservar rúbrica proporcional; separar reviewer que evalúa de autor que corrige y normalizar salida con alcance |

No mover ni eliminar archivos existentes. ADR-011 ya respalda roles estables y configuración única; no hace falta un ADR de dominio nuevo.

## D. Principios y alternativas

Decisión de diseño: una representación canónica `.agents/skills/<name>/SKILL.md` y adaptadores finos. Diez playbooks por trabajo/riesgo; catálogo en `.ai/skills.md`, con fuentes de dominio enlazadas y carga progresiva. Git versiona archivos; sin skill_version independiente, generador, paquete Python, installer, plugin ni framework.

Se descartan: una mega-skill por contexto indiscriminado; skill por comando/módulo por solapamiento; tres copias completas por deriva; diez wrappers Claude por coste sin nueva capacidad necesaria; symlinks por dependencia Windows; imports del catálogo/playbooks en adapters por carga ansiosa. La alternativa Claude textual sacrifica discovery/slash nativo, pero conserva una sola fuente y el routing por tarea; esa limitación es visible, no portabilidad fingida.

## E. AGENTS final

Router universal breve: producto/estado, autoridad, skill primaria, protocolo y límites universales. No copia reglas contables/fiscales ni obliga a leer los 86 Markdown. Las instrucciones directas gobiernan alcance dentro de las políticas de sistema/harness; un documento externo no hereda esa autoridad.

## F. Claude final

Adaptador con import único a AGENTS y carga textual explícita desde catálogo. No son slash commands instalados. Si la herramienta no puede leer el archivo canónico, detener esa parte e informar la ruta faltante; no reconstruir la skill de memoria. No configurar tools ni hooks.

## G. Gemini final

Import AGENTS y discovery del alias compartido, sujeto a versión, trust y consentimiento del harness. Fallback por lectura explícita solo cuando la ubicación no tenga discovery y la lectura esté permitida; nunca para eludir una activación denegada. No copia dominio ni declara permisos.

## H. Protocolo compartido

AGENTS → catálogo → playbook elegido → protocolo y estado ya cargados → contrato del dueño/spec/sección/gates → trabajo permitido → reviewer separado. .ai/README posee roles/autoridad/configuración; workflow posee secuencia; work-order campos del encargo; review criterio de evaluación; catálogo selección, no reglas de dominio. Los roles pueden ejecutarse secuencialmente en sesiones distintas si el host no ofrece delegación.

## I. Análisis de boundaries

| Playbook propuesto | Trabajo repetible / contexto común | Frontera y coste evitado |
|---|---|---|
| caspro-work-order | Preparar encargo acotado desde hito/spec/gates/perfil | Resultado WO, separado de ejecutar o copiar fichas SP2; frecuencia futura alta |
| caspro-review | Evaluar delta/candidato/evidencia sin editarlo | Independencia y equivalencia QA compartidas entre dominios |
| caspro-architecture | Amendment, ownership, mantenimiento de contratos o trazabilidad decisional | Cambia/proporciona razón del contrato; no absorbido por implementación local |
| caspro-economic-flow | Inventory, Treasury, P2P y Sales internos | Comparten CM0/hechos/atomicidad; seleccionar una rama por dueño, sin fusionar sus reglas |
| caspro-accounting | Posting, cierre, políticas representadas y EEFF | Ledger/política/linaje/goldens distintos de dinero operativo |
| caspro-compliance | Tax y actos Corporate/financiación | Preparación/activación profesional por hechos y período; no asumir que todo cambio requiere research legal |
| caspro-external-effects | Jumpseller, CPE/Documents, email y proveedores | Autorización de efectos, contrato externo y resultado incierto; no decide pago ni impuesto |
| caspro-ui | Apariencia, teclado, interacción y presentación | Cargar UI y dueño solo ante cambio de acción/estado; no ledger para color |
| caspro-platform | Runtime, maestros, acceso/seguridad y operación | M01–M02/aislamiento/recuperación; modos separados evitan cargar restore para campo Party |
| caspro-normative-research | Vigencia, nueva norma, RTF, procedencia y aplicabilidad | Fuentes/profesional/amendment; separado de rutinas contables/fiscales con contrato ya fijado |

Frecuencia es una expectativa derivada de las tarjetas M01–M09, no telemetría medida. Agrupar reduce metadata; separar Accounting, compliance y proveedores limita errores costosos. No se crea skill IA económica: candidatos IA consumen el contrato de asistencia y el dueño del efecto; nunca adquieren confirmación propia.

## J–M. Matriz de routing previa a los archivos definitivos

Propuesta registrada antes de crear SKILL.md. Base común: router, estado, protocolo y skill elegida; las fuentes siguientes son secciones pertinentes, no lectura exhaustiva de cada carpeta. Reviewer significa rol separado, no marca/modelo. Secundaria solo cuando el delta cruza su frontera.

| Familia | Primaria | Secundaria opcional | Contexto canónico específico | Escalación / reviewer | Por qué no otra |
|---|---|---|---|---|---|
| Crear WO | work-order | Dueño si falta criterio | programa, spec/hito, gaps, QA, plantilla | Falta contrato/autorización de preparación; orquestador separado | Produce encargo, no código |
| Implementar M01 | platform | ui si login | runtime-masters M01, tecnología, QA, gates | Sin WO autorizada: no implementar; seguridad/arquitectura | Infraestructura antes de operación |
| Revisar RLS | review | platform | tenancy-access, threat-model, B02/QA, delta | Evidencia inexistente; seguridad | Veredicto, no reparación |
| Inventory | economic-flow | accounting si valoración contable | inventory-costing, inventory-deep, CM0/hechos | Contrato/guardas; integridad | Coste operativo no ledger |
| Treasury | economic-flow | compliance si financiación | treasury-finance, sales-stock-treasury, CM0 | Política/dinero; integridad | Dinero no asiento |
| Conciliación bancaria | economic-flow | external-effects si parser externo | M06, Treasury, hechos, C05/QA | Muestra/autorización; integridad | Match no crea dinero |
| P2P | economic-flow | compliance si impuesto | procure-to-pay, M05, CM0/hechos | Política/owner; integridad | Expediente de compra interno |
| Registrar CPE | external-effects | compliance si interpretación fiscal | cpe-document-delivery y Sales/Procurement dueño | Efecto/validez; dominio + seguridad | Archivo/transporte no Tax completo |
| Jumpseller | external-effects | economic-flow si caso interno | jumpseller-external-work, integrations, dueño | C11/efecto; contratos + seguridad | Observación no confirma pago |
| Posting | accounting | economic-flow si productor afectado | Accounting, M07, hechos, política aplicable | C01/C02; Accounting | Treasury no posee ledger |
| Cierre contable | accounting | compliance si conciliación fiscal | M07, política, reporting/QA | Datos/política; Accounting | Cierre no cambia fuente operativa |
| EEFF | accounting | normative-research si cambia marco | npif-reporting, M08/G1–G7, mappings | Aplicabilidad; Accounting | Golden no se deriva del output |
| Tax | compliance | normative-research si vigencia | Tax, M09, gaps sección aplicable | C07–09; profesional Tax | No recargar fuentes sin trigger |
| Mutuo | compliance | economic-flow/accounting según efecto | Corporate, M06, C06, contrato Tax pertinente | Antes de financiar; legal/Tax/contador | Separar acto, dinero, ledger |
| UI | ui | dueño cuando cambia acción | UI, spec local, B09/C12 si aplica | Semántica; UX proporcional | Color no investigación fiscal |
| Seguridad / corregir RLS | platform | dueño expuesto | tenancy-access, threat-model, M01, QA | B02/negativa; seguridad independiente | Corrección no autoaceptación |
| Provider integration | external-effects | platform si secretos/infra | integrations, flow/puerto, fuente oficial por capacidad | Efecto/credencial; seguridad/contratos | SDK no dueño de hechos |
| Research normativo | normative-research | compliance/accounting | registro normativo, dueño, texto oficial vigente | Aplicabilidad/posición; profesional | Fuente no política |
| PR review | review | especialista según delta | base/head/tree, WO/spec, QA | Claim sin prueba; reviewer proporcional | Autor no se acepta |
| Architecture amendment | architecture | dueño | overview/boundaries, ADR afectado, spec, gaps | Cambio semántico; architect + dueño | Skill no modifica regla silenciosamente |
| Party / maestros | platform | architecture si nuevo hecho | runtime-masters M02, C11, data/access | Falta significado del campo; dueño + acceso | No skill por tabla |
| Restore | platform | external-effects para efectos pendientes | delivery, M01 recuperación, B13/C10 | Sin mandato/entorno: no restaurar; operaciones/seguridad | No implica desplegar |
| Motivo histórico | architecture | — | ADR actual; registro histórico exacto solo si necesario | Contradicción actual: reportar; revisión documental | Consulta acotada, no importar history |

La arquitectura escogida, catálogo definitivo, compatibilidad, pruebas y límites se completarán en este expediente después de escribir y evaluar los playbooks. Este checkpoint no declara pruebas pasadas.
