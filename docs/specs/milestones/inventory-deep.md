# M03–M04 — Inventario, valoración y cierre del circuito B2C

Estado: **SPECIFIED — candidato; política de valoración propuesta pendiente de validación contable y ejecutable**. Hereda [CM0 y extensiones](../cross-cutting/economic-facts.md). SP2 [Sales/Stock/Treasury](../flows/sales-stock-treasury.md) sigue siendo dueño de C13–C26; esta spec precisa coste, fechas y cortes, sin sustituir HP1–HP5.

## Dimensiones e invariantes

Inventory posee movimiento/posición/reserva/serial/valoración operativa. Separar cantidad física, condición vendible/no vendible, reserva y propiedad; una baja contable no es salida física. El pool W del candidato es entidad + SKU + propietario económico + moneda de coste, común entre ubicaciones propias. Posición P añade ubicación/condición; transferir entre posiciones del mismo pool conserva valor, no compra ni resultado. Existencias de terceros no se suman al pool propio. Es CASPRO DECISION de diseño candidata a freeze, no obligación NPIF ni elección todavía abierta entre pools. Cambiar granularidad/método requiere amendment; validar costes admisibles y parámetros de TILMUX limita activación ([C03](../../roadmap/decisions-gaps.md#activation-gates)), y probar precisión/replay limita implementación ([B04–B05](../../roadmap/decisions-gaps.md#implementation-gates)).

Cantidad usa Decimal en unidad base; dinero monetario se liquida a escala de moneda; coste unitario/intermedio admite más precisión. Candidato: cantidad 6 decimales, coste unitario 12, importes de valoración 6, liquidación PEN 2 y redondeo HALF_UP; límites y capacidad de almacenamiento se fijan con extremos sintéticos y política contable. No se presume que todas las unidades permiten fracciones. El residuo se conserva en el valor total del pool; última salida completa consume exactamente ese valor. Un tipo de cambio no usa float.

Para entrada de cantidad q y coste conocido c: `Q' = Q+q`, `V' = V+c`, `promedio'=V'/Q'`. Salida q usa promedio previo, manteniendo residuo de precisión; no puede producir Q<0 ni V residual cuando Q llega a cero. Reversal de salida añade la cantidad/valor original atribuible, no compra al promedio actual. NPIF §11 permite promedio; los detalles de implementación y granularidad son política CasPro.

UNKNOWN es una dimensión, no importe cero. Una entrada desconocida contamina la valoración posterior del pool hasta completar su coste: cantidad puede ser cierta con valor incompleto. Kardex muestra componentes conocidos y pendientes; no publica margen/COGS definitivo ni cierre sin resolver la parte afectada. Un coste cero solo existe con evidencia y política que lo justifica. HP3 permite operación física con coste pendiente según guardas SP2; no aprobar un paquete financiero incompleto como final.

## Cronología: dos fechas y una secuencia

Cada movimiento conserva fecha física declarada y registro/confirmación. La secuencia de valoración se asigna bajo W y es inmutable. Un recibo registrado tarde **no se inserta silenciosamente antes de salidas confirmadas**. Se registra ahora, con fecha física histórica, caso de discrepancia y evaluación del período financiero. Si explica una salida antes imposible, no se autoriza fabricar stock negativo retroactivo: investigación de apertura/conteo/identidad y ajuste documentado.

Coste tardío de una entrada ya valorada: candidato de recalculo controlado por revisión desde esa entrada, reproduciendo movimientos del pool por la secuencia confirmada. Conserva todas las valoraciones previas y produce deltas por salida, stock remanente y retorno enlazado. Preview fuera de TX, con hash de movimientos/política/corte; aceptación toma W y revisiones, exige misma secuencia y confirma nueva revisión completa. No adopta solo `delta × stock actual / compra original`: otras entradas/salidas cambian el promedio.

Si un período Accounting está cerrado, el nuevo cálculo operativo se conserva con su fecha de conocimiento y Accounting decide ajuste permitido en período abierto o reapertura explícita según marco. No cambia asientos cerrados ni informe firmado. Una política de error NPIF puede diferir de IAS 8; la fecha física no determina por sí sola dónde reconocer el delta. Registros fiscales conservan su corte independiente.

## Comandos profundos

Todas las filas heredan intención, autorización, transacción, auditoría, errores y compensación comunes. No I/O externo dentro del comando; una alteración de disponibilidad puede crear trabajo de reconciliación J al final, sujeto al gate Jumpseller.

| ID / capacidad / clase | Reads y locks | Writes / guardas / corrección |
|---|---|---|
| INV01 apertura/ajuste (amplía C13) / inventory.opening o inventory.adjust / D | Evidencia, unidad, seriales, corte I→K si integrado→M→Q si corte→W→P→U→V→J | Movimiento firmado, saldo, hecho y valoración conocida/UNKNOWN. Apertura única por lote/fila. Ajuste negativo no consume reservado: liberar/reasignar por coordinador autorizado primero; serial/cantidad deben conciliar. Error se corrige con movimiento referenciado |
| INV02 transferencia de ubicación/condición / inventory.transfer / D | Origen/destino/propiedad, reservas I→M→W→P→U→V | Dos piernas atómicas, misma cantidad/valor, sin Treasury. Reserva se mueve solo con política explícita y referencias coherentes; dañado no vendible. Cambio de propietario es otro negocio, no transferencia simple |
| INV03 preparar/aceptar coste tardío / inventory.value / D | Factura/coste admisible, movimientos completos, política, períodos I→M→S/O si compra→Q→W→P→C | Deltas versionados y hechos; input ya utilizado no se imputa dos veces. Preview obsoleto rechaza. Política fiscal/contable pendiente no se convierte en landed cost. Corrección genera otra revisión |
| INV04 conteo / inventory.count, inventory.approve_count / D y V | Alcance exacto, snapshot, movimientos en curso I→M→W→P→U→V | Abrir corte de posiciones, bloquear sus movimientos/reservas y esperar TX previas; capturar cantidades, discrepancias y aprobación. Revisión concurrente invalida; aceptar genera ajustes y libera corte atómicamente. Cancelar conserva capturas y libera sin ajustar |
| INV05 retorno cliente (C21) / sales.return + inventory.receive_return / D | Venta/entrega/retornos y coste atribuido I→K→E→M→S→T si cambia obligación→W→P→U→V→C→J | Cantidad acumulada ≤ entregada neta; ciclo de posesión inequívoco; entrada inicialmente no vendible y valor de salida original ajustado por revisiones explícitas. Refund es otro comando Treasury. Reingreso no confirma nota fiscal |
| INV06 devolución proveedor / procurement.return + inventory.dispatch_supplier_return / D | Compra, recepción, saldo disponible y autorización I→M→O→T si obligación cambia→W→P→U→V→C | Salida al promedio vigente del pool (última salida consume residuo), vinculada a recepción. Crédito comercial se negocia por separado; diferencia se conserva para Accounting. No aplicar automáticamente precio original como coste operativo |
| INV07 disposición posterior / inventory.inspect / D | Retorno/daño, evidencia de inspección I→M→W→P→U→V | No vendible→vendible exige evidencia y autorización; reparación no cambia coste sin INV03/política. Baja física registra destino y motivo; deterioro contable no la sustituye |

INV04 es un corte acotado por posiciones con ventana explícita. UX avisa antes y muestra operaciones bloqueadas. Cierre contable Q no congela almacén completo. Un conteo inesperado no borra reservas: debe resolverlas antes del ajuste negativo o mantener excepción pendiente.

## Casos de aceptación con números sintéticos

1. Entrada 10 a S/10 + entrada 10 a S/20 → Q20, V300, promedio15. Salida6 → Q14, V210, coste90. Salida14 → Q0, V0, coste210. Repetir intención no cambia nada.
2. Sobre esa secuencia, coste adicional S/40 para segunda entrada, aceptado después de las dos salidas: revisión nueva promedio17, salidas102 y238, delta COGS40 y stock0. La primera revisión permanece consultable; período cerrado no se reabre solo.
3. Entrada10 con UNKNOWN y otra10 con coste200: no dividir200/20 y llamarlo coste10. Mostrar Q20/valor incompleto; resolver primer coste100 produce revisión300 y propagación a salidas dependientes.
4. Salida6 a15, retorno2 antes de otro ajuste: entra30 en no vendible; refund comercial puede ser distinto. Retorno3 adicional y retorno2 simultáneos compiten por entrega: acumulado no supera6.
5. Devolver3 al proveedor con promedio15 y nota comercial60: salida45, diferencia15 explícita; no inventar ingreso/IGV sin tratamiento aprobado.
6. Dos despachos por última unidad: solo uno consume; conteo y despacho no pasan ambos con snapshot viejo. Pago íntegro se vuelve a comprobar bajo las mismas raíces de Treasury/Sales que una des-aplicación/refund.
7. Movimiento atrasado, coste tardío y cierre concurrentes producen orden verificable; ninguna ruta muta valoración anterior ni el asiento cerrado.
8. Cantidades fraccionarias mínimas, valores grandes, última unidad y cien transferencias no crean residuo espurio ni valor físico nuevo. Costo/condición de serial concilia con pool/posición sin doble posesión.

## M04: completar B2C y frontera de evidencia

El contrato de [CPE externo](../flows/cpe-document-delivery.md) permite anticipos/saldo/notas; no impone uno por venta ni posterga obligación legal hasta que Treasury confirme. El dossier exhibe asignaciones de cobertura documental, distintas de aplicaciones de dinero. HP1 exige pago íntegro aceptado de la venta antes de cada despacho físico, incluso parcial; un pago PAID remoto, PDF o extracto no lo satisface.

Lecturas: trabajo pendiente por excepción, pedido externo→venta→reserva→entregas/retornos, cobertura total/parcial y hechos Treasury, CPE/estado externo y entrega documental, costes conocidos/pendientes y fecha de reconciliación de stock. Document Flow no impone orden cronológico falso: CPE/anticipo puede preceder venta; la línea visual muestra relaciones reales y tiempos.

Salida M03: goldens de coste, PROPERTY/DOMAIN de conservación, PostgreSQL de atomicidad/constraints y CONCURRENCY en W/P/S/T/R. Salida M04: HP1–HP5 + CPE multipartes, replay/webhook desordenado, refund vs dispatch y aceptación de sandbox de stock. Si no existe fencing remoto/stock reservation demostrable, no habilitar PUT positivo; reconciliación/manual o canal controlado es el fallback, no promesa de evitar toda carrera.

Roles: Astra arquitectura/costeo/checkpoint; Sol orquestación; implementador/reviewer distintos. Permitido afinar índices/escala tras evidencia sin perder exactitud; prohibido cambiar pool, método, backdating, reconocimiento, stock negativo, HP1 o auto-confirmación. Entradas: esta spec, SP2, NPIF §11 y [políticas](../../accounting/npif-policy-catalog.md). Revisión contable de política y [DH3](../../roadmap/decisions-gaps.md#dh3)/[DH4](../../roadmap/decisions-gaps.md#dh4) deben quedar registradas antes de operaciones dependientes.

## Incremento profesional M03 propuesto

**Amendment aceptado por revisión independiente**, conforme a review. [Catalog/traslados](../flows/catalog-sites-warehouses.md) completa multialmacén y kits; [costo elegido A](../../research/normative/operational-completeness.md) conserva pool/promedio/replay y distingue FIFO físico. [Importaciones](../flows/sourcing-imports.md) consumen estas primitivas en M05+. WT hereda corte de conteo y K/J; no se omiten por fila resumida.
