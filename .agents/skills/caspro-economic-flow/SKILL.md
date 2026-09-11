---
name: caspro-economic-flow
description: "Trabajar flujos internos CasPro de Inventory, Treasury, Procurement o Sales y su coordinación; no contabilizar ni ejecutar acciones de proveedores."
---

# caspro-economic-flow

Lee el [protocolo](../../../.ai/README.md) y el [estado](../../../docs/review.md) si no están en contexto. Esta skill no concede permiso: implementación requiere WO regenerada y autorización explícita; hoy solo análisis/documentación del alcance encargado. No generar WOs reales en la misión de agentes. Docs poseen las reglas; ante contradicción detener el efecto afectado y escalar, sin editar el contrato silenciosamente.

## Entrada y base local

Requiere dueño, comando/caso, entidad/actor como requisitos (sin datos privados en prompts), efecto esperado, spec y WO si se solicita implementar. Leer [invariantes](../../../docs/domain/invariants.md), secciones aplicables de [CM0](../../../docs/specs/cross-cutting/command-matrix.md#cm0), [hechos](../../../docs/specs/cross-cutting/economic-facts.md) y [gaps](../../../docs/roadmap/decisions-gaps.md). Elegir una rama; añadir participante solo por recurso/contrato realmente compartido.

| Rama | Contexto de tarea |
|---|---|
| Stock/costeo | [Inventory](../../../docs/domain/inventory-costing.md), [M03–M04](../../../docs/specs/milestones/inventory-deep.md) y ficha afectada |
| Dinero/cobro/refund | [Treasury](../../../docs/domain/treasury-finance.md), [SP2 dinero](../../../docs/specs/flows/sales-stock-treasury.md) |
| Conciliación bancaria | Treasury y [M06](../../../docs/specs/milestones/treasury-corporate-deep.md), secciones matching/corrección; C05 si formato/datos reales |
| Compra/recepción/obligación | [P2P](../../../docs/domain/procure-to-pay.md), [M05](../../../docs/specs/milestones/procurement-deep.md) |
| Venta/entrega/retorno | [SP2](../../../docs/specs/flows/sales-stock-treasury.md) y propietario de stock/dinero participante |

## Aplicar y escalar

Trazar entrada → dueño/guardas → recursos/transacción → hechos/corrección → evidencia según spec. No importar todo el circuito si solo cambia una rama. Leer [transacciones](../../../docs/architecture/transactions.md) ante deadlock/concurrencia y QA para evidencia. Seleccionar B02–06/B10 según efecto, C03–06/C13 cuando aplique; los IDs remiten al registro, no sustituyen su condición.

Si la solicitud viene de webhook o IA, leer el contrato de [asistencia](../../../docs/architecture/ai-assistance.md) o canal que produzca la observación. Distinguir candidato/observación de comando autorizado; no confirmar dinero por sugerencia. Ledger va a Accounting; acto/política de mutuo a compliance; publicación/email a external-effects. No reescribir reconocimiento/costeo/gates para arreglar un fallo.

## Salida / revisión

Análisis o delta autorizado con dueño/comando, contexto, invariantes enlazados, corrección y evidencia obtenida/pendiente. Dinero/stock exige reviewer independiente de integridad y especialista si cruza política; una prueba inexistente no cierra el mecanismo. Falta WO/autorización: detener implementación y entregar ruta/faltantes.
