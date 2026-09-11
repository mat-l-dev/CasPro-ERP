# NPIF — catálogo de políticas y refutación de la guía

Propietario: Accounting. Corte 2026-09-11; target 2027. **SPECIFIED CANDIDATE / PROFESSIONAL VALIDATION REQUIRED**: define decisiones que el producto debe representar, no aprueba las políticas de una empresa. Aplica únicamente con perfil NPIF elegible y vigente. Las reglas tributarias permanecen en Tax.

## Fuentes y lectura efectiva

Se leyó íntegramente la [NPIF oficial, 31 páginas](https://cdn.www.gob.pe/uploads/document/file/5775793/5126738-norma_peruana_para_microempresas.pdf), SHA-256 `01be48e99862949bd30148231ccfd73525ab8995cc2a8d73705401783cb02d1f`, y la [guía práctica oficial, 40 páginas](https://cdn.www.gob.pe/uploads/document/file/8541823/7076966-guia_-practica_npif.pdf), SHA-256 `b9f47b68f60a8f43b0f32961f68b837702ec7700848cfdbdf305c8a45d4f9229`. La guía declara en p.4 que la norma prevalece en discrepancias. Su Excel ilustra un caso; CasPro debe producir los estados y notas desde sus propios hechos/ledger sin depender de esa hoja.

La elegibilidad se resuelve separadamente del RER: [RCNC 003-2022](https://www.mef.gob.pe/es/consejo-normativo-de-contabilidad/resoluciones-2/resoluciones-cnc/30196-resolucion-n-003-2022-ef-30/file) arts.1–3 distingue ingresos ordinarios, dos ejercicios para ciertos cambios, inicio/reinicio por estimación y regímenes de supervisados. La NPIF cubre microempresas hasta 150 UIT según su alcance y resolución de aprobación. Ni “SAC” ni “RER” acreditan automáticamente esa condición. Deben constar ejercicio de referencia, UIT pertinente, ingresos/estimación documentados, supervisor, marco anterior y elección válida.

## Reglas por sección y contrato del producto

Cada política contiene entidad, marco/edición, ID/revisión, vigencias sin solapamiento, texto/fuente/párrafo, alcance de hechos, decisión/juicio, parámetros aprobados, autor/revisor y casos de aceptación. Modificarla crea versión; no reinterpreta historia silenciosamente. El período afectado se decide en la revisión del cambio.

| ID / sección NPIF | Reconocimiento, medición o presentación | Datos y salida exigidos | Decisión pendiente / contraejemplo |
|---|---|---|---|
| NP-01 / 1 Alcance | Microempresa elegible; no confundir tamaño contable con régimen fiscal | Perfil y evidencia de ingresos/supervisión; declaración de marco | Validar TILMUX y permanencia/transición; no copiar `<150` |
| NP-02 / 2 Conceptos | Devengo 2.50; criterios de reconocimiento/fiabilidad; materialidad específica 2.13; estimación razonable posible | Fecha del hecho y de registro distintas; juicio/materialidad y evidencia mínima | Desconocido no es cero; estimar no autoriza inventar una factura |
| NP-03 / 3 Presentación | Anual 31/12; comparativos y notas; 3.8 conjunto y 3.9 opcionalidad ECP/EFE | Paquete de cuatro estados y notas por decisión del propietario | No declarar que NPIF obliga universalmente a los cuatro; producto sí los exige |
| NP-04 / 4 ESF | Corriente/no corriente o liquidez si presentación más fiable; activos/pasivos y patrimonio separados | Vencimientos, restricciones, anticipos, devengos sin factura, provisiones, reservas y resultados | Cuenta PCGE no determina sola vencimiento ni compensación |
| NP-05 / 5 ER | Presentación de gastos por función; ingreso/costo y otros resultados trazables | Mapeo naturaleza→función con base y asignación reproducible | RER 1.5% del ejemplo no decide presentación ni alcance de impuesto a ganancias en otros marcos |
| NP-06 / 6 ECP | Movimientos de cada componente, resultado, propietarios y ajustes identificados | Capital, aportes pendientes, reservas, dividendos, acumulados y transición | Dinero del socio no es capital por defecto; no usar cuenta puente para cuadrar |
| NP-07 / 7 EFE | Actividades operación/inversión/financiación; 7.3/7.6 categorías brutas; no mezclar operaciones sin efectivo | Movimiento bancario/caja, moneda, origen y categoría con versión; conciliación de efectivo | Producto elige directo. La guía p.9 dice que el método no es exigido; conservar esa discrepancia de formulación, no crear dos políticas contradictorias |
| NP-08 / 8 Efectivo | Nominal; equivalentes de alta liquidez y bajo riesgo, vencimiento original ≤3 meses, compromisos cortos; restricciones reveladas | Fecha original/vencimiento, naturaleza, disponibilidad, moneda, conciliación | Un depósito a 12 meses al que quedan 2 no se vuelve equivalente automáticamente |
| NP-09 / 9 Inversiones | Inicial costo; posterior valor razonable salvo falta de información, entonces costo; intereses devengados | Contrato, valor fuente/fecha, rendimiento, vencimiento, deterioro | “NPIF todo al histórico” es falso; cuenta bancaria no define clasificación |
| NP-10 / 10 CxC | Costo histórico/valor de sustento; evidencia objetiva de deterioro por 2.44–2.46 | Antigüedad, garantías, cobros posteriores, disputa y estimación revisable | No copiar 90 días del ejemplo como deterioro automático ni 365 del encabezado contradictorio |
| NP-11 / 11 Inventarios | Costo adquisición/puesta a disposición; descuentos comerciales iniciales reducen costo; descuentos posteriores, como pronto pago, van a resultados (11.6); interés/FX de compra a crédito a gasto (11.7) | Cantidad/valor fuente, naturaleza y fecha de descuento, gastos atribuibles, método uniforme | Promedio móvil operativo aceptado; política financiera de ajuste y atribución debe seguir NPIF, no IAS 2 importada |
| NP-12 / 12 PPE | Costo menos depreciación/deterioro; no revaluación posterior 12.7; componentes/reemplazos/bajas; depreciar desde disponible para uso y también inactivo salvo excepciones del método | Activo/componente, disponibilidad, vida/residual/método, ubicación/custodio, rollforward | Tasas fiscales solo si reflejan vida útil; compra≠disponibilidad; terreno separado |
| NP-13 / 13 Otros activos | Clasificación y medición según naturaleza; no depósito genérico de desembolsos difíciles | Derecho/beneficio, costo, recuperación, evidencia y deterioro | SaaS/prepago/intangible necesita análisis específico, no código 38 automático |
| NP-14 / 14 Pasivos | Obligación financiera/CxP a costo histórico; devengo de intereses, vencimientos, extinción sustentada | Principal, tasa contractual, cuota, interés devengado/pagado, condonación/capitalización | Mutuo gratuito no adopta descuento NIIF 9 por analogía automática; Tax evalúa mercado por separado |
| NP-15 / 15 Empleados | Obligación por servicios/beneficios según alcance del marco | Condición de empleador, servicio, concepto, período, estimación, pago | Sin trabajadores conocidos: trigger, no nómina inventada; prestaciones compradas no se reclasifican por etiqueta |
| NP-16 / 16 Ingresos | Para bienes, cinco condiciones de 16.4, incluidas transferencia de riesgos/beneficios, ausencia de gestión/control continuado, medición/probabilidad/costo fiables | Contrato/entrega/aceptación, descuentos, devoluciones, anticipos y evidencia | Ni CPE, PAID ni cobro ni despacho aislado prueban todas las condiciones; COGS coincide con período del ingreso (11.12) |
| NP-17 / 17 Arrendamientos | Derecho de uso vs servicio; con opción de compra 17.2 reconoce PPE; sin opción 17.3 gasto por devengo | Contrato/activo, opción, pagos, plazo, aceptación, saldo/corriente | No implantar NIIF 16 universalmente en NPIF; compra de hosting no es arrendamiento por nombre |
| NP-18 / 18 Primera adopción | ESFA al comienzo del primer período presentado; ajustes de transición en acumulados; costo atribuido/elecciones delimitados; conciliaciones y explicación | Saldos previos/evidencia, ajustes y marco anterior, fecha, elecciones, comparativos | No afirmar que inicio de software es primera adopción; ausencia de EEFF previos se revela, no genera ceros ficticios |

## Políticas transversales que requieren tratamiento explícito

**Deterioro y reversión (2.44–2.46).** Revisar evidencia objetiva al cierre; pérdida frente a mejor estimación de importe realizable y reversión limitada al valor sin deterioro. Inventory mantiene cantidad y costo operativo; Accounting conserva ajuste separado y su fuente. Un retorno no vendible exige inspección, pero no es automáticamente destrucción, pérdida total o deducción fiscal. El deterioro NPIF no se etiqueta indistintamente NIC 2/NIC 36.

**Errores (2.52–2.53), estimaciones y políticas.** Error anterior NPIF se corrige en resultados del período de detección y se explica naturaleza/rubros/importes; no aplicar por defecto retrospectiva NIC 8. Cambio de estimación no es error porque cambió información disponible. Cambio de marco tiene expediente de transición propio. Una fecha cerrada no justifica cambiar la fecha del hecho original.

**FX (2.54–2.55).** Estados en soles; conservar moneda funcional como evaluación aparte. Tasa, fuente SBS, fecha y sentido compra/venta y partida aplicada se guardan con el cálculo. Párrafo 2.55 menciona activos/pasivos al cierre e ingresos/gastos a fecha de transacción: el alcance para partidas no monetarias y su relación con medición específica necesita interpretación profesional; no copiar un algoritmo “revalorizar todo saldo en USD”. Ganancias/pérdidas no se confunden con flujos de efectivo.

**Vacíos/otras bases (3.1 y 2.9).** Registrar cuestión concreta, principio PYMES pertinente, edición consultada y justificación de compatibilidad; la NPIF se basa en PYMES 2015, mientras PYMES 2025 entra en vigor en 2027. No actualizar automáticamente la referencia supletoria ni mezclar selectivamente tratamientos favorables. Otra base de medición implica todas sus consecuencias y no anula prohibiciones específicas como 12.7. Intangibles, provisiones/contingencias complejas y efectos de impuesto diferido requieren memo por caso antes de automatizar.

**Notas.** Catálogo de aplicabilidad, no texto fijo: actividad/bases/políticas, juicios, efectivo/restricciones, inversiones, CxC/deterioro, inventario/deterioro, PPE/rollforward, otros activos, deudas/CxP, empleados, provisiones, anticipos, ingresos, costo/gastos, FX, impuestos y transición. Partes relacionadas se evalúan por relevancia, presentación fiel y política del marco; no afirmar NIC 24 íntegra obligatoria bajo NPIF. Cada nota enlaza cifras y evidencia y admite narración revisada.

## Discrepancias verificadas de la guía; no convertirlas en goldens sin revisión

| Página | Observación concreta | Tratamiento CasPro |
|---|---|---|
| 9 frente a NPIF 7.3/7.6 | Guía recomienda directo y dice que no es exigido; NPIF pide categorías brutas | Elegir directo por producto; no resolver jurídicamente la tensión por paráfrasis |
| 10 | Remite clasificación corriente a “6.3.1–6.3.6” aunque la norma trata ESF en sección 4; rótulo de total no corriente dice corriente | Enlazar párrafos reales, no copiar referencias/rótulos |
| 17 y 29 | Texto/política usa mora >90 días; encabezado de tabla dice >365, con importes de 105–136 días deteriorados | Evidencia específica y política profesional; ningún umbral universal |
| 20 y 29 | Vida de edificio 35 años en cuadro y 33 en política; tasas enteras aproximan reciprocales | Guardar vida/método/fecha; cuantización aprobada; no importar tasas del ejemplo |
| 14, 21 y 35 | Depreciación inicial 10,154 en antecedentes frente a 10,153 en desarrollo/rollforward | Golden propio concilia céntimos; no “tolerancia” para esconder una diferencia |
| 25 y 31 | Subtotal inicial corriente 114,607 frente a suma/conciliación 114,608 | Reconciliación de filas obligatoria; no reproducir total inconsistente |
| 33 | Nota dice CxC dentro del plazo, pero antigüedad presenta vencidos | Narración debe validarse contra cifras; IA no puede aprobarla |
| 27 | Falta EFE comparativo por información no disponible en el caso | Registrar limitación y fundamento del paquete concreto, no eximir todos los comparativos |
| 23 | 1.50% tributario explícitamente referencial | Tax determina régimen/base/tasa mensual aplicable; no inferir obligaciones por un ejemplo anual |

## Gate de política

Para activar NP-01–NP-18 en un libro real: hechos/elecciones acreditados, interpretación profesional, casos pertinentes y trazabilidad norma→política→regla→asiento→estado/nota. La arquitectura de política y su representación se revisan mediante [M07](../specs/milestones/accounting-deep.md); la aprobación de valores, estimaciones y aplicabilidad reales es [C01/C03](../roadmap/decisions-gaps.md#activation-gates), no una aprobación pendiente de toda la arquitectura. Una respuesta profesional que exija datos, reconocimiento o salida fuera de los contratos especificados abre un amendment A antes de ampliar/activar ese alcance. No se autoriza un intérprete genérico para suplir una regla ausente. Freeze documental no declara aprobadas políticas reales ni permite emitir EEFF oficiales.
