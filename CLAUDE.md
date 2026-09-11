# Claude Code — adaptador CasPro

@AGENTS.md

Claude Code importa únicamente el router. Selecciona en el [catálogo](.ai/skills.md) y lee explícitamente el SKILL.md canónico indicado antes de trabajar; no importes todos los playbooks mediante @.

Aquí las skills están en `.agents/skills`, no en el discovery nativo `.claude/skills`: el soporte CasPro para Claude es **routing y lectura textual**, sin slash commands propios ni activación nativa garantizada. No simules que `/caspro-*` está instalado. Si no puedes leer el archivo, informa la ruta y detén ese alcance.

Conserva permisos/trust efectivos de Claude; no uses hooks, imports o allowed-tools para ampliar autorización. Un subagente recibe objetivo, candidato, fuentes mínimas y límites explícitos del [protocolo](.ai/README.md), no una supuesta memoria heredada. Estos detalles son convenciones del harness, no otra fuente CasPro; [compatibilidad investigada](docs/evidence/agent-system-research.md#b-research-externo-oficial).
