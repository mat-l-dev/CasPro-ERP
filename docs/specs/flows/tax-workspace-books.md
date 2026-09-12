# Workspace fiscal, FX y libros por obligación

Propuesta del amendment; [review](../../review.md) posee fase. Extiende [M09](../milestones/tax-deep.md) y [Tax](../../tax/architecture.md), conserva fuentes/conciliaciones X01–X05. [Universo de libros](../../research/normative/tax-book-universe.md), [ND Portugal](../../research/normative/jumpseller-portugal-service.md) y [normativa operacional](../../research/normative/operational-completeness.md) sustentan diseño; aplicación real C08. No presentación, emisión de CPE, DAM ni pago SUNAT desde CasPro.

El [External Tax Filing Mirror](external-tax-filing-mirror.md) extiende registro externo, casillas/revisión/linaje histórico y las tres verdades preparado/presentado/liquidado. Preserva esta fundación; versión/canal del formulario y eficacia legal se verifican por obligación.

## Datos y obligaciones

TaxObligationRevision por entidad/tributo/libro/período y sistema: régimen/actividad/ingresos base y ejercicio/UIT/cohorte, regla/fuente/edición/vigencia, required/not_applicable/pending con razón, responsable y aprobación. RER no activa todos los libros; readiness registra hechos ricos desde primer día, y UI muestra obligaciones activas más una vista separada de preparación futura. Cambio de régimen conserva períodos anteriores y diagnóstico de datos faltantes; backfill es evidencia/revisión autorizada, no reconstrucción ficticia.

TaxPeriodWorkspace contiene ventas/compras/CPE, IGV débito/crédito, renta RER/RMT/General, SIRE, SPOT, retenciones/percepciones, ND, importaciones, FX, pagos, libros, excepciones y evidencia. No un estado lineal único: cada obligación tiene dimensiones sourceCompleteness (INCOMPLETE/COMPLETE), preparation (DRAFT/PREPARED/REVIEWED/READY_FOR_EXTERNAL_FILING), externalFiling (NOT_RECORDED/DECLARED_EXTERNALLY/RECTIFIED), settlement (UNPAID/PARTIAL/PAID), evidence (MISSING/ATTACHED/VERIFIED) y reconciliation (OPEN/DIFFERENCE/RECONCILED). Un impuesto puede pagarse antes de adjuntar constancia; no inventar declaración por PAID ni conciliación por archivo adjunto.

PreparedPackage versionado: universo de hechos/revisiones, corte/manifest completo, reglas de obligación/cálculo/estructura/FX/mapping, originales y exclusiones justificadas, totales y puente. Toda corrección después de revisión produce nueva versión y conserva paquete presentado externo. No desplazar un archivo ya declarado con una regeneración del mismo nombre. La oportunidad tributaria y el cierre contable son fechas distintas; período contable cerrado no reescribe hecho fiscal tardío.

## Observaciones FX por finalidad

Integrations adquiere referencia autorizada de fuente oficial o import manual verificable y publica valores; no una tasa global SUNAT. FXObservation immutable: par base/cotizada, fecha de observación/aplicación, compra/venta/otra categoría, finalidad elegible, fuente SBS/SUNAT/Aduanas/banco según caso, página/API/edición, acquired_at, valor Decimal, raw reference/hash, corrección/supersedes. Duplicados idénticos pueden compartir observación; corrección oficial conserva edición anterior.

PolicySelection Accounting/Tax/Treasury identifica observación y regla efectiva por operación: contabilidad reconocimiento/cierre NPIF y política C01; IGV operación en moneda extranjera regla art5.17 promedio ponderado venta SBS a fecha de nacimiento y regla de ausencia de publicación; importación IGV según fecha de pago prevista por esa norma y reglas aduaneras aplicables; retención ND según regla específica aprobada; banco tipo real aplicado por entidad financiera; comparativo de ofertas es finalidad comercial y no determina tributo. No sustituir por última tasa disponible sin regla documentada; no invertir buy/sell mecánicamente sin par y propósito.

Fecha económica/documento/pago/aduana/cierre se guarda separada. Dato ausente/contradictorio produce FX_MISSING/REVIEW_REQUIRED y bloqueo de cálculo final dependiente; permite guardar operación original en moneda. Conversión persiste operandos/tasa/regla/resultado/residuo; corregir observación no altera asiento/declaración histórica sin flujo autorizado.

