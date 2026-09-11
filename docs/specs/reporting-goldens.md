# M08 — Cuatro estados, notas y goldens de aceptación

Estado: **SPECIFIED — candidato; aritmética documental contrastable, software NO demostrado**. Owner Accounting. Hereda [M07](accounting-deep.md) y [NPIF reporting](../accounting/npif-reporting.md). Estas cifras son enteramente sintéticas; no representan TILMUX ni una política tributaria aprobada.

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

Fixture PEN, moneda funcional/presentación PEN, cifras a centavos. Comparativo P0 es un snapshot contable de prueba provisto como entrada, con soporte sintético; no se infiere una exoneración fiscal real de sus cifras. P1 tiene operaciones gravadas hipotéticas con IGV18% e inputs de crédito plenamente elegible **solo para este caso**. RER1.5% se usa como cálculo fiscal; su clasificación de gasto en este golden es candidata y requiere H1. No deducir regla legal de una columna de prueba.

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
