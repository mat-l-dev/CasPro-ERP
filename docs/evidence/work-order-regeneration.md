# Regeneración de Work Orders — expediente del autor

**Expediente histórico del autor. IMPLEMENTATION NOT AUTHORIZED.** La aceptación independiente posterior comunicada por el propietario está registrada en [review](../review.md): PASS — CURRENT CASPRO WORK ORDER SET ACCEPTED; candidato `9fadf6569e98298d7db3a5fbd6bc53575adf4ff7`, tree `9189869d1495dd25a5d2d68d6874990348053618`; F-WO-01/F-WO-02 PASS. Las 84 WOs cubren el alcance anterior a Marketing. Los estados pendientes y REQUEST CHANGES que siguen pertenecen al expediente histórico; no se reescriben como autoaceptación.

Este informe registra preparación documental, no aceptación independiente ni ejecución. El propietario encargó regenerar todo M01–M09 desde main final aceptado, con rama/commit/push y PR abierto. No se cambió arquitectura, gates, skills ni programa; ningún WO fue ejecutado. La [matriz previa](../work-orders/coverage.md) se escribió antes de las fichas individuales. Se aplicó caspro-work-order y la plantilla vigente; no se creó otra plantilla ni skill.

## Independent review remediation — PR #10

Revisión independiente comunicada por el propietario: **REQUEST CHANGES — TWO SURGICAL WO CORRECTIONS REQUIRED**, candidato `3ef9bc740dcde9f57236229ce24bfa32b1cbcf84`, tree `445231128b9419223b1ef9b36a1cfd8867bbc9c2`. Rama local/remota `docs/regenerate-work-orders`, PR #10 OPEN/no merged, árbol limpio y sin divergencia al comenzar. Encargo exclusivamente F-WO-01/F-WO-02 y búsqueda exhaustiva de esas clases; no regeneración del conjunto.

Estado final del autor: **F-WO-01 / F-WO-02 FIXED_PENDING_INDEPENDENT_RE_REVIEW.** No aceptación independiente de las correcciones. La revisión inicial y el expediente de generación se conservan.

### F-WO-01 — Semántica de gates

Causa: trasladar etiquetas generales («aprobación», «pago», «tax», «automatización») a gates cuyo owner/efecto es más específico. La existencia literal del ID no prueba pertinencia semántica.

[WO-M04-15](../work-orders/M04/WO-M04-15.md): se retira C04; C05 queda limitado a dinero/aplicaciones Treasury, C13 a grants/aprobadores/POL-08 reales. C07/C08 se explicitan **solo si** la operación requiere CPE o tratamiento fiscal; D03 conserva propietario canónico Product/Architecture y activación con POL-08 versionada/aprobada, permisos/pruebas/autorización. Sales sigue poseyendo crédito/exposición/cobranza. OFF impide nueva exposición, no cobrar deuda existente; COD sigue diferido.

Inventario exhaustivo de las 84 fichas: **450 pares WO→C/D**, incluyendo tabla local y referencias condicionales fuera de ella; **185 filas locales** y 265 pares adicionales. La matriz interna registra WO, ID/clase, owner/significado canónico, razón/efecto local, estado y acción. Se contrastó con [gates y extensiones aceptadas](../roadmap/decisions-gaps.md), contrato local de cada efecto y [privacidad](../security/personal-data-lifecycle.md), sin cambios canónicos. Recursos CM0 C70/D80 no se cuentan como gates; D04 no tiene referencia local y permanece diferido.

| Gate | Filas locales antes | Otros pares condicionales/exclusiones antes |
|---|---:|---:|
| C01 | 29 | 0 |
| C02 | 5 | 0 |
| C03 | 15 | 0 |
| C04 | 9 | 0 |
| C05 | 13 | 0 |
| C06 | 23 | 60 |
| C07 | 8 | 0 |
| C08 | 26 | 0 |
| C09 | 1 | 0 |
| C10 | 13 | 71 |
| C11 | 13 | 70 |
| C12 | 2 | 0 |
| C13 | 20 | 63 |
| D01 | 5 | 0 |
| D02 | 1 | 0 |
| D03 | 1 | 0 |
| D05 | 0 | 1 |
| D06 | 1 | 0 |

