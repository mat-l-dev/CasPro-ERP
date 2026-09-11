# Invariantes fundacionales

Estas propiedades establecen el comportamiento que debe sobrevivir parcialidades, errores, reversión y concurrencia. Su mecanismo está en [transacciones](../architecture/transactions.md); sus escenarios completos se definirán en las specs.

## Dinero y liquidación

Para cada cobro r, entidad y moneda:

- N(r): importe neto confirmado del cobro tras sus devoluciones/reversiones vinculadas. No incluye gastos bancarios independientes ni sumas de otra moneda.
- A(r): suma neta de aplicaciones activas de ese cobro, descontando las des-aplicaciones referenciadas.
- U(r) = N(r) − A(r): dinero todavía sin aplicar.
- Debe cumplirse 0 ≤ A(r) ≤ N(r) y U(r) ≥ 0. Las reversiones no pueden exceder el hecho pendiente de revertir. Un contracargo adicional que exceda el cobro exige otro hecho de deuda/gasto explícito, no un N negativo silencioso.

Para cada objetivo comercial o:

- A(o): dinero neto aplicado, sin duplicados ni aplicaciones de otra entidad/moneda.
- L(o): límite comercial vigente publicado por su propietario, con revisión.
- 0 ≤ A(o) ≤ L(o). Un exceso queda sin aplicar o se rechaza según el caso; no se inventa ingreso.
- Disminuir L(o) obliga a resolver el exceso dentro del mismo flujo antes de confirmar. Un ajuste de factura no puede dejar su proyección financiera antigua.

Los límites de conservación se aplican simétricamente a pagos de proveedor y recuperaciones de esos pagos, usando magnitudes no negativas y dirección explícita. Devolver un cobro produce una salida; recuperar un pago produce una entrada. Un objetivo por cobrar recibe aplicaciones de cobros y uno por pagar, de pagos. Compartir contraparte, entidad o moneda no autoriza compensarlos entre sí: cualquier compensación exige su propio caso de uso y política posterior.

La elegibilidad de una nueva entrega al contado compara el valor acumulado exigible de las entregas, incluida la propuesta, con el dinero neto aplicable actual a sus obligaciones. Ambos importes usan la misma base comercial y moneda, y se leen bajo los recursos comunes del flujo.

Devolver dinero no borra una entrega pasada. Debe reducir disponibilidad futura y, si deja bienes entregados sin cobertura, registrar deuda/retorno/ajuste autorizado y bloquear nuevas entregas al contado hasta resolverlo. Ninguna reclasificación a crédito se hace automáticamente. La política de devoluciones será validada por el propietario.

Contraejemplos que deberán refutar la implementación: un cobro 100 aplicado 80+80 a dos obligaciones; dos cobros que exceden una obligación; entregar mientras se devuelve su cobro; repetir el mismo refund; corregir el importe comercial mientras otro proceso aplica dinero.

## Stock y parcialidades

- Existencia por posición = entradas confirmadas − salidas confirmadas, incluidas correcciones vinculadas. La primera política rechaza stock físico negativo; cualquier excepción requiere decisión y escenario propio.
- Importar un pedido o un estado del canal no descuenta stock físico. Reserva y despacho coordinados consumen el mismo compromiso una vez; la publicación/observación de stock externo no genera otro movimiento. El cálculo publicable pertenece a Inventory, según [integraciones](../architecture/integrations.md).
- Recepción, entrega y devolución identifican dirección, movimiento original y cantidades netas ya ejecutadas o corregidas. Las parcialidades no exceden el remanente de esa referencia; no se limita toda la vida del SKU o serial a una sola operación.
- Devolución de cliente: entrada que referencia una salida anterior y repone su coste atribuible. Devolución a proveedor: salida que referencia la recepción correspondiente; no repone inventario. [INV06](../specs/milestones/inventory-deep.md) valora esa salida al promedio vigente del pool; el crédito comercial del proveedor se registra separadamente. La diferencia entre ambos valores requiere interpretación Accounting/Tax, nunca dinero ni stock ficticios para igualarlos.
- Cuando se reparte un coste original entre parcialidades, el reparto conserva el total y asigna el resto exacto a la que lo agota; no reconstruye ese total usando un unitario redondeado.
- La identidad serial conserva un único recorrido físico compatible. Una salida consume una posesión disponible y una devolución entrante referencia la salida que corrige. Se rechaza duplicar esa salida o devolver de nuevo la misma unidad contra la misma salida sin un nuevo ciclo válido. Venta → devolución → reventa → nueva devolución es admisible si cada paso acredita posesión, referencia y guardas; no equivale a autorizar automáticamente la reventa de cualquier bien devuelto.
- Retirar un maestro no destruye obligaciones previas. Cada operación distingue compromiso nuevo de ejecución/corrección existente.

## Identidad, evidencia y estados

- Un hecho no cambia de entidad propietaria. Una referencia a otro objeto debe demostrar pertenencia compatible.
- Un reintento de la misma intención produce el mismo efecto confirmado; una clave repetida con contenido distinto produce conflicto.
- Confirmar una transición económica implica persistir sus cambios, hecho económico necesario y auditoría crítica en una sola transacción.
- El expediente preparado, el dato capturado de emisión y la verificación externa no son equivalentes.
- Artefacto adquirido, representación generada y entrega por email son dimensiones distintas; ninguna representación reconstruida se etiqueta como original ni un resultado de email cambia la validez del CPE o la venta.
- Una referencia o hash no se trata como prueba de autenticidad, firma, autorización o titularidad.

## Contrato de máquina de estados

No existe un enum universal de ERP. Cada agregado especificará transición, origen/destino, actor/capacidad, guardas, efectos, recursos bloqueados, evento, auditoría, idempotencia, fallos y reversión.

Separar dimensiones ortogonales: estado del pedido, progreso físico, liquidación y estado fiscal. Pagado/parcialmente pagado son resultados del saldo válido; si se materializan para lectura, se reconcilian con su fuente. Cancelar un remanente no anula silenciosamente hechos ya ejecutados.

Estas invariantes son decisiones de integridad, no afirmaciones sobre tasas, asientos, normativa de emisión o marco contable. Esas reglas permanecen PENDING DOMAIN/REGULATORY VALIDATION cuando falte fuente aplicable.
