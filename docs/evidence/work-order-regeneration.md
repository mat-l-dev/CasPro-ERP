# Regeneración de Work Orders — expediente del autor

**READY FOR INDEPENDENT REVIEW. IMPLEMENTATION NOT AUTHORIZED.**

Este informe registra preparación documental, no aceptación independiente ni ejecución. El propietario encargó regenerar todo M01–M09 desde main final aceptado, con rama/commit/push y PR abierto. No se cambió arquitectura, gates, skills ni programa; ningún WO fue ejecutado. La [matriz previa](../work-orders/coverage.md) se escribió antes de las fichas individuales. Se aplicó caspro-work-order y la plantilla vigente; no se creó otra plantilla ni skill.

## A–F — Base, inventario y cobertura

| Campo | Resultado |
|---|---|
| A. Baseline verificada | HEAD `b27e5eeb280b8b654b18218a11181e9c4a8eb7b1`; tree `c0f314722f1d5fa5d2e36cb5b2aad7759710e6d8`; main == origin/main, limpio antes de la rama. PR8/PR9 MERGED. |
| B. Rama | `docs/regenerate-work-orders`, nueva desde esa baseline. |
| C. Inventario | Solo seis WO-SP2-01–06 en docs/history/work-orders-sp2.md; históricas/no ejecutables. Ninguna otra WO actual. |
| D. Supersesión | SUPERSEDED FOR CURRENT PLANNING; conceptos PARTIALLY_REUSABLE, nunca órdenes antiguas ejecutables. Se conserva íntegro el archivo histórico. |
| E. Hitos | M01: Runtime, access and recoverability; M02: Party and goods masters; M03: Operational stock, money and channel intake; M04: Safe first B2C sale; M05: Controlled Procure-to-Pay; M06: Treasury reconciliation and Corporate; M07: Accounting ledger and close; M08: Complete NPIF reporting; M09: Tax operations foundation. M04+ no renumera B2C; entrega profesional posterior y crédito confirmado OFF. |
| F. Cobertura | 89 filas canónicas: 87/87 con construcción confirmada mapeadas; COD/WhatsApp diferidas explícitamente. Suplementos runtime/privacidad/recuperación cubiertos. 0 capacidades confirmadas sin WO, 0 WOs huérfanas. [Matriz completa](../work-orders/coverage.md). |

## G–M — Descomposición y grafo

**G. Total: 84 WOs.** No se fijó cuota. Se separaron por ciclo/dueño/transacción/evidencia; se retuvo una unidad coordinada cuando dividirla produciría estado parcial inválido. Accounting tiene unidades distintas de devengo y prepago, FX y medición de instrumento, patrimonio y disclosure de relacionadas. Renta Procurement consume contrato Corporate existente; no adquiere su propiedad.

| H. Hito | WOs |
|---|---:|
| M01 | 8 |
| M02 | 3 |
| M03 | 11 |
| M04 | 15 |
| M05 | 7 |
| M06 | 10 |
| M07 | 22 |
| M08 | 3 |
| M09 | 5 |

| I. Responsable principal | WOs |
|---|---:|
| Platform | 1 |
| Audit | 1 |
| Identity | 1 |
| Access | 4 |
| Operations | 2 |
| Parties | 1 |
| Catalog | 1 |
| Organization | 1 |
| Documents | 5 |
| Inventory | 4 |
| Treasury | 6 |
| Integrations | 3 |
| Sales | 11 |
| UI projection | 2 |
| Procurement | 7 |
| Corporate | 4 |
| Accounting | 24 |
| AIService | 1 |
| Tax | 5 |

J/K. DAG de 84 nodos y **178 aristas HARD**, única raíz [WO-M01-01](../work-orders/M01/WO-M01-01.md); índice contiene predecesores inmediatos y cada ficha distingue HARD/SOFT/ACTIVATION_ONLY/EVIDENCE_ONLY. No ciclo HARD. Dependencias de activación de restore pueden volver sobre el checkpoint técnico, sin convertirse en ciclo de construcción. Primitivas de contrato aún no entregadas se prueban con DTO sintético, nunca con bypass temporal expuesto.

L. Paralelo solo tras HARD, con propietarios/archivos disjuntos. Maestros Parties/Catalog/Site después del bootstrap; Inventory y Treasury después de sus fuentes; M06 conciliación sin esperar M05; auxiliares contables separados después de ledger y fuentes propias; Tax perfil/mirror no esperan todo M08. Mismo schema exige merges serializados/revalidación.

