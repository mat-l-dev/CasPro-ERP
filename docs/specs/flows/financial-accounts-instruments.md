# Cuentas financieras, instrumentos, caja chica y locales

Propuesta del amendment; autorización en [review](../../review.md). Extiende [Treasury M06](../milestones/treasury-corporate-deep.md), [Accounting M07](../milestones/accounting-deep.md) y [financiación aceptada](financing-events-statements.md). Cuenta, instrumento, contrato, movimiento, aplicación, extracto y asiento conservan dueños/identidades distintos. Todo nuevo comando aplica CM0 y contratos públicos, sin llamadas inversas Accounting→Treasury.

## Cuenta Treasury y perfil contable

FinancialAccount Treasury: entidad/titular probado, tipo banco/caja/caja chica/custodia, institución/referencia enmascarada, moneda, vigencia/estado y permisos. Instrumentos de crédito referencian sus cuentas de liquidación; límite disponible no se agrega a efectivo. Destino bancario de proveedor es otro maestro versionado, no cuenta propia.

AccountPostingProfile pertenece a **Accounting**: FinancialAccount ID, entidad/libro/moneda/tipo, cuenta GL principal y reglas por componente (comisiones/intereses/transferencia/custodia), vigencia desde/hasta, versión/catálogo PCGE/política, aprobador y evidencia. Un namespace PCGE no decide reconocimiento. Evitar solapamientos para el mismo hecho; mapping ausente/inválido bloquea posting dependiente y muestra pendiente, no suspense automático ni selección libre de cuenta por operador de caja.

Posting conserva perfil/policy/FX/componentes efectivos en fecha según regla, y cuenta realmente usada. Cambiar mapping no mueve saldos históricos; reclasificación requiere asiento autorizado con puente de saldo por cuenta/fecha. Reconciliación por tres capas: banco externo↔movimientos Treasury; movimientos/aplicaciones↔objetivos y caja; hechos/interpretaciones↔GL. Una transferencia en tránsito o un asiento pendiente explica diferencia; no ajustar saldo para igualar. Cuenta cerrada bloquea nuevos movimientos ordinarios; reversión/corrección histórica tiene autorización propia y no se borra.

## Préstamo, línea bancaria y tarjeta

BankFacility Treasury: prestamista Party, contrato/versión, moneda, límite/plazo/disponibilidad/no dispuesto, desembolsos, amortizaciones, garantías/restricciones, estado DRAFT/APPROVED/ACTIVE/SUSPENDED/CLOSED y aprobaciones. Corporate conserva facultades/documento legal; Treasury saldo/principal y eventos; Accounting medición/FX/presentación; Tax deducción/retenciones. Línea aprobada sin desembolso tiene principal0 y efectivo0. Incrementar límite no registra ingreso.

Drawdown evidencia fecha/importes bruto/neto, cuenta receptora, cargos retenidos y naturaleza, contrato y cronograma; principal bruto puede diferir de efectivo recibido y cargos deben conciliar. InstallmentScheduleRevision distingue vencimiento/capital/interés/seguro/comisión/impuesto, tasa fija/variable y referencia contractual/observación. Cronograma previsto no es movimiento ocurrido ni devengo automáticamente aprobado. Evento de interés devengado deriva de regla/periodo/evidencia con revisión; cargos del banco se contrastan con contrato, no se aceptan por importarse.

PaymentAllocation descompone cada cuota real: capital/interés/comisión/seguro/tributo y residual, objetivos exactos; principal no es gasto y abono no identifica por sí mismo naturaleza. Prepago, penalidad, mora, cambio tasa y reestructuración requieren nueva revisión contractual/calendario y conciliación viejo→nuevo; no borrar interés anterior. Accounting clasifica corto/largo plazo según vencimientos/condiciones y marco, no por tipo de cuenta. C01/C05/C06/C08 aprueban instrumento real/política, sin activar NIIF9 por nombre «préstamo».

CorporateCard: entidad, emisor/instrumento, tarjeta enmascarada/token de referencia (sin PAN/CVV), custodio/usuarios, moneda/límites/ciclo/corte/vencimiento y política de uso. Authorization/pendiente del emisor no es cargo liquidado; CardTransaction conserva ID externo/fecha comercio/contabilización, importe/moneda/FX/comercio/categoría/beneficiario y estado UNIDENTIFIED→DOCUMENT_PENDING→CLASSIFIED/DISPUTED→RECONCILED. Comprobante y adquisición causal los posee Procurement, no se crea gasto fiscal por extracto.

Gasto personal/no identificado queda HOLD y posible cuenta por cobrar al responsable solo tras decisión competente; no gasto automático ni negación del pasivo real frente al banco. Cuotas de compra ligan adquisición original, principal y financiación; no registrar gasto total en cada cuota. Statement por período conserva saldo anterior+cargos/intereses/comisiones−abonos/devoluciones=saldo final, diferencias y vencimiento. Pagar tarjeta cancela pasivo y sale banco, no compra otra vez. Reembolso del comercio referencia cargo/disputa original; reversal conserva historia y no duplica crédito.

## Caja chica

