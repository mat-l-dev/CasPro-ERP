# Orden de implementación futuro y dependencias

**Plan documental; 0 WOs ejecutadas. IMPLEMENTATION NOT AUTHORIZED.**

## Lectura del DAG

HARD exige contrato entregado/aceptado antes de integrar la WO consumidora; su cierre transitivo determina merge order. SOFT permite construir contra DTO sintético canónico, identificando integración pendiente. ACTIVATION_ONLY retiene el efecto real/reapertura, no construcción; puede volver sobre un checkpoint de recuperación y no forma parte del DAG de construcción. EVIDENCE_ONLY identifica ensayos/specs o equivalencia; no se trata como software previamente aprobado. Ningún stub demuestra el gate de su integración real.

Única raíz: [WO-M01-01](M01/WO-M01-01.md). IDs M01–M09 conservan tarjetas del [programa](../roadmap/program.md); no son orden lineal de ejecución. En cada nivel, solo owners/rutas disjuntos pueden trabajar en paralelo; un cambio de contrato público obliga revalidar consumidores.

## Capas topológicas HARD

Las capas expresan precedencia, no semanas, duración ni compromiso de entrega. No se inventan estimaciones de esfuerzo. Una WO puede avanzar cuando sus predecesores concretos estén aceptados sin esperar toda la capa.

| Capa | WOs elegibles después de predecesores |
|---|---|
| 1 | [WO-M01-01](M01/WO-M01-01.md) |
| 2 | [WO-M01-02](M01/WO-M01-02.md) |
| 3 | [WO-M01-03](M01/WO-M01-03.md) |
| 4 | [WO-M01-04](M01/WO-M01-04.md) |
| 5 | [WO-M01-05](M01/WO-M01-05.md) |
| 6 | [WO-M01-06](M01/WO-M01-06.md) |
| 7 | [WO-M01-07](M01/WO-M01-07.md) |
| 8 | [WO-M01-08](M01/WO-M01-08.md), [WO-M02-01](M02/WO-M02-01.md), [WO-M02-02](M02/WO-M02-02.md), [WO-M02-03](M02/WO-M02-03.md) |
| 9 | [WO-M03-01](M03/WO-M03-01.md), [WO-M09-01](M09/WO-M09-01.md) |
| 10 | [WO-M03-02](M03/WO-M03-02.md), [WO-M03-04](M03/WO-M03-04.md), [WO-M03-08](M03/WO-M03-08.md), [WO-M03-09](M03/WO-M03-09.md), [WO-M04-05](M04/WO-M04-05.md), [WO-M06-03](M06/WO-M06-03.md), [WO-M09-04](M09/WO-M09-04.md) |
| 11 | [WO-M03-03](M03/WO-M03-03.md), [WO-M03-05](M03/WO-M03-05.md), [WO-M03-06](M03/WO-M03-06.md), [WO-M03-07](M03/WO-M03-07.md), [WO-M03-10](M03/WO-M03-10.md), [WO-M05-02](M05/WO-M05-02.md), [WO-M07-01](M07/WO-M07-01.md), [WO-M07-17](M07/WO-M07-17.md) |
| 12 | [WO-M03-11](M03/WO-M03-11.md), [WO-M04-01](M04/WO-M04-01.md) |
| 13 | [WO-M04-02](M04/WO-M04-02.md), [WO-M04-04](M04/WO-M04-04.md) |
| 14 | [WO-M04-03](M04/WO-M04-03.md), [WO-M04-06](M04/WO-M04-06.md), [WO-M05-01](M05/WO-M05-01.md), [WO-M06-01](M06/WO-M06-01.md) |
| 15 | [WO-M04-07](M04/WO-M04-07.md), [WO-M05-03](M05/WO-M05-03.md), [WO-M05-04](M05/WO-M05-04.md), [WO-M06-02](M06/WO-M06-02.md), [WO-M06-05](M06/WO-M06-05.md), [WO-M06-06](M06/WO-M06-06.md), [WO-M06-07](M06/WO-M06-07.md) |
| 16 | [WO-M04-08](M04/WO-M04-08.md), [WO-M04-09](M04/WO-M04-09.md), [WO-M04-14](M04/WO-M04-14.md), [WO-M05-05](M05/WO-M05-05.md) |
| 17 | [WO-M04-10](M04/WO-M04-10.md), [WO-M04-13](M04/WO-M04-13.md), [WO-M04-15](M04/WO-M04-15.md), [WO-M05-06](M05/WO-M05-06.md), [WO-M05-07](M05/WO-M05-07.md), [WO-M06-08](M06/WO-M06-08.md), [WO-M06-10](M06/WO-M06-10.md), [WO-M07-02](M07/WO-M07-02.md) |
| 18 | [WO-M04-11](M04/WO-M04-11.md), [WO-M06-09](M06/WO-M06-09.md), [WO-M07-03](M07/WO-M07-03.md), [WO-M07-04](M07/WO-M07-04.md), [WO-M07-05](M07/WO-M07-05.md), [WO-M07-06](M07/WO-M07-06.md), [WO-M07-07](M07/WO-M07-07.md), [WO-M07-08](M07/WO-M07-08.md), [WO-M07-09](M07/WO-M07-09.md), [WO-M07-10](M07/WO-M07-10.md), [WO-M07-11](M07/WO-M07-11.md), [WO-M07-12](M07/WO-M07-12.md), [WO-M07-13](M07/WO-M07-13.md), [WO-M07-14](M07/WO-M07-14.md), [WO-M07-16](M07/WO-M07-16.md), [WO-M09-02](M09/WO-M09-02.md), [WO-M07-20](M07/WO-M07-20.md), [WO-M07-21](M07/WO-M07-21.md), [WO-M07-22](M07/WO-M07-22.md) |
| 19 | [WO-M04-12](M04/WO-M04-12.md), [WO-M06-04](M06/WO-M06-04.md), [WO-M07-15](M07/WO-M07-15.md), [WO-M07-18](M07/WO-M07-18.md), [WO-M09-03](M09/WO-M09-03.md) |
| 20 | [WO-M07-19](M07/WO-M07-19.md), [WO-M08-01](M08/WO-M08-01.md), [WO-M09-05](M09/WO-M09-05.md) |
| 21 | [WO-M08-02](M08/WO-M08-02.md) |
| 22 | [WO-M08-03](M08/WO-M08-03.md) |