M. Camino estructural más largo: **22 WOs**, sin duración ficticia. [DAG y capas completas](../work-orders/roadmap.md); Case Flow B2C tiene profundidad 15, paquete NPIF 21, conciliación de casillas 20. IA/shadow no condicionan libro manual ni cuatro EEFF oficiales.

## N–R — Slices

- N. Primer uso interno: bootstrap autorizado/contexto/privacidad → Parties/Catalog/Site → Documents → stock/costo y cobro sintéticos. No canal obligatorio; restore completo antes de uso que comprometa recuperación.
- O. B2C: inbox/propuesta → aceptación íntegra → cobro/aplicación/cobertura → despacho; CPE puede preceder despacho según oportunidad fiscal, y evidencia/entrega documental cierra recorrido. Gates de canal/publicación y recuperación no se confunden.
- P. B2B: B2C primero, luego dossier directo/OC opcional, cotización, contrato, fulfillment y sitio según caso. Crédito se construye después de B2B/Treasury y queda DISABLED; COD no se promueve.
- Q. Accounting/reporting: catálogo/política/perfil → interpretación/ledger → auxiliares aplicables → cierre/corte completo → cuatro EEFF/notas. G1–G7 se referencian como especificaciones de evidencia, incluyendo triggers de marco, no pruebas ejecutadas ni norma inventada.
- R. Tax: datos fiscales de origen desde CPE/Procurement/FX, perfil/reglas → determinaciones/SIRE → workspace/paquetes; mirror histórico independiente de paquete previo → casillas/revisión. Sin SUNAT ni pagos automáticos; C08 antes del efecto real dependiente.

## S–Y — Riesgos, gates y ownership

S. **A0 / B16 / C13 / D6**; todos B/C/D OPEN. B01–B13/B15–B16 aparecen por mecanismo/consumidor en fichas; B14 condicional a reutilización, sin heredar evidencia. Todos los C01–C13 tienen consumidores; D01/D03 distinguen construcción confirmada OFF, D02 preserva transición por trigger, D04/D05/D06 no crean grid/KPI/engine anticipado. [Mapa y momentos](../work-orders/roadmap.md).

T. Profesional: contador valida marco/estimaciones/PCGE/Tax; legal/profesional valida actos/facultades/requisitos/finalidad/retención según efecto; propietario valida datos/grants/política operacional y efectos. Preparador técnico no reemplaza ninguna autoridad. Inputs pendientes mantienen efecto desactivado, no ausencia ficticia de contrato.

U. Privacidad específica: [WO-M01-07](../work-orders/M01/WO-M01-07.md) Purpose/Context por dueño y DataRestriction Access; [WO-M03-02](../work-orders/M03/WO-M03-02.md) DataSubjectRequest Documents; [WO-M03-03](../work-orders/M03/WO-M03-03.md) PrivacyIncidentCase Operations y diario externo posterior al backup. Todas las lecturas/imports/derivados/exports/IA incorporan restricciones/finalidad. Regla privacy.context.prepare conserva conjunción exacta de capability explícita + autoridad de preparación de dominio resuelta por descriptor + configuration.prepare con mandato/delegación misma familia/entidad/P/scope/revisión/epoch/SoD. No rol informal ni herencia/wildcard. Documents custodia, Operations coordina, dueño ejecuta, responsable legal aprueba.

V. Efectos externos/infraestructura sensible planificados (reales OFF): WO-M03-03, WO-M03-09, WO-M03-11, WO-M04-06, WO-M04-14, WO-M05-02, WO-M06-04, WO-M07-17, WO-M07-18, WO-M07-19, WO-M08-03. Adapter, dirección/entorno, secreto por referencia, intención/outbox, I/O fuera de locks, UNKNOWN y conciliación se concretan en contrato local. Firma/correo/FX/Jumpseller/DeepSeek requieren mandatos separados; recording de filing o C40 no ejecuta el efecto registrado.

