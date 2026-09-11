# Auditoría de repositorios — Astra 2026-09-11

Estado: investigación documental en curso; hallazgos comprobados a continuación. La aceptación del programa se decide en [review](../review.md), no mediante este inventario. No hay autorización de implementación.

## CasPro

Inicio: árbol limpio, rama `docs/grand-master-program`, HEAD y seguimiento remoto `cd01a361f3491dc7114988f670b098eb3fc06bb0`; base `main`/`origin/main` `5c925e2acb1487c68dab2738e969cef6afe33539`. [PR #2](https://github.com/mat-l-dev/CasPro-ERP/pull/2) abierta, sin merge. Diferencia inicial: 34 archivos Markdown, 1,027 inserciones y 45 eliminaciones. El árbol visible contiene raíz documental, `.ai`, `docs` y `.git`; no existe código funcional de CasPro que permita acreditar RLS, concurrencia o reportes ejecutables.

La auditoría distingue lectura de archivos, comparación de cambios, investigación externa y prueba ejecutada. “PASS documental” histórico no prueba readiness de módulos futuros ni aceptación independiente del nuevo programa.

## Wbpro: procedencia y protección

Baseline canónica autorizada: **`5cc50696d896a35c12875dfb530c6ccb8d30dd84`**. Todas las consultas de baseline usan ese SHA, no “HEAD actual” como sustituto. Al comenzar esta revisión autorizada: 73 archivos modificados, 9 no seguidos; diff seguido 5,267 inserciones y 865 eliminaciones. Los cambios conocidos no bloquean la investigación.

Se conservó fuera de Wbpro un manifiesto de hashes de 643 archivos seguidos/no ignorados y su estado Git para detectar cambios durante la revisión. No se copiaron expedientes privados al repositorio CasPro. Quedan excluidos `archive`, `15-history`, legacy y Webrax. No se ejecutan tests, aplicación, migraciones, formateadores, checkout, stash, reset, clean, commit ni ninguna escritura en Wbpro.

| Etiqueta | Autoridad y uso |
|---|---|
| `COMMITTED WBPRO` | Código/documentación del SHA canónico; evidencia histórica interna, no aprobación CasPro |
| `UNCOMMITTED WBPRO` | WORKING-TREE / UNCOMMITTED EVIDENCE; candidato **NON-AUTHORITATIVE** hasta corroboración |
| `EXTERNAL VERIFIED SOURCE` | Fuente primaria actual leída y citada; su alcance manda sobre una interpretación heredada |
| `CASPRO DECISION` | Decisión actual identificada en su fuente local; distinguir principio aceptado, diseño candidato y política pendiente |

Precedencia técnica de transferencia: fuente externa verificada > decisión CasPro actual > Wbpro committed > Wbpro uncommitted. Una fuente técnica no amplía el alcance autorizado por el propietario. Contradicciones se registran, no se resuelven escogiendo silenciosamente el working tree. Hallazgo solo uncommitted conserva RESEARCH AGAIN/PENDING VALIDATION; no entra como regla aprobada.

## Código selectivamente examinado y contraejemplos

| Procedencia / archivo y símbolo | Evidencia observable | Resultado CasPro |
|---|---|---|
| COMMITTED WBPRO y comparación UNCOMMITTED; `src/wbpro/modules/inventory/services.py`, `_entry_value`, `_locked_balance`, `_apply_entry_to_balance`, `_apply_exit_to_balance` | Cantidad/valor bajo lock y promedio con Decimal; saldo se inicializa en cero. Salida usa tasa redondeada, luego fuerza valor cero al agotar cantidad | ADAPT atomicidad; REJECT cero como representación de coste desconocido. Contraejemplo estático con escala observada de seis decimales: Q=30,000,V=1,tasa redondeada 0.000033; salida total=0.99 y valor final forzado a cero, perdiendo 0.01 de la ecuación del movimiento. CasPro exige que última salida consuma exactamente V. No se afirma reproducción ejecutada en Wbpro |
| UNCOMMITTED WBPRO; `treasury/services.py`, `settled_amount_for_document` | Consulta suma aplicaciones positivas; su propio contrato advierte que un contramovimiento de devolución no las reduce y que no toma locks | NON-AUTHORITATIVE como técnica transferible; sí aporta un contraejemplo de diseño. No copiar autorización de entrega basada en suma histórica. Treasury CasPro conserva aplicaciones netas y decisión coordinada con Sales |
| UNCOMMITTED WBPRO; `sales/services.py`, guarda de `create_dispatch` | Consulta Treasury dentro del lock de venta y compara valor entregado+solicitado; exige expediente preparado de CPE | REJECT como equivalente de HP1: CasPro exige **pedido íntegramente pagado antes de cualquier parcial**. Un lock Sales por sí solo no excluye un refund Treasury. Un expediente preparado no acredita emisión externa o cumplimiento de oportunidad legal |
| COMMITTED WBPRO; `docs/06-corporate-legal/partes-relacionadas-y-mutuo.md` | Afirma conclusiones de control, partes relacionadas, financiación gratis y marco aplicable usando hechos propios | REJECT conclusiones automáticas; el expediente CasPro necesita hechos acreditados y validación profesional temprana |
| COMMITTED/UNCOMMITTED; `docs/04-accounting/marco-contable.md` | Working tree agrega ausencia de runtime/puente externo, sin corregir premisas regulatorias heredadas | Contradicción con aspiración de EEFF internos CasPro; no importar su bridge como destino. Revalidar elegibilidad y contenido NPIF |
| UNCOMMITTED; `docs/07-functional-modules/spec-contabilidad.md`, `spec-tesoreria.md` y research ERP 2026-09-09 no seguido | Cockpit, drillback, conciliación y correcciones en revisión | ADAPT solo después de investigación primaria y decisión CasPro. No importar estado IN_REVIEW como aprobación |

El defecto de residuo es un **contraejemplo aritmético al diseño observado**, condicionado a escalas/valores admitidos, no una afirmación de pérdida productiva ocurrida. La comparación no convierte auditoría selectiva en revisión de las 643 rutas ni en certificación de Wbpro. La extracción previa que llamó a todos los documentos “actuales” sin separar commit/working tree queda corregida por este contrato y por [su matriz](wbpro-knowledge.md).

La [auditoría pcge-peru](pcge-code-audit.md) tiene identidad, prueba, límites y adapter propuesto separados. Sus pruebas externas no autorizan código CasPro.