## Dependencias no HARD

| WO | Tipo | Destino / condición |
|---|---|---|
| [WO-M01-08](M01/WO-M01-08.md) | ACTIVATION_ONLY | [WO-M03-03](M03/WO-M03-03.md); condición concreta en ficha |
| [WO-M02-01](M02/WO-M02-01.md) | SOFT | [WO-M03-01](M03/WO-M03-01.md); condición concreta en ficha |
| [WO-M02-02](M02/WO-M02-02.md) | SOFT | [WO-M03-01](M03/WO-M03-01.md); condición concreta en ficha |
| [WO-M03-04](M03/WO-M03-04.md) | SOFT | [WO-M03-09](M03/WO-M03-09.md); condición concreta en ficha |
| [WO-M04-02](M04/WO-M04-02.md) | SOFT | [WO-M04-15](M04/WO-M04-15.md); condición concreta en ficha |
| [WO-M04-03](M04/WO-M04-03.md) | ACTIVATION_ONLY | [WO-M04-04](M04/WO-M04-04.md); condición concreta en ficha |
| [WO-M04-11](M04/WO-M04-11.md) | SOFT | [WO-M06-04](M06/WO-M06-04.md); condición concreta en ficha |
| [WO-M04-11](M04/WO-M04-11.md) | ACTIVATION_ONLY | [WO-M06-03](M06/WO-M06-03.md); condición concreta en ficha |
| [WO-M04-12](M04/WO-M04-12.md) | SOFT | [WO-M05-01](M05/WO-M05-01.md), [WO-M04-13](M04/WO-M04-13.md); condición concreta en ficha |
| [WO-M04-13](M04/WO-M04-13.md) | SOFT | [WO-M04-12](M04/WO-M04-12.md); condición concreta en ficha |
| [WO-M06-01](M06/WO-M06-01.md) | SOFT | [WO-M05-05](M05/WO-M05-05.md); condición concreta en ficha |
| [WO-M06-03](M06/WO-M06-03.md) | SOFT | [WO-M06-04](M06/WO-M06-04.md); condición concreta en ficha |
| [WO-M06-05](M06/WO-M06-05.md) | SOFT | [WO-M05-05](M05/WO-M05-05.md), [WO-M06-02](M06/WO-M06-02.md); condición concreta en ficha |
| [WO-M06-06](M06/WO-M06-06.md) | SOFT | [WO-M05-05](M05/WO-M05-05.md); condición concreta en ficha |
| [WO-M06-09](M06/WO-M06-09.md) | SOFT | [WO-M06-02](M06/WO-M06-02.md); condición concreta en ficha |
| [WO-M07-02](M07/WO-M07-02.md) | SOFT | [WO-M06-07](M06/WO-M06-07.md), [WO-M06-10](M06/WO-M06-10.md), [WO-M06-05](M06/WO-M06-05.md); condición concreta en ficha |
| [WO-M07-11](M07/WO-M07-11.md) | SOFT | [WO-M04-15](M04/WO-M04-15.md); condición concreta en ficha |
| [WO-M07-13](M07/WO-M07-13.md) | SOFT | [WO-M09-02](M09/WO-M09-02.md); condición concreta en ficha |
| [WO-M07-13](M07/WO-M07-13.md) | ACTIVATION_ONLY | [WO-M09-02](M09/WO-M09-02.md); condición concreta en ficha |
| Todas | EVIDENCE_ONLY | QA/perfiles/casos/goldens canónicos; pruebas futuras, no resultados CasPro. B14 solo para reutilizar evidencia identificada. |

