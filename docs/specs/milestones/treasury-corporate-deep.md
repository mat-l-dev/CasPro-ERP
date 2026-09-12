# M06 — Treasury, conciliación y Corporate

Estado: **SPECIFIED — candidato; financiación PENDING PROFESSIONAL VALIDATION**. Hereda [contrato común](../cross-cutting/economic-facts.md), [Treasury](../../domain/treasury-finance.md), [Corporate](../../corporate/architecture.md) y [mutuo investigado](../../research/normative/mutuo-tax-corporate.md). La validación del mutuo precede al primer contrato/desembolso, aunque su UI sea M06.

## Dinero y conciliación son dimensiones distintas

Treasury posee cuentas, cobros/pagos/transferencias, aplicaciones y correcciones. Extractos son evidencia externa inmutable importada, no movimientos internos. Estados: propuesta de dinero→confirmado/rechazado; aplicación vigente/revertida; línea bancaria sin conciliar/parcial/conciliada; grupo propuesto/confirmado/revertido; período/corte abierto/cerrado. Un grupo confirmado no autoriza al banco, no cambia beneficiario ni crea un journal.

Saldo por cuenta/moneda = apertura + entradas confirmadas − salidas confirmadas ± correcciones explícitas. Dinero no identificado conserva pagador desconocido y evidencia; dinero no aplicado tiene propietario/moneda pero no obligación asignada. Son problemas diferentes. SP2 conserva límites de aplicación, refund y cobertura total; una nota de crédito o devolución no acredita salida bancaria.

Transferencia propia tiene dos piernas vinculadas y moneda de cada cuenta. Misma moneda: importes iguales; FX: ambos importes reales, tipo/tasas/comisión separados y evidencia, sin generar una conversión retrospectiva por editar maestro. Transferencia en tránsito distingue salida confirmada de entrada todavía observada; no exige afirmar recepción no ocurrida ni rompe la explicación del saldo.

## Importación bancaria y matching

Preservar archivo/version/hash, banco/cuenta/moneda/período, parser y formato, fecha operación/valor, referencia exacta y texto original, signo, importe y saldo cuando exista. Parsear fuera de TX; preview muestra totales, fechas fuera de rango, saldos, duplicados y errores. BBVA es banco inicial, **formato real no verificado**: no inventar columnas ni prometer API bancaria. El núcleo neutral se construye con fixtures sintéticos; la WO del parser BBVA requiere contrato del formato y muestra autorizada privada/sanitizada, conforme a B06/C05. Esa muestra no condiciona todo el módulo M06.

Identidad fuerte de línea del banco si existe, única por cuenta. Si no existe, fingerprint de fecha/importe/texto solo detecta candidatos: dos pagos iguales pueden ser reales. Mantener ocurrencia/posición en archivo, solapamiento de extractos y resolución humana de duplicados. Importar otro archivo con distinto hash no crea derecho a duplicar líneas ya identificadas; tampoco elimina una línea legítima por coincidencia débil.

Matching propone secuencialmente: identificadores deterministas, heurísticas acotadas, IA opcional, decisión humana. Cuenta/entidad/moneda/dirección y saldos son restricciones duras, no features compensables por un score. Ventana de fechas y nombres abreviados ordenan candidatos; no confirman. “82%” solo si probabilidad calibrada con evaluación comparable; de otro modo mostrar puntuación orientativa sin porcentaje probabilístico.

Grupo N:M registra asignaciones explícitas entre piernas monetarias y líneas externas con importe en moneda de cuenta. La suma firmada de componentes internos debe igualar la externa; cada componente conserva dirección, no se concilian importes absolutos ignorando cargo/abono. Remanentes ≥0 y consumo total ≤importe de cada línea/movimiento. Un neto bancario97 frente a cobro100 requiere pago de comisión3 confirmado por Treasury, no tolerancia que borre3. Diferencia0.03 sigue excepción hasta evidencia/decisión; no auto-asiento de redondeo.

## Comandos Treasury

