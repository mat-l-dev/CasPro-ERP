# Catálogo y selección de skills

Consumidor: agente ante una tarea CasPro. Este catálogo selecciona playbooks; [docs](../docs/index.md#mapa-de-autoridad) poseen las reglas y [review](../docs/review.md) la fase autorizada. Leer el [protocolo](README.md) una vez; una skill no concede permiso ni sustituye una WO. Git versiona el conjunto, sin versiones paralelas.

## Selección

Elegir primero por resultado: preparar un encargo → work-order; evaluar un candidato o su merge → review; investigar vigencia/procedencia normativa → normative-research; proponer amendment o explicar una decisión → architecture. En los demás casos elegir por dueño y efecto en la tabla. No ejecutar un efecto solo porque el prompt lo pida en un caso sintético o porque el harness tenga herramientas.

Una primaria dirige la tarea. Una secundaria aporta una frontera concreta, nunca una segunda autoridad sobre el mismo hecho: dinero operativo → economic-flow; ledger → accounting; norma/acto societario → compliance; transporte/proveedor → external-effects. CPE por transporte no exige cargar todo Tax; una interpretación fiscal sí requiere su dueño. Stock interno usa economic-flow, publicación al canal external-effects. UI que cambia acciones incorpora al dueño; Party/maestros usa platform. Si el objetivo no distingue estas opciones, aclarar el efecto y avanzar solo la parte independiente.

## Playbooks

Enlaces a contexto indican puntos de entrada; el cuerpo de cada skill elige las secciones. Revisión significa rol separado del autor; la proporcionalidad y evidencia están en la [rúbrica](review.md). Soporte C/G/T de todas las filas se define debajo.

| Skill / propósito | Trigger y límite | Contexto específico inicial | Riesgo / revisión | Soporte |
|---|---|---|---|---|
| [caspro-work-order](../.agents/skills/caspro-work-order/SKILL.md): acotar un encargo futuro | Preparar WO cuando esa fase sea autorizada; no ejecutarla | [Programa](../docs/roadmap/program.md), spec del hito, gates, [plantilla](work-order.md) y QA | Según alcance; orquestador/reviewer y especialista si corresponde | C/G/T |
| [caspro-review](../.agents/skills/caspro-review/SKILL.md): evaluar candidato/evidencia | Review de PR, preparación de decisión de merge; no corregir durante review | Base/head/tree, WO/spec afectada, [rúbrica](review.md), QA | Según delta; reviewer separado y especialista por riesgo | C/G/T |
| [caspro-architecture](../.agents/skills/caspro-architecture/SKILL.md): mantener fronteras y decisiones | Amendment, ownership, motivo histórico o transferencia Wbpro; no rediseño implícito | [Boundaries](../docs/architecture/boundaries.md), contrato/ADR afectado | Transversal; Architecture + dueño | C/G/T |
| [caspro-economic-flow](../.agents/skills/caspro-economic-flow/SKILL.md): flujos internos | Inventory, Treasury, P2P, Sales y conciliación; no ledger ni publicación externa | Dueño local, spec, [CM0](../docs/specs/cross-cutting/command-matrix.md#cm0), hechos/transacciones pertinentes | Alto; integridad/dueño independiente | C/G/T |
| [caspro-accounting](../.agents/skills/caspro-accounting/SKILL.md): ledger y reporting | Posting, cierre, EEFF; no inventar mapping/política | [Accounting](../docs/accounting/architecture.md), M07/M08 y política/golden aplicable | Alto; Accounting independiente + validación profesional local | C/G/T |
| [caspro-compliance](../.agents/skills/caspro-compliance/SKILL.md): Tax y actos Corporate | Tax, BF, mutuo; no transporte CPE ni aprobación profesional por IA | [Tax](../docs/tax/architecture.md) o [Corporate](../docs/corporate/architecture.md), M09/M06 y gates | Alto; profesional competente + reviewer independiente | C/G/T |
| [caspro-external-effects](../.agents/skills/caspro-external-effects/SKILL.md): fronteras de proveedor | Jumpseller, CPE/Documents, email y otros proveedores; no confirmar dinero | [Integraciones](../docs/architecture/integrations.md), flow del proveedor y dueño | Alto; contratos/seguridad + dueño independiente | C/G/T |
| [caspro-ui](../.agents/skills/caspro-ui/SKILL.md): interfaz | Color, teclado, presentación/interacción; no alterar semántica de negocio | [UI](../docs/architecture/ui.md), spec de superficie | Visual: proporcional; acción sensible: reviewer del dueño | C/G/T |
| [caspro-platform](../.agents/skills/caspro-platform/SKILL.md): plataforma por modo | M01, Party/M02, RLS/seguridad, restore; no cargar todos los modos | [M01–M02](../docs/specs/milestones/runtime-masters.md) y contrato del modo | Acceso/operación alto; seguridad/operaciones independiente | C/G/T |
| [caspro-normative-research](../.agents/skills/caspro-normative-research/SKILL.md): comprobar evidencia normativa | Nueva norma, vigencia, RTF, PCGE o aplicabilidad; no sustituir política | [Registro normativo](../docs/research/normative/normative-register.md), fuente oficial y dueño | Alto si afecta política; profesional + dueño/reviewer | C/G/T |

## Contexto ganado por la tarea

Base compartida: router + estado + protocolo ya cargados; catálogo para seleccionar, no diez cuerpos. Tarea: una skill, sección de contrato/spec del dueño, gates locales y WO cuando aplique. Contexto opcional solo por condición del cuerpo: otra frontera, QA/evidencia de un claim, research de vigencia/procedencia o ADR/history para una pregunta histórica. Por defecto no cargar carpetas completas, history, WOs antiguas, todo research/evidence, todos los hitos o todas las skills. Si falta contrato, declarar la incertidumbre y escalar esa parte; no suplirla leyendo indiscriminadamente.

## Compatibilidad efectiva

**C — Codex:** AGENTS como router y `.agents/skills` como ubicación de discovery documentada; la selección real depende de sesión/configuración y presupuesto de metadata. **G — Gemini CLI:** [adaptador](../GEMINI.md), import de AGENTS y alias `.agents/skills`, sujeto a trust/consent y comprobación de discovery en raíz. **T — Claude Code, lectura textual:** [adaptador](../CLAUDE.md) importa AGENTS y dirige al archivo elegido; esta ubicación compartida no instala skills nativas `.claude/skills` ni comandos `/caspro-*`.

Los tres leen el mismo Markdown; solo C/G tienen discovery documentado en esta ubicación. No hay symlinks, copias, wrappers por skill, hooks ni configuración que eleve permisos. Si falta discovery puede usarse lectura explícita permitida; nunca eludir consentimiento denegado. [Research oficial y límites](../docs/evidence/agent-system-research.md#b-research-externo-oficial) documentan las diferencias; esta tabla no acredita ejecución real en cada harness.