Audit/Identity se construyen con contexto/actor explícitos y pruebas sintéticas antes de Access; ninguna consulta/export sensible se habilita hasta [WO-M01-04](M01/WO-M01-04.md) y [WO-M01-07](M01/WO-M01-07.md). Los primeros maestros pueden prepararse con referencias documentales tipadas; ingestión/custodia real requiere [WO-M03-01](M03/WO-M03-01.md). Esas son condiciones de activación de entradas, no autorización para exponer un bypass temporal.

## Caminos y primeras slices

Cada lista implica el cierre transitivo HARD; no omite esos predecesores para aparentar una slice menor. Gates reales se suman por efecto. «Usable» describe aceptación futura en entorno sintético controlado; producción requiere autorización y C pertinentes.

| Slice / resultado | Camino de entrega y checkpoint |
|---|---|
| Primer uso interno | Runtime→Audit→Identity→Access→roles/config/privacidad; [WO-M02-03](M02/WO-M02-03.md) → [WO-M02-01](M02/WO-M02-01.md) → [WO-M02-02](M02/WO-M02-02.md) → [WO-M03-01](M03/WO-M03-01.md) → [WO-M03-04](M03/WO-M03-04.md) → [WO-M03-08](M03/WO-M03-08.md); alta sintética, existencia/costo y cobro sustentado consultables. [WO-M03-03](M03/WO-M03-03.md) antes de uso con recuperación comprometida. Sin depender del canal, compras, financiación o IA. |
| Primer B2C completo | [WO-M03-09](M03/WO-M03-09.md) → [WO-M03-10](M03/WO-M03-10.md) → [WO-M04-01](M04/WO-M04-01.md) → [WO-M04-02](M04/WO-M04-02.md) → [WO-M04-03](M04/WO-M04-03.md) → [WO-M04-04](M04/WO-M04-04.md) → [WO-M04-05](M04/WO-M04-05.md) → [WO-M04-06](M04/WO-M04-06.md) → [WO-M04-07](M04/WO-M04-07.md) (orden parcial: CPE puede preceder despacho; HP4 manda). CPE/entrega y restore/privacy forman checkpoint antes del efecto real; ATS positivo sigue B11 separado. |
| B2B profesional | Primer B2C → [WO-M04-09](M04/WO-M04-09.md) → [WO-M04-10](M04/WO-M04-10.md) → [WO-M04-11](M04/WO-M04-11.md) → [WO-M04-12](M04/WO-M04-12.md); [WO-M04-13](M04/WO-M04-13.md) paralelo al contrato cuando sus fuentes estén listas. [WO-M04-15](M04/WO-M04-15.md) después de B2B/Treasury, construido DISABLED. Firma/facultades antes del acto que las requiera; subcontrato integra M05. |
| P2P | [WO-M05-01](M05/WO-M05-01.md) → [WO-M05-04](M05/WO-M05-04.md) → [WO-M05-05](M05/WO-M05-05.md) con stock/dinero existentes; sourcing/importación/supplier return amplían sus propios ciclos. PO/factura no fabrican pago. |
| Control diario bancario | [WO-M03-08](M03/WO-M03-08.md) → [WO-M04-02](M04/WO-M04-02.md) → [WO-M06-01](M06/WO-M06-01.md) → [WO-M06-02](M06/WO-M06-02.md); conciliación puede preceder M05. Compra real se conecta después; no esperar financiación para conciliar. |
| Accounting / reporting | [WO-M07-01](M07/WO-M07-01.md) → [WO-M07-02](M07/WO-M07-02.md) → auxiliares por hecho/medición aplicable → [WO-M07-15](M07/WO-M07-15.md) → [WO-M08-01](M08/WO-M08-01.md) → [WO-M08-02](M08/WO-M08-02.md); paquete completo usa todos los auxiliares definidos con casos sintéticos aplicables/no aplicables justificados. IA/shadow/comparador no bloquean ledger manual/EEFF. |
| Tax | Datos fiscales CPE/AP/FX desde M04/M05 → [WO-M09-01](M09/WO-M09-01.md) → [WO-M09-02](M09/WO-M09-02.md) → [WO-M09-03](M09/WO-M09-03.md); [WO-M09-04](M09/WO-M09-04.md) se construye sin PreparedPackage previo y se une en [WO-M09-05](M09/WO-M09-05.md). No llamada SUNAT. C08 antes de hecho fiscal real, no al terminar UI M09. |