| ID / capacidad / clase | Inputs/reads y locks | Writes / guardas / corrección |
|---|---|---|
| T01 importar extracto / treasury.import_statement / D | Archivo/cuenta/parser I→B→F→L→D | Preview y aceptación separadas; lote confirmado conserva líneas y resolución de identidad. Repetición mismo archivo/contrato devuelve lote. Parse parcial no confirma filas silenciosamente |
| T02 confirmar pago / treasury.confirm_payment / D | Evidencia, cuenta, destinatario real, payability/preparación y obligación I→M→O si compra/financiación→T→F→R→D | Pago confirmado y aplicación autorizada solo si se pidió expresamente; guardas de AP/anticipo y bancarización. Pago real sin proceso se registra como excepción, no se rechaza su existencia. Reversal requiere hecho correctivo, no edición del original |
| T03 transferencia / treasury.confirm_transfer / D | Cuentas/monedas y ambas evidencias I→F todas→R→D | Piernas/estado de tránsito; resultado atómico para las piernas conocidas. Completar llegada con nueva intención bajo mismo grupo; no segunda salida. Comisión independiente |
| T04 proponer conciliación / treasury.reconcile / D | Líneas y movimientos elegibles, versiones, reglas/modelo I→F→L→R | Grupo candidato con asignaciones/evidencia/contraevidencia; no cambia dinero/aplicaciones. Candidato obsoleto no se confirma |
| T05 confirmar conciliación / treasury.reconcile / D | Set completo grupo/líneas/movimientos, remanentes y revisión I→F→L→R | Consumo de remanentes y estado del grupo atómicos; igualdad exacta por moneda/cuenta, sin doble uso. Otros candidatos quedan obsoletos. No llama comandos de dinero implícitamente |
| T06 desconciliar / treasury.unreconcile / D | Grupo original, corte y permisos I→O si libro→Q si corte→F→L→R | Reversión del vínculo y liberación de remanentes, motivo; no revierte cobro, pago, aplicación ni GL. Corte cerrado requiere reapertura controlada o excepción del siguiente corte, no borrado |
| T07 cerrar corte de cuenta / treasury.close_statement / D | Saldo inicial/final, líneas y movimientos, pendientes I→O de corte→Q→F→L→R | Snapshot reconciliado o con excepciones explicitadas y aprobadas; ningún faltante oculto por neteo. Reabrir crea revisión y conserva informe anterior |
| T08 proponer/confirmar comisión / treasury.propose_payment y treasury.confirm_payment / D | Cargo bancario/evidencia, beneficiario, clasificación candidata I→F→L→R→D | Propuesta no dinero; confirmación humana T02. Clasificación contable/fiscal posterior; no se ejecuta por IA o por regla de match |

Para correcciones de movimientos ya conciliados se descubre el set L/R completo, se revierte la conciliación afectada en el coordinador autorizado antes de compensar dinero, conservando ambos hechos. Si afecta aplicaciones Sales, se añaden todas S/T antes de F/L/R y se revalida HP1. Nunca se descubre una S después de tomar R.

## Corporate y financiación

Registro societario: entidad y forma, estatuto/versiones, acciones y matrícula, accionistas/participaciones por fecha, actos/acuerdos/actas, poderes/alcance/vigencia, contratos, relaciones y beneficiarios finales con evidencia. El ERP conserva expediente; no sustituye libro societario formal, escritura, inscripción o validación profesional. S.A.C. sin directorio no significa sin límites de representación.

Instrumento financiero: propuesta→validado legal/tributario/contable→autorizado→vigente→terminado; documentación incompleta y disputa son dimensiones propias. Línea rotativa, gratuidad, intereses, moneda, plazo, restitución, garantías, vinculación y residencia son hechos/decisiones por validar; no defaults. Acuerdo privado gratuito puede coexistir con consecuencia fiscal a valor de mercado. Dinero del socio se identifica como financiación pendiente de clasificación cuando falte contrato, no ingreso ni capital automático.

