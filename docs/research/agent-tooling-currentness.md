# Compatibilidad actual de instrucciones y skills

Corte de consulta: **2026-09-12 — RESEARCH_CUTOFF**. Seguimiento documental del [expediente histórico](../evidence/agent-system-research.md), cuyo corte no se modifica. Fuentes oficiales web mutables abiertas en esta misión; no release fijada ni prueba de ejecución en los tres clientes. Este memo describe discovery; [protocolo](../../.ai/README.md) y [review](../review.md) conservan autoridad y fase CasPro. No se instalaron herramientas ni cambiaron trust, permisos o configuración del host.

## Codex

**VERIFIED_CURRENT — conservar AGENTS y `.agents/skills`.** No se encontró `codex` en PATH mediante consulta local; se recurrió a documentación oficial. La metadata de esta sesión anuncia las diez skills CasPro, pero no demuestra todas las variantes del CLI.

| Fuente | Hecho comprobado | Implicación CasPro |
|---|---|---|
| P01 — [AGENTS.md oficial](https://learn.chatgpt.com/docs/agent-configuration/agents-md), redirigido desde developers.openai.com/codex/guides/agents-md | Cadena al iniciar: global y raíz→directorio actual. Por nivel: AGENTS.override.md, luego AGENTS.md, luego fallback configurado; máximo un archivo no vacío por directorio. Lo más cercano prevalece. Tope agregado project_doc_max_bytes: 32 KiB por defecto | Root compacto, sin override/fallback nuevo; no asumir lectura de todas las subcarpetas ni que el límite sea presupuesto total del modelo |
| P02 — [Skills oficial](https://learn.chatgpt.com/docs/build-skills), redirigido desde developers.openai.com/codex/skills | Discovery de `.agents/skills` desde CWD hasta raíz Git; metadata inicial, cuerpo bajo demanda. Names iguales no se fusionan. Lista inicial limitada a 2% del contexto o 8.000 caracteres si se desconoce; puede truncar descripciones/omitir skills. SKILL.md requiere name y description | Diez nombres únicos; catálogo explícito para resolver fuente si metadata no basta, nunca ampliar permisos por discovery |
| P09 — [Configuración oficial](https://learn.chatgpt.com/docs/config-file/config-basic) | Flags/overrides preceden configuración del proyecto; `.codex/config.toml` se carga en proyectos confiables, con prioridad del directorio más próximo | No existe configuración de proyecto aquí. Documentación no sustituye restricciones reales del harness |

## Claude Code

**VERIFIED_CURRENT — conservar adaptador textual.** Solo se cambia su enlace de investigación. No se instala `/caspro-*`, plugin ni wrapper.

| Fuente | Hecho comprobado | Implicación CasPro |
|---|---|---|
| P03 — [Memoria e instrucciones](https://code.claude.com/docs/en/memory) | Managed/user/project y directorios aportan contexto; CLAUDE.local.md se añade después de CLAUDE.md por nivel. Ancestros cargan al inicio; descendientes cuando se leen. Se concatenan, no son una política ejecutable de override. Imports @ relativos al archivo, hasta cuatro saltos; archivos importados consumen contexto. AGENTS necesita import explícito. Recomendación: menos de 200 líneas por CLAUDE.md | `@AGENTS.md` conserva fuente única; no importar catálogo y diez cuerpos. No afirmar precedencia de permisos desde el orden del texto |
| P04 — [Skills](https://code.claude.com/docs/en/skills) | Rutas documentadas usan `.claude/skills` en proyecto/usuario/entorno administrado, además de plugins y otras ubicaciones declaradas. El catálogo de rutas no documenta `.agents/skills` como discovery nativo | La lectura por enlace sigue siendo textual. Ausencia en la lista oficial no se presenta como prueba de que ningún plugin pueda habilitarlo; CasPro no instala tal mecanismo |
| P05 — [Seguridad](https://code.claude.com/docs/en/security) | Trust y controles dependen del modo; la verificación interactiva no equivale al modo no interactivo. No hay inmunidad universal a inyección | Mantener límites efectivos; no convertir import, skill o allowlist en autorización del propietario |
| P10 — [Subagentes](https://code.claude.com/docs/en/sub-agents) | Hay contextos separados y forks que heredan conversación; herramientas/permisos dependen de configuración y modo | Handoff explícito del protocolo sigue válido; no afirmar que todo subagente carece de memoria o que todo fork es independiente. No se ejecutó delegación |

## Gemini CLI

**VERIFIED_CURRENT — conservar import, alias y comandos.** Solo se cambia el enlace de investigación; no se activa trust desde esta misión.

| Fuente | Hecho comprobado | Implicación CasPro |
|---|---|---|
| P06 — [GEMINI.md](https://geminicli.com/docs/cli/gemini-md/) | Concatena contexto global, workspace/ancestros y JIT hasta raíz confiable. Imports @ admiten rutas relativas/absolutas. `/memory show` inspecciona contexto; `/memory reload` lo recarga | `@./AGENTS.md` permanece correcto; no confundir carga de memoria con discovery de skills |
| P07 — [Skills](https://geminicli.com/docs/cli/skills/) | Built-in < extensión < usuario < workspace. `.agents/skills` es alias y prevalece sobre `.gemini/skills` dentro del mismo nivel. Discovery carga metadata; activate_skill requiere consentimiento y añade cuerpo/estructura. `/skills list` y `/skills reload` siguen vigentes; refresh es alternativa documentada | Raíz y skill nombrada comprobables; fallback textual solo si lectura permitida, nunca tras rechazo de activación. No duplicar skills para cada cliente |
| P08 — [Trusted folders](https://geminicli.com/docs/cli/trusted-folders/) | Folder Trust es configurable y está desactivado por defecto según esta página; habilitado, workspace no confiable restringe funciones y headless puede fallar. No es una barrera siempre activa | El adaptador exige respetar trust efectivo, no promete enforcement universal. Verificar configuración al habilitar el host; no usar bypass para simular compatibilidad |

## Límites y próxima verificación

Las tres rutas siguen documentadas; no se demostró cambio incompatible desde el expediente anterior. La ausencia de configuraciones Copilot/Cursor/Windsurf/MCP locales no justifica crearlas ni investigar proveedores adicionales. No hay garantía de portabilidad de metadata externa, permisos, plugins o comandos entre hosts.

Antes de una WO ejecutable que dependa del harness: identificar versión/configuración reales y comprobar discovery/lectura de la skill elegida con los controles efectivos. Reabrir esta investigación solo ante cambio de cliente/versión, warning de discovery, contradicción o tarea que dependa de un hecho mutable. Esa comprobación no autoriza la WO ni es requisito para declarar correcta una simple edición documental.
