# M08 — Cuatro estados, notas y goldens de aceptación

Estado: **SPECIFIED — candidato; aritmética documental contrastable, software NO demostrado**. Owner Accounting. Hereda [M07](../milestones/accounting-deep.md) y [NPIF reporting](../../accounting/npif-reporting.md). Estas cifras son enteramente sintéticas; no representan TILMUX ni una política tributaria aprobada.

## Contrato de paquete

Entrada: entidad, libro/marco/edición, ejercicio/corte, comparativo, cierre/revisión, plan/políticas/rubros versionados, moneda/escala, manifest exacto de líneas, auxiliares y notas. Salida: situación financiera, resultados, cambios en patrimonio, EFE directo y notas; HTML navegable y artefacto preservado por Documents, sin Excel obligatorio. Comparativo faltante es NOT AVAILABLE con explicación, nunca columna de ceros inventada.

Rubro contiene membresía de líneas, signo, regla de agregación y versión; cuenta puede desagregarse por dimensión, vencimiento y naturaleza si política lo exige. Reglas detectan líneas sin asignar o doble asignadas dentro del mismo estado. Una línea puede aparecer legítimamente en diferentes estados/notas; no deduplicar globalmente entre estados. Corriente/no corriente usa condiciones a fecha de corte, no primer dígito PCGE. Cuentas correctoras se explican, no desaparecen por neteo opaco.

EFE utiliza movimientos brutos y asignaciones aprobadas por naturaleza; transferencias internas se excluyen, no monetarias se revelan fuera del flujo, FX de efectivo se concilia separadamente. Cobro de anticipo puede ser flujo operacional antes de ingreso. La cifra de resultado no reemplaza efectivo. Una clasificación no resuelta impide marcar EFE final.

| ID / capacidad / clase | Reads / locks | Writes / corrección |
|---|---|---|
| R01 preparar paquete / accounting.report / D | Manifest, cierre, políticas/rubros/notas I→M→O→Q | Preview reproducible con controles/excepciones y fingerprints; render fuera de TX. Preview no firma ni cambia cierre |
| R02 autorizar paquete / accounting.approve_reports / D | Revisión, cierre vigente, comparativos/notas y mandato I→M→O→Q→D | Snapshot aprobado, fecha de autorización/actor, manifest y trabajo durable de render. Cambio desde preview rechaza; narrativas IA nunca aprueban cumplimiento |
| R03 preservar representación / documents.render / D | Snapshot aprobado, renderer/template/versiones I→O→Q→D | Bytes/hash ligados al mismo contenido; fallo de render deja paquete aprobado con representación pendiente, no lo regenera con datos vivos |
| R04 sustituir / accounting.approve_reports / D | Original, correcciones y nuevo cierre I→M→O→Q→D | Nueva versión con explicación/puente, anterior preservada y marcada sustituida. No sobrescribir PDF firmado ni enlace histórico |

Descarga y drill-through verifican autorización por dueño. Usuario con permiso de paquete pero sin expediente privado ve cifra y referencia permitida, no obtiene acceso al contrato por seguir un enlace. Pérdida de detalle autorizado se explica sin filtrar datos ajenos.

R02/R03 son un caso coordinado por Accounting: entrega a Documents un snapshot/mandato autorizado por valor y recibe identidad/hash de la representación. Documents no consulta el mayor ni llama hacia Accounting para reconstruir cifras. Render/lectura de bytes ocurren fuera de locks; la fase corta final verifica snapshot/revisión y vincula el artefacto. Una representación tardía de un paquete sustituido permanece identificada como tal, no vuelve a publicarlo como vigente.

## Golden G1: período completo y comparativo

