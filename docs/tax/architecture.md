# Arquitectura Tax Perú

Propietario: Tax. Estado: investigación y [policy spec M09 candidata](../specs/milestones/tax-deep.md), PENDING FACT / PENDING PROFESSIONAL VALIDATION. Tax no es Accounting ni un generador de hechos operativos.

## Frontera

```text
hecho operativo + documento + interpretación contable
          ↓
regla tributaria versionada por período y ámbito
          ↓
posición/cálculo/registro/conciliación/expediente Tax
          ↓
salida preparada para revisión humana
```

Tax posee perfil y vigencia del régimen, reglas/fuentes, base fiscal, tratamientos, impuestos, detracciones/retenciones/percepciones, conciliación libro-impuesto, RVIE/RCE/SIRE, obligaciones/calendario y expedientes de declaración. No altera venta, pago, stock o mayor para hacerlos coincidir con una casilla. En esta etapa no presenta declaraciones, libros, CPE ni información a SUNAT.

## RER inicial

RER es declaración del propietario, pendiente de verificar en ficha RUC/acogimiento y actividad. La orientación SUNAT vigente al corte indica cuota mensual 1,5% de ingresos netos, IGV 18%, límites de S/525.000 en ingresos/compras, activos fijos y trabajadores, Registro de Ventas y Registro de Compras, y ausencia de DJ anual del IR. La spec no hardcodeará estos valores sin período/fuente porque pueden cambiar y existen páginas oficiales históricas con reglas anteriores.

Datos a preservar desde V1: base/IGV por línea, descuentos/devoluciones, fecha de emisión/operación, tipo/serie/número/estado CPE, identidad fiscal versionada, adquisición/destino, crédito fiscal y sustento, pago/medio, retención/percepción/detracción y constancia, importes de ingresos/compras acumulados, activos y personal como inputs de elegibilidad cuando existan. El marco financiero NPIF no se deriva de RER.

## Componentes futuros

| Capability | Resultado | Gate |
|---|---|---|
| Perfil tributario | Régimen, entidad, período, estado y evidencia | RUC/alta real; no inferir de configuración vieja |
| Motor de reglas acotado | Regla tipada, fuente, vigencia, condiciones y cálculo reproducible | Especificación por tributo; sin DSL general |
| CPE/validación | Identidad, artefactos, estado observado, vínculo y excepciones | Normativa y capacidad oficial actual; CasPro no emite inicialmente |
| IGV | Débito/crédito y ajustes por período | Ley/reglamento y derecho a crédito por caso |
| SPOT/retención/percepción | Aplicabilidad, base, tasa, depósito/constancia/saldo | Bien/servicio y padrón vigente, no nombre libre |
| SIRE | Propuestas RVIE/RCE, aceptación/ajuste y evidencia | Fecha real de incorporación; API/canal comprobado |
| RER→RMT/General | Cambio fechado sin reescribir períodos | Decisión/acogimiento y reglas del nuevo régimen |
| Conciliación fiscal | Libro, base fiscal, diferencias permanentes/temporales cuando proceda | Marco financiero y política profesional |
| Obligaciones | Calendario, preparación, aprobación, presentación externa y acuse | Presentación futura exige mandato e integración separada |

## Mutuos y partes relacionadas

El contrato gratuito y el tratamiento fiscal son dimensiones distintas. Para vinculadas se evalúa valor de mercado/precios de transferencia; para no vinculadas puede operar la presunción del art. 26 con su prueba. Bancarización aplica a entrega y devolución cualquiera sea el monto. Tax conserva relación, acuerdo, principal, moneda, fechas, tasa pactada/benchmark, comparables, devengos, pagos, documentación y posición. RTF 08044-1-2022 se registra como precedente de hechos concretos, no regla universal u observancia obligatoria acreditada.

## Validaciones pendientes

Delta aceptado B2B/financiación: [matriz oficial N030–N043](../research/normative/b2b-financing-evidence.md) distingue CPE/traslado/medios de pago/crédito/registros de controles comerciales. OC, pago o estado mensual no certifican fehaciencia integral. Pago de tercero al proveedor y posterior reembolso se separan del receptor tercero designado (SUNAT038-2022); no crear comunicación SUNAT universal. Gratuidad, ajustes32-A, reportes/retención y BF requieren hechos propios; desembolso/principal devuelto acreditados no son venta por movimiento de banco. C06/C07/C08/C09 se mantienen por efecto, sin automatizar tasa, deducción ni declaración.

Antes de primera operación: RUC/régimen, obligaciones CPE y SIRE, afectación IGV por catálogo real, adquisiciones sujetas a SPOT/percepción/retención, calendario, tratamiento de CPE externos y evidencia. Antes del mutuo: dictamen legal-tributario-contable. Antes de RMT/General: base fiscal, pagos a cuenta, DJ anual, libros, activos/depreciación y diferencias. Todas las salidas son `PREPARED` hasta revisión; la IA puede explicar/anotar candidatos, nunca determinar ni presentar.

Fuentes canónicas: [registro normativo](../research/normative/normative-register.md), [revisión tributaria actual](../research/normative/tax-current-review.md) y [memorando mutuo](../research/normative/mutuo-tax-corporate.md). La spec M09 cita esas fuentes; cada activación fija texto/vigencia, hechos, alcance, carácter vinculante y límites. La investigación documental no aprueba el perfil empresarial real.
