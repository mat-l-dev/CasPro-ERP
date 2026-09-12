# M09 — Tax Perú: fundamento, determinación y expediente

Estado: **SPECIFIED — candidato; perfil real y políticas PENDING PROFESSIONAL VALIDATION**. Owner Tax. Entradas: [investigación actual](../../research/normative/tax-current-review.md), [mutuo](../../research/normative/mutuo-tax-corporate.md), [registro normativo](../../research/normative/normative-register.md), [contrato profundo](../cross-cutting/economic-facts.md). M09 no posterga obligaciones legales activadas en M03–M06. Antes de UI tributaria, expediente/manual profesional y evidencia conservada son gate operativo.

## Perfil y regla versionados

La regla existente conserva componentes IGV/IPM cuando el consumidor fiscal/aduanero/layout los exige: entidad, propósito, naturaleza/fecha legal del hecho, período y revisión de fuente determinan la selección, nunca fecha de carga o de reporte. [Transición Ley32387 y tabla SUNAT](../../research/normative/igv-ipm-transition.md) fija el desglose general2026–2029 sin cambiar total18% ni G1. Persistir versión/componentes/total/linaje; hueco, solapamiento o cambio normativo no conciliado mantiene REVIEW_REQUIRED. Corrección histórica preserva norma del hecho y original. B04/B08/B14 deben validar fronteras y C08/C07 la aplicación real.

Entidad/período conserva RUC privado, inicio/activación, actividades, régimen y acogimiento, ingresos/adquisiciones/activos/personal pertinentes, condición de emisor electrónico/SEE, obligación de registros, padrones de agentes, residencia/vinculación y fuentes. NPIF y RER se evalúan por separado. Perfil DRAFT→VERIFIED→ACTIVE/SUPERSEDED; no hay valor “RER para siempre”. Cambio de régimen no reescribe períodos.

Una regla tributaria identifica norma/artículo, emisor, publicación, vigencia, modificaciones/derogación, hechos requeridos, alcance, base, tasa, redondeo, moneda/tipo de cambio, momento, sujeto obligado, excepciones, evidencia, responsable y golden. Aprobación tiene persona/fecha/versión. Regla no codificada o hecho faltante produce REVIEW_REQUIRED, no impuesto0. Las tasas del calendario se revalidan para 2027 antes de activar; una fecha de consulta2026 no prueba estabilidad futura.

Determinación guarda hecho origen/versión, regla exacta, datos/base/tasa/cálculo, tratamiento, período, motivos y documentos. Tiene estado propuesta/aprobada/sustituida; libro/registro fiscal preparado/presentado/rectificado son otros estados. Presentar no paga; pagar no prueba presentación; propuesta SUNAT no es aceptación del contribuyente. Accounting decide reconocimiento/presentación contable a partir del hecho fiscal y su propio marco.

## Matriz operativa inicial

| Operación / trigger | Datos y decisión obligatoria | Salida / limitación |
|---|---|---|
| Venta de bien local B2C | Lugar/naturaleza, base/descuento, entrega/cobro, cliente/identificación, emisor/SEE, exoneración si se invoca | IGV y cuota RER según reglas aprobadas; CPE según oportunidad legal. El monto de una aplicación Treasury no sustituye base de ingreso tributario |
| Anticipo, devolución y nota | Fecha/percepción, porción afectada, CPE referenciado, causa y acreditación | Momento tributario y ajuste/documento por operación; no recalcular todo desde venta final borrando anticipos |
| Compra local stock/no stock/servicio | Naturaleza real, factura/estado, proveedor, destino, anotación, período, bancarización y restricciones | IGV recuperable/no recuperable/pendiente separado; precio sin factura no acredita crédito. Gasto contable y deducibilidad futura son decisiones distintas |
| SPOT | Bien/servicio/código y alcance de anexo/regla especial, importe/base, exclusiones, sujeto/plazo y cuenta BN | Propuesta de depósito y hold pertinente, constancia y fecha; no “todo servicio12%” ni umbral700 universal |
| Retención/percepción IGV | Designación/padrón con vigencia, operación/exclusiones, comprobante y pago | Obligación/constancia/saldo/aplicación fiscal; agente no se infiere del nombre o tamaño de empresa |
| Servicio de no domiciliado | Proveedor/residencia, contrato, lugar de utilización, pago, documento, IGV e IR por separado | RS047-2026: declaración informativa previa y pago virtual correspondiente si alcance; retención IR/tasa/CDI requieren análisis adicional, no usar IGV como prueba de retención |
| Mutuo/aporte/capitalización | Vinculación y residencia, instrumento, fechas, principal/interés, bancarización y comparabilidad | Evaluación art26 vs32-A, imputación/retención según hechos; tasa civil0 no neutralidad fiscal; aporte requiere acto real |
| Bancarización | Obligación, umbral o regla mutuo de todo monto, pagador/acreedor/tercero designado, medio y constancia | Evidencia y consecuencias tributarias separadas del registro del dinero real; no bloquear conservación del hecho ocurrido |
| Beneficiario final | Cohorte normativa, ingreso base2024 si corresponde, RUC/activación, propiedad/control por fecha | Expediente y período de vencimiento específico; RS168-2025 no implica noviembre2026 para toda empresa |
| Cambio RER→RMT/General | Trigger/legalidad/fecha, ingresos, activos, coste, diferencias book/tax, pérdidas y pagos | Perfil nuevo y transición revisada; preservar datos desde V1 sin construir todas las reglas del General ahora |

