# M06 — hechos de financiación y estados periódicos

Owner: Corporate para relación/instrumento/naturaleza; Treasury para dinero propio y liquidación; Procurement para obligación de proveedor; Accounting/Tax para interpretación; Documents para artefactos. **Delta semántico aceptado por revisión independiente según [review](../../review.md).** Complementa [M06](../milestones/treasury-corporate-deep.md), [hechos/locks](../cross-cutting/economic-facts.md) y [research](../../research/normative/b2b-financing-evidence.md). No valida el contrato gratuito rotativo ni crea código/WOs.

## L. Relación, instrumento y eventos individuales

Relación financiera identifica entidad, acreedor Party, naturaleza, moneda y acuerdos aplicables; una relación puede tener varios instrumentos y otras obligaciones con ese socio. Contrato marco versionado conserva partes/facultades, firma, vigencia, disponibilidad comprometida o discrecional, límite/moneda, plazo por disposición, interés/gratuidad/mora, condiciones de reposición, garantías, reembolso y terminación. No se presuponen esos términos por el título «línea rotativa». Contrato/adenda firmado en Documents es evidencia del acuerdo, nunca de que ingresó el límite entero a la caja.

| Hecho individual | Fuente/owner del hecho y efecto | Prohibición |
|---|---|---|
| Desembolso dinerario recibido | Treasury confirma entrada en cuenta propia y pagador real; Corporate vincula importe a disposición/instrumento validado o deja clasificación pendiente | No crear otra entrada al registrar el vínculo ni usar límite aprobado como saldo |
| Pago personal por cuenta de empresa | Corporate conserva evidencia del pago del socio y fundamento del derecho a restitución; Procurement confirma obligación cubierta; Treasury registra liquidación por tercero según sección N | No entrada/salida ficticia de cuenta TILMUX |
| Reembolso de adelanto reconocido | Treasury confirma salida propia al acreedor real; aplicación explícita al derecho de reembolso originado en pago(s) por cuenta de empresa | No reducir principal del mutuo por defecto ni recrear gasto de proveedor |
| Devolución/amortización de principal | Treasury confirma salida propia; Corporate identifica disposición y reducción de principal por aplicación | No llamarla distribución, interés o reembolso de gasto por similitud de importe |
| Interés/costo contractual | Corporate acredita obligación/condiciones; Treasury acredita pago si ocurre; Accounting/Tax evalúan por separado | Gratuidad o ajuste fiscal no crean automáticamente interés civil a pagar |
| Corrección/reversión/reclasificación | Dueño del hecho conserva original, motivo, fuente, fecha efectiva/conocimiento y relación correctiva; se coordinan remanentes/objetivos afectados | No dinero nuevo por corregir una etiqueta; no reescribir un evento o snapshot firmado |
| Capitalización/condonación/compensación | Acto jurídico propio y aprobado, crédito afectado y requisitos; Accounting/Tax interpretan | Fuera del total monetario; no extinguir deuda por sumar columnas o cambiar categoría |

Cada evento tiene ID estable, entidad, instrumento/revisión si conocido, Party pagador y beneficiario reales, importe/moneda, fechas de hecho/valor/registro, actor, procedencia, naturaleza candidata/revisada, obligación y porciones cubiertas, evidencia versionada, aprobación y estado de disputa/revisión. La ausencia de datos no se rellena; el hecho observado se preserva con incertidumbre. Identidad bancaria fuerte se contrasta con Treasury; importe+fecha no deduplican dos movimientos legítimos.

Un evento Corporate que referencia dinero Treasury no es otra contribución de efectivo ni otro pasivo por sí mismo. Correlación común y rol de cada componente permiten al consumidor Accounting reconocer la contribución económica una vez. El estado mensual no publica nuevamente desembolsos/gastos como hechos nuevos.

## N. Pago personal directo al proveedor

Ejemplo sintético: socio paga S/350 desde **su** cuenta a proveedor X por obligación de la empresa. Captura conserva pagador real, beneficiario real, cuenta/medio externo con titularidad sustentada, obligación Procurement o referencia empresarial pendiente, CPE/evidencia de adquisición, fechas, importe/moneda, finalidad, autorización previa o excepción, y evidencia del pago. La cuenta personal se referencia como fuente externa; no se da de alta como cuenta financiera disponible de TILMUX ni se importa su actividad ajena al caso.

Tres decisiones separadas: (1) evidencia de que ocurrió el pago; (2) cuánto de la obligación empresarial extinguió; (3) si existe deuda y de qué naturaleza con el socio. Si faltan CPE o conformidad, preservar evidencia y saldo candidato/disputa; no confirmar gasto deducible, crédito fiscal ni financiación válida. Un CPE a nombre personal exige análisis de adquisición/beneficiario, no se corrige el receptor editando metadata.

**Extensión explícita de liquidación Treasury:** la obligación Procurement mantiene su importe comercial. Treasury admite una asignación de extinción acreditada por pago de tercero, con ID de evidencia Corporate y remanente consumible propio, separada de aplicaciones de dinero de cuentas propias. Es una liquidación no monetaria para la caja de la entidad, no un cobro/pago interno ni un nuevo mecanismo de bancarización. Procurement certifica deuda/cobertura por contratos; Corporate certifica naturaleza/acuerdo; el coordinador confirma esas referencias y la asignación Treasury juntos. Nunca escribe tablas ajenas directamente.

