---
name: caspro-economic-flow
description: "Trabajar flujos internos CasPro de Inventory, Treasury, Procurement o Sales y su coordinación; no contabilizar ni ejecutar acciones de proveedores."
---

# caspro-economic-flow

Consulta el [estado](../../../docs/review.md) para la fase vigente y aplica el [protocolo](../../../.ai/README.md#autoridad-y-autorización). Esta skill no concede permiso: implementación solo con fase habilitada y WO regenerada explícitamente autorizada, respetando todos sus límites. Preparar WOs también requiere autorización vigente. Docs poseen las reglas; ante contradicción, detener la parte afectada y escalar.

## Entrada y base local

Requiere dueño, comando/caso, entidad/actor como requisitos (sin datos privados en prompts), efecto esperado, spec y WO si se solicita implementar. Leer [invariantes](../../../docs/domain/invariants.md), secciones aplicables de [CM0](../../../docs/specs/cross-cutting/command-matrix.md#cm0), [hechos](../../../docs/specs/cross-cutting/economic-facts.md) y [gaps](../../../docs/roadmap/decisions-gaps.md). Elegir una rama; añadir participante solo por recurso/contrato realmente compartido.

| Rama | Contexto de tarea |
|---|---|
| Stock/costeo | [Inventory](../../../docs/domain/inventory-costing.md), [M03–M04](../../../docs/specs/milestones/inventory-deep.md) y ficha afectada |
| Dinero/cobro/refund | [Treasury](../../../docs/domain/treasury-finance.md), [SP2 dinero](../../../docs/specs/flows/sales-stock-treasury.md) |
| Conciliación bancaria | Treasury y [M06](../../../docs/specs/milestones/treasury-corporate-deep.md), secciones matching/corrección; C05 si formato/datos reales |
| Compra/recepción/obligación | [P2P](../../../docs/domain/procure-to-pay.md), [M05](../../../docs/specs/milestones/procurement-deep.md) |
| Venta/entrega/retorno | [SP2](../../../docs/specs/flows/sales-stock-treasury.md) y propietario de stock/dinero participante |
| B2B/crédito/sitio | [Dossier B2B](../../../docs/specs/flows/b2b-commercial-dossier.md), [ventas profesionales](../../../docs/specs/flows/professional-sales.md) y [construcción/activación del crédito](../../../docs/architecture/configuration-governance.md#crédito-b2b-y-extensibilidad); no leer D03 como opcionalidad universal |
| Pago por tercero/reembolso/estado de financiación | [Eventos y estados](../../../docs/specs/flows/financing-events-statements.md); Corporate posee acto/naturaleza, Treasury conserva su dinero y liquidación |

## Aplicar y escalar

Trazar entrada → dueño/guardas → recursos/transacción → hechos/corrección → evidencia según spec. No importar todo el circuito si solo cambia una rama. Leer [transacciones](../../../docs/architecture/transactions.md) ante deadlock/concurrencia y QA para evidencia. Seleccionar B02–06/B10 según efecto, C03–06/C13 cuando aplique; los IDs remiten al registro, no sustituyen su condición.

Cambiar comando/actor exige [IDs y conjunciones exactos](../../../docs/architecture/capability-registry.md). En stock, comprobar en el contrato de costeo la distinción promedio ponderado/pool y selección física FIFO; no inferir valoración contable de la secuencia física.

Si la solicitud viene de webhook o IA, leer el contrato de [asistencia](../../../docs/architecture/ai-assistance.md) o canal que produzca la observación. Distinguir candidato/observación de comando autorizado; no confirmar dinero por sugerencia. Ledger va a Accounting; acto/política de mutuo a compliance; publicación/email a external-effects. No reescribir reconocimiento/costeo/gates para arreglar un fallo.

## Salida / revisión

Análisis o delta autorizado con dueño/comando, contexto, invariantes enlazados, corrección y evidencia obtenida/pendiente. Dinero/stock exige reviewer independiente de integridad y especialista si cruza política; una prueba inexistente no cierra el mecanismo. Falta WO/autorización: detener implementación y entregar ruta/faltantes.
