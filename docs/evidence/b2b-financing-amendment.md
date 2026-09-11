# Amendment semántico B2B y financiación — expediente del autor

Corte: 2026-09-11. Encargo del propietario: B2B general, financiación de partes relacionadas y reconocimiento de WhatsApp futuro; documentación, commits, push y PR abierto, sin merge, código ni WOs. **READY FOR INDEPENDENT REVIEW — evaluación documental del autor.** Esta evaluación del autor no acepta el amendment ni valida operaciones reales.

## A. Baseline y autorización

Antes de editar contratos se ejecutó fetch y se verificaron main y origin/main en `be5a1c6c3dc4102155c255785ee74964afbcfc78`, tree `64ce46f29d4c0109e5e81d03ebbbc293ea76fec1`; árbol de trabajo limpio y única rama local main. Rama de trabajo creada: `docs/b2b-financing-amendment`. Freeze, information architecture y sistema de agentes aceptados permanecen baseline. IMPLEMENTATION: NOT AUTHORIZED.

## B–D. Matriz de impacto previa a edición de contratos

Preparada desde las fuentes del baseline antes del delta. Todas las filas: CODE NOW = **NO**. WO impact describe alcance futuro a regenerar después de aceptación/autorización; no son WOs ni permiso de ejecución. Gate IDs se resuelven en [gaps](../roadmap/decisions-gaps.md).

| Requirement | Current coverage | Gap real | Owner | Affected milestone | Affected contract | Semantic change? | New gate? | WO impact |
|---|---|---|---|---|---|---|---|---|
| B2B core | Party ORGANIZATION, pedidos, obligaciones y snapshots | Entrada comercial independiente de Jumpseller y decisión B2B | Sales | Incremento B2B posterior a M04 | Product, Sales/SP2, roadmap | Sí: producto y entrada | No; B02–04/C13 existentes | Futuro incremento Sales |
| Customer PO | Documents genérico y referencia externa | Identidad por emisor, líneas, revisión, discrepancias y aceptación separada | Sales/Documents | B2B | Modelo y flujo Sales | Sí | No; B10 | Captura/vínculo/revisión comercial |
| Quotes | Propuesta de pedido externo | Cotización propia opcional con vigencia y revisiones | Sales | B2B | Sales | Sí | No | Cotización acotada, sin CRM |
| Payment terms | HP1 contado, cobros parciales sin despacho | Separar tipo de cliente y condiciones; crédito futuro bloqueado | Sales/Treasury | B2B; expansión posterior | Product/SP2/gaps | Sí; prepago inicial conserva HP1 | Reutilizar D03 para crédito/contraentrega | Política versionada; sin motor AR general |
| Partial fulfillment | Reservas y entregas parciales SP2 | Conectar cantidades a revisión OC/aceptación | Sales/Inventory | B2B | Sales/SP2 | Extensión trazable | No; B03–05 | Reusar entrega/retorno |
| B2B dossier | Document Flow y varios CPE | Cadena comercial opcional navegable | Sales/UI | B2B/M06 conciliación | UI/CPE | Sí | No; B09 | Lecturas compuestas |
| External document sending | Guardas mencionan envío externo conocido | Falta captura, niveles de evidencia y resolución concurrente | Documents | M04 | CPE/Documents/integraciones | Sí | No; B10/B12/C11 | Registro de hecho externo, sin dispatch |
| Mutuo agreement | Contrato/límite/gratuidad con C06 | Condiciones por disposición y adenda aplicables al estado mensual | Corporate | M06 | Corporate/M06 | Precisión material | No; C06 | Instrumento versionado |
| Loan disbursement | Cada drawdown y Treasury | Relación única a hecho de dinero y principal | Corporate/Treasury | M06 | M06/hechos | Sí | No; B03/B06/C05/C06 | Asignación sin duplicar dinero |
| Personal payment on behalf | Prohibida cuenta TILMUX ficticia | Hecho con pagador real, aplicación a obligación y derecho a reembolso | Corporate/Procurement/Treasury | M06; M05 para obligación proveedor | M06/Treasury/hechos | Sí | No; C04–06/C08 | Liquidación por tercero sin caja propia |
| Reimbursement | CO03 usa término también para principal | Separar reembolso de pago adelantado | Corporate/Treasury | M06 | CO03/M06 | Sí: desambiguación económica | No | Remanente por adelanto reconocido |
| Principal repayment | Devolución contractual | Asignación a principal separado de otras obligaciones | Corporate/Treasury | M06 | CO03/M06 | Sí | No | Amortización por disposición |
| Monthly financing statement | Snapshots genéricos y cortes | Manifiesto reproducible, sub-saldos y firmas/versiones | Corporate/Documents | M06; M07–08 consumidores | M06/Accounting | Sí | No; B06–08/C06 | Estado derivado, nunca fuente monetaria |
| Legal-document repository | Corporate hechos + Documents bytes | Explicitar constitución/escritura/partida, vigencia y alcance probatorio | Corporate/Documents | M06 | Corporate | Precisión; sin vault nuevo | No; C06/C09/C10 | Reusar registros y versiones |
| WhatsApp future trigger | D03 nuevos canales | Nombrarlo y preservar conceptos neutrales mínimos | Integrations/Documents/Sales | M10 por trigger | Integraciones/roadmap | Sí: opción futura identificada | No; extender D03 | Ninguna WO ahora |

