# Treasury y finanzas objetivo

Propietario: Treasury. Estado: ARCHITECTED / NEEDS DEEP SPEC. El circuito B2C existente sigue siendo el primer alcance; este documento ordena su evolución.

## Hechos separados

Cuenta financiera, línea de extracto, movimiento interno confirmado, objetivo por cobrar/pagar, aplicación, transferencia, comisión, refund y conciliación tienen identidades distintas. Un estado de canal, CPE, orden, saldo de pantalla o candidato de IA no crea dinero. Treasury confirma dinero con evidencia suficiente y conserva fuente, fecha valor/operación, importe/moneda, cuenta, contraparte observada y referencia.

## Capacidades

- cuentas bancarias/caja con titularidad y vigencia probadas;
- cobros, pagos, transferencias de dos lados y movimientos compensatorios;
- anticipos/unapplied money, depósitos no identificados y aplicaciones N:M;
- propuestas/AP payments, HOLD, aprobaciones, reversiones y refunds;
- importación versionada del extracto original, dedupe, conciliación y desconciliación;
- cargos/comisiones como hechos identificados; reglas no crean gastos sin autorización;
- moneda/tipo de cambio con fuente y momento; posición de caja y aging derivados;
- financiamiento/capital con origen Corporate y tratamiento Accounting/Tax;
- corte de período y conciliación banco↔movimientos↔aplicaciones↔GL.

## Conciliación por capas

1. **Deterministic match:** identificadores inequívocos y reglas exactas.
2. **Heuristic candidates:** importe, ventana, referencia, pagador asociado, comisión y cardinalidad, con versión y explicación.
3. **AI suggestion:** candidatos estructurados, confianza, coincidencias, diferencias y contraevidencia; datos mínimos/redactados.
4. **Human confirmation:** el operador elige asignación e importe; inicialmente obligatorio para casos no inequívocos y para confirmar cobro B2C.
5. **Audit/evaluation:** regla/modelo/prompt, entradas, resultado, decisión y reversión.

El candidato nunca altera movimientos, aplicaciones o ledger. El fallback sin IA mantiene matching manual/determinista. Una línea puede corresponder a varios movimientos y viceversa si la política lo permite; los centavos o nombres parecidos no habilitan auto-match. Aprender significa ajustar configuración/evaluación futura, no reescribir decisiones pasadas.

## Reglas de integridad

- Movimiento confirmado es append-only bajo interfaz ordinaria; corrección por reversión relacionada.
- Aplicación no excede disponibles netos ni cruza entidad/moneda/dirección; concurrencia bloquea movimiento y objetivos afectados.
- Importar un extracto no crea dinero interno; una acción autorizada puede registrar el movimiento faltante con evidencia.
- Transferencia interna produce salida y entrada relacionadas, no ingreso/gasto por defecto.
- Pago del socio a proveedor desde cuenta personal no es movimiento bancario de TILMUX: origina evidencia y posible obligación/financiamiento a clasificar por Corporate/Accounting/Tax.
- Forecast es proyección identificada, separada de posición confirmada.

Primera spec profunda: importación BBVA/CSV, esquema de referencia, dedupe, cobro/aplicación B2C, líneas no identificadas, desconciliación y cierre diario. Pagos automáticos, open banking, FX avanzado, cash pooling y forecasting predictivo permanecen fuera hasta necesidad y proveedor comprobados.