## Camino crítico estructural y merge order

El camino de mayor longitud HARD contiene **22 WOs**:

[WO-M01-01](M01/WO-M01-01.md) → [WO-M01-02](M01/WO-M01-02.md) → [WO-M01-03](M01/WO-M01-03.md) → [WO-M01-04](M01/WO-M01-04.md) → [WO-M01-05](M01/WO-M01-05.md) → [WO-M01-06](M01/WO-M01-06.md) → [WO-M01-07](M01/WO-M01-07.md) → [WO-M02-03](M02/WO-M02-03.md) → [WO-M03-01](M03/WO-M03-01.md) → [WO-M03-09](M03/WO-M03-09.md) → [WO-M03-10](M03/WO-M03-10.md) → [WO-M04-01](M04/WO-M04-01.md) → [WO-M04-02](M04/WO-M04-02.md) → [WO-M05-01](M05/WO-M05-01.md) → [WO-M05-04](M05/WO-M05-04.md) → [WO-M05-05](M05/WO-M05-05.md) → [WO-M07-02](M07/WO-M07-02.md) → [WO-M07-03](M07/WO-M07-03.md) → [WO-M07-15](M07/WO-M07-15.md) → [WO-M08-01](M08/WO-M08-01.md) → [WO-M08-02](M08/WO-M08-02.md) → [WO-M08-03](M08/WO-M08-03.md).

Es un límite de precedencia sin duraciones, no un calendario ni demostración de cuál tardará más. Para el primer B2C, el camino estructural hasta Case Flow contiene 15 WOs; hasta paquete NPIF completo, 21; hasta conciliación fiscal de casillas, 20. El reviewer debe comprobar estos cierres y que los branches de AI/shadow no condicionen el paquete oficial.