## Expedientes específicos y conciliación

ND genérico: factura extranjera/contrato/período/naturaleza/derechos/país/sujeto, causalidad, domicilio/residencia/CRF, tratado/artículo/EP/beneficiario efectivo si procede, análisis doméstico y antiabuso/versiones, importe bruto/neto/gross-up si pactado, pago/acreditación, retención y constancia, IGV uso/base/FX/informativa/pago/anotación/crédito. No flag de exención por vendor. Art7 preferido para Jumpseller típico no autoriza tasa real sin hechos. RS047-2026, informativa y boleta1662 con código de tributo1041 se conservan en versión aplicable; ejecución afuera, resultado ingresado con evidencia.

Importación consume [dossier Procurement](sourcing-imports.md): factura/PO/transporte/seguro/origen/control/DAM-series/levante/pago y revisiones. Tax determina valor aduana/derechos/IGV/IPM/ISC/percepción solo aplicables y crédito; Accounting determina costo inventario/tributos recuperables/FX. Puente explícito factura→valor aduana→liquidación tributos→pago→crédito fiscal→landed cost→GL; diferencias clasificadas, no mismas bases forzadas. Reembolso al socio/tercero no crea segundo crédito ni cancela deber de probar cada pago.

SIRE compara propuesta SUNAT vs hechos internos, documento por documento: faltante, duplicado, anulado, nota sin original, importe/FX/fecha divergente, crédito no elegible y fuente tardía. Importar propuesta no acepta ni presenta registro. Libro Diario/Mayor/inventarios usa ledger/auxiliares y formato de TB; cuenta financiera no pasa a ser cuenta fiscal por nombre. Conciliación mantiene saldo anterior+movimientos±ajustes=saldo y todos los miembros, incluso si un total cuadrado oculta omisión.

## Preparación, export y evidencia externa

| ID / capacidad | Lecturas/guardas y locks CM0 | Efecto / rechazo / corrección |
|---|---|---|
| TX1 evaluar obligación / tax.profile.approve | Perfil entidad/período, fuentes/régimen/ingresos/cohorte y aprobador; revisión efectiva | Nueva obligación razonada, no obligación por UI; cambio material invalida preparación dependiente |
| TX2 preparar libro/tributo / tax.prepare | Contratos de hechos/ledger, cortes completos y layouts vigentes; manifiesto | Paquete interno con errores/faltantes; sin estructura validada no READY |
| TX3 revisar/liberar / tax.review | Paquete exacto, reconciliaciones/materialidad explícita, evidencia/capacidad; lock período/paquete | Firma de revisión y versión READY_FOR_EXTERNAL_FILING; diferencias no se compensan editando total |
| TX4 exportar / tax.export | Permiso de contenido/entidad, versión sellada y formato/purpose | TXT/CSV/XLSX/PDF según autoridad/uso, hash/tamaño/manifest; hoja interna no se etiqueta presentación legal |
| TX5 registrar presentación externa y vincular liquidación / tax.external.record; dinero por comandos Treasury | Identidad/obligación/período/versión, artefacto y nivel de verificación; dedupe/capacidad. Registro histórico admite evidencia incompleta sin marcar verificado; pago y PreparedPackage no son prerrequisitos del hecho externo | Filing/captura inmutables y revisiones según [mirror](external-tax-filing-mirror.md); constancia, casillas y pago se concilian por separado. No endpoint de envío/pago ni dinero ficticio; nueva presentación externa conserva original |

Import maestro/hechos utiliza VALIDATE→PREVIEW→CONFIRM con schema/revisión/parser/fuente, errores por fila y manifest/digest de preview, sin overwrite de hechos vivos. Confirmar revalida revisiones/permiso y ejecuta comandos del dueño por unidad atómica declarada; cambio desde preview exige repetirlo, no aprobación caducada. Export de texto/CSV neutraliza fórmulas en vistas humanas, preservando valor fuente; formato tributario técnico sigue schema exacto, no sanitización que altere dato sin error visible. Archivos sensibles privados con B10/C10.

Casos de aceptación documental en [expediente](../../evidence/professional-operational-completeness.md). B04/B07/B08/B10/B12 prueban posteriormente precisión/layout/cortes/hostilidad/externo incierto; C01/C07/C08/C10/C11/C13 activan únicamente función y datos aprobados.