Las referencias transversales C06/C10/C11/C13 dicen «tratamiento real ... cuando corresponda»: son **CONDITIONAL_BUT_VALID**, no gates generales de construir cada módulo. C06 retiene autoridad/finalidad legal concreta; C10 conservación/recuperación; C11 solo encargado/transferencia/efecto externo real; C13 identidad/grants/datos reales. Sin ese efecto, no se usan por analogía. Por ejemplo, el C11 condicional de privacidad en Tax no impide preparar/exportar localmente un paquete sin transporte. D05 fuera de tabla es una exclusión que preserva margen básico, no gate del margen.

| Clasificación | Antes | Después |
|---|---:|---:|
| VALID | 169 | 172 |
| INVALID | 5 | 0 |
| NEEDS_NARROWING | 11 | 0 |
| CONDITIONAL_BUT_VALID | 265 | 276 |
| Total pares | 450 | 448 |

Después: **182 filas locales**, 266 pares adicionales; diferencia por cinco asignaciones retiradas y C07/C08 condicionales incorporados a crédito. C11 de WO-M09-03 permanece únicamente como referencia de privacidad condicional, no en su tabla local. Los conteos son de referencias documentales, no cambios al registro global.

| Asignación INVALID antes | Corrección / fundamento |
|---|---|
| [WO-M04-15](../work-orders/M04/WO-M04-15.md) → C04 | Retirar de tabla/índice: Sales crédito no ejecuta conformidad, payability ni aprobación de compra Procurement. |
| [WO-M07-16](../work-orders/M07/WO-M07-16.md) → D01 | Retirar de tabla/índice: Plantillas/reglas/recurrencia determinísticas a draft no activan IA; mandato auto-post sigue separado y OFF. |
| [WO-M07-09](../work-orders/M07/WO-M07-09.md) → C08 | Retirar de tabla/índice: Selección/reexpresión FX financiera sigue C01; selección fiscal C08 pertenece al consumidor Tax, no a este cálculo Accounting. |
| [WO-M07-22](../work-orders/M07/WO-M07-22.md) → C08 | Retirar de tabla/índice: Disclosure financiero de relacionadas no realiza evaluación tributaria 32-A, expresamente separada. |
| [WO-M09-03](../work-orders/M09/WO-M09-03.md) → C11 | Retirar de tabla/índice: Workspace prepara/exporta paquete y registra evidencia externa; no contiene transporte ni ejecución SUNAT. |

Las cuatro últimas son hallazgos adicionales de la **misma clase F-WO-01**, no nuevos A. D01 no condiciona JournalTemplates determinísticos; auto-post sigue OFF y sujeto a su mandato existente. Quitar C08 de FX/disclosure no elimina C01 ni la evaluación fiscal separada de Tax. Quitar C11 del workspace no habilita SUNAT.

