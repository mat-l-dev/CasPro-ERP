# External Tax Filing Mirror y conciliación de declaraciones

Owner: Tax. Extensión de [TaxPeriodWorkspace / PreparedPackage / TX5](tax-workspace-books.md) y [M09 X05/X06/X08](../milestones/tax-deep.md), aceptada documentalmente conforme [review](../../review.md). [Fuentes oficiales al 2026-09-12](../../research/deepseek-tax-filing-final-delta.md#sunat-universo-acotado-canales-y-revisión-de-formatos) distinguen familia, canal, versión y aplicabilidad. Accounting interpreta; Treasury posee dinero; Documents conserva artefactos; Tax determina, captura y concilia. No módulo Accountant, Tax DSL, Shadow Tax ni ejecución SUNAT.

## Tres verdades y soporte por familia

PreparedPackage es la determinación interna congelada; ExternalTaxFilingRevision es evidencia de lo presentado afuera; settlement es lo pagado/aplicado o extinguido con sustento. Ninguna implica las otras. Registrar una declaración histórica no exige que CasPro la hubiera preparado. Propuesta SUNAT/SIRE, archivo exportado para presentar, constancia de recepción y respuesta aceptada/rechazada son evidencias distintas. El comparador SIRE documento a documento permanece separado del comparador de casillas efectivamente declaradas.

TaxFormDefinitionRevision identifica familia/número oficial como texto (con ceros), nombre, autoridad/fuentes/hash/edición, canal/sistema, variante, versión de aplicativo si conocida, layout/parser/mapping revision, vigencia por período y fecha de presentación, tipo de declaración admitido y reglas de compatibilidad; características oficiales de cálculo/visualización y relaciones entre campos cuando acreditadas. UNKNOWN es explícito: número conocido no demuestra versión. Código de tributo es otro campo; 1041 no es formulario, 1662 es boleta de pago. Cada definición lista casilla/campo/clave de fila repetida, nombre oficial, significado/base, tipo (Decimal, importe, tasa, fecha, enum, texto, booleano), moneda/unidad, escala/rango, obligatoriedad condicional tipada, signo, fuente y regla de redondeo si acreditada. Conserva valores brutos, nulos, no aplicable y desconocido; nunca traduce ausencia a cero.

La familia usa adapter/parser/mapping tipados registrados y metadata declarativa limitada a campos/validaciones seguras. Nueva semántica requiere spec y, cuando se autorice implementar, handler y validación de formato/cálculo propios; no expresiones arbitrarias, SQL, lenguaje de impuestos ni motor universal. Cambios oficiales crean revisiones: no remapear el histórico con la última tabla.

EntityFilingProfile referencia TaxObligationRevision por entidad, obligación/tributo, período y hechos vigentes. Distingue REQUIRED, OBSERVED, NOT_APPLICABLE y PENDING_VALIDATION con fundamento/actor/fecha. OBSERVED significa evidencia encontrada, no obligación legal aprobada. Catálogo de familias no activa todas para TILMUX; C08/C09 siguen aplicabilidad profesional y C10 privacidad. No se solicita ahora inventario privado al propietario.

| Familia investigada | Alcance de diseño inicial / límite |
|---|---|
| Declara Fácil621 / PDT621 histórico o contingente | Prioridad de conciliación mensual; casillas soportadas exigen layout/mapping aprobado por revisión. No se afirma calculador de todo621 ni parser implementado |
| Declara Fácil617 / PDT617 histórico; informativa ND y boleta1662 | Inventario/evidencia por concepto y período; mapping incremental. Informativa y pago no se fusionan; tributo1041 separado |
| PLAME Web/PDT0601; DF626/633/697 | Reconocimiento/importación documental si hechos aplicables; cálculo/conciliación por revisión tipada posterior. No nómina nueva ni designación automática como agente |
| FV710; DAOT3500; FV3800 | Catálogo y evidencia condicionados a ejercicio/obligación. No preparación completa ni activación por existencia del número |
| SIRE RVIE/RCE | Mantiene contrato de registros/comparación propio; vínculo a declaración cuando existe, sin convertir aceptación de registros en filing621 |
| Familia desconocida | IMPORT_EVIDENCE con identidad por resolver; sin extracción confiable ni reconciliación final hasta soporte validado |

SupportProfileRevision es un vector por familia/versión: KNOWN_METADATA_ONLY, IMPORT_EVIDENCE, FIELD_EXTRACTION, FULL_FIELD_RECONCILIATION, PREPARATION_SUPPORTED, EXPORT_SUPPORTED, cada capacidad NOT_SUPPORTED / SPECIFIED / VALIDATED con cobertura de campos, límites y evidencia. No una escalera que habilite cálculo por importar PDF. FULL requiere todos los campos relevantes declarados en alcance y cobertura explícita de los excluidos; una cobertura parcial nunca lleva ese badge. En esta misión solo hay diseño/research: ninguna capacidad está validada como software ni activada con datos reales.

## Inventario, captura y revisión externa

Inventario histórico autorizado: período/entidad declarados, artefacto/hash, familia/canal candidatos, referencia oficial, tipo de declaración, fecha, importador, fuente y estado de identificación. Primero conservar lo suministrado; luego identificar definición oficial, validar pertenencia/aplicabilidad, importar revisión, y conciliar solo lo soportado. No inspección automática de cuentas SOL ni búsqueda de datos privados.

ExternalTaxFilingRevision es append-only: ID estable de filing/linaje; entidad, identidad fiscal privada, obligación(es)/tributos/período(s); familia/definición/layout/canal; tipo ORIGINAL / SUSTITUTORIA / RECTIFICATORIA u otro autorizado por la familia; secuencia/versión externa si consta, UNKNOWN si no, aparte del orden local de captura; fecha real de presentación con zona, referencia/número de orden/acuse, presentador externo si consta, importador CasPro, fuente/artefactos, campos brutos y normalizados, respuesta externa y evidencia, relación replaces/corrects y razón, revisiones previas, capturedAt. Actor desconocido permanece desconocido: importar no demuestra quién presentó.

FilingCaptureRevision conserva extracción/transcripción y correcciones de captura del mismo evento externo. Corregir un dígito mal transcrito crea nueva captura con diff/razón/revisor, **no nueva rectificatoria SUNAT**. Se preservan capturas anteriores y conciliaciones que las usaron. Nueva presentación externa crea ExternalTaxFilingRevision nueva, aun si los valores son iguales. Si una referencia externa aparenta otro contenido, retener conflicto de identidad para revisión; no overwrite ni dedupe ciego.

Filtrado de entidad antes de relacionar evidencia: entidad equivocada se rechaza/cuarentena bajo Documents, sin arista a expediente ajeno. Dedupe por entidad + identidad oficial compuesta (familia/obligación/período/referencia), más hashes y tipo de artefacto; hash o número de constancia aislados no prueban duplicidad. Mismo recibo puede vincular varias obligaciones legítimas sin duplicar hecho/pago; reimport idéntico devuelve referencia existente. Dos imports concurrentes usan unicidad/idempotencia del mismo evento, no dos deudas.

Importar usa VALIDATE → PREVIEW → CONFIRM de TX: esquema/parser/locale/definición/artefacto exactos, filas/errores, vista antes/después, digest/manifest, revisión esperada y unidad atómica por filing con sus campos. Cada campo conserva sourceKind STRUCTURED_OFFICIAL / OFFICIAL_PDF_EXTRACTED / ACCOUNTANT_FILE / MANUAL_TRANSCRIPTION / OTHER_VERIFIED_SOURCE, sin que el nombre del origen le conceda verificación. Prioridad a archivo estructurado oficial disponible; parser limitado/sandbox, límites de tamaño/filas y sin contenido ejecutable. PDF/texto extraído es propuesta con página/ubicación/confianza por campo y faltantes; OCR no acredita autoridad. Transcripción manual conserva valor original, operador y referencia exacta, revisión contra evidencia y corrección trazada. Sin valor legible conserva UNKNOWN; no autocompleta desde CasPro lo que supuestamente declaró el contador. Export humano neutraliza fórmulas sin modificar valor fuente; export técnico exige schema propio.

Extractar/parsear ocurre fuera de transacción. Confirmar revalida permisos, entidad, hash, versión/parser/perfil y digest de preview; cambios exigen nuevo preview. Evidencia no verificada puede guardarse como OBSERVED_UNVERIFIED; no se rechaza historia por faltar constancia ni se marca DECLARED_VERIFIED por adjuntar cualquier archivo. Constancia sin casillas permite verificar recepción/presentación según su contenido, dejando fieldCoverage INCOMPLETE y comparación pendiente. Revisor verifica afirmaciones concretas, no certifica todo el expediente con un solo checkbox.

## Mapping, comparación y revisión

TaxFieldMappingRevision pertenece a Tax: familia/versión/alcance/vigencias, preparador/aprobador competente, norma/fuente, función tipada, inputs/campos, agregaciones/desagregaciones N:M, filtros de elegibilidad, signos, unidades, FX y redondeo, exclusiones y ejemplos de referencia. No cuenta GL = casilla por nombre. Cada contribución identifica registro/componente/versión/importe/casilla/clave de fila y regla; guardas evitan consumir dos veces una base en la misma agregación. Campos derivados preservan linaje sin sumarse otra vez a base. Un campo solo externo puede ser NOT_COMPARABLE y uno sin mapping UNMAPPED; jamás igualdad presumida.

TaxFilingReconciliationRevision fija manifest/corte: entidad/obligaciones/período, PreparedPackage exacto (o reconstrucción etiquetada), ExternalTaxFilingRevision + FilingCaptureRevision, definición/mapping/políticas/fuentes, cobertura y snapshot de settlement/evidencia/eficacia legal. No elige automáticamente MAX(fecha) de cada lado. Comprueba identidad, compatibilidad y completitud **antes** de comparar; fuentes tardías generan nueva revisión, no alteración de resultados sellados.

Cada FieldComparison conserva valor interno y externo bruto/normalizado, tipo/escala/unidad, fórmula/contribuciones, regla aplicada, diferencia Decimal **CasPro menos presentado**, motivo/faltantes/evidencia y revisión. Comparación exacta es default. Redondeo oficial solo con regla/versiones/scope acreditados: mostrar valores antes/después y diferencia bruta aunque normalizados coincidan. Materialidad profesional es otra dimensión de priorización, no epsilon ni ocultación de diferencia tributaria. La materialidad contable nunca elimina una unidad fiscal relevante.

| Dimensión | Estados / interpretación |
|---|---|
| Compatibilidad/cobertura | COMPATIBLE, INPUT_MISMATCH, INCOMPLETE, UNMAPPED, UNSUPPORTED; faltante no es match |
| Comparación numérica | NOT_COMPARED, EXACT_MATCH, DIFFERENCE_DETECTED, MATCH_AFTER_DOCUMENTED_ROUNDING; alcance/denominador visibles |
| Revisión | NOT_REQUIRED con fundamento, REVIEW_REQUIRED, IN_REVIEW, RESOLVED; resolución no fuerza igualdad numérica |
| Atribución revisada | UNDETERMINED, CASPRO_ERROR_CONFIRMED, EXTERNAL_FILING_ERROR_CONFIRMED, SOURCE_MISSING, ELIGIBILITY_DIFFERENCE_JUSTIFIED, TIMING_OR_MAPPING_DIFFERENCE, PROFESSIONAL_JUDGMENT_UNRESOLVED; puede haber causas por campo diferentes |
| Resultado del expediente | RECONCILED solo con cobertura exigida, diferencias explicadas/resueltas y aprobación explícita; no significa PAID ni obligación extinguida |

TaxDifferenceReview vincula discrepancias/campos y versión de comparación, hipótesis, documentos/cálculos, elegibilidad/oportunidad, norma, responsable/revisor competente, acción propuesta, materialidad/urgencia separadas, comentarios, decisión/razón/fecha y resolución. Un total distinto solo dice DIFFERENCE_DETECTED / REVIEW_REQUIRED, nunca «error del contador». Omisión externa es error confirmado solo tras validar elegibilidad; excluir documento no elegible puede ser correcto. Error interno exige corregir fuentes/mapping/determinación con dueño, nueva preparación y comparación. Error externo confirmado permite recomendar rectificación externa y registrar evidencia cuando realmente ocurra. Opinión pendiente queda abierta; IA, operador técnico o coincidencia de cifras no acreditan conclusión profesional.

## Linaje, eficacia y retrospectiva

Original → sustitución/rectificación → segunda rectificación son eventos distintos con constancias/campos/fechas intactos. Relaciones tipadas admitidas por familia y norma del caso; no toda informativa/PLAME/ND sigue idéntico procedimiento. Registrar motivo, alcance por obligación/tributo y quién constató el efecto. La captura de «última presentada» se muestra aparte de «versión jurídicamente eficaz para esta obligación»; recepción, aceptación técnica y eficacia legal son dimensiones independientes.

LegalEffectReviewRevision conserva regla/fuente, estado UNKNOWN/PENDING/VERIFIED_EFFECTIVE/NOT_EFFECTIVE/DISPUTED, alcance, evidencia/acto/plazo y validación competente. Art88.2 investigado distingue sustitución o rectificación y efectos según obligación determinada/condiciones. No declarar eficacia firme solo porque transcurrió un temporizador, se recibió un PDF o la versión es más nueva; una familia con varios tributos puede necesitar conclusión diferenciada. Reducción presentada no crea automáticamente crédito/reembolso ni cambia aplicaciones Treasury. Una nueva comparación puede referirse a la última presentada mientras la conciliación del saldo exigible conserva la eficacia pendiente visible.

Backfill separa FILING_HISTORY_ONLY de RETROSPECTIVE_CASPRO_RECONSTRUCTION. Primero inventario de declaraciones y constancias verificables, aunque no haya hechos internos del período. Reconstrucción es paquete nuevo con fecha real de creación, período económico histórico, corte/asOf, datos disponibles/faltantes, reglas históricas y fuentes/profesional; jamás se etiqueta paquete preparado contemporáneamente ni se fuerza dato inexistente. Comparaciones retrospectivas son explícitas, INCOMPLETE si faltan hechos; no afectan posting/cierre contable ni fabrican asientos. Tax tardío puede originar revisión/corrección legítima posterior del dueño sin reabrir silenciosamente Accounting cerrado.

## Liquidación y dinero

La comparación de casillas y la conciliación de settlement tienen resultados separados. Mostrar declarado por tributo/componente, importe exigible según regla/eficacia, pago externo alegado, dinero verificado Treasury, aplicaciones fiscales y saldo conocido/pendiente. Pago parcial, varios pagos a una obligación y aplicación N:M solo cuando norma/medio lo permiten, conservando importe disponible y distribución aprobada sin consumo duplicado. Principal tributario, interés moratorio, multa y otros conceptos no se compensan por total: fecha/base/regla/fuente propias, cálculo revisado y referencias.

Treasury registra movimiento real y aplicaciones monetarias según su contrato; una constancia que dice pagado sin movimiento conciliado produce PAYMENT_EVIDENCE_UNRECONCILED, no caja ficticia. Movimiento Treasury sin filing produce FILING_EVIDENCE_MISSING, no declaración inferida. Créditos/compensaciones/otras extinciones no monetarias requieren hecho y fundamento fiscal de aplicación aprobados por Tax, no movimiento bancario inventado. La liquidación puede cambiar con nueva evidencia/rectificación eficaz conservando revisiones previas; nunca actualizar el monto presentado histórico para que coincida con pago.

## Permisos, auditoría y publicación

Se reutilizan [roles/capacidades](../../architecture/roles-delegation.md), sin IDs nuevos. TX5 conserva tax.external.record para registro externo; M09 X05 conserva tax.record_filing en su ruta existente, sin alias que permita bypass entre comandos. tax.review verifica captura/evidencia y revisa discrepancia bajo ámbito/competencia; tax.reconcile produce/revisa el puente por X08; tax.correct por X06 registra corrección de captura o vínculo de nueva presentación y su causa, sin enviar nada a SUNAT. tax.prepare produce paquete; tax.export prepara export autorizado; tax.profile.approve gobierna aplicabilidad. Configurar layout requiere gobierno de configuración y aprobación Tax existentes, no aprobación profesional por rol admin.

Lectura tax.view es por entidad/expediente; Documents view/preview/download se verifica separadamente por artefacto y acción, sin permiso implícito por ver resumen. Revisión/aprobación aplica SoD/excepción de arranque ya definida con declaración explícita, nunca título «contador» como permiso. Treasury requiere sus capacidades para registrar/aplicar dinero; Tax solo vincula referencias autorizadas. Ingestión no verifica el filing; permiso de envío no nace de exportarlo.

CM0 se conserva: idempotencia I, autoridad A5 cuando corresponda, política/perfil M, expediente/linaje O y período Q, documentos D en orden global; confirmación usa locks del dueño, revisiones esperadas y unicidad de identidad/parent. Dos rectificaciones concurrentes del mismo parent no crean ambas «vigente»: conservar evidencia y conflicto pendiente de orden/eficacia. Coordinación Treasury respeta su orden T/F/R antes de C/D y comandos propios; no escritura cruzada. Job de comparación lee snapshots fuera de locks prolongados y publica revisión sellada solo tras revalidar manifest/epoch/permisos; cambios generan STALE y nueva comparación. Ni red SUNAT, OCR ni IA dentro de transacción oficial.

Auditoría append-only por acción: actor/entidad/período, identidad y versión de formulario, fuente/artefacto/hash/parser, PreparedPackage nullable justificado, filing/captura/mapping/comparación, valores/diferencias, motivo, revisión/resolución, rectificación/eficacia, timestamp e idempotency/intent. Cambio de permisos invalida accesos/proyecciones conforme contrato existente; logs minimizados y retención gobernada, sin copiar PDF privado a bitácora pública.

## Revisión profesional y experiencia

TaxDifferenceReviewPackage congelado para revisión interna o export autorizado: entidad/período, formulario/versión, comparación exacta/cobertura, casillas y contribuciones, originales/constancias por referencia, reglas/mapping, motivos/hipótesis, faltantes, revisión/decisiones y recomendación de acción. Incluye diferencias pequeñas fiscalmente relevantes y pendientes, no solo materiales. Identifica destinatario/propósito/alcance cuando se exporta; archivos sensibles requieren permisos separados. No se envía automáticamente al contador ni indica que CasPro ya rectificó.

Ejemplo **sintético, no TILMUX ni casillas legales reales**, período YYYY-MM, FORM X:

| Campo | CasPro | Presentado | Diferencia |
|---|---|---|---|
| A | 100.00 | 100.00 | 0.00 |
| B | 200.00 | 180.00 | 20.00 |
| C | 36.00 | 32.40 | 3.60 |

Vista mensual por obligación/familia muestra aplicabilidad y las columnas preparación, filing, evidencia, comparación, revisión, eficacia y settlement independientemente; diferencias totales, materialidad revisada/pendiente, faltantes y rectificación recomendada con denominador/corte. Por ejemplo, filing verificado + preparación incompleta + pago parcial sigue mostrando las tres condiciones; no badge verde único de período.

Estado REVIEW_REQUIRED. Abrir B/C muestra registros contribuyentes autorizados, evidencia externa, fuente/regla, mapping revision, explicación y resultado de revisión. No calcula culpabilidad ni atribuye fórmula tributaria a estos números de ejemplo.

[Case Flow y preview](../cross-cutting/case-flow-preview.md) siguen proyección de objetos existentes: período → paquete si existe → filing original; filing enlaza pago/aplicación real y DifferenceReview; revisión puede mostrar recomendación → filing rectificatorio **solo al registrarse** → nueva conciliación. No nodos ficticios para completar diagrama, aristas que paguen/presenten ni grafo como autoridad. Resumen puede mostrar diferencia sin habilitar PDF; enlaces/preview aplican disclosure/redacción y permisos del contrato ya definido.

LATER: propósito separado TAX_DIFFERENCE_EXPLANATION, inicialmente OFF y asignación presupuestaria0. Tax proporcionaría únicamente comparación revisable/valores mínimos/refs tokenizadas y reglas autorizadas a AIService; schema de explicación/abstención/citas, evaluación y privacidad propias. No reutiliza permiso/prompt de clasificación Accounting, no cambia mapping, declara error, da aprobación legal, envía ni paga. El control de las tres verdades funciona íntegramente sin IA. REQUIRED_NOW: contratos/versiones/evidencia/conciliación anteriores. REJECT: credenciales SOL, presentación/rectificación/pago automáticos y ShadowERP.

## Evidencia y gates

Casos estáticos en [informe final AF](../../evidence/final-ai-tax-filing-delta.md#af-casos-adversariales). C08/C09 perfil/criterio, C01 interpretación, C05 dinero y C10/C11/C13 datos/roles según operación; B02/B03 permisos/concurrencia, B04 precisión, B07/B08 cálculo/cortes, B10 parsing, B12 efectos y B13 recuperación se validarán antes de aceptación ejecutable/activación pertinente. Se conserva A0/B16/C13/D6. Diseño documental no demuestra parser, presentación, aislamiento ni prueba con datos reales.