Merge futuro: orden topológico de la tabla, una PR por WO con rebase/revalidación contra main entonces aceptado; contratos públicos antes de consumidor, schema del owner serializado. Ninguna fusión está autorizada en esta regeneración. Primer lote recomendado: **[WO-M01-01](M01/WO-M01-01.md) y después [WO-M01-02](M01/WO-M01-02.md)**, exclusivamente runtime/entrega y sink de auditoría. Es pequeño, verificable y no habilita negocio; Access/Identity forman el siguiente checkpoint separado, no «todo M01» de una vez.

## Paralelismo seguro y schemas

| Lane | Primer schema / contrato | Regla de integración |
|---|---|---|
| Platform | [WO-M01-01](M01/WO-M01-01.md) | Ampliaciones solo esta unidad: no dos cambios simultáneos sobre el mismo schema; serializar merge y revalidar dependencias. |
| Audit | [WO-M01-02](M01/WO-M01-02.md) | Ampliaciones solo esta unidad: no dos cambios simultáneos sobre el mismo schema; serializar merge y revalidar dependencias. |
| Identity | [WO-M01-03](M01/WO-M01-03.md) | Ampliaciones solo esta unidad: no dos cambios simultáneos sobre el mismo schema; serializar merge y revalidar dependencias. |
| Access | [WO-M01-04](M01/WO-M01-04.md) | Ampliaciones [WO-M01-05](M01/WO-M01-05.md), [WO-M01-06](M01/WO-M01-06.md), [WO-M01-07](M01/WO-M01-07.md): no dos cambios simultáneos sobre el mismo schema; serializar merge y revalidar dependencias. |
| Operations | [WO-M01-08](M01/WO-M01-08.md) | Ampliaciones [WO-M03-03](M03/WO-M03-03.md): no dos cambios simultáneos sobre el mismo schema; serializar merge y revalidar dependencias. |
| Parties | [WO-M02-01](M02/WO-M02-01.md) | Ampliaciones solo esta unidad: no dos cambios simultáneos sobre el mismo schema; serializar merge y revalidar dependencias. |
| Catalog | [WO-M02-02](M02/WO-M02-02.md) | Ampliaciones solo esta unidad: no dos cambios simultáneos sobre el mismo schema; serializar merge y revalidar dependencias. |
| Organization | [WO-M02-03](M02/WO-M02-03.md) | Ampliaciones solo esta unidad: no dos cambios simultáneos sobre el mismo schema; serializar merge y revalidar dependencias. |
| Documents | [WO-M03-01](M03/WO-M03-01.md) | Ampliaciones [WO-M03-02](M03/WO-M03-02.md), [WO-M04-05](M04/WO-M04-05.md), [WO-M04-06](M04/WO-M04-06.md), [WO-M06-04](M06/WO-M06-04.md): no dos cambios simultáneos sobre el mismo schema; serializar merge y revalidar dependencias. |
| Inventory | [WO-M03-04](M03/WO-M03-04.md) | Ampliaciones [WO-M03-05](M03/WO-M03-05.md), [WO-M03-06](M03/WO-M03-06.md), [WO-M03-07](M03/WO-M03-07.md): no dos cambios simultáneos sobre el mismo schema; serializar merge y revalidar dependencias. |
| Treasury | [WO-M03-08](M03/WO-M03-08.md) | Ampliaciones [WO-M04-02](M04/WO-M04-02.md), [WO-M06-01](M06/WO-M06-01.md), [WO-M06-02](M06/WO-M06-02.md), [WO-M06-05](M06/WO-M06-05.md), [WO-M06-06](M06/WO-M06-06.md): no dos cambios simultáneos sobre el mismo schema; serializar merge y revalidar dependencias. |
| Integrations | [WO-M03-09](M03/WO-M03-09.md) | Ampliaciones [WO-M03-11](M03/WO-M03-11.md), [WO-M05-02](M05/WO-M05-02.md): no dos cambios simultáneos sobre el mismo schema; serializar merge y revalidar dependencias. |
| Sales | [WO-M03-10](M03/WO-M03-10.md) | Ampliaciones [WO-M04-01](M04/WO-M04-01.md), [WO-M04-03](M04/WO-M04-03.md), [WO-M04-04](M04/WO-M04-04.md), [WO-M04-09](M04/WO-M04-09.md), [WO-M04-10](M04/WO-M04-10.md), [WO-M04-11](M04/WO-M04-11.md), [WO-M04-12](M04/WO-M04-12.md), [WO-M04-13](M04/WO-M04-13.md), [WO-M04-14](M04/WO-M04-14.md), [WO-M04-15](M04/WO-M04-15.md): no dos cambios simultáneos sobre el mismo schema; serializar merge y revalidar dependencias. |
| UI projection | [WO-M04-07](M04/WO-M04-07.md) | Ampliaciones [WO-M04-08](M04/WO-M04-08.md): no dos cambios simultáneos sobre el mismo schema; serializar merge y revalidar dependencias. |
| Procurement | [WO-M05-01](M05/WO-M05-01.md) | Ampliaciones [WO-M05-03](M05/WO-M05-03.md), [WO-M05-04](M05/WO-M05-04.md), [WO-M05-05](M05/WO-M05-05.md), [WO-M05-06](M05/WO-M05-06.md), [WO-M05-07](M05/WO-M05-07.md), [WO-M06-10](M06/WO-M06-10.md): no dos cambios simultáneos sobre el mismo schema; serializar merge y revalidar dependencias. |
| Corporate | [WO-M06-03](M06/WO-M06-03.md) | Ampliaciones [WO-M06-07](M06/WO-M06-07.md), [WO-M06-08](M06/WO-M06-08.md), [WO-M06-09](M06/WO-M06-09.md): no dos cambios simultáneos sobre el mismo schema; serializar merge y revalidar dependencias. |
| Accounting | [WO-M07-01](M07/WO-M07-01.md) | Ampliaciones [WO-M07-02](M07/WO-M07-02.md), [WO-M07-03](M07/WO-M07-03.md), [WO-M07-04](M07/WO-M07-04.md), [WO-M07-05](M07/WO-M07-05.md), [WO-M07-06](M07/WO-M07-06.md), [WO-M07-07](M07/WO-M07-07.md), [WO-M07-08](M07/WO-M07-08.md), [WO-M07-09](M07/WO-M07-09.md), [WO-M07-10](M07/WO-M07-10.md), [WO-M07-11](M07/WO-M07-11.md), [WO-M07-12](M07/WO-M07-12.md), [WO-M07-13](M07/WO-M07-13.md), [WO-M07-14](M07/WO-M07-14.md), [WO-M07-15](M07/WO-M07-15.md), [WO-M07-16](M07/WO-M07-16.md), [WO-M07-18](M07/WO-M07-18.md), [WO-M07-19](M07/WO-M07-19.md), [WO-M08-01](M08/WO-M08-01.md), [WO-M08-02](M08/WO-M08-02.md), [WO-M08-03](M08/WO-M08-03.md), [WO-M07-20](M07/WO-M07-20.md), [WO-M07-21](M07/WO-M07-21.md), [WO-M07-22](M07/WO-M07-22.md): no dos cambios simultáneos sobre el mismo schema; serializar merge y revalidar dependencias. |
| AIService | [WO-M07-17](M07/WO-M07-17.md) | Ampliaciones solo esta unidad: no dos cambios simultáneos sobre el mismo schema; serializar merge y revalidar dependencias. |
| Tax | [WO-M09-01](M09/WO-M09-01.md) | Ampliaciones [WO-M09-02](M09/WO-M09-02.md), [WO-M09-03](M09/WO-M09-03.md), [WO-M09-04](M09/WO-M09-04.md), [WO-M09-05](M09/WO-M09-05.md): no dos cambios simultáneos sobre el mismo schema; serializar merge y revalidar dependencias. |