Para un objetivo por pagar: `pendiente = obligación vigente − aplicaciones netas de pagos propios − liquidaciones netas acreditadas por tercero − otras extinciones expresamente autorizadas`. Componentes no negativos, suma ≤ obligación, misma entidad/moneda y evidencia; consumo de cada pago externo ≤ importe probado. Una línea cubierta no puede pagarse otra vez al proveedor. Derecho a reembolso al socio tiene otro objetivo, originado por Corporate, importe reconocido y vínculo a las porciones de obligación cubiertas. La mera captura no lo crea automáticamente. Se conserva cualquier diferencia entre pago probado, deuda cubierta y derecho reconocido.

Esta es una ampliación de las invariantes de liquidación, no redefinición de N/A/U de los cobros. Dinero propio Treasury sigue cumpliendo sus límites. Si falta la obligación M05, puede capturarse referencia pendiente; no declarar extinción/reembolso aprobados hasta resolverla. La falta de procedimiento no impide registrar dinero **ya ocurrido** como excepción; bloquea autorización futura o clasificación automática, no la existencia del hecho.

Si el contrato validado permite que ese pago constituya disposición de línea, una decisión Corporate explícita lo clasifica como principal, con evidencia y vigencia. Se reclasifica el derecho reconocido sin sumarlo simultáneamente como principal y adelanto reembolsable; no se simula abono en banco. Su tratamiento jurídico/tributario se resuelve en C06/C08, nunca por nombre.

## O. Asignaciones, reembolsos y límite

Una salida real al socio puede cubrir varias obligaciones con asignaciones por naturaleza. Total asignado no excede salida neta; cada componente no excede su saldo reconocido. Reembolso350 contra adelanto350 reduce ese derecho; devolución350 contra disposición1000 reduce principal a650. Mismo importe no implica mismo hecho. Reembolso solicitado mayor al remanente → bloquear autorización/aplicación excesiva; si salida ya ocurrió, registrarla y dejar exceso sin aplicación/en investigación, sin ocultar dinero ni inventar gasto.

Pagos sin evidencia suficiente permanecen observados; contrato o firma mensual no los promueven a dinero confirmado. Un asiento tampoco confirma banco. Revolvencia se calcula exclusivamente de disposiciones y reducciones elegibles bajo versión contractual: no reponer disponibilidad por reembolso de una deuda ajena a la línea, conciliación, firma, promesa ni reversión de vínculo.

Adenda con nuevo límite tiene fecha de firma, vigencia, aprobaciones y regla de transición. Límite reducido debajo del saldo existente muestra exceso y bloquea nuevas disposiciones según términos; no reduce deuda pasada. Si no hay regla para disposiciones anteriores, no se modifica su vencimiento/costo por inferencia. No se mezclan monedas ni instrumentos para aparentar disponibilidad.

## M. Estado mensual reproducible

Denominación de producto: **Estado de movimientos y saldos de financiación y pagos por cuenta de la empresa**. Puede llevar subtítulo «liquidación mensual» si las partes lo usan; no es liquidación de compra, CPE, extracto bancario ni sustituto de libro/contrato. Research delimita qué se encontró y qué falta validar jurídicamente.

Clave conceptual: entidad + relación + moneda + período económico + corte de conocimiento + versión. Sub-saldos por instrumento/disposición/naturaleza, sin compensarlos: principal, derechos de reembolso y otros componentes identificados. Total informativo solo de componentes compatibles reconocidos; pendientes/disputados separados, no escondidos ni sumados como aprobados. Saldo de financiación no es saldo de caja ni necesariamente valor contable por medición/FX.

| Septiembre 2026, fixture S/ | Principal | Adelantos reconocidos | Total informativo |
|---|---:|---:|---:|
| Saldo inicial sustentado | 1.000 | 0 | 1.000 |
| Desembolso D1 | 600 | 0 | 600 |
| Desembolso D2 | 400 | 0 | 400 |
| Socio paga proveedor P1 | 0 | 350 | 350 |
| Empresa reembolsa P1 | 0 | -200 | -200 |
| Empresa devuelve principal | -300 | 0 | -300 |
| Correcciones | 0 | 0 | 0 |
| Saldo final | **1.700** | **150** | **1.850** |

Flujos propios del mes: entradas1.000, salidas500, variación de caja+500; pago personal350 no forma parte de esas entradas/salidas. El saldo inicial1.000 exige hechos previos o apertura sustentada. Este cuadro es fixture aritmético, no asiento ni operación real. Si una política contabiliza un componente de otra forma, el puente explica diferencia; no edita el cuadro para cuadrar GL.

Reproducibilidad requiere:

