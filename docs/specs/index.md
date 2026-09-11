# Deep specs y readiness documental

Propietario: Architecture con dueños de dominio. Este archivo conserva la matriz de readiness con la que M01–M09 se presentaron a revisión; la aceptación independiente posterior del freeze se registra únicamente en [review](../review.md), y [gaps](../roadmap/decisions-gaps.md) conserva los pendientes. Las etiquetas READY_FOR_FREEZE_REVIEW siguientes describen el candidato revisado, no una aceptación todavía pendiente ni evidencia de software, políticas reales aprobadas o permiso de implementación.

## Matriz de cobertura y readiness

| Hito | Readiness | Contrato local profundo | Gates pertinentes del registro |
|---|---|---|---|
| M01 | **READY_FOR_FREEZE_REVIEW** | [Runtime/access/audit/operations](milestones/runtime-masters.md) | A0; B01–04/B10/B13–15; C10/C12/C13 |
| M02 | **READY_FOR_FREEZE_REVIEW** | [Maestros/importación](milestones/runtime-masters.md) | A0; B02–04/B09/B10/B15; C03/C13 |
| M03 | **READY_FOR_FREEZE_REVIEW** | [Inventory](milestones/inventory-deep.md), [Treasury SP2](flows/sales-stock-treasury.md), [canal](flows/jumpseller-external-work.md) | A0; B02–06/B09–12/B15; C03/C05/C11/C13; D05 |
| M04 | **READY_FOR_FREEZE_REVIEW** | [B2C](milestones/inventory-deep.md), [CPE](flows/cpe-document-delivery.md), [hechos](cross-cutting/economic-facts.md) | A0; B02–05/B09–12; C03/C05/C07/C11; D05 |
| M05 | **READY_FOR_FREEZE_REVIEW** | [Procure-to-Pay](milestones/procurement-deep.md) | A0; B02–06/B09/B10; C03–05/C07/C08/C13 |
| M06 | **READY_FOR_FREEZE_REVIEW** | [Treasury/Corporate](milestones/treasury-corporate-deep.md) | A0; B02–04/B06/B09/B10/B12; C05/C06/C09; D01 con B16 solo si piloto |
| M07 | **READY_FOR_FREEZE_REVIEW** | [Accounting](milestones/accounting-deep.md), [NPIF](../accounting/npif-policy-catalog.md) | A0; B02–05/B07; C01–03/C06/C08 cuando aplique; D02 |
| M08 | **READY_FOR_FREEZE_REVIEW** | [Paquete financiero/G1–G7](acceptance/reporting-goldens.md) | A0; B02/B07–10/B12–15; C01–03/C10/C12; D02 |
| M09 | **READY_FOR_FREEZE_REVIEW** | [Tax Perú](milestones/tax-deep.md) | A0; B02–04/B07/B08/B10/B12; C07–09 y C06 si financiación; D02 |

B14 (equivalencia de evidencia), B02 (acceso de nuevas entradas), B03 cuando haya efecto crítico y C10/C13 antes de producción se aplican transversalmente aunque una fila destaque otros gates. D03/D04/D06 solo se abren por su trigger; no bloquean estos hitos. Gates compartidos se cuentan una vez en gaps. C06 precede a cualquier financiación real, aunque ocurra antes de M06; sin esa activación no bloquea otros hitos.

Las nueve filas tienen entradas/salidas, propietarios, estados/comandos, guardas, atomicidad, acceso, corrección/replay, evidencia, UX y aceptación futura en sus fuentes. El [contrato de hechos](cross-cutting/economic-facts.md) extiende CM0 para P2P, conciliación, valoración, cortes y libros. IDs de comandos no son clases/tablas anticipadas. El [memo UX](../evidence/ux-reconciliation.md) resuelve DDR-01–12 sin crear otra spec.

## Criterios de revisión independiente

1. Un dueño por hecho/estado; referencias y autorización conservan entidad en todos los caminos.
2. Los productores anteriores a M07 preservan hechos/componentes y completitud; Accounting no reconstruye historia desde estado mutable ni la consume dos veces.
3. Marco, catálogo, plan aplicado, política y fuente/edición/vigencia son conceptos distintos; PCGE no decide reconocimiento.
4. Correcciones tienen desenlace explícito: refund/despacho, pago/cambio de proveedor, factura/recepción, late cost/cierre, posting/cierre y restore/replay.
5. No hay incógnita A sin resolver. Toda B tiene hipótesis/ensayo/pase/fallo/owner; C identifica función y momento; D tiene trigger. Una política real fuera de superficie tipada requiere amendment.
6. G1 prueba documentalmente hecho→interpretación→posting→mayor→mapping→valor de los cuatro estados y notas, sin doble conteo, plug ni linaje inventado; B07/B08 siguen sin ejecutar.
7. UI respeta estados/autoridad del dueño, incertidumbre y PREPARE ≠ EXECUTE; accesibilidad, teclas y rendimiento no se declaran probados.
8. Obligatoriedad profesional/regulatoria se resuelve antes de la activación pertinente; no espera a que exista su interfaz ni bloquea sin causa toda construcción.
9. Reviewer separado usa identidad exacta y registra PASS/FAIL con evidencia; el autor no se acepta a sí mismo.

## Handoff posterior

La secuencia obligatoria es aceptación independiente del freeze → investigación dedicada de skills útiles → regeneración de WOs acotadas → autorización explícita de implementación. Las [seis WOs SP2](../history/work-orders-sp2.md) son insumos históricos NEEDS REGENERATION AFTER FREEZE: incorporar hechos tempranos, pool/revisiones, CM0 extendido, CPE, UX y gates locales antes de encargarlas.

Contexto futuro: AGENTS → review → tarjeta de hito → spec y dependencias concretas → gates/perfil de evidencia. Sol orquesta; implementador y reviewer trabajan separados; Astra revisa arquitectura, dinero/stock, Accounting/Tax/Legal, seguridad o contraejemplo transversal. Ninguna etiqueta de readiness ni skill autoriza funciones, migraciones, pruebas o despliegues.
