# Información financiera inicial bajo NPIF

Propietario: Accounting. Alcance: arquitectura del paquete formal inicial, no política aprobada para una operación real ni software construido. Corte de investigación: 2026-09-10; períodos objetivo: 2027. La [arquitectura contable](architecture.md) gobierna registro y cierre; el [registro normativo](../research/normative-register.md) gobierna fuentes, vigencias e incertidumbres.

## Marco y aplicabilidad

NPIF es el marco inicial elegido por el propietario, condicionado a comprobar la elegibilidad de TILMUX. RER es un perfil tributario independiente. No inferir ninguno del otro. La RCNC 003-2022-EF/30, arts. 1–4, reemplazó los umbrales de la RCNC 002-2021-EF/30: contempla hasta 150 UIT, más de 150 hasta 2.300 UIT, condiciones de permanencia y dos ejercicios para determinados cambios; al iniciar actividades utiliza ingresos estimados. La prueba de elegibilidad debe conservar ejercicio, UIT de referencia, estimación/ingresos y condición de supervisión, sin inventar hechos. [Resolución oficial](https://busquedas.elperuano.pe/dispositivo/NL/2127835-1).

Se leyeron las 31 páginas de la NPIF y las 40 de su guía oficial. NPIF rige desde el ejercicio 2025; la guía orienta su aplicación y declara que no sustituye a la norma. Fuentes: [NPIF oficial](https://cdn.www.gob.pe/uploads/document/file/5775793/5126738-norma_peruana_para_microempresas.pdf?v=1706559712), [guía CNC](https://cdn.www.gob.pe/uploads/document/file/8541823/7076966-guia_-practica_npif.pdf?v=1756135043), [resolución de aprobación de NPIF](https://www.gob.pe/institucion/mef/normas-legales/5126738-001-2024-ef-30), [resolución de la guía](https://www.gob.pe/institucion/mef/normas-legales/7076966-003-2025-ef-30).

**Distinción normativa que no debe desaparecer:** NPIF 2.2/3.8 enumera cuatro estados y notas; 3.9 permite que cambios en el patrimonio y flujos de efectivo sean opcionales según la necesidad. La guía §3 confirma esa opción. En CasPro ambos son **obligatorios por requisito del propietario**, junto con situación financiera, resultados y notas. No atribuir esa ampliación de producto a una obligación legal universal.

## Contrato del paquete contable V1

Una versión contable solo es usable cuando produce el conjunto completo siguiente para las operaciones dentro de su alcance. Un mayor o dos reportes sueltos no satisfacen este gate.

| Pieza | Insumos y control propios de CasPro | Trazabilidad y aceptación futura |
|---|---|---|
| Situación financiera | Apertura y saldos por rubro; clasificación corriente/no corriente y cuentas correctoras separadas | Activo = pasivo + patrimonio; cada celda conserva membresía exacta de líneas y mapeo |
| Resultados | Ingresos, coste de ventas, gastos por función, otros resultados e impuesto aplicable | Resultado reconcilia con cambios patrimoniales; distinguir margen operativo de resultado formal |
| Cambios en patrimonio | Apertura, resultado, aportes, distribuciones y otros cambios identificados | Movimiento no monetario no se pierde; contrato/aporte/acuerdo no sustituye dinero ni asiento |
| Flujos de efectivo | Movimientos y asignaciones brutas a operación/inversión/financiación; transferencias internas y partidas no monetarias identificadas | Saldo inicial + flujos + efectos de conversión que correspondan = saldo final; no derivar todo del saldo neto de una cuenta |
| Notas y políticas | Datos cuantitativos reproducibles y narrativas revisadas, con referencias a rubros | Nota identificada, versión, autor/revisor, evidencia y comparativo; una nota no cura reconocimiento incorrecto |
| Comparativos y transición | Períodos y marcos expresos, apertura/ESFA y conciliaciones de transición | No presentar ausencia de información como cero; no fabricar ejercicio anterior de una entidad nueva |

CasPro adopta como dirección el flujo directo para el reporte inicial, por utilidad al operador y datos disponibles. La guía §4.7 lo recomienda; no convertir el ejemplo en un mandato de formato rígido. La especificación de dominio deberá resolver transferencias entre cuentas, equivalentes de efectivo, moneda extranjera y operaciones mixtas sin duplicar flujos.

La cadena es: **paquete → estado/nota → rubro y versión del mapeo → cuenta aplicada → líneas/asiento → interpretación y política → hecho versionado → evidencia**. Navegar exige autorización en cada dueño. La vista agregada no concede lectura del documento privado. El paquete persistido conserva corte, entidad, marco, moneda, versiones de políticas/mapeos, datos de cierre y estado de aprobación. Su PDF es una representación generada conservada por Documents, nunca un CPE original.

## Cobertura leída y trabajo de política pendiente

Esta matriz rastrea las 18 secciones; sus acciones son requisitos de diseño de CasPro. No copia textos normativos ni presume que todos los supuestos ocurran en TILMUX.

| Sección NPIF | Alcance revisado | Evidencia/datos y especificación de CasPro |
|---|---|---|
| 1 | Microempresas | Expediente de elegibilidad separado del régimen fiscal; revisión ante crecimiento o supervisión |
| 2 | Principios, devengo, reconocimiento, medición, deterioro, baja, errores, conversión | Distinguir estimación de dato ausente, fecha económica de registro, corrección de cambio de estimación y transición de error; política documentada |
| 3 | Presentación, negocio en marcha, comparativos, notas | Evaluación gerencial y fecha de autorización; catálogo de revelaciones aplicables; ausencia de comparativo explicada |
| 4 | Situación financiera | Vencimientos, liquidez, restricciones, partidas correctoras y clasificación justificable |
| 5 | Resultados | Función del gasto, ingresos ordinarios, coste, impuestos y partidas materiales separables |
| 6 | Patrimonio | Conciliación por componente, aportes y distribuciones sustentados; obligatorio en producto |
| 7 | Efectivo | Clasificación de cobros/pagos brutos y exclusión de operaciones no monetarias del flujo; obligatorio en producto |
| 8 | Efectivo y equivalentes | Titularidad, moneda, restricciones, vencimiento original y finalidad; no todo depósito es equivalente |
| 9 | Inversiones | Instrumento, coste, cotización/fuente, intereses y deterioro; activar solo ante inversión real |
| 10 | Cuentas por cobrar | Derecho, vencimiento, cobros, deterioro y movimientos de estimaciones; prepago B2C no elimina otras cuentas por cobrar |
| 11 | Inventarios | Promedio ponderado móvil elegido, costes fuente y ajustes diferenciados; deterioro separado del kardex físico |
| 12 | PPE | Componentes, disponibilidad para uso, coste, vida útil, depreciación, bajas y conciliación; tasas tributarias no sustituyen estimaciones económicas |
| 13 | Otros activos | Clasificación sustentada; no usar como bolsa para partidas sin análisis |
| 14 | Pasivos financieros/CxP | Contrato, principal, intereses, vencimientos, extinción y saldo; límite de crédito disponible no es pasivo desembolsado |
| 15 | Obligaciones laborales | Preservar evidencia de servicios y beneficios si existen trabajadores; no crear nómina completa sin trigger |
| 16 | Ingresos | Evaluar condiciones de venta de bienes, descuentos, impuestos y coste fiable; cobro/CPE/despacho no equivalen por sí solos a ingreso |
| 17 | Arrendamientos | Contrato, opción de compra, cuotas, renovaciones y restricciones; no imponer automáticamente el modelo NIIF 16 |
| 18 | Primera adopción | ESFA, reconocimiento/reclasificaciones/mediciones, ajustes de transición y conciliaciones; no confundir transición con corrección corriente |

Las notas iniciales cubren entidad/actividad, bases y políticas, juicios/estimaciones; las demás se activan por hechos: efectivo restringido, inversiones, CxC/deterioro, inventario, PPE, otros activos, deuda/intereses, CxP, trabajo, provisiones, anticipos, ingresos, costes, gastos e impuestos. Añadir información material necesaria aunque no exista un casillero de ejemplo. No generar notas de negocios ficticios ni texto de cumplimiento mediante IA sin revisión.

## Diferencias que requieren políticas explícitas

- NPIF 2.52–2.53 trata errores anteriores en el resultado del período de detección y exige revelación; no heredar por defecto la reexpresión retrospectiva de NIC 8. Conservar fecha del hecho, período afectado, detección y motivo permite ambas interpretaciones cuando cambie el marco.
- NPIF 2.54–2.55 contempla moneda funcional y presentación en soles. La afirmación histórica de Wbpro de que la norma guarda silencio sobre moneda/errores es incorrecta. Los detalles de tipo de cambio y posibles tensiones de la redacción requieren política revisada, no improvisación del implementador.
- NPIF 3.1 remite a principios pertinentes de NIIF para PYMES para actividades no incluidas. La selección de edición y el análisis de partes relacionadas, garantías o hechos posteriores debe ser explícito. No afirmar que toda NIC 24 se vuelve obligatoria directamente porque NPIF no tenga una sección del mismo nombre.
- NPIF 2.9 permite otras bases bajo condiciones; no autoriza mezclar libremente tratamientos incompatibles. Cada excepción necesita análisis integral y aprobación profesional. La matriz NIIF identifica evolución, no cumplimiento simultáneo.
- La guía contiene ejemplos y detalles que no deben convertirse en reglas universales: deterioro a 90 días, probabilidad de 51%, vidas útiles de ejemplo y cifras tributarias referenciales. Se detectaron rótulos/referencias inconsistentes (p. 10 refiere a numeración inexistente en la NPIF leída; p. 17 mezcla 90/365 días). CasPro deriva políticas de la norma y hechos, no de esos umbrales ilustrativos.
- La guía §3 dice que la NPIF no exige por sí misma el PCGE; las obligaciones del catálogo proceden de sus resoluciones propias. CasPro utiliza PCGE por diseño y aplicabilidad verificada, sin presentar el plan como marco de reconocimiento.

## Gate previo a dominio congelado

Pendiente: confirmar elegibilidad empresarial, política NPIF por cada hecho del primer año y notas aplicables; resolver tratamiento de operaciones no cubiertas usando la remisión correcta; especificar apertura, precisión, clasificación de flujos, moneda y correcciones. La validación profesional recae en políticas y hechos, no se reemplaza por una aprobación de arquitectura.

La evidencia ejecutable futura deberá recorrer un período sintético con apertura, compra de bienes y servicio, cobro previo, venta, devolución, pago/financiamiento, deterioro y reversión, depreciación si aplica, corrección y cierre. Debe reconciliar cada estado y nota con el mayor y sus fuentes, demostrar aislamiento y congelación de versiones y generar el paquete sin dependencia obligatoria de Excel. Aquí no se ejecutó esa evidencia.
