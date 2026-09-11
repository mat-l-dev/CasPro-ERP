# Inventory, kardex y frontera contable

Propietario: Inventory para realidad física/coste operativo; Accounting para medición financiera. Estado: arquitectura con [deep spec M03 candidata](../specs/milestones/inventory-deep.md); HP3 fija método, UNKNOWN y condición del retorno, con parámetros de política pendientes.

## Promedio ponderado móvil

Cada entrada elegible actualiza cantidad y coste acumulado exactos; el promedio se deriva sin `float`. Cada salida confirmada toma el coste operativo vigente de la posición/lote de valoración definido. Escala y redondeo se decidirán con datos reales; el reparto conserva total y residuo. Costo ausente queda `UNKNOWN`, bloquea cualquier cifra que requiera certeza y nunca equivale a cero.

Recepciones tardías, costes adicionales y movimientos retroactivos no reescriben filas confirmadas silenciosamente. La [deep spec M03](../specs/milestones/inventory-deep.md) define secuencia confirmada, pool candidato y recalculo controlado por revisiones con deltas; política pendiente de revisión profesional/ejecutable. Un cierre Accounting no cierra por sí solo el almacén, pero una fecha contable protegida limita el efecto financiero de backdating.

## Condición, devolución y conteo

- Devolución de cliente referencia entrega y ciclo de posesión; ingresa inicialmente a condición no vendible y repone el coste atribuible original, no un promedio actual por comodidad.
- Devolución a proveedor referencia recepción y sale físicamente; su coste operativo y el crédito comercial pueden diferir.
- Daño, obsolescencia, faltante y sobrante se confirman como ajustes físicos con conteo, motivo, actor y evidencia.
- Conteo físico sigue `plan → freeze/snapshot → captura → comparación → aprobación → ajustes`; diferencias no se corrigen editando posición.
- Serial solo ocupa una posesión/ubicación por ciclo; cantidades seriadas concilian con unidades.

## Reconciliaciones

Inventory expone por entidad/fecha/SKU/ubicación: entradas, salidas, condición, cantidad y coste operativo. Accounting mantiene valoración, COGS, VNR/deterioro/reversión y diferencias de cierre. La conciliación explica:

```text
saldo inicial + entradas − salidas ± ajustes = saldo físico
valor operativo ± efectos contables separados = saldo contable
```

VNR no modifica recepción, coste fuente ni posesión. La política NIC 2/NPIF se activa bajo el marco aplicable; IAS 36 no se usa para inventarios. Tax deriva su propio tratamiento.

Stock publicable Jumpseller usa cantidades elegibles, reservas, demanda externa y buffer versionado. La fórmula/PUT positivo siguen pendientes del gate técnico; ninguna decisión de costeo autoriza publicar.
