# Catálogo profesional, sedes y transferencias

Propuesta semántica del amendment de completitud; aceptación/ejecución según [review](../../review.md). Extiende [M02](../milestones/runtime-masters.md) y [M03](../milestones/inventory-deep.md), sin reemplazar CM0, pool, replay ni aislamiento. Catalog posee producto; Organization sede; Inventory almacén/posesión; Corporate tenencia; Tax cumplimiento. Evidencia: [normativa](../../research/normative/operational-completeness.md) y [benchmark](../../research/professional-erp-benchmark.md).

## Catálogo y perfiles

SKU estable por entidad, activo/discontinuado/bloqueado, nombre/descripcion diferenciada interna/comercial/fiscal/técnica, marca/modelo/MPN, familia/departamento, GTIN opcional validado, referencias de proveedor/cliente y fabricante con vigencia. No usar nombre como identidad. Variantes comercialmente distintas tienen SKU propio y relación de familia; cambiar marca/modelo material crea nueva revisión/SKU según identidad, sin reasignar serial histórico.

Catalog mantiene definición tipada de atributos por familia: código, nombre, tipo (decimal/unidad, enum, boolean, texto acotado), cardinalidad, rango/catálogo, requerido por uso, vigencia y responsable. Valores validados contra esa revisión, no100 columnas opcionales ni EAV arbitrario que almacene hechos de stock/impuestos. Ejemplos: tensión/potencia/capacidad/Wh/química batería, protocolo/conector/frecuencia/IP rating, lúmenes/autonomía, resolución y compatibilidad. Un atributo técnico no acredita certificación.

Unidad base de stock exacta; unidades compra/venta y conversiones específicas SKU vigentes. Rollo305m, caja de unidades y metro fraccionable no se confunden; snapshot de conversión por línea, precisión y residuo conforme Data/C03. Cambio de factor no recalcula historia; corte/merma de cable es hecho Inventory con evidencia, no conversión que invente cantidad. Producto seriado exige unidades enteras y perfil de identificadores (serial, IMEI, MAC), normalización/namespace y unicidad por fabricante/modelo donde corresponda. Lote solo con trazabilidad/vence/regulación/caso que lo justifique; no lote automático por departamento.

Ficha, manual, certificado, homologación, origen, garantía del fabricante, plazo/condición y compatibilidad tienen emisor, modelo/serie/país/alcance, versión/fecha/expiración y Document reference. Dueño del cumplimiento (Tax/Procurement/Sales) evalúa aplicabilidad y bloqueo; Catalog conserva metadatos técnicos y referencias, no lee expedientes privados. Tariff candidate ≠ clasificación aprobada; peso/dimensiones/neto/bruto y transporte peligroso requieren fuente/unidad/configuración. Garantía informativa no activa RMA completo.

## Matriz de departamentos

P = posible según SKU/operación, C = habitual a perfilar sin mandato universal, — = sin necesidad general; toda exigencia regulatoria requiere aplicabilidad. Los seis usan ficha técnica, garantía informativa, compatibilidad/accesorios y kits cuando exista composición comercial; no módulos departamentales.

| Departamento / estado | Serial/IMEI/MAC | Lote | UOM especial | Instalación | Calibración | Homologación | Certificados técnicos | Restricción import/transporte | Site/minería | Fichas/garantía/compatibilidad/kits |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 Seguridad: cámaras/alarmas/acceso/incendio — CONFIRMED | C serial;P MAC/IMEI | P | Cable/rollo/caja | C incluida | P instrumentos | P radio/telecom | P modelo/uso/incendio | P | P | Sí por producto |
| 2 Energía/electricidad: UPS/solar/LiFePO4 — CONFIRMED | C serial;P comunicaciones | P batería/trazabilidad | Cable/kit/unidad | C incluida | P medición | P radio incorporada | P electricidad/batería | P química/Wh/config/ruta | P | Sí por producto |
| 3 Redes/telecom: Starlink/router/PoE/fibra — CONFIRMED | C serial/MAC;P IMEI | P | Metro/rollo/bobina/caja | C incluida | P certificador | P modelo/supuesto | P red/telecom | P telecom/baterías | P | Sí por producto |
| 4 Iluminación/emergencia/señalización — CONFIRMED | P | P | Unidad/caja/metro | P incluida | P instrumento | P radio incorporada | P seguridad/uso | P batería/otros | P | Sí por producto |
| 5 Herramientas/calibración — CANDIDATE | P serie de equipo | P | Unidad/juego | P demostración | C cuando instrumento | P radio | P calibración/seguridad | P | P | Perfil preparado;activar por catálogo real |
| 6 IT comercial — CANDIDATE | C serial;P MAC/IMEI | P | Unidad/caja | P incluida | — general | P radio/terminal | P técnico | P batería/telecom | P | Perfil preparado;activar por catálogo real |

## Kits comerciales

