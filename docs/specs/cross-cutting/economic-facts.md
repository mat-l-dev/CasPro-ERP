# Contrato de hechos y extensiones transaccionales M01–M09

Estado: **SPECIFIED — candidato; PENDING EXECUTABLE VALIDATION**. Autoridad: CASPRO DECISION de arquitectura propuesta; no aprobación contable. Complementa [CM0](command-matrix.md#cm0), obligatorio en cada operación de estas deep specs. No instala un bus, event sourcing ni un motor genérico de workflow.

## Hecho mínimo desde el primer productor

Sales, Inventory, Procurement, Treasury y Corporate poseen sus hechos. Accounting posee interpretación/asiento; Tax, interpretación fiscal. Una confirmación económica escribe su hecho inmutable, auditoría e identidad idempotente en la misma transacción que el estado. Si falla cualquiera, no confirma. Una edición de borrador no es hecho económico.

Envelope común: UUID estable, entidad, productor/tipo/versión, raíz/revisión, intención, correlación/causación, fecha económica y zona horaria cuando importa, instante de registro UTC, actor/mandato, referencia a hecho corregido, referencias documentales versionadas. Payload con unidades/moneda/importes Decimal, contraparte y condición pertinente; nunca cuentas PCGE decididas por Sales ni datos derivados del estado actual de un maestro. El snapshot guarda lo que se conocía al confirmar; una corrección crea otro hecho y explica qué conocimiento cambió.

| Productor | Datos adicionales que no se pueden perder | Consumidor / prohibición |
|---|---|---|
| Sales | Líneas, cantidad, precio/descuento/base/impuestos declarados, moneda, contraparte histórica, condiciones, derechos/obligaciones y evidencia de entrega/control/aceptación; anticipo/cancelación/retorno referenciados | Accounting evalúa reconocimiento; pago, CPE o despacho aislado no prueba toda condición NPIF §16 |
| Inventory | Movimiento, posesión/propiedad/condición, origen/destino, cantidad, valoración y su versión, UNKNOWN explícito, coste de salida atribuido, ajustes posteriores y motivo | Accounting concilia cantidad/coste; VNR no escribe kardex |
| Procurement | PO o autorización directa, recepción/conformidad, período de servicio, precio contractual/facturado, descuentos y naturaleza, impuesto recuperable pendiente, recepción por facturar y disputas | Un servicio nunca crea stock; factura no confirma recepción |
| Treasury | Dinero observado/confirmado por separado, cuenta, moneda/importe bruto, fecha valor/operación/registro, pagador/beneficiario real, aplicaciones/reversiones, transferencias y comisiones explícitas | Conciliación no crea dinero; aplicación no duplica cobro |
| Corporate | Instrumento/versión contractual, acreedor, vinculación/fecha, moneda, derecho de restitución, condiciones, desembolso/reembolso/capitalización jurídicamente acreditados | Dinero de socio no es ingreso ni capital por su procedencia |
| Accounting | Política, marco, libro/período, valoración/estimación con inputs, tipo de cambio/fuente/fecha, reversión, juicio/aprobador, movimientos auxiliares | Tax consume sin modificar ledger |

Antes de M07 se conserva este contrato en almacenamiento del productor y se publica solo si existe consumidor durable. No se exige una cola operativa vacía. Al introducir Accounting se usa manifest de IDs de hechos elegibles, versión de extractor y hashes por lote; anti-join contra identidades consumidas y repetición hasta agotar pendientes. **No usar MAX(id), timestamp o secuencia asignada antes del commit como único watermark**: una transacción anterior puede confirmar tarde. Un corte completo exige barrera controlada sobre productores pertinentes, espera de transacciones en curso y manifest cerrado; los nuevos hechos van al siguiente corte. Reanudación/replay no vuelve a postear identidades consumidas.

Un productor sin el dato obligatorio genera excepción visible que bloquea la interpretación afectada. No rellena cero, fecha de hoy, tercero genérico ni cuenta transitoria automática para ocultarla. Un hecho ocurrido debe poder preservarse aunque su interpretación siga pendiente.

## Recursos adicionales y orden

**Delta semántico aceptado:** [B2B](../flows/b2b-commercial-dossier.md) añade fuentes OC/cotización/revisión aceptada bajo Sales. [Financiación](../flows/financing-events-statements.md) separa hecho Corporate de pago por cuenta, obligación Procurement extinguida, asignación Treasury por tercero y derecho al socio; su correlación/componentes evitan duplicar reconocimiento. No emitir un segundo flujo de caja por hecho Corporate que referencia movimiento Treasury; estado mensual es proyección sin contribución económica nueva. No reetiquetar reembolso de adelanto como amortización de principal. La extensión conserva el envelope y orden de recursos siguientes, con todas las raíces afectadas descubiertas antes de confirmar.

Se conserva el orden de CM0. Estas extensiones pertenecen a esa misma matriz, no a un segundo orden:

| Rango | Extensión | Exclusión / creación |
|---|---|---|
| 25 M | Política versionada, catálogo/plan aplicado, identidad societaria | Identidad UNIQUE; versiones publicadas inmutables. No lock durante consulta externa |
| 30 S/O | Raíz Sales o raíz de compra, expediente societario, libro contable | Orden total `(entidad, tipo, ID)` entre raíces distintas; crear con I y UNIQUE. O no implica una tabla común |
| 35 Q | Período contable/fiscal o corte de valoración | Bajo libro/raíz existente; un cierre y todo posting/ajuste compiten por el mismo período |
| 40 T | También obligación AP, anticipo o financiación de Treasury | Referencia única al propietario; no reasignar dueño al corregir |
| 47 L | Línea de extracto y grupo de conciliación | Identidad de importación en I/B; líneas existentes antes de conciliar |
| 50 R | También pagos, transferencias y correcciones de dinero | Comparten exclusión con cobros/aplicaciones originales |
| 55 W | Pool de valoración de Inventory | Entidad + SKU + propietario económico + moneda de coste; UNIQUE y creación bajo M. Antes de posiciones |
| 70 C | También factura/nota de proveedor y asignaciones de match | Unicidad de documento por emisor/tipo/serie/número/entidad receptora, validación fiscal separada |

Cada comando hereda CM0, autorización al confirmar, revisión esperada, respuestas/códigos, auditoría crítica, compensación y prohibición de I/O bajo locks. D incluye I; V incluye revisión. Los conjuntos afectados se descubren/releen enteros. Las filas de cada spec enumeran reads, locks, writes, corrección y aceptación especial; **efectos externos: ninguno**, salvo fila que indique trabajo durable y fases separadas. Una capacidad indicada es un permiso futuro, no una concesión existente.

**Regla transversal de disponibilidad:** toda confirmación que cambie cantidad, reserva, condición/ubicación elegible, mapping, buffer o corte de conteo de un destino integrado descubre todas sus K antes de M/S/O/W/P, invalida revisión/generación bajo K y persiste el trabajo J al final. Aplica a INV01/02/04/05/06/07, P03/P09 y comandos SP2 afectados aunque su fila abrevie K/J. Ninguna compra o devolución de proveedor deja READY un objetivo anterior. INV03 que solo cambie coste no invalida ATS; si cambia además elegibilidad aplica la misma regla. Si el conjunto de destinos cambia al releer, rollback/redescubrimiento. Nunca adquirir K después de W/P.

**Conteo humano:** abrir INV04 persiste un bloqueo de negocio por posición bajo P y libera la transacción antes de la captura humana. Toda ruta de movimiento/reserva de esa posición revalida ese bloqueo bajo P; una simple consulta de saldo no lo evade. Confirmar/cancelar conteo toma otra transacción, revisiones y las mismas raíces; conserva capturas y motivo y levanta el bloqueo. No mantener locks de PostgreSQL durante minutos de conteo ni bloquear por accidente todo el pool compartido entre almacenes.

## Contratos de lectura y reconciliación

Lecturas llevan entidad, corte económico y corte de conocimiento, filtros, paginación estable y revisión del resultado. Respuestas distinguen estado operacional, financiero, documental, contable y fiscal. Una projection atrasada muestra su corte/lag; no habilita comandos usando sumas cacheadas. Permisos filtran tanto nodos como totales, búsqueda, exportación y enlaces. Document Flow deriva aristas tipadas con IDs reales; no posee un estado empresarial adicional.

Un extracto de reconciliación contiene saldo inicial, entradas, salidas, ajustes y saldo final; enlaces al detalle y lista de excepciones. No se considera conciliado por tener sumas iguales si existen hechos omitidos, duplicados, moneda mezclada o compensaciones sin soporte. Restore conserva identidades y estados de resultado externo desconocido; replay no reenvía ni confirma automáticamente.

## Evidencia de salida transversal

La WO posterior debe demostrar: atomicidad estado/hecho/audit; creación simultánea de la misma identidad; replay con nueva sesión; commit desconocido; miembro revocado; referencia de otra entidad; dato faltante; corrección sin borrar; migración del esquema de payload con lectura de versión antigua; manifest con commit tardío; corte concurrente; recuperación DB+objetos. STATIC hoy no acredita ninguna de esas ejecuciones.

## Delta profesional propuesto: productores y concurrencia

El amendment de [completitud](../../evidence/professional-operational-completeness.md) añade productores sin nueva infraestructura: Catalog revisión/perfiles/kit; Inventory traslado/custodia/costo; Sales cotización/contrato/hitos/crédito/reclamación/paquete sitio; Procurement necesidad/RFQ/award/importación/renta; Treasury instrumentos/caja; Documents original/derivado/firma/custodia; Tax obligación/paquete. Hecho comercial/documental no origina reconocimiento por etiqueta; Accounting interpreta componentes económicos una vez. Estados de revisión, fecha económica, registro y evidencia siguen separados.

Extensión del mismo orden CM0: **27 H**, raíz de exposición de crédito por entidad/cliente/moneda, creada bajo Party M y UNIQUE/I; precede todas las raíces S/O30. Toda aceptación/cancelación/ajuste/aplicación/desaplicación/reversión que cambie exposición toma H, incluso cuando procede de Treasury, nunca H después de T/R. Expone contratos de valores, no llamada Treasury→Sales: coordinador descubierto antes de confirmar. **S/O30** incluye raíces cotización/contrato/requisición/RFQ/award/importación/transferencia/instrumento/fondo/arrendamiento/paquete sitio/reclamación; orden total por tipo/ID. No todas compiten entre sí, solo conjunto afectado. Perfil contable25M y libro30O→período35Q; Document80D/custodia→intención90N.

En traslados/kits/sourcing se mantiene K antes de M/raíces/W/P y J al final cuando cambia disponibilidad integrada. Cotización no reserva; adjudicación no recibe; estimación de landed cost no crea AP; recepción no acredita levante; firmado no acredita dinero. Transferencias propias no generan compra/venta/COGS; pérdida real sí publica componente aparte. Deltas de costo sobre ventas pasadas usan el replay/corte existente.

Comandos nuevos CT/WT, QS/CR/FS, PC/IM, FI, DR/SP/LR y TX se leen con CM0 y sus fichas. Creación de raíces, consumo/asignación, movimiento, aceptación/contrato, hito, rendición, documento generado, firma/entrega, paquete/export retenido y registro externo son **D**; cambio de borrador/aprobación sobre revisión existente sin nuevo efecto es **V**; consulta/preview sin persistencia empresarial es **R**. Una variante V que además produce efectos hereda D. Cada revisión preserva capacidad específica, intención/correlación, readset y conjunto de locks; unicidad natural impide duplicar por clave nueva. Hechos/audit/trabajo durable se confirman juntos y la corrección produce revisión/compensación, nunca DELETE. No I/O externo durante TX.

Evidencia futura adicional: H protege dos pedidos/monedas/límites y pago concurrentes; WT protege origen/tránsito/destino/serial; IM conserva fuente de costo/reparto/residuo y cierre; FI conserva principal/interés/caja; DR conserva bytes/firmas; TX conserva miembros/formatos/obligaciones. Estas extensiones invalidan únicamente claims afectados según B14, no reutilizan PASS ejecutable inexistente.