PettyCashFund por entidad/sede/custodio/moneda, monto autorizado y límites/evidencia/política efectiva. OPENING_PENDING→OPEN→RENDERING→RECONCILED→CLOSED; suspensión/arqueo son eventos, no borrar fondo. Constitución es transferencia de dinero a caja/custodia y confirmación de recibido; no gasto. Vale/anticipo interno referencia responsable/destino y saldo pendiente; gasto rendido requiere documento/adquisición/aprobación y aplica una vez. Rendición agrupa vales/gastos/devoluciones/efectivo contado, fecha/corte/custodio/revisor y excepciones; costo/gasto/IGV se clasifican por Accounting/Tax.

Reposición se calcula desde gastos aprobados y necesidad/límite, produce transferencia distinta, no segundo gasto. Arqueo conserva denominaciones/conteo y saldo esperado; faltante/sobrante crea discrepancia, investigación y ajuste/recuperación aprobados, no edición del saldo. Cierre exige liquidar vales, retornar efectivo y resolver diferencia con evidencia; cambio de custodio necesita entrega/recepción a fecha, no reemplazar nombre histórico. Concurrencia bloquea raíz fondo y aplicaciones para impedir doble rendición/reposición.

## Constancia individual y custodia mutuo

Corporate genera una **constancia por disposición/pago por cuenta** desde evento aceptado, acuerdo y versión: identidades/roles, moneda, importe, fecha económica y de documento, modo/destino real, referencias de obligación/proveedor/banco cuando existan, principal vs derecho reembolsable, firmas y anexos. Nombre comercial «liquidación» no la vuelve CPE ni prueba suficiente de transferencia. Estado PREPARED→GENERATED→PRINTED→WET_SIGNED→SCANNED→VERIFIED, con fechas reales independientes y localizador físico; firma digital según [Documents](records-signatures-site-packs.md).

Si aún no ocurrió desembolso, imprimir propuesta rotulada PENDING_FUNDS no confirma dinero/principal. Scan distinto del generado se conserva como documento recibido con diferencia pendiente, sin reemplazar original ni validar automáticamente. Verificador coteja contenido/monto/partes/firmas/versiones, fecha y correspondencia al evento; el documento puede firmarse después del movimiento conservando ambas fechas. Estado mensual aceptado sigue derivado de eventos y revisiones; esta constancia no repostea financiación, no mezcla reembolso con amortización ni crea caja ficticia por pago personal.

## Arrendamiento de sede

SiteContract Corporate: sede Organization, arrendador Party/representante, contrato y opción de compra si existe, vigencia, renta/moneda/periodicidad, depósito/garantía, ajustes/indexación contractual con fuente, renovación/preaviso/terminación, permisos y evidencia. DRAFT→REVIEWED→SIGNED→ACTIVE→EXPIRED/TERMINATED; obligaciones/custodia/stock pueden seguir abiertos tras expiración. No cierre destructivo de sede/almacén.

Procurement crea obligación recurrente por **contrato+período+componente**, una vez; revisión de índice modifica solo períodos autorizados. Conformidad/documento del arrendador según naturaleza, no factura ficticia; depósito recuperable separado de renta, devolución/retención por daños sustentadas. Treasury aplica pago; Accounting devenga renta/prepagos/depósito según NPIF17/política y evalúa opción de compra, no IFRS16 automáticamente. Tax conserva sustento/retención/IGV que corresponda al arrendador y operación. Terminación calcula renta devengada/penalidad/devolución garantía por aprobación y acuerdo, no por borrar contrato.

## Matriz de comandos / evidencia

| ID / capacidad | Guardas, locks y efecto atómico | Corrección/fallo |
|---|---|---|
| FI1 aprobar mapping / accounting.policy.approve | Cuenta pública válida, libro/catálogo/vigencia no superpuesta; lock perfil/libro | Nueva revisión auditada; histórico intacto; sin mapping posting queda pendiente |
| FI2 disponer/amortizar / treasury.finance.confirm | Instrumento/cronograma/objetivos/movimiento, residuales y evidencia; lock instrumento+fuentes/aplicaciones en CM0 | Hechos/componentes una vez; no capital por documento; reversión coordinada con consumidores |
| FI3 clasificar tarjeta/rendir caja / treasury.expense.approve + Procurement | Fuente/gasto no aplicado antes, responsable/política/revisión; lock instrumento/fondo/obligaciones | Relación a adquisición real, residual exacto, HOLD fiscal si falta CPE; cuenta por cobrar solo aprobada |
| FI4 reponer/arqueo/cierre / treasury.petty.manage | Corte consistente, conteo/vales/movimientos, dinero devuelto acreditado | Transferencia/ajuste distintos; faltante impide cierre limpio hasta resolución |
| FI5 documentar disposición / corporate.finance.document | Snapshot evento/acuerdo y revisión, plantilla y autor; Documents recibe valores | Intent/version/hash durable; firmado no cambia saldo; incongruencia produce expediente pendiente |
| FI6 devengar renta / procurement.rent.confirm | Contrato/período/componente únicos, ajuste contractual aprobado | Objetivo/hecho + audit; reintento no duplica renta; corrección por delta/aprobación |

Accounting consume source components por identidad/revisión y política bajo M07: AP/AR, bancos, inventario/COGS, PPE/depreciación, pasivos/intereses/cargos, caja chica, depósitos/renta, relacionados, FX y tributos. Prepagos/accruals/recurrencias tienen regla/fecha/soporte/revisión y reversión, no asientos automáticos sin mandato. Cierre reconcilia auxiliares→GL→balance→cuatro EEFF/notas. B03–08/B10/B13 deben validar estas extensiones; no se ejecutan ahora.
