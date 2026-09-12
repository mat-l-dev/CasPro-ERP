# PR #7 — informe del autor A–AS: automatización, Case Flow y Accounting IA

Fecha/corte2026-09-12. Expediente del **autor**, no revisión independiente ni autoaceptación. [Review](../review.md) posee fase. Delta acotado encargado después del PASS inicial; no reabre normativa ni producto aceptado. Investigación pública/documentación y razonamiento adversarial; **no tests, builds, Docker, runtime, migraciones ni WOs**. Las protecciones propuestas requieren validación ejecutable posterior. No se probaron proveedores ni se enviaron datos empresariales.

## A. Baseline y PR verificados

Antes de editar: rama `docs/governance-roles-configuration-policies`, working tree limpio, fetch y comparación con origin; PR #7 OPEN, base main, head `9213275ffd49bbd59bb666459ba57a11bac1261f`, tree `3352ca1e376c1f320725b37ac707c3565b765630`. main/origin/main `17086593d28c2619fba6cca6827fd998525bb158`, tree `e24e999a3de4541c2a398b9372bf41591f9df634`. Coincidencia con encargo y GitHub verificada. El PASS inicial comunicado por propietario sigue válido para ese candidato; su aplicabilidad al nuevo HEAD queda superada por requisitos nuevos, no por revisión equivocada. [Expediente anterior](governance-roles-configuration-policies.md) se preserva sin reescritura.

## B. Investigación de ERP maduros

[Benchmark AF-S01–13 y28–30](../research/automation-flow-ai-benchmark.md): SAP S/4HANA/Fiori, Dynamics Finance, NetSuite y Odoo19; templates/posting profiles/account determination, recurring/periodic, devengo, matching bancario, scheduler/eventos, workspaces/approvals y ledger predictivo. Se distingue R/U/T/N, edición/consulta y límite de acceso. Patrón elegido: hecho/plantilla/regla/ocurrencia/mandato separados. Allocation engine universal queda trigger; ledger predictivo SAP no demuestra LLM ni normativa CasPro. Fuentes oficiales, sin tenant ni comparativo empírico de productos.

## C. Investigación UX de procesos

SAP lanes/zoom/relaciones, related records NetSuite, contexto Chatter, workspace de cierre Dynamics y canvas n8n como referencia visual; BPMN como notación, sin conformidad/ejecución asumida. Se adopta lectura de relaciones reales y navegación al dueño; se rechaza secuencia ficticia y constructor de procesos. Guía Fiori recuperada es versión anterior identificada, no se presenta como UI5 vigente2026.

## D. Comparación de bibliotecas