| ID / capacidad / clase | Reads / locks | Writes / corrección y fallo |
|---|---|---|
| CO01 registrar acto/poder/relación / corporate.record / D | Entidad/partes, documento, fechas y alcance I→M→O→D | Versión y estado de verificación; relación contable NIC24 y fiscal RLIR24 se clasifican separadamente. Corrección no elimina vigencia histórica ni atribuye facultades por nombre de cargo |
| CO02 validar/autorización de financiación / corporate.approve_financing / D | Expediente completo, aprobaciones profesionales nominales y poder I→M→O→D | Condiciones autorizadas/versionadas y límites; roles de revisor real con fecha/evidencia. Falta un dictamen requerido→PENDING, no “aprobado por Astra” |
| CO03 preparar desembolso, devolución de principal o reembolso de adelanto / treasury.prepare_financing / D | Naturaleza explícita, instrumento/derecho reconocido vigente, remanente por disposición o pago por cuenta, moneda, acreedor y cuenta pertinente I→M→O→T→F→R→D | Objetivo/plan; no confirma dinero. Cada disposición tiene identidad/evidencia. Devolución amortiza principal identificado; reembolso reduce derecho de restitución por pago adelantado. No asignar uno al otro ni reponer línea por todo egreso al socio. [Delta aceptado](../flows/financing-events-statements.md) |
| CO04 registrar capitalización / corporate.record_capitalization / D | Acuerdo, formalidades aplicables, deuda confirmada y aprobación I→M→O→T→R→D | Hecho societario y extinción de obligación por mecanismo acreditado; no movimiento ficticio de caja. Accounting determina fecha/clasificación; cancelación posterior necesita acto/corrección, no editar capital |
| CO05 preparar beneficiario final / corporate.prepare_beneficial_owner / D | Cadena propiedad/control y fechas, perfil de obligación I→M→O→D | Expediente/versiones y propuesta de declaración; envío fuera del ERP inicialmente. Constancia preservada por acto separado; no inferir persona final del representante |

Investigación y validación de mutuo son gate de activación temprano antes de contratar/financiar, incluso si ocurre durante M03/M04; no esperar UI M06. No bloquean diseñar Treasury/Corporate ni construir M01–M05 sin activar financiación. RTF 08044-1-2022 se usa con sus hechos/límites y no como aprobación de tasa0. No aplicar automáticamente artículos26 y32-A simultáneamente. Capitalización, dividendos, fondos para futuro aporte y préstamo mantienen evidencia y evaluación propias; [C06/DH2](../../roadmap/decisions-gaps.md#dh2) conserva la pregunta profesional.

## Aceptación, UX y handoff

El [contrato aceptado de hechos y estados de financiación](../flows/financing-events-statements.md) amplía M06: pago por tercero y extinción sin caja propia, reembolso separado de principal, manifest de estado mensual, adendas/correcciones/firma y consumo único Accounting. Es delta semántico aceptado según [review](../../review.md), sin acreditar implementación de este hito. Requiere M05 para reconocer la obligación Procurement afectada; evidencia ocurrida puede capturarse antes como pendiente. El estado mensual no sustituye los hechos ni el corte bancario T07.

Vista dividida banco/Treasury con selección N:M, saldo de cada fila, diferencias y contraevidencia; nombre del pagador distinto abre investigación, no merge ni rechazo automático. Confirmación muestra montos/destino/período y queda fuera de atajo directo. Lecturas cash position, money-unidentified, unapplied, tránsito, pendientes bancarios y bank↔Treasury↔GL tienen cortes y drill-through.

Casos: dos cobros60/40 contra línea100; dos líneas50/50 contra cobro100; neto97/cobro100/comisión3; mismo nombre/importe dos días, referencias incompatibles; pareja paga por cliente con evidencia; dos usuarios consumen última línea; import solapado con pagos idénticos legítimos; desconciliar no cambia dinero; cobro revocado afecta cobertura/dispatch; cuenta ajena rechazada; ingreso de socio no ventas; capitalización sin caja; gratuidad sin dictamen bloquea autorización; cierre con cargo desconocido visible; IA maliciosa no dispone de puerto de escritura.

DOMAIN conservación/asignaciones; PostgreSQL/CONCURRENCY para consumo único y correcciones; CONTRACT parser; golden financiación con Accounting/Tax; E2E de conciliación y RECOVERY de replay. Astra checkpoint de financiación/conciliación; Sol orquesta; implementador/reviewer distintos. Prohibido inventar formato BBVA, facultades, neutralidad fiscal o tolerancias que creen dinero. [DH2](../../roadmap/decisions-gaps.md#dh2)/[DH3](../../roadmap/decisions-gaps.md#dh3) y profesionales cierran hechos antes de uso; M06 opcional IA no bloquea la alternativa manual.

## Incremento profesional M06 propuesto

**Amendment aceptado por revisión independiente**, conforme a review. [Cuentas/instrumentos/caja/renta](../flows/financial-accounts-instruments.md) y [crédito/COD](../flows/professional-sales.md) completan consumidores conocidos. Mapping lo posee Accounting, exposición Sales; coordinación hereda H27 antes de T/R. Firma/custodia usa [Documents](../flows/records-signatures-site-packs.md); no confirma movimiento por documento.