| Asignación NEEDS_NARROWING antes | Precisión necesaria incorporada |
|---|---|
| [WO-M04-15](../work-orders/M04/WO-M04-15.md) → C05 | Solo cuentas, dinero y aplicaciones Treasury consumidos por la exposición/cobranza; no aprobación genérica de crédito; retiene cobro/aplicación real sin evidencia/política treasury; no bloquea construir crédito off. |
| [WO-M04-15](../work-orders/M04/WO-M04-15.md) → C13 | Grants/aprobadores reales de Sales y configuración de POL-08 en entidad/scope autorizados; retiene habilitar actores/configuración real sin validación; sin pol-08 aprobada el crédito sigue off. |
| [WO-M04-15](../work-orders/M04/WO-M04-15.md) → D03 | Owner: Product/Architecture + propietario; Sales posee POL-08. Crédito B2B requerido; activación exige POL-08 real versionada/aprobada, permisos, pruebas y autorización; retiene nueva exposición a crédito off hasta activación; cobranza de deuda existente permitida; cod conserva trigger propio. |
| [WO-M04-07](../work-orders/M04/WO-M04-07.md) → D06 | Owner: Product/dueño de caso. Solo evolución futura hacia SLA/escalamiento o motor genérico; Case Flow actual sigue siendo proyección; retiene iniciar esa evolución sin necesidad/política/spec; no retiene la proyección confirmada. |
| [WO-M07-14](../work-orders/M07/WO-M07-14.md) → D02 | Owner: Accounting/Tax. Solo cambio acreditado de marco/elegibilidad/edición o transacción que active otra base; retiene aplicar nuevo marco sin revisión; apertura contable actual bajo C01. |
| [WO-M02-03](../work-orders/M02/WO-M02-03.md) → C06 | Condicional a tenencia/licencia o uso de sede que exija facultad/requisito legal; Corporate conserva ese hecho; retiene ese uso/acto real sin sustento; no el alta ordinaria de identidad/dirección de sede. |
| [WO-M04-09](../work-orders/M04/WO-M04-09.md) → C06 | Solo facultad o condición contractual/legal concreta del compromiso que la requiera; retiene acto real dependiente sin evidencia; b2b comercial puro no exige dictamen universal. |
| [WO-M04-10](../work-orders/M04/WO-M04-10.md) → C06 | Solo términos/facultades legales que la cotización o su aceptación efectivamente requieran; retiene aceptación del término/acto dependiente sin sustento; no toda cotización ordinaria. |
| [WO-M03-05](../work-orders/M03/WO-M03-05.md) → C01 | Solo elegibilidad/atribución financiera aprobada que el costo tardío consuma de Accounting; C03 posee parámetros del pool; retiene uso de ese componente financiero sin política; no todo replay técnico ni registro del costo pendiente. |
| [WO-M05-02](../work-orders/M05/WO-M05-02.md) → C01 | Condicional al consumo contable: Accounting elige regla/observación por finalidad financiera; retiene conversión contable dependiente sin política; no adquisición/registro de fxobservation en integrations. |
| [WO-M05-02](../work-orders/M05/WO-M05-02.md) → C08 | Condicional al consumo fiscal: Tax elige fuente/fecha/sentido por tributo y operación; retiene cálculo fiscal dependiente sin regla; no captura de observación ni comparación comercial. |

Tres de esas once filas tenían owner canónico desalineado: D03 (Product/Architecture), D06 (Product/dueño de caso), D02 (Accounting/Tax). El profesional/propietario conserva su función de aprobación; no sustituye al owner del registro. Resto de pares: significado/owner/efecto coherentes, incluidos C04 de compras/caja chica/pago por tercero, C05 de fuentes Treasury, C08 de componentes fiscales efectivamente consumidos, y D01 de IA/shadow/comparador. No se añadieron gates por similitud de vocabulario ni a todas las fichas.

**INVALID_C_GATE_ASSIGNMENTS = 0; INVALID_D_GATE_ASSIGNMENTS = 0; GATE_OWNER_SEMANTIC_MISMATCHES = 0.** Resultado del autor pendiente de re-revisión.

### F-WO-02 — Bootstrap inicial y upgrade posterior

Se inspeccionaron las 84 fichas: **84 líneas con lenguaje de upgrade/release en 81 WOs** del candidato inicial; 80 VALID_LATER_INCREMENT, 2 GENERIC_MECHANISM_ONLY y **2 INVALID_FIRST_RUNTIME**, ambas en WO-M01-01 (Files expected y aceptación). INVALID_FIRST_SCHEMA_OF_OWNER = 0: una primera ficha de dominio puede ampliar el runtime CasPro ya aceptado. Otra línea en roadmap corresponde a «cada ampliación» y es VALID_LATER_INCREMENT; total ampliado inspeccionado: 85 líneas. Es conteo de líneas/contextos auditados, no versiones reales existentes.

Causa: copiar el perfil de upgrade de un incremento a la única raíz que crea el primer runtime. [WO-M01-01](../work-orders/M01/WO-M01-01.md) ahora exige inicialización limpia desde estado vacío/inicial documentado, entorno/bootstrap reproducible, identidad de schema/versión/configuración, roles separados, mecanismo de migración y rollback/recuperación del schema inicial. Probar esa maquinaria no prueba un upgrade histórico. No endpoints económicos ni secretos comprometidos. Un release CasPro real aceptado habilita la comparación real obligatoria en sus sucesores; Wbpro, otro proyecto anterior, no es release CasPro y no se usó como baseline. CasPro no fue eliminado/recreado.