## Decisiones preliminares que guían el delta

M04 conserva la primera venta B2C. Se propone un incremento B2B acotado después de M04, sin esperar compras M05 para vender existencias; conciliación usa Treasury de M06. M06 concentra financiación y depende de Procurement M05 para el reconocimiento completo de obligaciones de proveedor pagadas por el socio. El registro de evidencia ocurrida nunca espera una futura UI.

Contradicción concreta a corregir: CO03 llama «reembolso» a una reducción de principal/interés. El nuevo contrato separará reembolso del pago por cuenta de la empresa y devolución de principal. No hay nueva interpretación contable automática.

La matriz es evidencia de análisis de impacto. Las reglas finales vivirán en las fuentes de sus dueños, no en este informe.

## E–U. Resultado y rutas para revisión

| Apartado del encargo | Resultado propuesto / fuente propietaria |
|---|---|
| E. B2B model | [Incremento Sales](../specs/flows/b2b-commercial-dossier.md): mismo pedido, Treasury/Inventory existentes, entrada comercial local sin conexión ficticia |
| F. Customer PO | Original Documents, interpretación Sales; identidad emisor/referencia/revisión, líneas y asignaciones N:M con remanentes, aceptación distinta de recepción |
| G. B2B dossier | Cliente/cotización/OC/revisión aceptada/condiciones/reservas/parciales/CPE/entrega documental/cobros/aplicaciones/conciliación/evidencia; nodos opcionales y estado por dueño |
| H. Payment terms | B2B prepago íntegro inicial, parcial no habilita despacho; crédito/contraentrega solicitados permanecen bloqueados D03 sin política/spec |
| I. Legal/tax mutuo | [Research](../research/normative/b2b-financing-evidence.md): civil, representación,26/32/32-A, medios de pago, terceros, reportes, NPIF, RER/BF; C06 no se cierra |
| J. RTF/official matrix | N030–N043: autoridad/edición/hechos/regla/inferencia/límites/owner/gates; RTF08044 reutiliza lectura previa con límites; RTF00890-2025 localizada sin texto íntegro fiable, excluida de nuevas conclusiones |
| K. Liquidation finding | No obligación mensual general identificada en corpus revisado; estado de movimientos y saldos propuesto como control interno. Firma/conformidad no prueba por sí sola dinero ni cumplimiento |
| L. Financing event model | [M06 hechos](../specs/flows/financing-events-statements.md): disposición, pago por cuenta, reembolso, amortización y corrección; estado no reemplaza eventos |
| M. Monthly consolidation | Período/corte/moneda/manifest, sub-saldos y versiones; fixture principal1.700+adelantos150=1.850; caja del mes+500, pago personal fuera |
| N. On-behalf payments | Pagador/beneficiario reales, obligación y evidencia; liquidación Treasury por tercero separada de caja propia; derecho al socio reconocido por Corporate |
| O. Reimbursement vs repayment | Cada salida se asigna por naturaleza y remanente. No reponer línea por reembolso ajeno ni duplicar gasto; exceso ocurrido conserva excepción |
| P. Corporate/Documents | [Corporate](../corporate/architecture.md) posee actos/acuerdos/facultades/vigencia; Documents archivos, originales/copias/versiones y snapshot. Sin vault nuevo |
| Q. Resend optionality | [C40](../specs/flows/cpe-document-delivery.md#c40) conserva envío externo sin callback/attempt; se comparte protección de primera finalidad. Resend es adaptador opcional |
| R. WhatsApp future | [Integraciones](../architecture/integrations.md): D03/M10, research al activar, propósito/Party/caso/evidencia mínimos; sin SDK/módulo/CRM |
| S. Scalability | Núcleo por dueño, IDs/contratos y políticas versionadas, adapters sustituibles; no GenericWorkflow/TaxDSL/ChannelEngine/ERPPluginSystem. Monedas/entidades/marcos conservan separación; expansión exige trigger propio |
| T. Roadmap | [Programa](../roadmap/program.md): incremento B2B después M04, independiente de M05 para vender stock; conciliación tramo M06. Financiación M06, obligación proveedor M05, consumidores M07–08; sin renumerar |
| U. Gates | [Registro](../roadmap/decisions-gaps.md): mismos A0/B16/C13/D6; amplía B06/B07/B08/B12, C06 y D03. No nuevo gate por formulario/pregunta ni dictamen universal para operación comercial B2B |

<a id="v-37-casos-adversariales"></a>
## V. 37 casos adversariales

Método: refutación **documental del autor**, leyendo precondición, dueño, efecto y corrección contra la spec enlazada. «PASS estático» significa que existe un desenlace explícito sin violar el contrato; no significa prueba de runtime, aprobación profesional ni revisión independiente. Ningún B/C/D se cierra por esta tabla.

| Caso | Contraejemplo / consecuencia comprobada documentalmente | Fuente / resultado |
|---|---|---|
| 01 | Empresa manda OC sin stock: recepción permanece; aceptación/reserva íntegra falla, no inventa compromiso ejecutable ni stock | B2B §Compromiso / PASS estático |
| 02 | OC100, TILMUX80: conserva100 observado,80 acordado,20 no aceptado; sin conformidad suficiente no afirmar acuerdo | B2B §Compromiso / PASS estático |
| 03 | Nueva OC tras aceptación: revisión separada y discrepancia; no sustituye venta/reserva/objetivo aceptados | B2B §Parcialidades / PASS estático |
| 04 | OC n.º7 de dos clientes: identidades por entidad/emisor, sin colisión global ni fusión heurística | B2B §F / PASS estático |
| 05 | OC con entregas parciales: cantidades contra línea/revisión aceptada, reserva y remanente; prepago total sigue exigible | B2B §Parcialidades/H / PASS estático |
| 06 | Varias entregas y CPE: múltiples identidades legítimas, asignación/anticipos sin duplicar cobertura; no un CPE obligatorio por parcial | B2B + CPE/C33 / PASS estático |
| 07 | Pago antes de OC: Treasury conserva anticipo/no aplicado; aplicación posterior explícita, oportunidad fiscal no espera documento | B2B §H / PASS estático |
| 08 | Empresa paga parcialmente: hecho y saldo visibles, sin despacho proporcional ni conversión a crédito | B2B §H / PASS estático |
| 09 | Venta B2B prepago: aceptación/reserva y dinero íntegro aplicado habilitan evaluación de despacho con demás guardas | B2B §H / PASS estático |
| 10 | Crédito no autorizado: capturable como condición solicitada, aceptación/despacho bajo esa modalidad bloqueados D03 | B2B §H + gaps / PASS estático |
| 11 | PO reference distinta en CPE: MISMATCH/revisión; no corregir original ni vincular por igual importe | B2B §Parcialidades + C33 / PASS estático |
| 12 | Archivo OC malicioso/falso: cuarentena/análisis, parsing sin autoridad; hash no acredita autenticidad, revisión comercial requerida | B2B §F + C31/C32/B10 / PASS estático |
| 13 | OC recibida: evidencia comercial, no aceptación ni pago/stock/entrega/CPE confirmado | B2B §F/Compromiso / PASS estático |
| 14 | Cancelación tras despacho parcial: cancelar solo remanente; preservar entrega y resolver objetivo/aplicaciones; sin borrar historia | B2B §Parcialidades / PASS estático |
| 15 | Devolución posterior: referencia salida original, stock no vendible inicial, nota/refund separados | B2B + SP2/C21/C22 / PASS estático |
| 16 | Dos desembolsos mensuales: D1/D2 conservan identidad/fuente, suman600+400, no se confunden por período | Financiación §L/M / PASS estático |
| 17 | Socio paga proveedor350: evidencia externa y obligación cubierta; caja TILMUX no tiene entrada/salida350 | Financiación §N / PASS estático |
| 18 | Empresa reembolsa200 de ese pago: salida real distinta y derecho restante150; no segundo gasto | Financiación §O/M / PASS estático |
| 19 | Devuelve300 de principal: reduce disposición/principal a1.700 en fixture; no derecho de reembolso | Financiación §O/M / PASS estático |
| 20 | Igual importe, distinta naturaleza: referencias y asignaciones determinan deuda reducida; identidad del socio no decide clasificación | Financiación §L/O / PASS estático |
| 21 | Estado omite movimiento: anti-join/manifest y conciliación de membresía bloquean aprobación aunque omita+100/−100 y saldo cuadre | Financiación §M / PASS estático |
| 22 | Corrección tras estado: nuevo hecho y versión/corte, snapshot firmado anterior intacto | Financiación §M/Acciones / PASS estático |
| 23 | Dos estados mismo período: misma intención/corte recupera versión; corrección nueva con linaje y una vigente por alcance | Financiación §M / PASS estático |
| 24 | Adenda reduce límite: vigencia y condiciones explícitas, muestra exceso si saldo superior; no reduce deuda histórica | Financiación §O / PASS estático |
| 25 | Banco no respalda supuesto desembolso: conservar observación/disputa, no dinero confirmado por contrato o firma mensual | Financiación §L/O / PASS estático |
| 26 | Pago personal sin CPE/evidencia: preservar hecho candidato y pendientes; no crédito fiscal/gasto/financiación aprobados por etiqueta | Financiación §N + researchN033/N038 / PASS estático |
| 27 | Reembolso mayor a adelanto: bloquear autorización/aplicación excedente; si ocurrió, salida y exceso sin aplicar/en investigación | Financiación §O / PASS estático |
| 28 | Saldo mensual no concilia hechos: provisional/observado, no plug, neteo ni edición manual de saldo | Financiación §M / PASS estático |
| 29 | Firma posterior: fecha de firma y hecho distintas; conformidad del snapshot no cambia fechas bancarias | Financiación §M + researchK / PASS estático |
| 30 | Mutuo no validado intenta activarse: C06 bloquea modalidad/efecto nuevo; hecho ocurrido sigue registrable como pendiente | M06/CO02 + C06 / PASS estático |
| 31 | CPE enviado desde correo corporativo externo: C40 registra propósito/documento/destinatario/actor/fuente y datos acreditados | CPE §Entrega externa/C40 / PASS estático |
| 32 | Sin callback CasPro: «envío externo registrado», no delivered técnico ni recepción probada | CPE §Entrega externa / PASS estático |
| 33 | Resend deshabilitado: archivo/consulta/preparación/C40 disponibles; nuevo dispatch bloqueado según política | CPE §Entrega externa / PASS estático |
| 34 | Otro proveedor de email: se conserva historia/identidad/HOLD; nueva configuración/capacidad y aprobación pertinentes | Integraciones §Entrega documental / PASS estático |
| 35 | Automatismo intenta reenviar externo: misma finalidad/historia bloquea original; C37 exige reenvío explícito. C40 contra C07 deja carrera visible si ya autorizado | CPE/C40 + CM0 / PASS estático |
| 36 | Intentan crear módulo WhatsApp ahora: fuera de alcance, D03/M10; ningún paquete o SDK materializado | Integraciones §Frontera futura / PASS estático |
| 37 | WhatsApp cambia API/política antes de activación: research nuevo obligatorio; no heredar capacidad/permiso de esta mención | Integraciones + D03 / PASS estático |

Contraejemplos adicionales revisados: doble aceptación concurrente contra una línea OC; revisión sin identidad de línea confiable; pago personal asignado dos veces a proveedor; revertir su reconocimiento después de reembolsarlo; estado con commit tardío; captura externa sin versión/hash. Sus salidas son revisión/rollback o pendiente explícito, nunca saldo inventado. La ejecución de concurrencia real queda B03/B06/B12.

## W. Mapa semántico OLD → NEW

| OLD baseline | NEW propuesto | Dueño / consumidores y evidencia afectada |
|---|---|---|
| Primera venta B2C, B2B como expansión genérica | B2B de bienes con entrada local, cotización/OC/revisión aceptada y expediente | Product/Sales; Parties/Catalog sin rediseño, Inventory/Treasury/CPE/UI; la evidencia de entrada Jumpseller no acredita aceptación B2B |
| Archivos/referencias de pedido genéricos | OC cliente con identidad, interpretación, diferencias y asignaciones N:M controladas | Sales/Documents; requiere B02/B03/B10 propios, no reaprovechar un PASS de upload como prueba comercial |
| Objetivo AP liquidado por aplicaciones de dinero propio | Extinción acreditada por pago de tercero como componente separado, con fuente y remanente | Treasury/Procurement/Corporate; **cambia contrato de liquidación/invariante**, requiere B06 y consumidores B07/B08 |
| CO03 usa reembolso también para principal | Reembolso de adelanto y amortización identificados por separado | Corporate/Treasury/Accounting/Tax; no equivalencia automática de evidencia CO03 previa |
| Snapshots/cortes genéricos | Estado de movimientos de relación derivado, sub-saldos/manifest/versiones y alcance de firma | Corporate/Documents/Accounting; B06–08, C06 profesional |
| Guardas mencionan historia externa sin captura propia | C40 conserva envío externo, proveedor opcional, deduplicación/race con dispatch | Documents/Integrations/UI; B10/B12, no callbacks simulados |
| Nuevos canales genéricos D03 | WhatsApp identificado como diferido con research futuro | Product/Integrations; sin código/API/SDK ni nuevo gate |

No equivale a cleanup editorial. Se preservan arquitectura de información, ownership base, monolito/PostgreSQL, M01/M02, SP2 prepago, emisión CPE externa, políticas NPIF y estados históricos aceptados. Ningún PASS del freeze acredita los nuevos contratos. Revisión independiente debe evaluar candidato exacto y estos deltas conforme a [calidad](../quality/strategy.md).

## X–Z. Archivos, commits y PR

Los archivos cambiados se obtienen del diff de la rama contra el baseline indicado; todos pertenecen a `docs/`. Las tres nuevas fuentes estables son Sales B2B, hechos/estados M06 y research normativo; este expediente reúne la evaluación del autor. Los contratos existentes, navegación, capability map, gates y estado se sincronizan por impacto real. Sin mover carpetas, modificar agentes/skills, leer Wbpro/legacy ni crear WOs.

Archivos del delta (32):

- [docs/accounting/architecture.md](../accounting/architecture.md)
- [docs/architecture/boundaries.md](../architecture/boundaries.md)
- [docs/architecture/integrations.md](../architecture/integrations.md)
- [docs/architecture/ui.md](../architecture/ui.md)
- [docs/corporate/architecture.md](../corporate/architecture.md)
- [docs/domain/invariants.md](../domain/invariants.md)
- [docs/domain/model.md](../domain/model.md)
- [docs/domain/procure-to-pay.md](../domain/procure-to-pay.md)
- [docs/domain/treasury-finance.md](../domain/treasury-finance.md)
- [docs/evidence/b2b-financing-amendment.md](../evidence/b2b-financing-amendment.md)
- [docs/evidence/index.md](../evidence/index.md)
- [docs/index.md](../index.md)
- [docs/product/charter.md](../product/charter.md)
- [docs/research/index.md](../research/index.md)
- [docs/research/normative/b2b-financing-evidence.md](../research/normative/b2b-financing-evidence.md)
- [docs/research/normative/mutuo-tax-corporate.md](../research/normative/mutuo-tax-corporate.md)
- [docs/research/normative/normative-register.md](../research/normative/normative-register.md)
- [docs/review.md](../review.md)
- [docs/roadmap/capabilities.md](../roadmap/capabilities.md)
- [docs/roadmap/decisions-gaps.md](../roadmap/decisions-gaps.md)
- [docs/roadmap/program.md](../roadmap/program.md)
- [docs/specs/cross-cutting/command-matrix.md](../specs/cross-cutting/command-matrix.md)
- [docs/specs/cross-cutting/economic-facts.md](../specs/cross-cutting/economic-facts.md)
- [docs/specs/flows/b2b-commercial-dossier.md](../specs/flows/b2b-commercial-dossier.md)
- [docs/specs/flows/cpe-document-delivery.md](../specs/flows/cpe-document-delivery.md)
- [docs/specs/flows/financing-events-statements.md](../specs/flows/financing-events-statements.md)
- [docs/specs/flows/first-operational-circuit.md](../specs/flows/first-operational-circuit.md)
- [docs/specs/flows/sales-stock-treasury.md](../specs/flows/sales-stock-treasury.md)
- [docs/specs/index.md](../specs/index.md)
- [docs/specs/milestones/procurement-deep.md](../specs/milestones/procurement-deep.md)
- [docs/specs/milestones/treasury-corporate-deep.md](../specs/milestones/treasury-corporate-deep.md)
- [docs/tax/architecture.md](../tax/architecture.md)

Checkpoints: `633bb3b` research; `253c26d` B2B/financiación y contratos; `613b976` entrega opcional/externa. El commit de cierre documental y su head/tree exactos se identifican en el PR para evitar autorreferencia circular en este archivo.

PR contra main: publicación pendiente del cierre; permanecerá abierto, aceptación independiente pendiente, sin merge ni efectos empresariales externos.

## Evidencia final del autor

Comprobaciones del autor: links/anchors locales y bloques Markdown sin errores; diff sin whitespace indebido; IDs01–37 completos y únicos; gates A0/B16/C13/D6; aritmética del fixture principal1.700, adelantos150, total1.850 y caja+500. Alcance: solo32 archivos Markdown de docs, sin cambios a M01/M02, agentes, skills, código, migraciones o WOs. Verificación de publicación/head/tree se completa en el PR. No se ejecutaron tests CasPro, conexión SUNAT/banco/email ni validación profesional. El trabajo de búsqueda normativa tiene los límites explícitos del memo, incluida jurisprudencia posterior no leída íntegramente.


**PASS — SCOPED SEMANTIC AMENDMENT READY FOR INDEPENDENT REVIEW.** Evaluación estática del autor, no aceptación del amendment. Pendientes: reviewer independiente del candidato; validación profesional de actos/políticas reales bajo sus gates; futuras pruebas de implementación solo con autorización. IMPLEMENTATION: NOT AUTHORIZED.