1. Definir período económico, corte de conocimiento, zona/moneda, versión de reglas de inclusión/clasificación y contratos aplicables. Saldo inicial deriva de hechos previos netos; enlazar snapshot previo y explicar diferencias por conocimiento tardío.
2. Cerrar un manifiesto de **IDs, revisiones, relaciones correctivas, porciones y hashes fuente** de todos los productores pertinentes. Usar barrera/corte de [hechos](../cross-cutting/economic-facts.md), espera de transacciones en curso y reconciliación de completitud; timestamp/MAX-ID o saldo igual solos no prueban conjunto completo.
3. Conciliar cada inclusión, exclusión y pendiente con fuentes Corporate/Treasury/Procurement. Sumas brutas por naturaleza, sin neteo de dos hechos iguales/opuestos. Cada fila abre original, contraparte, concepto, fecha del hecho/registro, documento/banco, actor, clasificación y revisión.
4. Generar representación fuera de transacción larga desde dataset congelado; Documents conserva snapshot, manifest referenciado, versión/render y hash. Corporate posee definición, aprobación y puntero a versión vigente. Auditoría distingue elaboración, revisión, firma y fecha de cada acto.
5. Firmar/revisar fija **ese** contenido y alcance de conformidad; cambio de hechos/conocimiento produce nueva versión, comparación y relación «sustituye», nunca mutación del firmado. Fecha de firma posterior no cambia fechas de movimientos.

Dos emisiones idénticas del mismo corte/intención recuperan la misma versión; corrección legítima produce otra con motivo, corte y linaje. Solo una versión es vigente para el mismo alcance de estado, pero todas son consultables. Un nuevo período no reescribe el anterior. Movimiento omitido detectado, membresía incompleta, desbalance entre sub-saldos y hechos o evidencia bancaria en conflicto → informe provisional/observado, no aprobarlo como reconciliado. Igualdad numérica con omisión de +100 y −100 sigue fallando por membresía.

## Acciones, concurrencia y corrección

Hereda CM0; son contratos conceptuales del delta, no WOs ejecutables. Permisos por dueño, entidad, revisión y motivo en cada acción; C06 condiciona modalidad real, C04/C05/C08 la obligación/dinero/interpretación afectada.

| Acción del dueño | Reads / recursos y confirmación | Error / corrección / efecto externo |
|---|---|---|
| Registrar/vincular disposición Corporate | I→M→O instrumento→T→F/R dinero propio si existe→D; leer revisiones/evidencia y saldo de línea, proteger identidad del vínculo | Evidencia insuficiente conserva observación; repetición no duplica principal; nuevo hecho para corregir. Ninguna transferencia |
| Reconocer pago por cuenta y derecho | I→M→todas O de obligación Procurement/relación Corporate→T proveedor/socio→R si pagos propios afectados→D; raíz Corporate serializa consumo del pago externo | Atómico reconocimiento/asignaciones/hechos/audit; exceso, otra moneda/entidad o revisión vieja rechazan. No F ficticia ni pago bancario creado |
| Preparar reembolso o amortización | CO03 indica naturaleza y saldos; T02 confirma solo dinero ocurrido; I→M→O→T→F→R→D | Solicitud/plan no dinero. Exceso ocurrido queda excepción sin aplicar; corrección revierte asignaciones pertinentes sin duplicar salida |
| Corregir pago/reconocimiento | Descubrir todas O/T, dinero R y líneas L de conciliación propias si afectadas, en orden CM0; raíz original y remanentes bajo exclusión | Deshacer primero vínculos incompatibles; deuda proveedor puede reabrirse, derecho socio ajustarse. Reembolso ya ocurrido no desaparece: diferencia pendiente explícita. Historial firmado intacto |
| Congelar/aprobar estado Corporate | Corte/barrera productores; I→M→O relación→Q corte y resto de recursos completos según manifest; render fuera de TX; aprobación relee versión y manifest | Concurrencia/corte incompleto bloquea aprobación; corrección crea versión. Firma externa solo se registra con evidencia; no servicio de firma activado |

Los locks descritos extienden recursos existentes, sin nuevo orden universal. Consulta previa solo descubre; al variar set se aborta y redescubre. No se mantiene un lock mientras una persona revisa o firma. Hecho/auditoría/resultado idempotente se confirman juntos; falla de cualquiera revierte cambio, conservando observación previa ya registrada.

## Navegación, consumidores y gates

Ancla «Relación de financiación»: acuerdo/adendas, disposiciones, pagos por cuenta, reembolsos, principal devuelto, estados de período, evidencia/auditoría. Mostrar naturaleza y remanente antes de cualquier acción. Document Flow proyecta referencias; Documents guarda snapshot; Treasury sigue mostrando únicamente cuentas propias y extinciones por tipo; Accounting reconcilia componentes a GL, Tax interpreta C06/C08 y BF C09 si hechos lo activan.

Casos16–30 del [expediente](../../evidence/b2b-financing-amendment.md#v-37-casos-adversariales) son verificación documental. B03/B06 requieren después concurrencia de doble asignación, reversión tras reembolso y corte con commit tardío; B07/B08 prueban consumo único y exclusión de pago personal del EFE propio. C01/C06/C08 antes de tratamiento real; no nueva cuenta PCGE, tasa, contrato firmable ni aprobación profesional aquí.