Fixture PEN, moneda funcional/presentación PEN, cifras a centavos. Comparativo P0 es un snapshot contable de prueba provisto como entrada, con soporte sintético; no se infiere una exoneración fiscal real de sus cifras. P1 tiene operaciones gravadas hipotéticas con IGV18% e inputs de crédito plenamente elegible **solo para este caso**. RER1.5% se usa como cálculo fiscal; su clasificación de gasto en este golden es candidata y requiere [DH1](../../roadmap/decisions-gaps.md#dh1). No deducir regla legal de una columna de prueba.

P0: aportes8000, préstamo4000, ventas/cobros5000, compras5000 de las que se pagan4000, PPE pagado3000, COGS3000 y depreciación600. Resultado1400; inventario2000, PPE neto2400, AP1000, banco10000, deuda4000 y patrimonio9400. Constituye apertura conciliada de P1; todos los eventos del fixture tienen IDs sintéticos, sin documentos reales.

| Hecho P1 | Reconocimiento/cálculo de referencia | Efectivo |
|---|---|---|
| Compra mercancía a crédito1000+180 | Inventario+1000, crédito IGV180, AP+1180 | 0 |
| Cobro y venta plenamente devengada2000+360 | Banco+2360, ingreso2000, IGV débito360; COGS1200 e inventario−1200 | +2360 |
| Retorno y refund200+36; coste atribuible120 | Ingreso−200, IGV débito−36, inventario no vendible+120, COGS−120 | −236 |
| Servicio anual prepagado1200+216; mes consumido100 | Prepago1200, crédito IGV216; consumo gasto100/prepago−100 | −1416 |
| PPE adquirido600+108 y disponible para uso | PPE+600, crédito IGV108; depreciación del período antiguo50+nuevo10 | −708 |
| Servicio recibido sin factura150 | Gasto150, obligación devengada150; sin crédito IGV inventado | 0 |
| Préstamo adicional1000; restitución principal500 | Deuda+1000−500; sin ingreso ni gasto | +500 neto, piernas separadas |
| Comisión bancaria20 confirmada | Gasto20 | −20 |
| Pago AP de apertura1000 | AP−1000 | −1000 |
| Deterioro inventario80 | Gasto80/correctora80, sin movimiento físico | 0 |
| Provisión por obligación presente120 | Gasto120/pasivo120, inputs jurídicos/probabilidad provistos por fixture | 0 |
| Cuota RER sobre1800 de ingreso neto | Gasto candidato27/pasivo27; no impuesto diferido automático | 0 |

### G1: cadena causal y mayor de referencia

Identidad del fixture: libro sintético G1, períodos P0/P1, política de prueba G1-POL-v1 y mapping G1-MAP-v1. Los símbolos siguientes **no son códigos PCGE oficiales ni una propuesta de plan aplicado**. Representan roles contables para verificar causalidad sin inventar cuentas oficiales. Un futuro adapter debe vincularlos a cuentas autorizadas y declarar esa traducción.

Cada fila define hechos sintéticos F, interpretación I, asiento J y líneas por lado/símbolo: por ejemplo `G1/P1/J04/D/COGS`. I conserva IDs/revisiones F, componente, regla G1-POL-v1 e inputs/evidencia; J referencia I. La membresía de rubro usa esas líneas y G1-MAP-v1, nunca solo el saldo final del objeto mutable. Un conjunto de hechos relacionados puede soportar varios componentes distintos; se controla unicidad económica por hecho/componente, no “una fila contable por documento”. No se duplica una entrada porque la misma evidencia llegue desde Treasury y el banco.

Supuestos explícitos de G1: en P1 se han satisfecho y documentado las condiciones de reconocimiento de cada venta/retorno, compra y servicio indicado. El CPE ni el cobro, por sí solos, prueban devengo. Los hechos de recepción/factura de F01 se interpretan juntos sin un devengo anterior en el fixture; si ya hubiera uno, se concilia/reclasifica su componente, no se vuelve a reconocer. IVA/IGV, clasificación RER, plazos y mediciones son entradas sintéticas ya declaradas, sujetas a C01/C08 para uso real.

P0 se conserva como comparativo firmado de prueba. Su soporte se hace explícito sin inferir condiciones fiscales omitidas: `G1/P0/F01..09` soportan respectivamente aporte, préstamo, compra, pago AP, PPE, venta devengada, cobro, salida y depreciación. `I01..09/J01..09` producen D/C: BANK8000/CAP8000; BANK4000/LOAN4000; INV5000/AP5000; AP4000/BANK4000; PPE3000/BANK3000; AR5000/REV5000; BANK5000/AR5000; COGS3000/INV3000; DEP600/ACCDEP600. Movimiento total por lado37600. El cierre técnico P0 lleva REV5000−COGS3000−DEP600 a RETAIN1400; apertura P1 conserva únicamente saldos patrimoniales. Un P0 real requeriría su expediente fiscal/contable; estos movimientos no afirman que TILMUX estaba exonerada.

| IDs P1: hecho(s) → interpretación/asiento | Dueño y componente interpretado | Débito | Crédito |
|---|---|---|---|
| F01-R/F01-C → I01/J01 | Procurement/Inventory recepción y factura; coste/derecho fiscal/AP sin devengo previo | INV1000 + IGVC180 | AP1180 |
| F02-S/F02-C → I02/J02 | Sales devengo y evidencia CPE; ingreso/impuesto/derecho | AR2360 | REV2000 + IGVD360 |
| F03 → I03/J03 | Treasury cobro y aplicación al derecho anterior | BANK2360 | AR2360 |
| F04 → I04/J04 | Inventory salida atribuible a venta devengada | COGS1200 | INV1200 |
| F05-S/F05-C → I05/J05 | Sales retorno comercial/corrección fiscal; obligación de refund | RET200 + IGVD36 | REFUND236 |
| F06 → I06/J06 | Inventory retorno físico no vendible, coste de F04 | INV120 | COGS120 |
| F07 → I07/J07 | Treasury refund de la obligación, no otra reducción de ingreso | REFUND236 | BANK236 |
| F08 → I08/J08 | Procurement derecho a servicio anual y factura | PREPAID1200 + IGVC216 | AP1416 |
| F09 → I09/J09 | Treasury pago de F08 | AP1416 | BANK1416 |
| F10 → I10/J10 | Accounting consumo mensual sustentado en cobertura | PREEXP100 | PREPAID100 |
| F11 → I11/J11 | Procurement/PPE adquirido y crédito fiscal | PPE600 + IGVC108 | AP708 |
| F12 → I12/J12 | Treasury pago de F11 | AP708 | BANK708 |
| F13-A/F13-B → I13/J13 | Accounting cuotas de activo anterior50 y nuevo10, entradas de vida/disponibilidad | DEP60 | ACCDEP60 |
| F14 → I14/J14 | Procurement servicio recibido; Accounting devengo sin factura | SVC150 | ACCR150 |
| F15 → I15/J15 | Corporate instrumento y Treasury desembolso recibido; principal | BANK1000 | LOAN1000 |
| F16 → I16/J16 | Treasury restitución vinculada al instrumento | LOAN500 | BANK500 |
| F17 → I17/J17 | Treasury débito bancario confirmado con naturaleza comisión aprobada | FEE20 | BANK20 |
| F18 → I18/J18 | Treasury pago de AP de apertura | AP1000 | BANK1000 |
| F19 → I19/J19 | Accounting medición de deterioro, sin movimiento de unidades | IMPEXP80 | IMPAIR80 |
| F20 → I20/J20 | Accounting obligación presente/estimación con soporte del caso | PROVEXP120 | PROV120 |
| F21 → I21/J21 | Tax determinación RER27; Accounting interpreta su clasificación candidata | TAXEXP27 | TAX27 |

La comisión F17 consume una sola contribución de efectivo: el match del extracto no crea J17 otra vez. F13 conserva dos componentes/inputs aunque la tabla agregue sus cuotas. F21 referencia la determinación fiscal y la política Accounting; Tax no escribe el asiento. Las 21 entradas P1 tienen débitos=créditos14997 por lado, excluyendo apertura/cierre. AR y REFUND terminan en cero por sus aplicaciones, no por borrado de fuentes.

| Saldo de mayor antes del cierre P1 | D | C | Membresía G1-MAP-v1 / origen |
|---|---:|---:|---|
| BANK | 9480 | 0 | ESF efectivo; apertura10000 y J03/07/09/12/15/16/17/18 |
| INV | 1920 | 0 | ESF inventario bruto; apertura2000 y J01/04/06 |
| IMPAIR | 0 | 80 | ESF correctora; J19 |
| PREPAID | 1100 | 0 | ESF prepago; J08/10 |
| IGVC / IGVD | 504 | 324 | ESF crédito neto180 del fixture; J01/02/05/08/11; conservar ambos componentes |
| PPE / ACCDEP | 3600 | 660 | ESF PPE neto2940; apertura3000/600 + J11/13 |
| AP | 0 | 1180 | ESF AP; apertura1000 + J01/08/09/11/12/18 |
| ACCR / PROV / TAX | 0 | 297 | ESF tres rubros separados150/120/27; J14/20/21 |
| LOAN | 0 | 4500 | ESF deuda; apertura4000 + J15/16 |
| CAP / RETAIN | 0 | 9400 | ESF/ECP capital8000/acumulado inicial1400 |
| REV / RET | 200 | 2000 | ER ventas netas1800; J02/05 |
| COGS | 1080 | 0 | ER coste neto1080; J04/06 |
| PREEXP / DEP / SVC / FEE | 330 | 0 | ER gastos100/60/150/20; J10/13/14/17 |
| IMPEXP / PROVEXP / TAXEXP | 227 | 0 | ER gastos80/120/27; J19/20/21 |
| AR / REFUND | 0 | 0 | Auxiliares J02/03 y J05/07, miembros conservados con saldo0 |
| **Balance de comprobación** | **18441** | **18441** | Balancear no basta: exige miembros y hechos completos |

Las celdas agregadas con varios símbolos conservan miembros individuales. Fórmulas independientes: ER = REV−RET−COGS−PREEXP−DEP−SVC−FEE−IMPEXP−PROVEXP−TAXEXP =163. ESF activo usa BANK+INV−IMPAIR+PREPAID+IGVC−IGVD+PPE−ACCDEP =15540; pasivo AP+ACCR+PROV+TAX+LOAN =5977; patrimonio CAP+RETAIN+resultado del período =9563. ECP muestra apertura9400, resultado163 y sin aporte/distribución P1. El cierre P1 transfiere163 a RETAIN mediante asiento de clase cierre: ER excluye ese asiento de transferencia, ESF/ECP usan acumulado después del cierre **o** acumulado anterior más resultado, nunca ambos. No hay plug para la diferencia Activo−Pasivo.

EFE tiene membresía sobre piernas de efectivo, con vínculo a J: operación J03+2360/J07−236/J09−1416/J17−20/J18−1000 =−312; inversión J12−708; financiación J15+1000/J16−500 =+500. Total−520; apertura10000→9480. No deriva flujo de la diferencia de balances de inventario/AP ni usa préstamo neto para ocultar dos piernas. Compra a crédito, mediciones y consumo no aparecen como cash. Transferencia entre cuentas propias requeriría excluir ambas piernas enlazadas, no aplicar esta fórmula a cada cuenta por separado sin consolidación.

Control de completitud: manifiesto esperado de hechos/componentes → manifiesto interpretado → líneas activas → rubros/notas; anti-joins en cada frontera detectan faltante o doble consumo aunque los débitos/créditos cuadren. Un mismo componente legítimamente aparece en ESF/nota y EFE por distinta dimensión; la regla de unicidad es dentro del estado/rubro conforme a su función, no deduplicación global. Fórmulas declaran operandos y grafo acíclico; notas narrativas referencian evidencia/juicio y se contrastan contra cifras. Ni el resultado ni una diferencia del propio estado pueden alimentar la fuente que los calcula. Revisión/ejecución B07–B08 debe inyectar omisión, duplicación, circularidad y mapeo incorrecto y rechazarlos, sin falsificar drill-through.

### Salidas esperadas

| Situación financiera | P0 | P1 |
|---|---:|---:|
| Efectivo | 10000 | 9480 |
| Inventario bruto | 2000 | 1920 |
| Correctora inventario | 0 | −80 |
| Prepago | 0 | 1100 |
| Crédito IGV neto | 0 | 180 |
| PPE bruto | 3000 | 3600 |
| Depreciación acumulada | −600 | −660 |
| **Activo total** | **14400** | **15540** |
| AP comercial | 1000 | 1180 |
| Servicio devengado | 0 | 150 |
| Provisión | 0 | 120 |
| Tributo pendiente | 0 | 27 |
| Préstamo | 4000 | 4500 |
| **Pasivo total** | **5000** | **5977** |
| Capital | 8000 | 8000 |
| Resultados acumulados, incluido ejercicio | 1400 | 1563 |
| **Patrimonio total** | **9400** | **9563** |

Vencimientos provistos por fixture clasifican AP/devengo/tributo/provisión corrientes y préstamo no corriente; cambiar fecha/condiciones debe cambiar presentación sin editar monto. El activo no se presenta como una única bolsa: PPE neto2940 no corriente; demás conforme a recuperación/uso del caso.

| Resultados | P0 | P1 |
|---|---:|---:|
| Ventas netas | 5000 | 1800 |
| Coste de ventas | −3000 | −1080 |
| Margen | 2000 | 720 |
| Servicio consumido | 0 | −100 |
| Depreciación | −600 | −60 |
| Servicio devengado | 0 | −150 |
| Comisión | 0 | −20 |
| Deterioro | 0 | −80 |
| Provisión | 0 | −120 |
| Tributo RER, clasificación candidata | 0 | −27 |
| **Resultado** | **1400** | **163** |

ECP P0: apertura0 + aporte8000 + resultado1400 =9400. ECP P1 por componentes: capital8000 sin movimientos; resultados1400 +163 =1563; patrimonio final9563. Deuda recibida1000 no entra en ECP. Cerrar cuentas de resultados no vuelve a sumar163.

| EFE directo | P0 | P1 |
|---|---:|---:|
| Cobros de clientes | 5000 | 2360 |
| Refunds | 0 | −236 |
| Pagos a proveedores/servicios/comisiones | −4000 | −2436 |
| **Operación** | **1000** | **−312** |
| PPE pagado, importe bruto según política del fixture | −3000 | −708 |
| **Inversión** | **−3000** | **−708** |
| Aportes | 8000 | 0 |
| Préstamos recibidos | 4000 | 1000 |
| Principal restituido | 0 | −500 |
| **Financiación** | **12000** | **500** |
| **Variación** | **10000** | **−520** |
| Efectivo inicial / final | 0 / 10000 | 10000 / 9480 |

Compra a crédito1180, devengo150, provisión120, depreciación60 y deterioro80 no son flujos. IGV: débito360−36=324; crédito180+216+108=504; activo neto180. La política de presentación del IGV en EFE (bruto por naturaleza de pago en este caso) debe aprobarse y mantenerse; no netear automáticamente contra toda caja tributaria.

### Notas mínimas del golden y drill-through

1. Entidad sintética, actividad, período, marco/edición, base y moneda; declaración de cumplimiento solo tras revisión real.
2. Políticas/estimaciones: promedio, coste/vida/residual de PPE, prepago, provisión, deterioro y clasificación del RER del fixture; discrepancias pendientes impiden usarlo como política real.
3. Efectivo9480: cuenta sintética y puente Treasury/banco/GL; restricciones y equivalentes explícitos.
4. Inventario2000+1000−1200+120=1920; correctora80, neto1840, retorno no vendible120; VNR sin alterar unidades.
5. PPE3000+600=3600; depreciación600+60=660; neto2940. Inputs de depreciación provistos; no inventar vida a partir de cuota.
6. Prepago1200−100=1100; devengo150, AP1000+1180−1000=1180 y provisión120, naturaleza/vencimientos.
7. Financiación4000+1000−500=4500, términos y relación sintéticos; cambios no monetarios0.
8. Impuestos/contingencias y relacionadas, decisiones de elegibilidad y estimaciones; IGV504−324=180 y RER27 con fuentes separadas.
9. Patrimonio y resultado163; hechos posteriores/negocio en marcha/autorización, evaluados con inputs del caso.

Ejemplo navegable: celda inventario1840 → inventario bruto1920/correctora80 → líneas y políticas → movimientos G1 de compra/salida/retorno y medición80 → evidencias sintéticas. Mostrar la valoración operativa original y revisada si aplica; un número sin membresía no pasa.

## Goldens adicionales obligatorios

| Caso | Resultado que debe demostrar el software posterior |
|---|---|
| G2 UNKNOWN/coste tardío | Mismo kardex de INV03, deltas exactos y bloqueo de informe final mientras falta coste; nueva revisión no muta G1 autorizado |
| G3 error vs estimación vs transición | Mismo hecho preservado; NPIF error en detección con nota, cambio de estimación prospectivo según política, primera adopción en ESFA; NIIF retroactividad solo en libro/marco correspondiente |
| G4 PPE/intangible/lease/trabajo | Activo disponible no pagado, componente reemplazado, vida revisada, amortización y contrato de arrendamiento; salario/beneficio devengado sin pago; ausencia de trigger documentada, no notas vacías |
| G5 FX/instrumento/relacionada | Principal/divisa/fechas/tasas y FX de caja separados de flujos; préstamo gratuito no ingreso y consecuencia fiscal separada; capitalización sin cash |
| G6 aislamiento/corrección/concurrencia | Dos entidades mismas cuentas; posting vs cierre; paquete con snapshot obsoleto rechaza; reversión doble; comparación versión antigua/nueva |
| G7 transición NIIF18 | Mismos hechos/mayor, nuevo mapeo de categorías/subtotales, comparativos y MPM si corresponde; no reconstruir Sales/Treasury |

Aritmética en este archivo es especificación esperada, no test de CasPro ni prueba de motor contable. WO ejecutará goldens y generará cuatro estados+notas/drill-through; validará números con un cálculo independiente y contador. QA: DOMAIN/POSTGRESQL/CONCURRENCY, golden contable, un E2E de navegación, render/accesibilidad y recovery de snapshot. Astra checkpoint final; Sol orquesta; implementador/reviewer distintos. No aceptar M08 por un balance de prueba o dos PDF aislados.