Organization y Access se inicializan juntos por contrato en [WO-M01-04](M01/WO-M01-04.md); [WO-M02-03](M02/WO-M02-03.md) solo añade Site, no recrea LegalEntity. El router Config y Case Flow no poseen schemas de hechos ajenos. Operations es capacidad técnica y Corporate capacidad de dominio; su agrupación física se resuelve según runtime B01 sin inventar app por nombre. Documents crea bytes privados/referencias una vez; consumidores añaden relaciones por contratos. Shadow usa DB/schema/credenciales independientes, no otra tabla oficial.

Cada primera migración declara constraints/FKs por entidad y permisos runtime/migrador; cada ampliación prueba clean install y upgrade desde release anterior con datos sintéticos y plan de rollback compatible. No SQL/migración ni dump se crea ahora. Shared solo primitives sin dueño empresarial; no adelantamiento de todos los schemas en foundations. Un coordinador escribe participantes mediante APIs públicas en la TX exterior, nunca importando modelos ajenos.

## Checkpoints por riesgo

- M01: aislamiento/último-admin/descriptores/privacidad antes de exponer entradas; no proxy de autorización desde is_staff.
- M03/M04: CM0, pool/promedio/UNKNOWN, race refund-despacho y barrier de restore; HTTP fuera de locks, UNKNOWN conciliado, stock positivo B11 retenido.
- M05/M06: N:M, landed cost tardío, dinero versus tercero, principal versus reembolso; no caja falsa ni PO pagable por sí sola.
- M07/M08: consumo activo sin versión en unicidad, corte completo, cuatro EEFF/notas equivalentes y aislamiento shadow; no post oficial de IA.
- M09: reglas por vigencia y prepared/filed/settled distintos; captura/rectificación/eficacia no se confunden.