RER: cuota cancelatoria sobre ingresos netos, no utilidad financiera. Art124-A mantiene una previsión legal de declaración anual de inventario; SUNAT indicó en cartilla publicada2025 que no estaba reglamentada/no era exigible en ese contexto. Es obligación potencial por revalidar, no calendario automático ni afirmación absoluta de inexistencia. Registro SIRE depende de cohorte y fecha; una discrecionalidad de sanciones no deroga la obligación.

## Comandos

CM0 aplica, D incluye I. Locks M de política/perfil, O de expediente/libro fiscal, Q de período, C/D de comprobantes/evidencias; Treasury se invoca por coordinación explícita respetando T/F/R antes de C/D. Ningún comando Tax escribe GL, stock o dinero confirmado.

| ID / capacidad / clase | Reads / locks | Writes / corrección / I/O |
|---|---|---|
| X01 activar perfil/regla / tax.configure / D | Fuentes/hechos y aprobación I→M→O→Q | Vigencias y versión sin solapamiento incompatible; cambio posterior produce revisión/impacto, no altera determinaciones anteriores |
| X02 determinar / tax.prepare / D | Manifest de operaciones/documentos, perfil/reglas/fechas I→M→O→Q→C→D | Propuestas y excepciones con cálculo reproducible; reutilizar hecho no duplica base. Fuente nueva/revisión cambia fingerprint y requiere nueva propuesta |
| X03 aprobar / tax.approve / D | Propuesta completa y revisiones I→M→O→Q→C→D | Determinación aprobada y expediente; no asiento automático. Actor único puede autoaprobar si política lo permite y se declara, sin inventar maker/checker |
| X04 preparar RVIE/RCE / tax.prepare_registers / D | CPE/determinaciones y propuesta SUNAT preservada, ajustes previos I→M→O→Q→C→D | Snapshot, diferencias y archivo según formato vigente; no acepta propuesta SUNAT por silencio. Parser/export fuera de TX, hash/versiones sellados |
| X05 registrar presentación/constancia / tax.record_filing / D | Evidencia externa, período/tipo/identidad y snapshot si existe; historia anterior admite ausencia explícita, I→O→Q→D | Hecho de presentación aceptada/rechazada según respuesta verificable; no “enviado=aceptado”. Uso inicial manual; API futura exige WO/contrato, credenciales fuera de repo |
| X06 rectificar/ajustar / tax.correct / D | Original, causa, nuevas reglas/hechos y restricciones I→M→O→Q→C→D | Nueva versión y vínculo de sustitución/ajuste, impacto en períodos/deuda/saldos; original/constancias quedan. No corrige GL de manera lateral |
| X07 preparar obligación/pago fiscal / tax.prepare_payment / D | Determinación/depósito/constancia requerida y plazo I→M→O→Q→T→D | Objetivo Treasury con autoridad/beneficiario/moneda y condición; confirmación Treasury aparte. Varias piernas proveedor/BN/fisco explicadas |
| X08 conciliar período / tax.reconcile / D | Registros, declaraciones, pagos, saldos, GL leído y excepciones I→M→O→Q→D | Puente firmado libro→base fiscal→declarado→pagado y saldo pendiente; diferencias identificadas, no asiento para forzar igualdad |

