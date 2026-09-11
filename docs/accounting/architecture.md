# Arquitectura objetivo de Accounting

Propietario: Accounting. Estado: arquitectura con [deep spec M07](../specs/milestones/accounting-deep.md) y [M08/goldens](../specs/acceptance/reporting-goldens.md) candidatas; no es implementación ni política profesional aprobada. Fuentes normativas: [registro](../research/normative/normative-register.md), [matriz NIIF](../research/normative/ifrs-applicability.md) y [reporte NPIF](npif-reporting.md).

## Cadena y ownership

```text
hecho operativo versionado
  → interpretación contable bajo marco/política vigente
  → propuesta o lote de contabilización
  → asiento balanceado e inmutable
  → mayor/submayor y conciliaciones
  → cierre y ajustes
  → paquete financiero versionado
  → rubro → cuenta → asiento → hecho → evidencia autorizada
```

Sales, Procurement, Inventory, Treasury y Corporate publican hechos neutrales; nunca eligen cuentas ni escriben líneas. Accounting posee marco financiero, plan aplicado, políticas/mapeos, períodos, interpretación, lotes, diarios/asientos, mayor, ajustes/reversiones, conciliaciones contables, cierre y reporting. Tax posee base/regla fiscal y conciliación libro-impuesto. Documents conserva bytes/snapshots y vínculos; no decide reconocimiento.

## Objetos conceptuales imprescindibles

| Objeto | Identidad y contenido | Regla |
|---|---|---|
| Marco financiero aplicado | Entidad, marco/edición, vigencia y aprobación | NPIF, PYMES y NIIF completas no se mezclan en un paquete |
| Plan contable aplicado | Entidad, versión PCGE base, extensiones y vigencia | Cambiar librería o catálogo no cambia el plan activo |
| Cuenta aplicada | Código oficial/interno, naturaleza, postabilidad, período | Códigos solo mediante mapeo/política; no dispersos en operación |
| Política y regla de posting | ID/versión, marco, trigger, condiciones, cuentas, dimensiones, redondeo, vigencia | Datos tipados y revisables; no DSL general ni edición retroactiva |
| Hecho recibido | ID productor+versión+secuencia, entidad, fechas, payload mínimo y hash/esquema | Dedupe por identidad; una versión incompatible queda en excepción |
| Interpretación | Hecho, marco, regla/política exactas, juicio y resultado | Reprocesar crea revisión; no altera el hecho |
| Lote/asiento/línea | Fuente, período, moneda, débito/crédito, cuenta, dimensiones y causación | Balanceado, inmutable; corrección mediante reversión/ajuste aprobado |
| Subledger/control | CxC, CxP, inventario, banco, activos cuando exista consumidor | Reconcilia con GL; no replica todo el dominio operativo |
| Período/cierre | Calendario, estado, checklist/evidencia, aprobaciones y excepciones | `OPEN → SOFT_CLOSED → HARD_CLOSED`; reapertura explícita y auditada |
| Paquete financiero | Entidad, corte, marco, comparativo, versiones, aprobación y snapshot | Reproducible; un preview no es cierre ni evidencia persistida |

## PCGE y `pcge-peru` v0.2.0

La [auditoría de código y distribución](../evidence/pcge-code-audit.md) fija identidad, API, datasets, prueba externa y límites de `pcge-peru` 0.2.0. Ofrece navegación/búsqueda/anomalías y valores congelados; el objeto catálogo mantiene estructuras internas mutables, por lo que no se presenta como profundamente inmutable. El loader valida integridad estructural y hash de entries, no autentica el PDF oficial. El adapter encapsula esos límites.

Contrato del adaptador CasPro:

1. fijar versión explícita y verificar metadata/provenance al activar;
2. usar la librería para catálogo, jerarquía y validación estructural;
3. persistir solo referencias y extensiones internas necesarias, sin copiar silenciosamente el dataset;
4. Accounting decide postabilidad, cuenta y mapeos por política;
5. revisar anomalías —incluida la ocurrencia duplicada `70992` reportada por la biblioteca— sin “corregir” códigos oficiales;
6. probar compatibilidad con una versión exacta antes de actualizar.

Un hash prueba integridad respecto del artefacto esperado, no autoridad normativa ni firma. La resolución oficial prevalece sobre la librería. PCGE 2019 continúa base normal a 2027; PCGE 2026 es anticipable y obligatorio desde 2028. La adopción anticipada queda pendiente de decisión contable.

## Costeo, CxC/CxP y cierres

- Inventory calcula promedio ponderado móvil operativo con cantidades y costes fuente. Accounting reconoce inventario/COGS conforme a política y registra VNR/deterioro/reversión sin cambiar kardex. Cada cierre reconcilia unidades y valoración por fuente.
- Sales/Procurement poseen obligaciones comerciales; Accounting mantiene controles contables derivados y reconciliables. Aplicar dinero en Treasury no borra la obligación ni reescribe un asiento.
- Un servicio comprado puede crear gasto, prepago, activo u otro tratamiento; Procurement describe el hecho y período del servicio, Accounting decide.
- `SOFT_CLOSED` bloquea contabilización rutinaria y permite excepciones autorizadas; `HARD_CLOSED` exige reapertura controlada o tratamiento en período actual según marco. Cierre de resultados y bloqueo de fechas son controles diferentes.
- Errores, cambios de estimación y política llevan tipo, período afectado, detectado, materialidad, fundamento y tratamiento. NPIF y NIC 8 difieren; el marco activo decide.

## Reporting NPIF V1

Delta del [amendment pendiente](../evidence/b2b-financing-amendment.md): [financiación M06](../specs/flows/financing-events-statements.md) aporta principal, pagos por cuenta, reembolsos y devoluciones con causalidad y componentes distintos. Reconocer obligación/adquisición, extinción frente a proveedor y derecho frente a socio una vez; el pago personal no entra en EFE como caja propia y el reembolso no crea segundo gasto. Estado mensual Corporate reconcilia a GL mediante puente por naturaleza, medición/FX y pendientes; no es un asiento ni una segunda fuente de saldo contable. NPIF14, presentación/revelación y política de relacionadas siguen C01/C06 y el [research](../research/normative/b2b-financing-evidence.md); no descuento NIIF9 ni NIC24 íntegra por analogía automática.

El primer producto contable usable genera situación financiera, resultados, cambios en patrimonio, flujos de efectivo y notas, con comparativos cuando correspondan, aunque NPIF haga opcionales los dos estados adicionales. El EFE directo se concreta como candidato en [M08](../specs/acceptance/reporting-goldens.md), incluida conciliación numérica. Reportes gerenciales no se etiquetan como EEFF formales. Ningún texto de cumplimiento se genera o aprueba automáticamente con IA.

## Gates para especificación y operación

Antes de código de Accounting: elegibilidad/marco de TILMUX; adopción PCGE; catálogo inicial de políticas; eventos de los hitos construidos; precisión; períodos/apertura; tratamiento RER; matriz de escenarios; aprobación profesional. Antes de operar: apertura reconciliada, balance de prueba, paquetes sintéticos completos sin Excel obligatorio, reversión/cierre/reapertura, aislamiento, concurrencia, actualización de reglas y trazabilidad hasta evidencia.

M07 especifica contratos de activos, provisiones, FX, instrumentos, devengos y demás auxiliares por trigger; requiere aprobar políticas/hechos antes de activarlos. Consolidación y otras expansiones M10 conservan estado CONCEPT/TRIGGERED. Ninguna spec declara tablas construidas ni tratamiento profesional aprobado.
