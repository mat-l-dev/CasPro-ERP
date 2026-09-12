# Gemini CLI — adaptador CasPro

@./AGENTS.md

Gemini CLI documenta `.agents/skills` como alias de workspace. Inicia en la raíz confiable del repositorio; usa `/skills list` y `/skills reload` para comprobar discovery según la versión instalada. El [catálogo](.ai/skills.md) selecciona el archivo compartido; no importes todos los playbooks en memoria.

Respeta trust, consentimiento de activación y permisos efectivos del harness. Si la versión no descubre el alias, selecciona por catálogo y solicita lectura explícita permitida del SKILL.md; describe ese modo como textual, no nativo. Esta alternativa no elude una activación/lectura denegada. Si la fuente no está accesible, detén esa parte y señala la limitación.

`/memory show` permite comprobar contexto cargado. El [protocolo](.ai/README.md) gobierna roles y handoff incluso si se usa un subagente; no se instalan extensiones, agentes remotos ni políticas de herramientas. [Compatibilidad investigada](docs/research/agent-tooling-currentness.md#gemini-cli).