W. Escrituras con B03: WO-M01-02, WO-M01-04, WO-M01-05, WO-M01-06, WO-M01-07, WO-M02-01, WO-M02-02, WO-M02-03, WO-M03-01, WO-M03-02, WO-M03-04, WO-M03-05, WO-M03-06, WO-M03-07, WO-M03-08, WO-M03-09, WO-M03-10, WO-M03-11, WO-M04-01, WO-M04-02, WO-M04-03, WO-M04-04, WO-M04-06, WO-M04-09, WO-M04-10, WO-M04-11, WO-M04-12, WO-M04-13, WO-M04-14, WO-M04-15, WO-M05-01, WO-M05-02, WO-M05-03, WO-M05-04, WO-M05-05, WO-M05-06, WO-M05-07, WO-M06-01, WO-M06-02, WO-M06-03, WO-M06-04, WO-M06-05, WO-M06-06, WO-M06-07, WO-M06-08, WO-M06-10, WO-M07-01, WO-M07-02, WO-M07-03, WO-M07-04, WO-M07-05, WO-M07-06, WO-M07-07, WO-M07-08, WO-M07-09, WO-M07-10, WO-M07-11, WO-M07-12, WO-M07-13, WO-M07-14, WO-M07-15, WO-M07-16, WO-M07-17, WO-M07-18, WO-M07-19, WO-M09-01, WO-M09-02, WO-M09-03, WO-M09-04, WO-M09-05, WO-M07-20, WO-M07-21, WO-M07-22. Cada ficha identifica raíces y orden CM0, identidad natural/idempotencia/fingerprint, auditoría/rollback, revalidación y corrección. Las proyecciones conservan corte/membresía, no poseen estado empresarial. Ningún mock se presenta como evidencia de concurrencia PostgreSQL.

X. Schema/migración: primer owner/contrato y ampliaciones en [roadmap](../work-orders/roadmap.md). Runtime no crea todo el ERP; Organization/Access bootstrap una vez, Documents una vez, propietario extiende su schema. Queries/coordinadores no importan modelos ajenos. Clean/upgrade/rollback compatible y manifiesto son ensayos futuros; ninguna migración ejecutada/creada. Shadow DB/proceso/credenciales separados, sin permisos Core.

Y. [Mapa completo de supersesión](../work-orders/supersession.md): SP2-01→runtime/audit/recovery; 02→Identity/Access/roles/config/privacy; 03→Parties/Catalog/Sites; 04→stock/replay/transfer/count; 05→money/applications/payments/bank; 06→inbound/proposal/ATS. Historia intacta.

## Z–AB — Revisión adversarial y validación

Z. Nuevos A detectados por el autor: **0**. No se cerró gate por texto ni se convirtió una omisión semántica en watch item. Esta conclusión debe ser refutada por la revisión independiente del candidato.

AA. Autoevaluación documental del autor, **no segunda revisión independiente**. Se seleccionó al menos una ficha por hito y fronteras críticas adicionales. Resultado describe corrección/coherencia de la ficha, no evidencia de software.

| Muestra | Contraejemplo evaluado | Resultado documental |
|---|---|---|
| M01 WO-M01-02, WO-M01-07 | Audit antes de Access podría exponer lectura; purpose role informal podría conceder preparación | Activación de lectura/export condicionada expresamente a Access/privacidad; conjunción exacta, propiedad separada, no bypass |
| M02 WO-M02-02 | Kit padre+piezas duplica stock; precio actualizado altera venta | Catálogo no posee stock; snapshot y revisión conservados; import exige owner y contexto |
| M03 WO-M03-04, WO-M03-05, WO-M03-03, WO-M03-11 | FIFO convertido en PEPS; coste0; backup viejo recupera PII; PUT sin fence | Promedio/replay/UNKNOWN explícitos; diario completo y ambas barreras OFF; publicación positiva retenida B11 |
| M04 WO-M04-03, WO-M04-07, WO-M04-15 | Pago60/objetivo100 entrega parcial; nodo oculto filtra; crédito declarado opcional | HP1 exige100 antes de despacho; filtro previo a layout/conteos; crédito construido OFF; margen básico no se difiere D05 |
| M05 WO-M05-05, WO-M05-07 | PO10/recibo6/facturas4+4; flete tras stock0 | Remanente2 sin excepción/nueva recepción; landed cost coordina replay, no DAM→stock ni costo aduanero automático |
| M06 WO-M06-08, WO-M06-09, WO-M06-10 | Personal350 crea caja; +100/−100 omitido; Procurement posee contrato de sede | Sin caja ficticia; tres decisiones y manifiesto íntegro; contrato Corporate consumido, obligación Procurement |
| M07 WO-M07-02, WO-M07-15, WO-M07-18, WO-M07-19 | Nueva versión duplica componente; IA acepta→post; sombra escribe Core | Unicidad activa sin versión, close con corte; accept_draft AND prepare sin post; DB/proceso/credenciales aislados y sello ciego |
| M07 granularidad | Devengo/prepago, FX/instrumento, patrimonio/disclosure podrían aterrizar separadamente | Divididos en WOs independientes con mismas fuentes/owners; cierre depende de todos los auxiliares confirmados |
| M08 WO-M08-01, WO-M08-02, WO-M08-03 | Balance correcto con fuente omitida, PDF recalculado, shadow declarado segundo EEFF | Manifiestos/linaje, snapshot común, notas aplicables y comparator separado; aprobación profesional pendiente |
| M09 WO-M09-04, WO-M09-05 | Captura corregida es rectificatoria; latest filed es legal effective; delta culpa contador | Historia/revisión/eficacia distintas; soporte por mapping; revisión profesional sin envío ni inferencia de error |
| DAG / alcance | Reclamos esperando B2B, sitio esperando instalación, Tax esperando notas, financiación esperando banco | HARD artificiales retirados; fuentes estrictas/soft por consumidor; grafo recalculado |
| Autoridad global | Merge/PASS o viejo prompt PR8/PR9 habilita ejecución | Current status nuevo, antecedentes conservados; 84 PREPARED, ninguna ejecutable; PR nuevo abierto |