[Matriz de renderers](../research/automation-flow-ai-benchmark.md#comparación-de-renderer): React Flow/xyflow, Cytoscape, D3, ELK y SVG/Canvas nativos; licencias/distribuciones, dependencias, SSR/HTMX, CSP, teclado/ARIA, layout, volumen, export y mantenimiento. Elección provisional Cytoscape vanilla lazy M04 con lista SSR equivalente; SVG pequeño antes, ELK solo necesidad de layout medida; React Flow alternativa condicionada, sin SPA. No bundle/latencia/WCAG acreditados; bytes npm son desempaquetados, no descarga final.

## E. Arquitectura Case Flow

[Contrato de flujo](../specs/cross-cutting/case-flow-preview.md#identidad-y-relaciones): projection owner de presentación, fuentes por dueño, identidad entidad/caso/revisión y manifest. Grafo/lista/timeline leen mismo DTO, sin autoridad de negocio, relaciones N:M/reversas/versiones y filtros Business/Documents/Money/Stock/Accounting/Compliance. Un pago a múltiples objetivos no se suma por arista.

## F. Estados y relaciones

Nodos conservan estado fuente y normalización versionada; COMPLETE/PENDING/ACTION_REQUIRED/WAITING_EXTERNAL/BLOCKED/HOLD/ERROR/UNKNOWN/NOT_APPLICABLE/SUPERSEDED. ORIGINATES_FROM/FULFILLS/SUPPORTS/ALLOCATES_TO/DELIVERS/DOCUMENTS/REVERSES/SUPERSEDES/SATISFIES_REQUIREMENT tienen owner y extremos válidos. Frescura va separada del estado empresarial. Layout no convierte ciclos históricos en transición inválida.

## G. Esperado pero faltante

[RequirementAssessment](../specs/cross-cutting/case-flow-preview.md#requisitos-estados-y-resumen) procede de obligación/compromiso/política de dueño, con revisión y razón. No contrato obligatorio universal. Instalación comprometida sí exige evidencia aplicable; opcional/N/A no bloquea completitud, UNKNOWN no se hace N/A automáticamente. COMPLETE solo a corte completo; vista restringida no certifica estado global.

## H. Próxima acción y excepciones

Detalle muestra qué falta/por qué/fuente/owner/revisión y acción válida. NextActionDescriptor referencia comando registrado y al confirmarlo revalida permisos/estado; no «cerrar expediente» genérico. Focus/filter/excepciones no desaparecen al colapsar grupo; dos paneles y retorno conservan posición/foco. Requisitos ocultos no se revelan por conteo/posición/color. Lista/teclado sustituye toda interacción necesaria del grafo.

## I. Read model y rendimiento

[Proyección](../specs/cross-cutting/case-flow-preview.md#proyección-seguridad-y-recuperación): outbox durable PostgreSQL, aplicación idempotente, generación/checkpoints de commits completos, reconciliación de huecos y rebuild con swap. Apertura no hace docenas de consultas de dominios. ACL vigente/disclosure_epoch en misma transacción de cambios de divulgación retiene proyección vieja antes de filtrar/layout; cache por entidad/alcance/revisión. No Kafka/Redis/event sourcing.

## J. Objetivos candidatos

[Tabla P50/P95](../specs/cross-cutting/case-flow-preview.md#objetivos-candidatos-de-rendimiento): shell, grafo inicial, detalle, filtro, PDF y comparación mensual. Datasets30/500/5000 nodos, hasta20000 aristas; primer vecindario50/100 o lista50. Dataset mensual5000 hechos/20000 líneas selladas, inferencia IA excluida del tiempo comparador. Dispositivo/red/concurrencia/caché y límites publicados como hipótesis, ninguna medición conseguida. Fallback lista/página/metadata y cancelación antes de ampliar recursos.

## K. Preview PDF/XML

[Preview](../specs/cross-cutting/case-flow-preview.md#preview-pdf-y-xml): original inmutable y hash, derivados versionados/redactados, render local aislado, visible/vecinos y límites, Range condicionado,100MB sin prefetch total. PDF activo/XML XXE/script/XSLT bloqueados; metadata/preview/download separados. Preview-only recibe representación, no URL/bytes originales. Revocación por gateway por request, signed bearer reconoce TTL residual. Original ausente no se reconstituye de raster; firma se verifica sobre bytes firmados, no OCR.

## L. Taxonomía de plantillas

[Ocho familias](../architecture/automation.md#familias-de-plantillas): contable, documental, comercial, email, import mapping, site form, reporte y AIRequestTemplate. Comparten descriptor de revisión/scope/vigencia/aprobación/variables/preview/evidencia/usos, no dueño ni motor de payload. Sin SQL/código/fórmulas abiertas ni settings genéricos.

## M. Journal templates

[JournalTemplate](../accounting/templates-automation-shadow.md#journal-templates-y-reglas-determinísticas): roles/cuentas aplicadas, líneas/Decimal/moneda/dimensiones, variables con fuente, policy refs y guardas. Ejemplos comisión, renta, prepago, devengo, reclasificación y cargo recurrente. Produce DRAFT; falta cuenta queda UNMAPPED sin suspense inventado; revisión usada se conserva.

## N. Taxonomía de automatización

[Ocho modos](../architecture/automation.md#modos-y-riesgo): MANUAL/TEMPLATE_DRAFT/RULE_AUTO_DRAFT/SCHEDULED_DRAFT/EVENT_AUTO_DRAFT/RULE_AUTO_EXECUTE/AI_SUGGEST/SHADOW_AI_EXECUTE. Modo conocido antes del modelo; low lectura, medium draft, high candidato económico, critical efecto oficial/externo. Ningún riesgo/toggle concede autoridad.

## O. Posting determinístico

Regla tipada de Accounting y A03 completo; autoexecute oficial OFF inicial, solo mandato separado vigente y validación profesional/técnica. Sugerencias/shadow no alimentan auto-post oficial. Identidad del ejecutor determinístico separada del modelo/shadow. Se corrige la prohibición absoluta de M07 «IA eligiendo cuentas»: ahora permite recomendar dentro del conjunto aplicado, sin decidir/postear oficial.

## P. Recurrencia

[Recurrencia](../architecture/automation.md#recurrencia-concurrencia-y-cambios): fuente real y cobertura/componente, clave de ocurrencia independiente de revisión de regla, tiempo local/zona/UTC, DST explícito, catch-up con preview, período cerrado HOLD y mandato vigente al efecto. Regla cambiada no genera doble obligación ni overwrite de draft manual.

## Q. Automation Center

[Centro](../architecture/automation.md#centro-observabilidad-y-simulación) indexa descriptores/runs de dueño y enlaza configuración/acción local. Último/próximo, por qué, fuentes/revisiones, responsable, riesgo/mandato, duración/efectos/retry/evidencia, pausadas/fallos/coste. No workflow editor ni nuevo módulo económico.

## R. Asistente Accounting IA

Diseño confirmado M07: tratamiento/cuenta candidata, razones cortas, alternativas/faltantes/abstención. Contexto autorizado y política aplicable; no decide obligación, marco ni regla fiscal. Human review conserva procedencia y corrección. Fallo proveedor conserva ruta manual/determinística.

## S. Neutralidad de proveedor

[Matriz OpenAI/Gemini/DeepSeek/local](../research/automation-flow-ai-benchmark.md#proveedores-ia-y-evidencia-disponible) y adapter propio de contrato: comparar schema/español/calidad/contexto/latencia/coste/privacidad/DPA/residencia/licencia/versiones/rate limits. Ningún ganador ni llamada real. Model card/endpoint no acreditan contrato TILMUX; local no elimina coste de operación o fuga por proceso. Cambiar adapter exige evaluar otra vez.

## T. Request minimizado

[Allowlist](../accounting/templates-automation-shadow.md#solicitud-minimizada-y-respuesta): monto/moneda/fechas/tipo/coverage/pago conocido, framework/policy narrow excerpts, dimensiones necesarias y cuentas candidatas. Identidad tokenizada, sin contratos/PDF/nombres/bancos/secretos por defecto; falta de contexto => abstención, no más exfiltración automática.

## U. Output estructurado

Schema cerrado, líneas Decimal string/cuentas/dimensiones del conjunto autorizado, treatment enum, rationale breve, policy refs conocidas, missingFacts/alternatives/warnings/abstain y confidence opcional no autoritativa. Refusal, vacío, mal JSON, ID inventado o NO_VALID_ACCOUNT_FOUND no producen propuesta ejecutable. Sin chain-of-thought ni confianza como permiso.

## V. Sugerencia a draft

[Aceptación](../accounting/templates-automation-shadow.md#sugerencia-y-aceptación-a-borrador) requiere accounting.ai.accept_draft AND accounting.prepare, revisión esperada, idempotencia, fuente/cuenta/período/política vigentes, balance/FX/dimensiones y scope. Aceptar rellena draft; humano edita con diff/origen. Posting humano posterior revalida A03/SoD; balance correcto no garantiza semántica.

## W. Promoción a regla

[Calidad/promoción](../accounting/templates-automation-shadow.md#promoción-a-regla-y-calidad): patrón→RuleCandidate→replay congelado y holdout temporal→handler/predicados tipados→revisión profesional→ImpactManifest→aprobación/vigencia. >=10 ejemplos revisados/2 fechas solo heurística de abrir evaluación. Contraejemplo material retiene; aceptación repetida/consenso no verdad ni entrenamiento automático.

## X. Prompt templates

AI-TPL-ACCOUNTING-CLASSIFY con revisión/hash/esquemas/input mínimo/policy/abstención/capacidades proveedor/suite/vigencia. Cada sugerencia/run conserva modelo efectivo además de alias, adapter/schema/template/policy y digest. Cambios invalidan comparabilidad; salida vieja no se sobrescribe ni se promociona sola.

## Y. Shadow Accounting

[Shadow](../accounting/templates-automation-shadow.md#shadow-accounting-e-aislamiento): cápsulas de hechos minimizados, journal experimental propio y corrección por nuevas revisiones, ninguna escritura oficial de ningún dominio. No maestros/contratos/bancos duplicados ni segundo ERP/EEFF. Modelo no accede a SQL/tools generales; executor solo sus operaciones shadow.

## Z. Aislamiento recomendado

Comparación tablas/Core schema/DB separada/cluster físico: se recomienda DB PostgreSQL separada en cluster existente, proceso/credenciales propios, sin CONNECT/FDW/dblink/HTTP-write Core. Recursos/superusuario siguen compartidos; B02/B13/B15/C10 validan riesgo residual. Exporter oficial solo lectura/cápsula técnica; comparator principal independiente readonly; IA no ve oficial/labels antes de sellar run.

## AA. Modos shadow

[Modos/recuperación](../accounting/templates-automation-shadow.md#modos-ledger-experimental-y-recuperación): inicial on-demand de período congelado M07; lote nocturno acotado M08 tras evidencia; async live por trigger. Run/policy/model/template/fact revisions inmutables, consumos por linaje, reversas/deltas sin duplicar bruto. Pérdida shadow no para Core; restaurar resultado no es regenerarlo con modelo nuevo.

## AB. Comparador

[Comparador](../accounting/templates-automation-shadow.md#comparador-oficial-versus-shadow): corte/población/fuentes compatibles, unidad hecho/componente/versión, contribución efectiva N:M, cuenta/lado/monto/moneda/período/dimensiones/timing/clasificación/devengo/COGS/FX/cobertura. MATCH/EQUIVALENT/PARTIAL_DIFFERENCE/MATERIAL_DIFFERENCE/SHADOW_ABSTAINED/OFFICIAL_PENDING/SHADOW_ONLY/OFFICIAL_ONLY; INCOMPLETE/INPUT_MISMATCH retienen conclusión. Equivalencia/materialidad aprobadas por Accounting, nunca votación IA.

## AC. Segunda revisión mensual

[Experiencia mensual](../accounting/templates-automation-shadow.md#experiencia-mensual-y-evaluación-mult-modelo): dashboard/lista de cobertura y diferencias, drills a hecho, oficial, shadow, política/provider/evidencia; denominadores explícitos y jobs pendientes visibles. No comparación final válida con población incompleta ni prueba de cierre; export experimental no EEFF.

## AD. Evaluación multimodelo

Mismo dataset/input minimizado/corte, A/B/baseline determinístico, sin respuestas/labels previos; runs sellados separados, métricas de calidad revisada/coste/latencia/abstención y confianza equivocada. No todas las APIs por cada hecho vivo ni acuerdo como verdad. Presupuesto y propósito aprobado por proveedor.

## AE. Ciclo de calidad

Separar aceptación/rechazo operativo de REVIEWED_CORRECT/WRONG/UNRESOLVED/INSUFFICIENT_INPUT con revisor/evidencia. Rechazo repetido pausa/investiga; aceptación incorrecta no entrena verdad. Overrides y correcciones conservan versión/origen. Fine-tuning/reuso privado necesita mandato separado; dataset sintético/anonimizado autorizado inicial, sin evaluación ejecutada ahora.

## AF. Observabilidad

Runs con trigger/razón/revisiones/input digest/actor/mandato/intención/resultado/efectos/duración/retry/last-next y suite aplicable. Alertas por lag, huecos, jobs pendientes, coste/expiración/cambio de política; verde técnico no éxito empresarial. Logs redactados, sin secretos ni prompts privados completos por defecto.

## AG. Simulación

Manifest congelado histórico autorizado/sintético, reloj y políticas explícitos, destino aislado sin puertos/credenciales de escritura canónica ni egress de efectos. Produce propuestas/diffs, no facts/asientos/documentos/intentos externos. El paso real reevalúa autorización/inputs; bandera dry-run de UI no es aislamiento suficiente.

## AH. Seguridad y privacidad

[Roles/capabilities](../architecture/roles-delegation.md#capacidades-del-delta-de-automatización):15 IDs nuevos,12 humanos/3 técnicos,21 roles existentes; scopes por capability sin grant automático, AND permisos de dueño. POL-18/19/21/23/26 extendidas sin IDs nuevos. Disclosure_epoch evita permiso documental obsoleto; preview-only no recibe original. Shadow DB/proceso sin Core writes, provider sin tools, budgets con reserva atómica y coste incierto retenido. Prompt injection/retención/modelo mutable cubiertos. A0/B16/C13/D6 y validaciones profesionales permanecen abiertos según su clase.

## AI. Descubrimientos adicionales

[16 mejoras](../research/automation-flow-ai-benchmark.md#descubrimientos-y-puntuación), basadas en los patrones inspeccionados y necesidades CasPro: home por rol, vistas guardadas, dossier, why-blocked, palette/search, autosave, bulk/dedup, cockpits, digest/help, setup, widgets, móvil, offline, builder, multimodelo live y Office. Solo vistas personales tipadas/dossier añaden conveniencias canónicas; el resto NOW profundiza lo ya exigido/existente.

## AJ. Puntuación

Research registra V valor/F frecuencia/E reducción error/A auditoría y C complejidad/P rendimiento/R seguridad-privacidad/K coste de infraestructura-operación en escala1–5, dependencia/hito y P0/P1/P2/P3/reject. Juicio de diseño, no puntuación empírica sumada como prueba. Coste de infraestructura/operación/seguridad explicitado en dependencias y decisiones; beneficio no excusa ocultar autoridad ni cargar todas las pantallas M01.

## AK. Ahora, después y rechazado

DISCOVERED_AND_RECOMMEND_NOW: vistas personales/dossier y profundización de colas/why-blocked/diff/cockpit/setup/mobile fallback existentes. DISCOVERED_BUT_LATER: palette/global recientes, autosave avanzado, digest personal, widgets y Office colaboración por necesidad medida. REJECTED_AS_OVERENGINEERING: escritura económica offline, BPMN/n8n ejecutable/Rule DSL y multimodelo automático por hecho/autoaprendizaje. NOW es recomendación de diseño del autor, nunca aceptación independiente.

## AL. Roadmap

[Programa](../roadmap/program.md): primitives M01, listas/fuentes M02–03, Case Flow/preview M04, compras/tesorería M05–06, templates/reglas/recurrencias/AI→draft/shadow base M07 y comparador mensual M08, Tax nodes M09. Sin renumerar ni retrasar crédito B2B confirmado a M10. D01 deja de describir Accounting IA como diseño opcional, mantiene activación y pilotos ajenos opcionales. WOs solo misión posterior autorizada.

## AM. Casos adversariales

Resultado de cada fila: **resuelto en contrato documental**, no prueba ejecutada ni PASS de runtime. F = [flujo/preview](../specs/cross-cutting/case-flow-preview.md); A = [automatización](../architecture/automation.md); C = [Accounting/AI/shadow](../accounting/templates-automation-shadow.md); R = [roles](../architecture/roles-delegation.md#capacidades-del-delta-de-automatización). IDs1–70 corresponden al encargo,71–80 amplían riesgos de frontera. Independiente debe refutar candidato exacto.

| Caso | Intento / contraejemplo | Resultado requerido y fundamento |
|---|---|---|
| 01 | Venta sin contrato, contrato N/A | F requisito de dueño; N/A no bloquea, no inventar contrato obligatorio |
| 02 | Instalación requerida sin evidencia | F nodo esperado REQUIRED, acción del dueño y resumen bloqueado |
| 03 | Entrega parcial | F ramas con cantidades/revisiones, sin completar toda venta por una entrega |
| 04 | Dos CPE para venta | F N:M DOCUMENTS, identidades/versiones separadas sin reemplazo ficticio |
| 05 | Pago aplicado a varios objetivos | F ALLOCATES_TO por aplicación; no sumar pago por arista |
| 06 | Refund/reversa | F rama REVERSES y hechos del dueño, sin borrar original |
| 07 | CPE sustituido | F SUPERSEDES conserva historia y distingue vigente |
| 08 | Nodo de documento privado | F ACL antes de DTO/layout/conteo; no fantasma/posición filtrada |
| 09 | Proyección antigua | F STALE/corte explícito, no COMPLETE vigente ni autoridad de comando |
| 10 | Actualización perdida | F outbox durable/reconciliación de huecos/rebuild por generación |
| 11 | Cientos de nodos | F vecindario/grupos/lista paginada/worker; sin DOM completo |
| 12 | Dominio no disponible | F UNKNOWN/INCOMPLETE y reintento, no estado inventado |
| 13 | Sales sin permiso Tax | F carriles/relaciones filtrados; vista parcial sin certificar caso global |
| 14 | Grafo completo con requisito bloqueado | F summary considera requisitos de dueño, no solo documentos presentes |
| 15 | Opcional impide completar | F OPTIONAL/N/A no bloquean COMPLETE |
| 16 | Next action errónea | F descriptor de comando del dueño; revalidación al uso, no transición UI |
| 17 | Nodo antiguo como vigente | F ID/revisión/corte y SUPERSEDED; abrir no sustituye silenciosamente |
| 18 | Caso de entidad equivocada | F/R entidad/scope/deep link/cache deniegan, sin confirmar existencia |
| 19 | PDF100MB | F metadata primero, páginas/Range condicionado, límite/cancelación/fallback |
| 20 | PDF malformado | F proceso aislado/límites/cuarentena; original no modificado |
| 21 | Contenido activo | F no JS/launch/externals; CSP/sandbox y sin egress |
| 22 | URL sin autorización | F gateway reautoriza objeto/revisión/request; storage privado |
| 23 | Derivado existe y original falta | F ORIGINAL_MISSING; no integridad completa ni reconstrucción de original |
| 24 | Preview viejo tras revisión | F clave hash/version, cancelar request vieja y descartar respuesta tardía |
| 25 | Derivado confundido con firmado | F etiqueta derivado; verificación solo bytes originales/evidencia real |
| 26 | XML enorme | F parseo bounded/incremental; metadata o download autorizado, sin DOM total |
| 27 | Formato no soportado | F estado explícito/metadata; no conversor universal automático |
| 28 | Metadata permitida sin download | F/R documents.view no implica preview/download; ningún byte original |
| 29 | Regla cambia tras draft | A/C STALE/diff/revisión, no overwrite ni permiso heredado |
| 30 | Mismo hecho dispara otra vez | A/C intent/occurrence y comando idempotentes; referencia existente |
| 31 | Ocurrencia recurrente duplicada | A clave fuente/período/componente sin ruleRevision; único consumo |
| 32 | Job ejecuta después de nueva política | A guardas actuales/epoch/M25; retener o reevaluar, no bypass |
| 33 | Cuenta retirada | C validar catálogo/vigencia/postabilidad; UNMAPPED, no remap silencioso |
| 34 | Período cerrado | A/C HOLD; no mover fecha ni reabrir automáticamente |
| 35 | Humano edita generado | A/C preservar diff/origen; regeneration requiere revisión explícita |
| 36 | Cuenta ausente en plantilla | C UNMAPPED; sin cuenta de suspense inventada |
| 37 | Cambio DST/timezone | A zona IANA/UTC/offset, hora ambigua/gap definidos y fecha económica separada |
| 38 | Mandato expirado | A validación al efecto, job no autoriza por haber sido programado |
| 39 | Regla cruza entidad | A/R ámbito por capability/fuente, reautorizar antes de comando |
| 40 | Simulación escribe canónico | A puertos/credenciales separados, sin egress/commit oficial |
| 41 | IA inventa PCGE | C conjunto cerrado AppliedAccountIds; rechazo/NO_VALID_ACCOUNT_FOUND |
| 42 | JSON inválido | C sin propuesta ejecutable; refusal/vacío/esquema aparte de semántica |
| 43 | Balanceado pero semántica errónea | C revisión humana/profesional, sin auto-post ni score como validación |
| 44 | Proveedor caído | C circuito/timeout/fallback manual; operación oficial continúa |
| 45 | Alias cambia modelo | C capturar versión efectiva; invalida evaluación/repro limitada |
| 46 | Prompt cambia | C nueva AIRequestTemplateRevision/hash/suite, no reusar aceptación vieja |
| 47 | Documento contiene inyección | C datos tipados/no tools/escritura/allowlist; abstener ante contaminación |
| 48 | Dato faltante induce alucinación | C missingFacts/INSUFFICIENT_INFORMATION; no inventar ni ampliar datos sola |
| 49 | Cuenta fuera de candidatos | C rechazo por allowlist incluso si existe en PCGE general |
| 50 | Humano rechaza repetidamente | C pausa/investiga fuente/template/modelo; no promocionar regla |
| 51 | Humano acepta respuesta errónea | C accepted≠reviewed correct; corrección por A03/reversa autorizada |
| 52 | Proveedores discrepan | C evaluación contra resultado revisado, no voto mayoritario |
| 53 | Confianza alta equivocada | C confianza no autoridad; registrar error/calibración y revisión |
| 54 | Costes superan límite | C reserva atómica previa/caps; PAUSED_BUDGET sin retries facturables ciegos |
| 55 | Retención contraria a política | C suspender envío; DPA/clases/retención antes de activar |
| 56 | Shadow ve otra entidad | C cápsula/credencial/scope aislados y sin lookup Core; deniega |
| 57 | Shadow asiento y oficial no | C distinguir OFFICIAL_PENDING de SHADOW_ONLY según elegibilidad/corte |
| 58 | Oficial asiento y shadow abstiene | C SHADOW_ABSTAINED, no missing ni match |
| 59 | Monto igual y período distinto | C diferencia de período/timing; no MATCH |
| 60 | Cuenta distinta equivalente | C EQUIVALENT solo mapping aprobado/vigente, no heurística IA |
| 61 | Hecho corregido procesado dos veces | C idempotencia por versión/componente y consumo por linaje/delta |
| 62 | Asiento oficial reversado | C contribución efectiva con linaje; snapshot correcto |
| 63 | Shadow compara superseded | C revisión/corte incompatibles retienen comparación, conservar historia |
| 64 | Política cambia a medio mes | C resolver por fecha/policy snapshot/cohorte, no última para todo |
| 65 | Shadow arregla pasado automáticamente | C run sellado inmutable; nuevo run/reversa/delta trazables |
| 66 | Input mínimo no permite decidir | C abstener/missingFacts; no autoexpansión a datos privados |
| 67 | DB shadow perdida | C Core sigue; restore separado/manifest, no reconstrucción oficial |
| 68 | Restore con modelo/template incompatible | C NON_REPRODUCIBLE/INCOMPLETE; no llamar nuevo modelo y afirmar mismo resultado |
| 69 | Comparación de cierre con jobs pendientes | C cobertura visible, sin comparación final válida ni cierre acreditado |
| 70 | Shadow se declara mejor por acuerdos | C prohibido inferir calidad desde acuerdo; resultado revisado/errores/cobertura |
| 71 | Revocación documental antes de actualizar proyección | F disclosure_epoch en misma transacción; DTO sensible retenido si difiere |
| 72 | Preview-only obtiene original por PDF.js | F servir raster/redactado; no URL original ni promesa DRM |
| 73 | Modelo copia asiento oficial usado para evaluarlo | C sellar run antes de comparator; modelos sin oficial/labels previos |
| 74 | Dos jobs reservan último presupuesto | C reserva atómica por entidad/propósito/proveedor; segundo se retiene |
| 75 | Editar calendario cambia clave de ocurrencia | A reglaRevision fuera de clave económica; no consumo duplicado |
| 76 | ID evento alto oculta commit tardío | F watermark de commits/corte completo y reconciliación, no MAX(id) |
| 77 | Fallo proveedor cambia a API no autorizada | C fallback solo adapter ya aprobado para datos/propósito; manual en otro caso |
| 78 | Export usa layout de nodos ocultos | F filtrar antes de layout y dossier por alcance/corte; sin geometría residual |
| 79 | Borrar input por retención conserva etiqueta reproducible | C registrar pérdida de reproducibilidad; hash no permite reconstruir dato |
| 80 | Modelo intenta invocar accounting.post | C/R no credenciales/puerto/grant oficial; shadow.post es otro ledger/principal |

## AN. Archivos del delta

18 archivos:5 nuevos y13 superficies existentes. Los contratos nuevos concentran reglas; rutas existentes solo sincronizan consumidor/autoridad/estado. Sin cambios en evidence anterior, history, archive, legacy, Wbpro, código o WOs.

| Archivo | Cambio |
|---|---|
| [research AF](../research/automation-flow-ai-benchmark.md) | Nuevo: fuentes, versiones/licencias, matrices ERP/UX/provider y16 mejoras |
| [Case Flow/preview](../specs/cross-cutting/case-flow-preview.md) | Nuevo: relaciones/requisitos/frescura/ACL/performance/documentos |
| [Automatización](../architecture/automation.md) | Nuevo:8 familias,8 modos, mandato/recurrencia/centro/simulación |
| [Accounting templates/IA/shadow](../accounting/templates-automation-shadow.md) | Nuevo: autoridad oficial, templates, AI→draft, promoción, aislamiento/comparador |
| [Este informe](intelligent-automation-visual-flow.md) | Nuevo: A–AS,80 casos y límites de evidencia |
| [Review](../review.md) | PASS inicial válido y nuevo delta pendiente re-revisión |
| [UI](../architecture/ui.md) | Ruta flujo/preview/automatización y límites |
| [IA](../architecture/ai-assistance.md) | Oficial vs shadow, diseño confirmado/provider-neutral |
| [Accounting architecture](../accounting/architecture.md) | Ruta extensión M07/M08 |
| [M07](../specs/milestones/accounting-deep.md) | Permite recomendar cuentas y separa draft/post/shadow |
| [Configuración](../architecture/configuration-governance.md) | Familias/ImpactManifest de templates/rules/IA |
| [Roles](../architecture/roles-delegation.md) |15 nuevos IDs exhaustivos;21 roles preservados |
| [POL register](../product/company-policy-register.md) | POL-18/19/21/23/26 extendidas;26 IDs preservados |
| [Capability map](../roadmap/capabilities.md) |8 filas del delta con dueño/input/output/dependencias/hito |
| [Programa](../roadmap/program.md) | Entrega progresiva y Accounting IA/shadow requeridos en diseño |
| [Gaps](../roadmap/decisions-gaps.md) | B16/D01 precisados, mismos A0/B16/C13/D6 |
| [Records](../specs/flows/records-signatures-site-packs.md) | Ruta preview/original/derivado/permiso |
| [Specs index](../specs/index.md) | Rutas del nuevo delta; readiness histórica preservada |

## AO. Commits

Research: `2d72ab7686d6ac81c8a74c804183c81584aad6a2`, tree `7d0ab254efc676521d0ed82bc8d24c3b491b9cff`. Segundo commit coherente reúne contratos/rutas/estado/este informe. Su hash final y tree se publican en cuerpo de PR #7 y entrega del autor después de sellar Git: incluir dentro del propio commit su hash sería autorreferencia imposible. Base de comparación del delta es `9213275ffd49bbd59bb666459ba57a11bac1261f`, no todo el diff de PR frente a main.

## AP. Identidad del nuevo candidato

La identidad exacta de HEAD/tree se obtiene después de commit y push y se re-verifica contra headRefOid de GitHub; se publica en PR/entrega final. El contenido de este informe pertenece al commit que lo introduce, identificable en Git. No usar el PASS previo como aceptación del nuevo contenido ni sustituir tree por nombre de rama mutable.

## AQ. Estado PR #7

[PR #7](https://github.com/mat-l-dev/CasPro-ERP/pull/7) es el único destino; mantener **OPEN**, misma rama/base, sin rebase, PR #8 ni merge. Estado requerido: **INITIAL INDEPENDENT PASS SUPERSEDED BY OWNER-REQUESTED BOUNDED DELTA — PENDING INDEPENDENT RE-REVIEW**. El cuerpo registra candidato original y nuevo HEAD/tree, alcance y ausencia de autorización de implementación. Re-verificación remota se informa en entrega final, no se anticipa un merge.

## AR. Decisiones del propietario y validación

**0 decisiones inmediatas del propietario; 0 nuevos bloqueadores de diseño identificados por el autor.** Se proponen renderer/topología/modo inicial y límites candidatos con fundamento; proveedor, datos/retención/coste/políticas reales y aval profesional quedan en gates existentes, no aprobados por este diseño. Se conserva promedio ponderado uniforme/FIFO físico, cuatro EEFF, crédito B2B requerido con activación controlada y todas las aceptaciones históricas.

Validación estática realizada:108 enlaces/anchors locales nuevos/tocados sin errores,18 archivos solo Markdown,80 casos completos y45 secciones A–AS;15 IDs nuevos y conjunciones,21 roles/26 políticas y A0/B16/C13/D6, ausencia de contradicción de autoridad en superficies actuales, graph projection/original inmutable/sin DSL/engine/settings genéricos y git diff --check. Casos1–80 son revisión estática del contrato, no tests. Rendimiento, CSP/WCAG, seguridad/restore/concurrencia, calidad/coste/retención de proveedor y actos contables reales permanecen REQUIRES LATER VALIDATION. Revisión independiente no ha evaluado aún este nuevo candidato.

## AS. Veredicto del autor

**PASS — INTELLIGENT AUTOMATION / VISUAL FLOW DELTA READY FOR INDEPENDENT RE-REVIEW**

**IMPLEMENTATION: NOT AUTHORIZED.** **A0 / B16 / C13 / D6.** Próxima acción: revisión independiente del HEAD/tree exactos de PR #7. Sin merge ni regeneración de Work Orders en esta misión.
