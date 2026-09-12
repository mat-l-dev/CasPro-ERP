# Perú — aplicabilidad de IA por propósito

Corte 2026-09-12; corrección F04. Investigación para IA de CasPro en ejecución, no selección de herramientas de desarrollo. No es dictamen de cumplimiento de TILMUX. DeepSeek API / V4.1-Flash sigue elegido inicialmente; arquitectura neutral y activación separadas.

## Fuentes oficiales y fechas

| Fuente | Comprobación / límite |
|---|---|
| [Ley31814, texto consolidado Congreso](https://leyes.congreso.gob.pe/Documentos/2021_2026/ADLP/Texto_Consolidado/31814-TXM.pdf) | Publicación2023-07-05, objeto y principios de uso responsable; contenido indexado oficial consultado, descarga directa403. Objeto y autoridad art.4 corroborados expresamente en considerandos del DS115; no se declara lectura íntegra de descarga fallida |
| [DS115-2025-PCM, texto oficial](https://busquedas.elperuano.pe/dispositivo/NL/2436426-1) | Publicado2025-09-09; arts.3–4,22–27,28–36 y disposiciones finales leídos. Vigencia general a partir de90 días hábiles siguientes; primera, segunda, cuarta y quinta DCF desde2025-09-10. Plazos graduales específicos abajo; al corte transcurrió vigencia general |
| [RM152-2026-PCM, ENIA2026–2030](https://busquedas.elperuano.pe/dispositivo/NL/2511535-1) | Complemento oficial actual: estrategia y disposiciones organizativas de entidades públicas. No convierte comités/Oficial de IA/plan público en obligación universal privada |
| [DS016-2024-JUS y Ley29733](privacy-current-review.md) | Art.26 del reglamento IA remite a privacidad vigente. DPA, transferencias y datos sensibles requieren evaluación propia |

La ley marco no da autorización para cualquier uso. La entrada general del DS no debe confundirse con vencimiento gradual ni con «IA exenta hasta2029». Antes de activar se fija fecha exacta del supuesto aplicable con calendario legal y norma vigente; no se afirma una fecha diaria de la regla90 días sin verificar calendario. Este límite no impide concluir que está vigente al corte. Consulta actual centrada en normas mencionadas y ENIA; revalidar complementos SGTD y hechos reales en D01/C06 antes de activación.

## Qué exige cada plano

Art.22 distingue uso indebido prohibido, riesgo alto y riesgo aceptable para lo que no encaje en arts.23–24. No se importan categorías UE ni se equipara HIGH de ingeniería con clasificación legal. Art.23 comprende manipulación perjudicial, capacidad letal autónoma civil, vigilancia masiva sin base/proporcionalidad, inferencias sensibles/discriminatorias y determinados usos biométricos/predicción delictiva, con excepciones específicas del propio texto. Revisión humana no vuelve lícito un uso prohibido.

Art.24 evalúa finalidad y consecuencias: activos críticos/servicios esenciales, selección/condiciones laborales, evaluación crediticia de personas (excepto detección de fraude), salud y demás supuestos/derechos. Una propuesta contable no es evaluación crediticia por contener montos; una salida «sugerencia» sí podría encajar si en realidad determina crédito, empleo o salud. Cambiar etiqueta no cambia el uso. El supuesto residual24.1.j exige valorar consecuencias y dificultad de supervisión; no declarar aceptable por defecto sin ese examen.

Arts.25–27: transparencia previa para alto riesgo (finalidad, funciones, decisiones), etiquetado cuando relevante y explicación si hay decisiones que impactan derechos. Excepción25.2 de etiquetado en apoyo administrativo interno sin impacto directo no exonera del resto de ley/privacidad. Privados art.31: políticas/protocolos de seguridad, privacidad, transparencia, explicabilidad y responsabilidad; educación interna; para alto riesgo, registro de funcionamiento/fuentes/lógica/impactos y supervisión capacitada con poder de detener/corregir/invalidar. Un click sin competencia, evidencia o poder efectivo no satisface el control.

Privados art.32: evaluación de impacto de alto riesgo voluntaria según ese artículo; si se hace, documentar hallazgos/medidas y conservar mínimo3 años desde emisión. Riesgos detectados requieren mitigación antes de implementar. Art.33 promueve estándares; no establece certificación ISO universal privada. Arts.28–30 y sexta DCF imponen obligaciones específicas al sector público (incluida evaluación obligatoria de alto riesgo y normas técnicas); no se trasladan automáticamente a TILMUX.

## Plazos de implementación específicos

Primera DCF aplica progresivamente art.25 y capítulo privado del TítuloVI, desde el día siguiente de publicación2025-09-09:

| Supuesto privado | Plazo | Fecha de referencia por aniversario |
|---|---|---|
| Usos en salud, educación, justicia, seguridad, economía y finanzas | 1 año | 2026-09-10 |
| Transporte, comercio y trabajo | 2 años | 2027-09-10 |
| Producción, agricultura, energía y minería | 3 años | 2028-09-10 |
| Otros usos | 4 años | 2029-09-10 |
| MYPE pequeña: ventas anuales >150 y ≤1700UIT | 2 años | 2027-09-10 |
| Microempresa: ventas anuales ≤150UIT y equivalentes normativos | 3 años | 2028-09-10 |

Son plazos de disposiciones enumeradas, no permiso temporal para usos prohibidos. Sector del uso, condición de desarrollador/implementador, ventas y regla MYPE aplicable se documentan por persona jurídica; NPIF, denominación SAC o vender a una mina no prueban ese supuesto. Caso financiero ordinario de1 año ya alcanzó fecha de referencia al corte; no seleccionar automáticamente plazo comercio o micro. C06/D01 exigen resolución competente con hechos reales antes de activar.

## Matriz candidata de los propósitos del alcance

Todas las filas: controles documentados, **ningún control runtime probado**. Actor técnico AIService/proveedor carece de autoridad sobre hechos oficiales; persona jurídica implementadora/responsable y personas naturales afectadas se identifican en la activación. Clasificación siguiente es inferencia condicionada al uso acotado, no dictamen ni configuración activa.

| Propósito / actor humano | Personas/proceso e inputs | Salida, efecto y autoridad / revisión | Clasificación candidata y fundamento | Obligaciones / fecha / evidencia y gate |
|---|---|---|---|---|
| ACCOUNTING_CLASSIFICATION / R-ACCOUNTING autorizado | Propuestas del libro; referencias minimizadas de hechos/categorías/cuentas y eventual dato de contraparte; no expediente personal completo | Candidato cuenta/tratamiento; aceptar a DRAFT. Sin efecto oficial directo; Accounting aprueba/postea con A03, juicio verificable y posibilidad de rechazar | Riesgo aceptable candidato art.22.2 si no encaja23/24, incluido24.1.j. No evalúa personas/crédito/empleo. Dependencia indebida de sugerencia o cambio de uso obliga reevaluar | Arts.26–27/31 generales; art.25/31 alto riesgo si clasificación cambia; plazo según uso/MYPE de tabla, sin asumir. Diseño: permisos, DRAFT, fuentes/redacción/versiones. Falta evidencia B16/B02/B15, contexto/proveedor/transferencia C06/C10/C11/C13/D01 |
| SHADOW_ACCOUNTING / R-ACCOUNTING solicita, R-ACCOUNTING-CONTROL revisa | Cápsula de hechos congelados minimizados; comparación experimental del libro, datos potenciales de contraparte | Interpretaciones/posting/corrección solo experimental; diferencia no manda en contabilidad, crédito ni personas. Humano revisa labels y fuente; nunca copia auto al GL | Riesgo aceptable candidato22.2 por aislamiento y finalidad de evaluación, condicionado23/24. Aislamiento no exime privacidad ni impacto de usos posteriores | Mismas obligaciones/plazo del contexto aplicable; diseño: DB/proceso aislados, caps técnicos, manifest. B02/B13/B15/B16 y C06/C10/C11/C13/D01 prueban aislamiento/contexto; ninguna ejecución probada |
| TAX_DIFFERENCE_EXPLANATION / R-TAX autorizado | Diferencias calculadas, casillas/linaje de preparación/filing/saldos, mínimos fiscales de persona/entidad | Explicación/citas, no cálculo ni presentación/settlement ni juicio fiscal vinculante. Profesional contrasta con fuente; Tax mantiene decisión | Riesgo aceptable candidato22.2 en explicación interna sin decisión sobre personas; reconsiderar24.1.j si se usa para efectos jurídicos en terceros. No «bajo» automático por tener humano | LATER/OFF conforme contrato existente; no nueva construcción obligatoria por esta matriz. Arts.26–27/31 y rama alto riesgo si aplica; plazo del uso/MYPE validado antes de habilitar. Fuentes/linaje diseñados; C08 además de C06/C10/C11/C13/D01 y B14/B16 pendientes |

Los demás pilotos de la tabla histórica de riesgos permanecen posibles, sin promoción a propósitos aprobados. No habilitar IA global por completar una fila. Nueva finalidad, datos, autoridad de salida, proveedor/alias/modelo resuelto, prompt/versión o cambio normativo: nueva revisión de AI-purpose applicability record, ImpactManifest y evaluación; mantener nuevas solicitudes OFF/pendientes hasta resolver. Revocación de finalidad invalida runs/export/cachés pendientes y activa ciclo de privacidad. DeepSeek seleccionado no equivale a contrato/DPA/país/retención aprobados.