## Gates y límites profesionales

**A0 / B16 / C13 / D6; todos B/C/D OPEN.** Las fichas asignan gates por efecto y momento, con responsable; el registro canónico posee clasificación/cierre. No se convierte una aprobación legal en propiedad de hechos ni un ensayo técnico en política aprobada.

| Clase / registro | Cobertura y límite |
|---|---|
| B01–B13, B15–B16 | Selección local en índice/ficha; mecanismo solo aceptable tras ensayo y evidencia del candidato real. |
| B14 | Condicional a invocar reutilización, en todas las fichas: manifiesto/claim/configuración/fixture y evaluación de impacto, nunca heredar PASS por nombre. |
| C01–C03 | Contador/mantenedor/owner validan marco, PCGE y medición real; construir auxiliares/versiones/fixtures no los cierra. |
| C04–C05/C13 | Propietario valida facultades/grants, maestros/cuentas/aprobadores y evidencia; confirmación de dinero no se infiere del canal. |
| C06–C09 | Legal/tax/contador validan acto/facultad/finalidad/CPE/régimen/obligación/beneficiario reales antes del efecto pertinente. |
| C10–C12 | Retención/backup/restore/entorno/destino/soporte real y autorización por efecto; inbound no autoriza outbound. |
| D01 | Construcción AIService/Accounting AI/shadow/comparador confirmada, activación OFF por propósito/presupuesto/evaluación. Banco IA opcional no es prerrequisito de conciliación. |
| D02 | Apertura/transición y datos preservados; nuevo marco completo solo tras trigger. |
| D03 | Crédito B2B construido DISABLED; COD/WhatsApp/servicio independiente/otras evoluciones no reciben WO obligatoria. |
| D04 | Sin grid/branding avanzado anticipado; UI accesible actual cubierta por tareas de cada consumidor. |
| D05 | KPIs adicionales diferidos; costo/margen básico y trazabilidad se entregan con fuentes y ledger/reportes, no se usa D05 para omitirlos. |
| D06 | Bandeja/Case Flow son proyecciones; sin SLA/workflow engine genérico. |

## Revalidación futura

Antes de cada ejecución autorizada: main aceptado actual, dependencias reales aceptadas, versiones/configuración/harness/trust/discovery efectivos cuando se usen, límites de datos/efectos y gates del caso. Verificar fuentes mutables de tooling/proveedor solo al depender de ellas. Si aparece regla semántica faltante, abrir amendment A para ese efecto y continuar solo lo independiente; no llamarlo watch item ni cerrar C por fixture.
