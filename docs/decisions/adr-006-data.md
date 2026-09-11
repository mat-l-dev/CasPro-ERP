# ADR-006 — Primitivas exactas e identidad proporcional

Fecha: 2026-09-10. **Estado autoritativo por alcance.** ACCEPTED acepta el contrato de diseño, no acredita ejecución ni aprobación empresarial.

| Alcance | Estado | Condición o límite |
|---|---|---|
| Decimal/numeric, unidades/moneda, fechas distintas e identidad proporcional | ACCEPTED | La exactitud exige controlar las operaciones; el identificador no concede acceso |
| Precisión 38, escalas candidatas, HALF_UP y traducción física de restricciones | PROVISIONAL | Justificar rangos/acumulaciones/cuantización y política; demostrar extremos, residuos y pertenencia en una fase ejecutable autorizada |

## Context

Dinero, coste, cantidad, fechas y números documentales tienen semánticas distintas. Un único tipo/ID/booleano para todo elimina información necesaria.

## Decision

Decimal/numeric, unidades y moneda explícitas; estados por agregado; bigint interno y UUIDv7 público donde circule una raíz; historia económica reversible y maestros versionables. [Data](../architecture/data.md) contiene precisión, temporalidad y reglas de persistencia.

## Alternatives

Float pierde exactitud; UUID para cada fila añade coste sin consumidor; JSON universal pierde restricciones; append-only universal impide purgar datos transitorios legítimamente.

## Consequences

Las escalas/políticas comerciales candidatas deben contrastarse al especificar operaciones, sin convertirse en normas fiscales. Relaciones compuestas y rangos físicos requieren validación posterior. Fuente técnica de UUID: [S03](../research/technical-sources.md); reglas empresariales: [invariantes](../domain/invariants.md).