AB. Validación estática final se registra tras ejecutar los controles documentales: IDs/índice, cobertura, fuentes/links/anchors, capabilities/gates, DAG, campos del template, alcance de diff y preservación histórica. Pruebas de aplicación, builds, Docker, migraciones, providers y WOs: **NOT EXECUTED / NOT AUTHORIZED**. No se invoca evidencia funcional previa; B14 no se cierra.

Resultados obtenidos sobre los archivos candidatos: 84 fichas / 84 entradas únicas del índice; 178 aristas HARD / 84 nodos visitados sin ciclo; 89 filas de cobertura, 87 cubiertas y 2 diferidas; núcleo obligatorio presente en las 84 fichas. 2480 enlaces locales/anchors comprobados sin destino ausente, 371 referencias literales de capability sin ID desconocido ni alias retirado y 572 referencias locales de gate válidas. El validador distingue gates de recursos CM0 como C70/D80. Recuento del registro: B16/C13/D6, clase A0 conservada; sin modificación del registro. Diff documental: 94 archivos previstos, 0 rutas inesperadas. Comparación Git de contratos canónicos, agentes/skills/plantilla e histórico SP2: sin cambios. Main remoto revalidado, sin avance. Diff whitespace y estado remoto final se verifican al publicar; resultados funcionales siguen pendientes.

## AC–AI — Entrega y límites

AC. Archivos: 84 fichas Markdown M01–M09; cuatro mapas (index/coverage/roadmap/supersession) en docs/work-orders; este expediente; modificaciones de descubribilidad/estado únicamente en docs/review.md, docs/index.md, docs/specs/index.md, docs/history/index.md y docs/evidence/index.md. Total esperado: **94 archivos**, solo Markdown. Ninguna fuente semántica, AGENTS, skill o plantilla modificada.

AD–AG. Commits, HEAD/tree final y PR se verifican después de materializar/publicar el candidato y se reportan en Git/PR y respuesta final; este documento no se autorreferencia con un SHA imposible de contener. Baseline exacta en A. PR contra main debe permanecer OPEN, sin merge y sin aceptación propia. La revisión independiente deberá fijar el HEAD/tree realmente revisado.

Publicación verificada: [PR #10](https://github.com/mat-l-dev/CasPro-ERP/pull/10), OPEN contra main, misma rama. Commit documental de generación `01d13dbde7e7062ad38e91b805481cb5f1e15bf1`, tree `ec8fb4a8b89620dd3aa1bf92af07b82857808ba8`; el cierre posterior solo registra esta publicación/estado. `git diff --cached --check` limpio antes de publicar. La PR y respuesta final identifican el candidato final tras ese cierre; no merge, aceptación independiente ni ejecución. Índice, 84 fichas, cobertura, DAG y supersesión no cambian en el cierre de publicación.

AH. Primer lote futuro recomendado: [WO-M01-01](../work-orders/M01/WO-M01-01.md) y luego [WO-M01-02](../work-orders/M01/WO-M01-02.md), limitado a runtime/entrega y sink append-only con lectura sensible OFF. Recomendación no es autorización; no ejecutar todo M01.

AI. Preguntas al propietario: **0**. Ningún dato real solicitado. Validaciones profesionales continúan bajo C/D existentes; si una futura respuesta cambia semántica, requiere amendment, no código unilateral.

## AJ — Veredicto del autor

**PASS — CURRENT CASPRO WORK ORDERS REGENERATED**
**READY FOR INDEPENDENT REVIEW**

**IMPLEMENTATION NOT AUTHORIZED**

El PASS es de preparación documental del autor. No se declara aceptación del conjunto ni implementación lista para ejecución. La misión termina con el nuevo PR abierto.