RS047-2026 exige preservar constancia informativa y pago separadamente. Sin CPE extranjero hay datos/identidad técnica del módulo, no documento fiscal fabricado. Sustituir antes de pago y rectificar tras pago siguen procedimientos distintos; evidencia de pago impide tratar una edición del formulario como sustitución simple. Fechas anteriores a julio2026 pagadas después requieren régimen transitorio analizado en la fuente.

Extensión X05/X06/X08: [External Tax Filing Mirror](../flows/external-tax-filing-mirror.md) define soporte por formulario/revisión, captura histórica incluso incompleta, comparación de casillas y revisión profesional. Filing verificado, preparación y settlement permanecen independientes; corregir captura no es presentar rectificatoria. La autoridad externa se registra solo hasta lo demostrado por su evidencia.

## Lecturas, UX y goldens fiscales

Cockpit por vencimiento/obligación, inputs faltantes, diferencias CPE/registros/GL, crédito pendiente, depósitos/retenciones/percepciones y constancias. Explica norma/versión/base/fecha y quién debe resolver. Al abrir documento extranjero, contenido es dato no confiable; PDF no ejecuta herramientas ni aprueba reglas. Calendario marca provisional cuando falta RUC/cronograma, no fecha inventada.

| Golden | Esperado |
|---|---|
| TX1 venta2000/retorno200 del G1 | Base neta1800 y cuota27 si perfil RER válido; IGV débito324, crédito aprobado504, saldo180; Accounting conserva su clasificación independiente |
| TX2 mismo dinero / distinta naturaleza | Cobro cliente, préstamo socio y aporte acreditado por igual importe no comparten automáticamente base RER |
| TX3 anticipo previo a despacho | Hecho fiscal/CPE puede anteceder ingreso contable; no duplica tributo al facturar saldo ni altera HP1 |
| TX4 documento incompleto/rechazado/tardío | Gasto/coste real preservado; crédito fiscal pendiente/rechazado según regla, no cero silencioso ni omisión de AP |
| TX5 SPOT/retención/percepción | Caso activado y caso excluido con fuente concreta; proveedor neto + depósito/retención = liquidación bruta; sin automatismo por nombre |
| TX6 no domiciliado | Informativa previa/pago/constancia, sustitución vs rectificación y transición2026; IGV e IR evaluados separadamente |
| TX7 perfil y norma cambian | Dos períodos con distintas reglas reproducibles; declaración antigua no se reescribe; supuesto beneficio exonerado sin evidencia bloqueado |
| TX8 relacionada gratuita | Vínculo y art32-A evaluados, comparación profesional pendiente no tasa0 aprobada; no posteos automáticos |
| TX9 rectificación y concurrency | Dos aceptaciones misma declaración/constancia no duplican deuda; corte compite con aprobación; Tax no logra modificar asiento |

Perfil futuro: DOMAIN y goldens fiscales versionados aprobados por profesional, PostgreSQL de unicidad/pertenencia, CONTRACT formatos/constancias, un E2E de excepción y conciliación. Sandbox solo si proveedor/autoridad ofrece mecanismo autorizado; no probar declaración real. Astra architect/checkpoint Tax/Legal; Sol orquesta; implementador/reviewer separados. Prohibido resolver criterios controvertidos por intuición, blogs, código Wbpro o respuesta de IA. [DH4](../../roadmap/decisions-gaps.md#dh4) y [DH2](../../roadmap/decisions-gaps.md#dh2)/[DH1](../../roadmap/decisions-gaps.md#dh1) según operación cierran el gate; no FROZEN con reglas materiales sin resolver.

## Incremento profesional M09 propuesto

**Amendment aceptado por revisión independiente**, conforme a review. [Workspace/libros/FX](../flows/tax-workspace-books.md), [matriz oficial](../../research/normative/tax-book-universe.md) y [ND Portugal](../../research/normative/jumpseller-portugal-service.md) concretan obligaciones presentes/futuras por régimen y datos de importación. Perfil real sigue C08; no salida oficial sin estructura efectiva validada ni presentación externa desde CasPro.
