# Delta final: proveedor IA, coste y conciliación de declaraciones externas

Informe del autor A–AM, corte2026-09-12. Documentación/research exclusivamente; no revisión independiente simulada, software probado, datos TILMUX ni ejecución externa. El [estado vigente](../review.md) posee aceptación/autorización. Este expediente complementa sin reescribir [A–AF](governance-roles-configuration-policies.md) y [A–AS](intelligent-automation-visual-flow.md).

## A. Baseline verificado

Antes de editar: working tree limpio; rama `docs/governance-roles-configuration-policies`; [PR #7](https://github.com/mat-l-dev/CasPro-ERP/pull/7) OPEN/no merged, head `5886b821040b2ce535e6865bb8159cfd203d17d0`, tree `9a0497d75bf7665a3c1913db184e7a0f42d94ee6`. main/origin main `17086593d28c2619fba6cca6827fd998525bb158`, tree `e24e999a3de4541c2a398b9372bf41591f9df634`, verificados tras fetch y lectura de PR. Sin divergencia inicial.

Historia del propietario preservada: PASS inicial para `9213275ffd49bbd59bb666459ba57a11bac1261f`/tree `3352ca1e376c1f320725b37ac707c3565b765630`; segundo **PASS — INTELLIGENT AUTOMATION / VISUAL FLOW DELTA IS INTERNALLY COHERENT** para5886/tree9a04. Ambos válidos para sus candidatos. Decisiones posteriores requieren revisión final del nuevo candidato, no invalidan esas revisiones.

## B. Hallazgos oficiales DeepSeek

[Fuentes DS-F01–06](../research/deepseek-tax-filing-final-delta.md#deepseek-identidad-tarifa-y-límites-observados): alias actual `deepseek-flash` corresponde a V4.1-Flash; contexto1M/salida máxima384K publicados, JSON/tools disponibles. JSON puede salir vacío/truncado y no acredita esquema/semántica CasPro. Flash2500 conexiones concurrentes por cuenta publicado, no objetivo local; CasPro propone2. No inferencias ni benchmarks ejecutados.

## C. Identidad del modelo

INITIAL_AI_PROVIDER=DEEPSEEK / INITIAL_AI_MODEL=DEEPSEEK_V4_1_FLASH son decisiones cerradas. [Contrato AI](../architecture/ai-assistance.md#presupuesto-y-programación-del-proveedor-inicial) registra alias solicitado, versión efectiva si obtenible, UNKNOWN/reproducibilidad limitada si no, template/schema/policy/adapter/parameters/timestamp/pricing/input/output digests. Alias no equivale a snapshot de pesos; output sellado no promete replay idéntico del modelo.

## D. Tarifas y ventanas

[Tabla fechada de investigación](../research/deepseek-tax-filing-final-delta.md#deepseek-identidad-tarifa-y-límites-observados) conserva precios peak/off-peak de entrada hit/miss y salida en USD/millón, con fuente/efectividad. PricingRevision versionada gobierna ejecución, no constante de Accounting. Cruce de ventana sin criterio de facturación concluyente: reserva conservadora peak y conciliación, PENDING BILLING VALIDATION. Anuncio y pricing/changelog discrepan sobre futuro V4-Pro; se documenta, sin convertir Pro en estrategia elegida ni prometer V4.1-Pro disponible.

## E. Conversión de zona

Fuente actual define UTC; SchedulingPolicyRevision conserva ventana/días y revisión tarifaria, tzdb, instantes y conversión local con fecha. Ejemplos de Lima en investigación son cálculo derivado, no horario hardcodeado. Día local anterior y fines de semana se convierten desde UTC. Cambio de ventana crea revisión; runs históricos conservan contexto.

## F. Gobierno del objetivo USD10

[Límites/reservas](../architecture/ai-assistance.md#límites-reservas-y-observabilidad): target10/mes, autorización operativa0 hasta activación; defaults candidatos warning8/crítico9.50/hard10, diario1/2. Pool único con cuotas explícitas de propósito/modelo/entidad; sugerencias4/shadow4/replay1/evaluación1. Reserva atómica conservadora por intento; exposición incierta no se libera por timeout/reset. Override versionado con autoridad, motivo/importe/expiración. No promesa de factura total≤10 ni compra/recarga automática.

## G. Observabilidad de consumo

Usage hit/miss/output/reasoning sin duplicar tokens, retries/fallos, estimado/confirmado/reservado/incierto y saldo por día/mes/scope. Conciliación con factura y ajustes append-only, cobertura de cuenta declarada; cargos tardíos no se ocultan ni consumo externo se atribuye a CasPro sin fuente. Cada costo tiene intento/purpose/caso y modelo/tarifa; asignación a ítems de microbatch sería estimada sumando exactamente el total.

## H. Programación de fondo

INTERACTIVE inmediato bajo política; BACKGROUND_ELASTIC preferentemente off-peak; BACKGROUND_DEADLINE busca intervalo barato que quepa antes de deadline y permite peak autorizado; CRITICAL_IMMEDIATE futuro inactivo. Cola shadow limitada/checkpoints/corte, procesamiento sin locks/red en commit oficial, resultados sellados y comparador existente. Caducidad de job queda visible; no falso mes completo. No se retrasa transacción oficial ni se bloquea ERP por coste/proveedor.

## I. Batching recomendado

Inicialmente un hecho/componente por request; lote de worker hasta25 no significa prompt multihecho. Prefijo común minimizado puede ahorrar cache sin mezclar casos. Microbatch2–5 LATER solo compatible por entidad/purpose/política/cuentas/versiones, con evaluación de overhead/cache/coste+retry/esquema/aislamiento/auditoría/latencia/límites. Error/contaminación jamás produce interpretación oficial. Defaults están propuestos, no medidos.

## J. Privacidad y contrato

[DS-F07–09](../research/deepseek-tax-filing-final-delta.md#contrato-privacidad-y-activación) distingue acuerdo específico API y política general. No acredita no-training/ZDR/DPA ejecutado, retención fija ni subprocesadores completos aplicables; política pública refiere China/mejora. §8.1 exige verificar compatibilidad del uso profesional asistido/shadow. PENDING CONTRACTUAL VALIDATION antes de datos reales; no asumir privacidad de API/store=false. Minimización actual intacta; no nombres/CPE/contratos/bancos/credenciales por conveniencia de cache.

## K. Activación pendiente

Sin nuevo bloqueador de diseño demostrado ni cambio de proveedor: D01/B16 más C01/C10/C11/C13 pertinentes retienen producción por contrato/datos, evaluación CasPro, política de gasto, identidad, seguridad/aislamiento y evidencia operativa aún no obtenidas. Umbrales de utilidad se fijan antes del ensayo; cien casos + veinte adversariales es plan inicial, no garantía estadística. Ejecución requiere además misión/WO/fase autorizadas.

## L. Neutralidad confirmada en diseño

AIService → ProviderAdapter → DeepSeekProviderAdapter; esquemas/cuentas/autoridad pertenecen a CasPro. Accounting no importa SDK/types del proveedor. Cambio futuro evaluado de adapter/config no reescribe dominio. Reglas/templates/manual funcionan con IA apagada; Tax mirror es determinístico y no depende de shadow.

## M. Arquitectura Tax Filing Mirror

[Contrato nuevo](../specs/flows/external-tax-filing-mirror.md) extiende Workspace/PreparedPackage/TX5 y M09 X05/X06/X08. Tax posee filing/mapping/comparación/revisión; Treasury dinero y Documents artefactos. No nueva autoridad de Case Flow, módulo Accountant, ShadowTax ni ejecución SUNAT.

## N. Universo SUNAT investigado

[TF-F01–12](../research/deepseek-tax-filing-final-delta.md#sunat-universo-acotado-canales-y-revisión-de-formatos): DF621/PDT histórico-contingente; DF617 desde mayo2026 y cambio ND julio; PLAME Web/PDT0601; DF626/633/697; SIRE separado; FV710/3500/3800 condicionados; boleta1662 y tributo1041 distintos. Catálogo acotado, no censo exhaustivo ni activación TILMUX. Fuentes actuales/fechas/versiones/desconocidos y límite de lectura gob.pe constan en investigación.

## O. Definiciones y versiones

TaxFormDefinitionRevision conserva número textual/familia/canal/variante/layout y vigencia de período/presentación, campos tipados/precisión/semántica/condiciones/fuentes/redondeo y parser/mapping. SupportProfileRevision distingue metadata/evidencia/extracción/conciliación/preparación/export por cobertura; ninguna capacidad ejecutable validada en esta misión. No tax DSL ni layout último aplicado retroactivamente.

## P. Revisión de filing externo

ExternalTaxFilingRevision immutable conserva entidad/obligaciones/períodos/tipo/secuencia/fechas/referencia/casillas/constancia/actores si conocidos y linaje. FilingCaptureRevision corrige extracción/transcripción sin inventar otra presentación. Presentación, verificación de evidencia y eficacia legal separados; dos archivos con identidad incompatible van a conflicto, no overwrite.

## Q. Inventario histórico

Registrar evidencia suministrada autorizadamente, identificar sistema/versión con fuente oficial, validar entidad/aplicabilidad, importar y conciliar solo cobertura soportada. Ausentes siguen UNKNOWN. No acceso a SOL ni archivos privados solicitado/ejecutado; presentador externo desconocido no se inventa a partir del importador.

## R. Casillas y mapping

TaxFieldMappingRevision tipada N:M, funciones/agregaciones/eligibilidad/FX/redondeo y fuentes, aprobación Tax, inputs/contribuciones por componente/versión. Comparación guarda PreparedPackage, filing/captura, definición/mapping, valores brutos/normalizados y delta CasPro−presentado. Metadata externa sin concepto interno conserva NOT_COMPARABLE; cobertura incompleta no es igualdad.

## S. Preparado, presentado y pagado

Son tres dimensiones de verdad, con evidencia/eficacia/reconciliación adicionales. Pago no demuestra filing correcto ni filing demuestra pago. Settlement conserva principal/intereses/multas, parciales y N:M permitido, saldo y conservación de aplicaciones. Compensación/crédito requiere hecho legal Tax; nunca caja ficticia Treasury ni ajuste de valor presentado para cuadrar.

## T. Estados de conciliación

Compatibilidad/cobertura primero; comparación exacta o diferencia; revisión y atribución después. Materialidad no borra delta; redondeo exige regla oficial versionada y preserva valores brutos. RECONCILED requiere alcance completo/revisión justificada y no significa pagado ni firmeza legal. Dashboard mensual muestra cada dimensión, faltantes y denominadores; ejemplo sintético en contrato.

## U. Atribución profesional

TaxDifferenceReview conserva hipótesis/elegibilidad/fuentes/criterio/revisor/decisión/resolución. Diferencia numérica solo alerta; CASPRO_ERROR_CONFIRMED o EXTERNAL_FILING_ERROR_CONFIRMED necesitan conclusión competente. Exclusión correcta de documento no elegible puede justificar diferencia. Juicio pendiente permanece unresolved, sin culpa por aritmética ni autoridad de LLM.

## V. Linaje y rectificación

Original → sustitución/rectificación → siguiente corrección mantiene cada evento/captura/constancia y comparación histórica. Tipo/procedimiento se toma de familia/norma aplicable. Última presentada difiere de jurídicamente eficaz por obligación/tributo; Art88.2 no es temporizador automático de firmeza. Recomendación interna → ejecución profesional afuera → registro real → nueva comparación, sin reescribir original.

## W. Paquete para revisión

TaxDifferenceReviewPackage congelado incluye período/formulario/versiones, fuentes/contribuciones/casillas/deltas, faltantes/regla/mapping, evidencia autorizada y revisión/acción recomendada. Incluye pendientes y diferencias fiscalmente relevantes pequeñas. Export autorizado para profesional, sin envío automático ni «orden SUNAT» ni privacidad heredada de ver resumen.

## X. Backfill

FILING_HISTORY_ONLY se admite sin PreparedPackage previo. RETROSPECTIVE_CASPRO_RECONSTRUCTION es paquete creado ahora con asOf/período histórico, fuentes/reglas/faltantes; no preparación contemporánea fabricada. Incompleto no acredita error ni altera cierre Accounting. Nuevas fuentes generan nuevas revisiones.

## Y. Importación

VALIDATE→PREVIEW→CONFIRM con hash/parser/schema/locale/revisión/permiso y errores visibles por campo. Prioridad estructurado oficial; PDF extraído requiere revisión con ubicación/confianza; archivo del contador y transcripción manual retienen fuente/actor. OCR no acredita presentado. Dedupe compuesto e import atómico por filing; cambio tras preview exige repetir.

## Z. Case Flow y preview

Proyección de período/paquete si existe/filing/pago/revisión/rectificatoria real/nueva conciliación. Sin nodos ficticios, segunda máquina de estados ni efectos desde arista. Permisos Tax y Documents se evalúan por separado para detalle/preview/download; grafo no hereda autoridad sobre artefacto.

## AA. Impacto en permisos

Sin nuevos IDs/roles: tax.prepare/review/reconcile/correct/export/profile.approve y TX5 tax.external.record/X05 tax.record_filing conservan rutas, scopes y responsabilidades. Revisión verifica afirmación concreta con competencia/SoD existente, no título ni admin. Treasury dinero y Documents acceso permanecen separados. Matriz de roles no necesita modificación.

## AB. Auditoría

Actor/entidad/período/formulario/versiones/fuente/artefacto, paquete nullable razonado, filing/captura/mapping, valores/delta, razón/revisión/resolución/rectificación/eficacia y timestamp por acción. Locks/revisiones esperadas/idempotencia CM0 protegen publicación; job no mantiene transacción mientras parsea/compara/espera. Evidencia/coste append-only con retención gobernada.

## AC. Explicación IA fiscal

LATER: TAX_DIFFERENCE_EXPLANATION, OFF/budget0, distinto de ACCOUNTING_CLASSIFICATION; AIService neutral con proveedor inicial seleccionado, allowlist/template/retención/evaluación propios. Sugiere hipótesis/registros/faltantes sobre comparación determinística; no corrige, acusa, determina obligación legal, presenta ni paga. No endpoint general de consulta fiscal empresarial.

## AD. Aplicabilidad TILMUX

EntityFilingProfile + TaxObligationRevision por hechos/régimen/actividad/cohorte/período y fuente oficial. RER declarado como perfil inicial de investigación no acredita activación real C08; no asumir RMT/General, agente, PLAME ni anual para todos. Política/config reales permanecen pendientes bajo gates existentes, sin preguntas inmediatas.

## AE. Formularios no conocidos

Evidencia por identificar → cotejo oficial → definición/canal/versión → perfil/obligación → captura → cobertura de reconciliación. Familia válida desconocida no se pierde; conocida con solo metadata no se presenta como calculador. Nuevo parser/mapping tipado futuro según semántica, sin rediseñar core ni lenguaje universal de impuestos.

## AF. Casos adversariales

Resultado **PASS documental** significa que el contrato contiene respuesta explícita al contraejemplo; no se ejecutó ningún caso runtime ni revisión independiente. Referencias AI: [identidad/política](../architecture/ai-assistance.md#presupuesto-y-programación-del-proveedor-inicial), [coste](../architecture/ai-assistance.md#límites-reservas-y-observabilidad), [cola/cache](../architecture/ai-assistance.md#clases-de-programación-y-cache), [privacidad/calidad](../architecture/ai-assistance.md#datos-evaluación-y-activación). Referencias Tax: [captura](../specs/flows/external-tax-filing-mirror.md#inventario-captura-y-revisión-externa), [comparación](../specs/flows/external-tax-filing-mirror.md#mapping-comparación-y-revisión), [linaje](../specs/flows/external-tax-filing-mirror.md#linaje-eficacia-y-retrospectiva), [settlement](../specs/flows/external-tax-filing-mirror.md#liquidación-y-dinero), [permisos](../specs/flows/external-tax-filing-mirror.md#permisos-auditoría-y-publicación).

| Caso | Contraejemplo | Respuesta del contrato / resultado estático |
|---|---|---|
| F01 | Alias cambia modelo | Identidad/evaluación se invalida, historial exacto conserva versión conocida o limitada; PASS |
| F02 | Precio cambia a mitad de mes | PricingRevision nueva, dispatch revalida, consumos anteriores conservados; PASS |
| F03 | Ventana off-peak cambia | Revisión de horario/precio y nueva planificación, sin alterar contexto histórico; PASS |
| F04 | Conversión de zona errónea | UTC/fecha/tzdb autoritativos, no hora Lima memorizada; ejemplos de día anterior; PASS |
| F05 | Inicia barato y termina peak | Regla de billing no comprobada; reserva peak, reconcilia costo observado; PASS |
| F06 | Dos jobs agotan último saldo | Reserva atómica multi-cuota; segundo retiene si saldo insuficiente; PASS |
| F07 | Timeout posiblemente facturado | Estado unknown/reserva mantenida; no liberación ni retry automático gratuito; PASS |
| F08 | Retry duplica coste | AttemptId y reserva propios, máximo3, factura incluye ambos si cobrados; PASS |
| F09 | Cache no obtiene hit | Estimación miss, usage real separa hit/miss; no exposición descubierta por descuento; PASS |
| F10 | JSON vacío | Sin sugerencia ejecutable, rechazo/fallback y coste registrado; PASS |
| F11 | JSON válido con cuenta inválida | Validador rechaza AppliedAccountId fuera del conjunto, no DRAFT aceptable; PASS |
| F12 | Modelo no disponible | Circuito/degradación, manual/reglas siguen; no proveedor alternativo no autorizado; PASS |
| F13 | Rate limit | Backoff acotado/Retry-After, presupuesto por intento, no concurrencia2500 local; PASS |
| F14 | Presupuesto agotado | PAUSED_BUDGET/circuito, continuidad ERP; no seguir cola opcional en silencio; PASS |
| F15 | Interactivo en peak | Ejecuta si presupuesto/mandato permiten, sin espera nocturna por centavos; PASS |
| F16 | Shadow llega antes de ventana barata | Cola elastic limitada, manifest/corte y pendiente visibles; oficial sigue; PASS |
| F17 | Deadline antes del off-peak | Peak autorizado/cap o escalación; obligación oficial no depende de inferencia; PASS |
| F18 | Cambian términos de privacidad | Revalidación contractual, pausa datos afectados; no elección de proveedor reabierta por popularidad; PASS |
| F19 | Modelo cambia después de evaluación | Evaluación previa no habilita versión nueva; preservar output antiguo y revalidar; PASS |
| F20 | Regresión de calidad Flash | Corpus/seguimiento y umbral previo, pausa/fallback; confianza no autoridad; PASS |
| F21 | Un hecho malformado en lote | Requests unitarios iniciales aíslan; microbatch futuro valida cada ítem y rechaza donde no aislable; PASS |
| F22 | Contaminación entre casos | No mezcla inicial; IDs/scope/contenido validado, rechazo del lote si integridad incierta; PASS |
| F23 | Cache aumenta datos sensibles | Allowlist manda; no ampliar candidatos/expediente por hit; PASS |
| F24 | Accounting sin IA | Templates/reglas/manual/A03 continúan por contrato vigente; PASS |
| F25 | Todas las casillas coinciden | EXACT_MATCH con identidad/compatibilidad/cobertura completas; no infiere pagado; PASS |
| F26 | Una casilla difiere | Delta por campo/contribución y REVIEW_REQUIRED, no culpa; PASS |
| F27 | Falta documento interno | INCOMPLETE/SOURCE_MISSING, no llenar desde filing ni error externo; PASS |
| F28 | Omisión externa elegible | Profesional verifica elegibilidad/fuentes antes de error confirmado y recomendación; PASS |
| F29 | Exclusión externa correcta | ELIGIBILITY_DIFFERENCE_JUSTIFIED con fuente; CasPro puede requerir corrección; PASS |
| F30 | Mapping de versión errónea | INPUT_MISMATCH/UNMAPPED y nueva revisión, no comparación verde; PASS |
| F31 | Original luego rectificada | Dos filings ligados/capturas/constancias intactas, comparación nueva; PASS |
| F32 | Dos rectificaciones | Cadena por evento/alcance y revisión de eficacia, no MAX(fecha) como verdad legal; PASS |
| F33 | Filing sin constancia | OBSERVED_UNVERIFIED, evidencia faltante visible sin borrar historia; PASS |
| F34 | Constancia sin campos | Verifica solo presentación acreditada, fieldCoverage INCOMPLETE; PASS |
| F35 | PDF incierto | Página/confianza/sourceKind, revisión/campos UNKNOWN; OCR no autoridad; PASS |
| F36 | Error de digitación | Nueva FilingCaptureRevision/diff/revisor, no rectificatoria SUNAT ficticia; PASS |
| F37 | Pago difiere de declarado | Puente separado con componentes/eficacia/aplicaciones; no editar filing; PASS |
| F38 | Pago parcial | Saldo/aplicación Treasury parcial, presentación intacta; PASS |
| F39 | Interés por demora | Componente con fecha/base/regla/evidencia, no confundir con tributo principal; PASS |
| F40 | Pago cubre varias obligaciones | N:M solo elegible, aplicaciones conservan suma/saldo sin duplicación; PASS |
| F41 | Cálculo CasPro probado incorrecto | CASPRO_ERROR_CONFIRMED y corrección del dueño/nueva preparación; PASS |
| F42 | Filing probado incorrecto | EXTERNAL_FILING_ERROR_CONFIRMED tras revisión; recomendación y ejecución afuera; PASS |
| F43 | Juicio profesional sin acuerdo | PROFESSIONAL_JUDGMENT_UNRESOLVED; no forzar igualdad/resolución; PASS |
| F44 | Mapping no es1:1 | Contribuciones N:M tipadas y lineage de derivados sin doble base; PASS |
| F45 | Layout cambia por período | Definición vigente para período y fecha/canal; nunca última tabla por nombre; PASS |
| F46 | Filing anterior a CasPro | FILING_HISTORY_ONLY sin paquete inexistente; PASS |
| F47 | Reconstrucción histórica incompleta | Retrospectiva etiquetada/asOf/faltantes, comparación INCOMPLETE; PASS |
| F48 | PDT desconocido válido | Conservar evidencia/identidad por resolver y soporte incremental oficial; PASS |
| F49 | Formulario conocido sin mapping | Metadata/evidencia no FULL_FIELD_RECONCILIATION ni calculador; PASS |
| F50 | Declarado con paquete incompleto | Dimensiones independientes, no forzar PREPARED por filing; PASS |
| F51 | Accounting cerrado y corrección fiscal tardía | Tax conserva nueva revisión, no edita GL/cierre; corrección Accounting por dueño si procede; PASS |
| F52 | Rectificación intenta overwrite | Original/capturas/constancias append-only, nueva relación y comparación; PASS |
| F53 | Resumen permitido, PDF restringido | Tax view no concede Documents preview/download; proyección redactada; PASS |
| F54 | Evidencia de otra entidad | Rechazo/cuarentena antes de vincular, sin disclosure ajeno; PASS |
| F55 | Filing duplicado importado | Identidad compuesta + idempotencia/unicidad; referencia existente, no deuda nueva; PASS |
| F56 | Constancia importada dos veces | Hash/identidad/entidad y referencias sin nuevo pago; conflicto si contenido difiere; PASS |
| F57 | Regla oficial de redondeo difiere | Mapping aprobado conserva bruto/normalizado/regla, no epsilon universal; PASS |
| F58 | Diferencia pequeña contable relevante fiscal | Delta intacto y revisión tributaria, materialidad separada; PASS |
| F59 | Filing dice pagado sin Treasury | PAYMENT_EVIDENCE_UNRECONCILED, no caja inventada; PASS |
| F60 | Treasury pago sin filing | FILING_EVIDENCE_MISSING, no declarado inferido; PASS |
| F61 | Rectificatoria menor con eficacia pendiente | LegalEffectReview por obligación, no firmeza automática por plazo/acuse; PASS |
| F62 | Costo incierto cruza cambio de mes | Mantiene exposición vigente, atribución original y conciliación; no reset que libere saldo; PASS |
| F63 | Otra aplicación usa cuenta DeepSeek | Cobertura parcial declarada, reconciliación de factura, key no aislamiento total; PASS |
| F64 | Anuncio Pro contradice pricing/changelog | Discrepancia fechada, no selección Pro ni disponibilidad futura inventada; PASS |
| F65 | Modelo no expone versión inmutable | UNKNOWN/REPRODUCIBILITY_LIMITED; no hash ficticio ni promesa de rerun exacto; PASS |
| F66 | Misma constancia corresponde a varios tributos | Identidad/alcance compuesto y relaciones legítimas sin duplicar dinero ni eficacia global asumida; PASS |
| F67 | Dos rectificaciones concurrentes del mismo padre | Locks/revisiones y conflicto de linaje/eficacia, no dos vigentes por carrera; PASS |
| F68 | Permiso o parser cambia tras preview | Revalidar confirmación, STALE/repetir preview, no aprobación obsoleta; PASS |

## AG. Archivos del delta y validación

Nuevos: [research](../research/deepseek-tax-filing-final-delta.md), [contrato mirror](../specs/flows/external-tax-filing-mirror.md) y este informe. Ajustados: [AI](../architecture/ai-assistance.md), [Accounting](../accounting/templates-automation-shadow.md), [POL](../product/company-policy-register.md), [workspace Tax](../specs/flows/tax-workspace-books.md), [M09](../specs/milestones/tax-deep.md), [capabilities](../roadmap/capabilities.md), [program](../roadmap/program.md), [gaps](../roadmap/decisions-gaps.md), [spec index](../specs/index.md), [review](../review.md). Trece archivos documentales; paquetes históricos y roles/configuración/Case Flow/taxonomía sin edición.

Validación estática completada:13 Markdown,295 referencias locales y67 anchors verificados,52 tablas consistentes,39 secciones A–AM y68 casos ordenados. POL-01–26 sin nuevos IDs; capacidades Tax referenciadas presentes en matriz de roles, sin modificarla; registros B16/C13/D6 idénticos al baseline y A0 preservado. Seis contratos/paquetes históricos clave comprobados sin diff. Búsqueda en documentación vigente sin las afirmaciones obsoletas de proveedor no elegido o estado inicial sustituido; antecedentes research/evidence separados. Revisión de autoridad: adapter neutral, precios versionados, continuidad oficial sin IA, tres verdades fiscales, linaje inmutable, diferencia sin culpa automática, sin Tax DSL/ShadowERP/ejecución SUNAT. `git diff --check` limpio; al stage se verifica también el delta completo de archivos nuevos. Casos AF son walkthrough estático del autor. No tests/builds/Docker, llamadas de inferencia ni datos TILMUX.

## AH. Commits

Un commit documental coherente sobre5886 para research, contratos e informe. La identidad exacta del commit de entrega se publica tras crearlo en el cuerpo de PR #7 y en la respuesta final; este archivo forma parte de su tree y no puede contener su propio hash final sin cambiarlo.

## AI. Nuevo HEAD

HEAD de entrega publicado y contrastado con GitHub después del push a la misma rama en PR #7; identificador exacto en cuerpo del PR/respuesta de entrega. No usar5886 como identidad del delta nuevo:5886 es el segundo candidato revisado, preservado como baseline.

## AJ. Nuevo tree

Tree de entrega obtenido de Git para ese HEAD y verificado tras push; identidad exacta junto al HEAD en PR/respuesta. La ausencia de autorreferencia hash en este archivo no sustituye la verificación del candidato externo.

## AK. PR final

Entrega prevista al mismo PR #7, que debe permanecer OPEN/no merged. Conservar baseline y ambos PASS independientes, añadir delta final y candidato exacto; sin PR #8, merge, rebase ni limpieza de rama. Revisión final independiente es siguiente acción, no WOs en esta misión.

## AL. Preguntas al propietario

**0 preguntas inmediatas.** Elección de proveedor/modelo/objetivo/off-peak y necesidad de espejo fiscal están decididas; defaults reversibles y validaciones futuras se resuelven en contratos/gates existentes.

## AM. Veredicto del autor

**PASS — FINAL AI PROVIDER / TAX FILING RECONCILIATION DELTA READY FOR INDEPENDENT FINAL REVIEW.** Cierre estático documentado en AG; no aceptación independiente, aprobación profesional ni producción. Se conservan A0/B16/C13/D6 y todas las aceptaciones históricas; **IMPLEMENTATION: NOT AUTHORIZED.**