**INVALID_FIRST_RUNTIME: 2 → 0. NO_ACCEPTANCE_CRITERION_REQUIRES_NONEXISTENT_HISTORICAL_CASPRO_RELEASE = 1.** Las líneas de upgrade de las otras 83 fichas se compararon literalmente contra el candidato revisado: sin cambios. Las 80 ocurrencias VALID_LATER_INCREMENT y la protección de Delivery/roadmap permanecen; no se cambió el primer schema de otros owners por una eliminación mecánica de requisitos.

### Alcance y control final

Archivos F-WO-01: [WO-M02-03](../work-orders/M02/WO-M02-03.md), [WO-M03-05](../work-orders/M03/WO-M03-05.md), [WO-M04-07](../work-orders/M04/WO-M04-07.md), [WO-M04-09](../work-orders/M04/WO-M04-09.md), [WO-M04-10](../work-orders/M04/WO-M04-10.md), [WO-M04-15](../work-orders/M04/WO-M04-15.md), [WO-M05-02](../work-orders/M05/WO-M05-02.md), [WO-M07-09](../work-orders/M07/WO-M07-09.md), [WO-M07-14](../work-orders/M07/WO-M07-14.md), [WO-M07-16](../work-orders/M07/WO-M07-16.md), [WO-M07-22](../work-orders/M07/WO-M07-22.md), [WO-M09-03](../work-orders/M09/WO-M09-03.md), docs/work-orders/index.md (cinco filas), este expediente y docs/review.md (estado). Cada cambio corresponde a una asignación inválida/ambigua o su reflejo; no cambios de comportamiento, capabilities, dependencias, IDs ni histórico SP2. Conteos esperados preservados: 84 WOs; M01–M09 **8/3/11/15/7/10/22/3/5**; cobertura87/87; 178 HARD, raíz WO-M01-01 y sin ciclos; **A0/B16/C13/D6, todos B/C/D OPEN**.

F-WO-02 añade únicamente docs/work-orders/M01/WO-M01-01.md y sincroniza este expediente/docs/review.md. Total de remediación: **16 archivos**, sin archivos nuevos en Git; 13 fichas, índice y dos registros de evidencia/estado. Roadmap/cobertura/supersesión no requirieron edición. Commit F-WO-01 separado del commit F-WO-02; identidades finales en Git/PR y reporte de entrega.

Recheck adversarial A–E/J: rechazar C04 por «approval» o todo gate de pago por «payment»; OFF admite cobranza existente y bloquea exposición nueva; POL-08 ausente mantiene crédito real OFF sin impedir construcción autorizada futura; COD no se promueve; otras asignaciones de la misma clase corregidas sin rediseño. F: bootstrap puede aceptarse sin release histórico inventado. G: sucesor con release real exige upgrade. H: Wbpro como supuesto release CasPro se rechaza. I: Accounting/Tax/Inventory posteriores conservan clean install/upgrade. Los diez casos son revisión documental del autor, no pruebas ejecutadas.

Validación estática final: 84 IDs/84 entradas únicas; vector de hitos intacto; cobertura87/87; 178 HARD sin cambios de aristas/tipos, 84 nodos visitados sin ciclo y única raíz WO-M01-01. Se comprobaron enlaces/anchors, 371 referencias literales de capability y existencia de gates; índice coincide con cada tabla. Los 448 pares C/D finales están reconciliados; C04 ausente del crédito. Histórico SP2 intacto/no ejecutable y sin enlace de autoridad desde fichas actuales; fuentes canónicas/skills/plantilla intactas. A0/B16/C13/D6, todos B/C/D OPEN. Diff whitespace limpio; todas las WOs siguen PREPARED — NOT AUTHORIZED FOR EXECUTION. Ninguna ejecución de WO/código de aplicación/migración/tests/builds/Docker/proveedor; solo Markdown y comprobación estática. Bloqueadores de esta remediación identificados por el autor: 0; preguntas al propietario: 0. PR #10 debe permanecer OPEN/sin merge, pendiente de re-revisión independiente.

El expediente A–AJ siguiente conserva la generación original y sus controles tal como fueron registrados; esta sección identifica qué corrigió la revisión independiente posterior.

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