KitRevision: parent comercial opcional, componentes SKU/cantidad/UOM/revisión, obligatorio/opcional, sustitutos aprobados y reglas de compatibilidad; sin ciclos ni componentes negativos. Instalación incluida es promesa Sales, no SKU de servicio vendido ni stock ficticio. Kit no crea producción/ensamblaje/BOM de fabricación. Precio puede ser global o suma; snapshot guarda asignación aprobada por línea para descuento/margen/impuesto, total y residuos exactos. C07 valida representación fiscal; pantalla no decide tributación.

Al cotizar, congela composición/precio. Al crear orden, confirma opciones/sustitución y revisiones; reserva atómicamente componentes. No reservar parent y componentes a la vez. Disponibilidad teórica de un kit = mínimo de enteros disponibles/cantidad requerida, pero varios kits y ventas sueltas comparten componentes: **no sumar disponibilidades independientes** para publicar. Jumpseller mapping identifica kit y versión; aceptación local revalida todos los componentes y rechaza faltante sin orden/reserva parcial. B11/C11 conservan gate de publicación positiva; fórmula de kits no resuelve carrera externa.

## Sede, almacén y transferencia

Site de Organization identifica entidad, tipo/uso, dirección privada, vigencia y estado DRAFT/ACTIVE/RESTRICTED/CLOSED. Corporate posee tenencia (propio/cesión/arrendamiento/otro probado), contrato y facultades. Tax evalúa anexo/RUC y permiso aplicable. Una sede puede tener varios almacenes; ubicaciones Inventory pertenecen a almacén, no a un departamento comercial. No se registran direcciones reales en Git. Cierre de sede con stock/reservas/tránsito/custodia documental o contrato abierto exige resolver/reubicar, no borrado en cascada.

Transferencia interna solo dentro de entidad y pool de valoración aceptado; entre entidades es otra operación y sigue D03. Raíz Inventory con origen/destino, líneas, revisiones, responsable y documentos. Estados REQUESTED→APPROVED→DISPATCHED→PARTIALLY_RECEIVED→RECEIVED; CANCELLED antes de expedición; después, devolución/reenvío/discrepancia documentada. Tránsito conserva propiedad y posesión única; no está vendible ni duplica existencia.

| Comando / capacidad | Precondiciones y atomicidad | Resultado, fallo y corrección |
|---|---|---|
| CT1 publicar revisión / catalog.manage | Maestro y aprobación/versiones, sin convertir identidad; CM0 I→A→M→D si evidencia | Revisión efectiva auditada; conflicto rechaza. Precio/atributo nuevo no altera cotización aceptada |
| CT2 aprobar kit / catalog.manage + autoridad política | Grafo sin ciclos, unidades, componentes activos y compatibilidad evidenciada | Revisión sellada. Sustituto posterior exige revisión comercial nueva |
| WT1 solicitar/aprobar traslado / inventory.transfer.prepare/approve | Misma entidad, sitios elegibles, cantidad/serial libre; locks CM0 raíz+posiciones/serial ordenados | Reserva de traslado identificada consume disponible; no doble reserva de venta/traslado. Rechazo sin efectos |
| WT2 expedir / inventory.transfer.dispatch | Revisión aprobada, posesión origen y documento de traslado exigible; locks raíz/reserva/posiciones/serial | Origen→tránsito en una TX con movimiento/custodia/audit/hecho e intención durable si procede. Sin venta/COGS; costo pool no cambia |
| WT3 recibir parcial / inventory.transfer.receive | Expedida; recibido+discrepancia resuelta<=expedido, serial exactamente enviado | Tránsito→destino por recibido; diferencia queda pendiente, no ajuste de destino para cuadrar |
| WT4 resolver pérdida/daño / inventory.adjust.approve | Evidencia investigación, autoridad; identificar remanente en tránsito | Movimiento de pérdida o condición no vendible, evento de costo/Accounting distinto; reclamo al transportista no repone stock |
| WT5 cancelar/devolver / inventory.transfer.correct | Antes de expedición libera reserva; después requiere flujo físico compensatorio | No borrar despacho; preservar documentos, cantidades y serial. Reintento misma intención no duplica recepción |

Conservación por SKU: origen+tránsito+destino permanece constante salvo ajuste real aprobado; serial tiene una ubicación/condición por ciclo. Conteo bloquea/interseca posiciones según M03; recibir durante corte requiere versión compatible o rechazo. Devolución de cliente puede llegar a almacén distinto: referencia entrega/ciclo/costo original, cuarentena inicial y nueva posesión, no reventa automática. FIFO físico es selector explicable; no cambia promedio de medición. Recepción/transferencia con UNKNOWN conserva incertidumbre y bloquea cifras finales dependientes.

Evidencia futura B02–05/B09–11: carreras traslado/venta, conteo/recepción, serial duplicado, kit compartido, conversiones y pérdida en tránsito. Activación C03/C07/C13 por operación; ningún ensayo ejecutado aquí.
