# Work Orders actuales — conjunto candidato

**PREPARED — NOT AUTHORIZED FOR EXECUTION. IMPLEMENTATION NOT AUTHORIZED.**

84 WOs preparadas desde main aceptado `b27e5eeb280b8b654b18218a11181e9c4a8eb7b1` / tree `c0f314722f1d5fa5d2e36cb5b2aad7759710e6d8`. Requieren revisión independiente del conjunto y posterior autorización explícita antes de ejecutar cada unidad. [Review](../review.md) es la única fuente de fase global; aceptación/merge no habilitan código por sí mismos.

Leer [cobertura/hallazgos previos](coverage.md), [DAG/roadmap y gates](roadmap.md), [supersesión](supersession.md) o [informe del autor](../evidence/work-order-regeneration.md) según la pregunta. Cada ficha completa la [plantilla existente](../../.ai/work-order.md); este índice no crea otro contrato de WO.

## Hitos y conteo

| Hito canónico | WOs |
|---|---:|
| M01 — Runtime, access and recoverability | 8 |
| M02 — Party and goods masters | 3 |
| M03 — Operational stock, money and channel intake | 11 |
| M04 — Safe first B2C sale | 15 |
| M05 — Controlled Procure-to-Pay | 7 |
| M06 — Treasury reconciliation and Corporate | 10 |
| M07 — Accounting ledger and close | 22 |
| M08 — Complete NPIF reporting | 3 |
| M09 — Tax operations foundation | 5 |

M04+ usa IDs M04 conservando entrega posterior al primer B2C; crédito confirmado OFF. Número de hito no impone orden absoluto: M06 conciliación puede preceder M05 y M09 perfil/mirror puede construirse con sus contratos antes del paquete final.

## Índice maestro

HARD enumera predecesores inmediatos (cierre transitivo en el DAG); otras dependencias tipadas están en la ficha y roadmap. Lane = propietario de implementación, sin permiso de escribir simultáneamente su schema. «Tras HARD» permite trabajo paralelo solo en owners/archivos disjuntos con contratos aceptados. Reviewer R1 = independiente del dueño + refuter de integridad/seguridad; R2 = Accounting independiente/contador + checkpoint Architecture/Astra; R3 = Compliance independiente/profesional + checkpoint Architecture/Astra; R4 = contratos/seguridad/UX proporcional. Los profesionales validan C, no sustituyen pruebas B.

| WO-ID / título | Hito | Dueño / lane | HARD | Paralelismo | Riesgo | Gates locales OPEN | Estado | Reviewer |
|---|---|---|---|---|---|---|---|---|
| [WO-M01-01](M01/WO-M01-01.md) — Runtime mínimo y entrega recuperable | M01 | Platform | Raíz | Tras HARD; owner disjunto | HIGH | B01/B13/C10 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R4 |
| [WO-M01-02](M01/WO-M01-02.md) — Auditoría mínima append-only | M01 | Audit | [WO-M01-01](M01/WO-M01-01.md) | Tras HARD; owner disjunto | HIGH | B02/B03/B10/C10/C13 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R4 |
| [WO-M01-03](M01/WO-M01-03.md) — Identidad, sesiones y recuperación segura | M01 | Identity | [WO-M01-02](M01/WO-M01-02.md) | Tras HARD; owner disjunto | HIGH | B01/B02/B10/C13 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R4 |
| [WO-M01-04](M01/WO-M01-04.md) — Entidad, membresía y aislamiento por recurso | M01 | Access | [WO-M01-03](M01/WO-M01-03.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B10/C13 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M01-05](M01/WO-M01-05.md) — Roles, delegación y última ruta administrativa | M01 | Access | [WO-M01-04](M01/WO-M01-04.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/C13 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M01-06](M01/WO-M01-06.md) — Router de configuración y familias de automatización | M01 | Access | [WO-M01-05](M01/WO-M01-05.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/C13 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M01-07](M01/WO-M01-07.md) — Finalidad por dueño y restricciones de Access | M01 | Access | [WO-M01-06](M01/WO-M01-06.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B10/C06/C10/C13 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M01-08](M01/WO-M01-08.md) — Backup y recuperación base con servicio cerrado | M01 | Operations | [WO-M01-07](M01/WO-M01-07.md) | Tras HARD; owner disjunto | CRITICAL | B02/B13/C10 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M02-01](M02/WO-M02-01.md) — Party versionada y onboarding por dueño | M02 | Parties | [WO-M01-07](M01/WO-M01-07.md) | Tras HARD; owner disjunto | HIGH | B02/B03/B10/C13 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R4 |
| [WO-M02-02](M02/WO-M02-02.md) — Catálogo profesional, kits y revisiones de precio | M02 | Catalog | [WO-M01-07](M01/WO-M01-07.md) | Tras HARD; owner disjunto | HIGH | B02/B03/B04/B10/C03/C13 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R4 |
| [WO-M02-03](M02/WO-M02-03.md) — Sedes por entidad sin confundir almacenes | M02 | Organization | [WO-M01-07](M01/WO-M01-07.md) | Tras HARD; owner disjunto | HIGH | B02/B03/C06/C13 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R4 |
| [WO-M03-01](M03/WO-M03-01.md) — Artefactos privados, versiones y custodia física | M03 | Documents | [WO-M01-07](M01/WO-M01-07.md), [WO-M02-03](M02/WO-M02-03.md) | Tras HARD; owner disjunto | HIGH | B02/B03/B10/B13/C06/C10/C13 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R4 |
| [WO-M03-02](M03/WO-M03-02.md) — Solicitudes de derechos y ejecución por propietarios | M03 | Documents | [WO-M03-01](M03/WO-M03-01.md) | Tras HARD; owner disjunto | HIGH | B02/B03/B10/C06/C10/C13 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R4 |
| [WO-M03-03](M03/WO-M03-03.md) — Incidentes de privacidad y barrera completa de restore | M03 | Operations | [WO-M01-08](M01/WO-M01-08.md), [WO-M03-01](M03/WO-M03-01.md), [WO-M03-02](M03/WO-M03-02.md) | Tras HARD; owner disjunto | CRITICAL | B02/B10/B13/B15/C06/C10/C11/C13 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M03-04](M03/WO-M03-04.md) — Apertura de stock, posiciones y promedio móvil | M03 | Inventory | [WO-M02-02](M02/WO-M02-02.md), [WO-M02-03](M02/WO-M02-03.md), [WO-M03-01](M03/WO-M03-01.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B05/C03/C13 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M03-05](M03/WO-M03-05.md) — Costos tardíos y replay íntegro del pool | M03 | Inventory | [WO-M03-04](M03/WO-M03-04.md) | Tras HARD; owner disjunto | CRITICAL | B03/B04/B05/C01/C03 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M03-06](M03/WO-M03-06.md) — Traslado interno y seriales en tránsito | M03 | Inventory | [WO-M03-04](M03/WO-M03-04.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B05/C03 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M03-07](M03/WO-M03-07.md) — Conteo físico y ajuste aprobado | M03 | Inventory | [WO-M03-04](M03/WO-M03-04.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/C03 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M03-08](M03/WO-M03-08.md) — Cuentas, cobro confirmado y dinero sustentado | M03 | Treasury | [WO-M02-01](M02/WO-M02-01.md), [WO-M03-01](M03/WO-M03-01.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/C05/C13 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M03-09](M03/WO-M03-09.md) — Inbox, jobs y observaciones Jumpseller | M03 | Integrations | [WO-M01-07](M01/WO-M01-07.md), [WO-M03-01](M03/WO-M03-01.md) | Tras HARD; owner disjunto | HIGH | B02/B03/B10/B11/B12/C11 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R4 |
| [WO-M03-10](M03/WO-M03-10.md) — Propuesta comercial desde observaciones externas | M03 | Sales | [WO-M03-09](M03/WO-M03-09.md), [WO-M02-01](M02/WO-M02-01.md), [WO-M02-02](M02/WO-M02-02.md), [WO-M03-04](M03/WO-M03-04.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B11/C11/C13 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M03-11](M03/WO-M03-11.md) — ATS calculado y publicación con incertidumbre visible | M03 | Integrations | [WO-M03-10](M03/WO-M03-10.md), [WO-M03-06](M03/WO-M03-06.md) | Tras HARD; owner disjunto | HIGH | B03/B11/B12/C03/C11 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R4 |
| [WO-M04-01](M04/WO-M04-01.md) — Aceptación B2C, compromiso y reserva íntegra | M04 | Sales | [WO-M03-10](M03/WO-M03-10.md), [WO-M03-08](M03/WO-M03-08.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B09/C03/C13 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M04-02](M04/WO-M04-02.md) — Aplicaciones, liberación y refunds separados | M04 | Treasury | [WO-M04-01](M04/WO-M04-01.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/C05 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M04-03](M04/WO-M04-03.md) — Entrega parcial cubierta y devolución B2C | M04 | Sales | [WO-M04-02](M04/WO-M04-02.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B05/B09/C03/C05/C07 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M04-04](M04/WO-M04-04.md) — Expediente CPE externo de Sales | M04 | Sales | [WO-M04-01](M04/WO-M04-01.md), [WO-M03-01](M03/WO-M03-01.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B10/C07/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M04-05](M04/WO-M04-05.md) — Preview seguro, derivados y descarga autorizada | M04 | Documents | [WO-M03-01](M03/WO-M03-01.md) | Tras HARD; owner disjunto | HIGH | B02/B10/B15/C10 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R4 |
| [WO-M04-06](M04/WO-M04-06.md) — Intención documental, envío y evidencia externa C40 | M04 | Documents | [WO-M04-04](M04/WO-M04-04.md), [WO-M04-05](M04/WO-M04-05.md), [WO-M03-09](M03/WO-M03-09.md) | Tras HARD; owner disjunto | HIGH | B02/B03/B10/B12/C07/C10/C11 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R4 |
| [WO-M04-07](M04/WO-M04-07.md) — Case Flow, búsqueda y bandeja sin hechos nuevos | M04 | UI projection | [WO-M04-03](M04/WO-M04-03.md), [WO-M04-04](M04/WO-M04-04.md), [WO-M04-05](M04/WO-M04-05.md) | Tras HARD; owner disjunto | HIGH | B02/B09/B10/B15/C12/D06 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R4 |
| [WO-M04-08](M04/WO-M04-08.md) — Vistas personales y dossier autorizado | M04 | UI projection | [WO-M04-07](M04/WO-M04-07.md), [WO-M04-06](M04/WO-M04-06.md) | Tras HARD; owner disjunto | HIGH | B02/B09/B10/B15/C10/C12 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R4 |
| [WO-M04-09](M04/WO-M04-09.md) — Dossier B2B, OC opcional y compromiso directo | M04 | Sales | [WO-M04-07](M04/WO-M04-07.md), [WO-M04-02](M04/WO-M04-02.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B09/C06/C13 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M04-10](M04/WO-M04-10.md) — Cotización profesional y aceptación por revisión | M04 | Sales | [WO-M04-09](M04/WO-M04-09.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B09/C06 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M04-11](M04/WO-M04-11.md) — Contrato comercial y adendas con facultades | M04 | Sales | [WO-M04-10](M04/WO-M04-10.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/C06 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M04-12](M04/WO-M04-12.md) — Instalación y puesta en servicio como fulfillment | M04 | Sales | [WO-M04-11](M04/WO-M04-11.md), [WO-M04-03](M04/WO-M04-03.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B09/C06 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M04-13](M04/WO-M04-13.md) — Paquetes de cumplimiento de sitio cliente | M04 | Sales | [WO-M04-09](M04/WO-M04-09.md), [WO-M04-05](M04/WO-M04-05.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B09/B10/C06/C10 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M04-14](M04/WO-M04-14.md) — Libro de Reclamaciones y respuesta acreditada | M04 | Sales | [WO-M04-07](M04/WO-M04-07.md), [WO-M04-06](M04/WO-M04-06.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B10/B12/C06/C11 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M04-15](M04/WO-M04-15.md) — Crédito B2B y cobranza con activación OFF | M04 | Sales | [WO-M04-09](M04/WO-M04-09.md), [WO-M04-02](M04/WO-M04-02.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/C04/C05/C13/D03 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M05-01](M05/WO-M05-01.md) — PO, compra directa y conceptos de servicio | M05 | Procurement | [WO-M02-01](M02/WO-M02-01.md), [WO-M02-02](M02/WO-M02-02.md), [WO-M03-01](M03/WO-M03-01.md), [WO-M04-02](M04/WO-M04-02.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B06/C04/C07/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M05-02](M05/WO-M05-02.md) — Observaciones FX por fuente y finalidad | M05 | Integrations | [WO-M03-09](M03/WO-M03-09.md) | Tras HARD; owner disjunto | HIGH | B02/B03/B04/B12/C01/C08/C11 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R4 |
| [WO-M05-03](M05/WO-M05-03.md) — Requisición, RFQ y adjudicación parcial | M05 | Procurement | [WO-M05-01](M05/WO-M05-01.md), [WO-M05-02](M05/WO-M05-02.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B09/C04/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M05-04](M05/WO-M05-04.md) — Recepción de bienes y aceptación de servicio | M05 | Procurement | [WO-M05-01](M05/WO-M05-01.md), [WO-M03-04](M03/WO-M03-04.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B05/B06/C03/C04 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M05-05](M05/WO-M05-05.md) — CPE proveedor, matching y payability | M05 | Procurement | [WO-M05-04](M05/WO-M05-04.md), [WO-M04-02](M04/WO-M04-02.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B06/C04/C07/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M05-06](M05/WO-M05-06.md) — Devolución a proveedor y corrección de obligación | M05 | Procurement | [WO-M05-05](M05/WO-M05-05.md), [WO-M03-06](M03/WO-M03-06.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B05/B06/C03/C04/C07 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M05-07](M05/WO-M05-07.md) — Expediente importación y asignación landed cost | M05 | Procurement | [WO-M05-03](M05/WO-M05-03.md), [WO-M05-05](M05/WO-M05-05.md), [WO-M03-05](M03/WO-M03-05.md), [WO-M05-02](M05/WO-M05-02.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B05/B10/C01/C03/C07/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M06-01](M06/WO-M06-01.md) — Pagos, destinos bancarios y transferencias internas | M06 | Treasury | [WO-M03-08](M03/WO-M03-08.md), [WO-M04-02](M04/WO-M04-02.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/C05/C13 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M06-02](M06/WO-M06-02.md) — Extractos y conciliación N:M a corte completo | M06 | Treasury | [WO-M06-01](M06/WO-M06-01.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B06/B10/C05 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M06-03](M06/WO-M06-03.md) — Actas, facultades y hechos societarios | M06 | Corporate | [WO-M02-01](M02/WO-M02-01.md), [WO-M03-01](M03/WO-M03-01.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B10/C06/C09 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R3 |
| [WO-M06-04](M06/WO-M06-04.md) — Sobre de firma y verificación documental | M06 | Documents | [WO-M03-01](M03/WO-M03-01.md), [WO-M04-11](M04/WO-M04-11.md) | Tras HARD; owner disjunto | HIGH | B02/B03/B10/B12/C06/C11 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R4 |
| [WO-M06-05](M06/WO-M06-05.md) — Préstamos bancarios, líneas y tarjetas | M06 | Treasury | [WO-M06-01](M06/WO-M06-01.md), [WO-M06-03](M06/WO-M06-03.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/C01/C05/C06/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M06-06](M06/WO-M06-06.md) — Caja chica, rendición y reposición | M06 | Treasury | [WO-M06-01](M06/WO-M06-01.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/C04/C05/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M06-07](M06/WO-M06-07.md) — Financiación relacionada y capitalización | M06 | Corporate | [WO-M06-03](M06/WO-M06-03.md), [WO-M06-01](M06/WO-M06-01.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/C01/C05/C06/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R3 |
| [WO-M06-08](M06/WO-M06-08.md) — Pago por tercero y derecho a restitución | M06 | Corporate | [WO-M06-07](M06/WO-M06-07.md), [WO-M05-05](M05/WO-M05-05.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B06/C04/C05/C06/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R3 |
| [WO-M06-09](M06/WO-M06-09.md) — Estado de financiación reproducible | M06 | Corporate | [WO-M06-08](M06/WO-M06-08.md) | Tras HARD; owner disjunto | CRITICAL | B02/B04/B05/B08/C06 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R3 |
| [WO-M06-10](M06/WO-M06-10.md) — Obligaciones de renta desde contrato de sede | M06 | Procurement | [WO-M06-03](M06/WO-M06-03.md), [WO-M02-03](M02/WO-M02-03.md), [WO-M05-05](M05/WO-M05-05.md), [WO-M06-01](M06/WO-M06-01.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/C01/C04/C06/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M07-01](M07/WO-M07-01.md) — Catálogo PCGE, políticas y perfiles de posting | M07 | Accounting | [WO-M01-06](M01/WO-M01-06.md), [WO-M03-08](M03/WO-M03-08.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B07/C01/C02/C03 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-02](M07/WO-M07-02.md) — Interpretación, diario oficial y consumo activo | M07 | Accounting | [WO-M07-01](M07/WO-M07-01.md), [WO-M04-03](M04/WO-M04-03.md), [WO-M05-05](M05/WO-M05-05.md), [WO-M06-01](M06/WO-M06-01.md), [WO-M03-05](M03/WO-M03-05.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B07/C01/C02/C03 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-03](M07/WO-M07-03.md) — PPE y depreciación por componentes | M07 | Accounting | [WO-M07-02](M07/WO-M07-02.md), [WO-M05-04](M05/WO-M05-04.md) | Tras HARD; owner disjunto | CRITICAL | B03/B04/B07/C01/C03 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-04](M07/WO-M07-04.md) — Intangibles, fases y amortización | M07 | Accounting | [WO-M07-02](M07/WO-M07-02.md), [WO-M05-04](M05/WO-M05-04.md) | Tras HARD; owner disjunto | CRITICAL | B03/B04/B07/C01 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-05](M07/WO-M07-05.md) — Devengos y gastos acumulados | M07 | Accounting | [WO-M07-02](M07/WO-M07-02.md), [WO-M05-05](M05/WO-M05-05.md), [WO-M04-02](M04/WO-M04-02.md) | Tras HARD; owner disjunto | CRITICAL | B03/B04/B07/C01/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-06](M07/WO-M07-06.md) — Provisiones y contingencias con revisiones | M07 | Accounting | [WO-M07-02](M07/WO-M07-02.md), [WO-M06-03](M06/WO-M06-03.md) | Tras HARD; owner disjunto | CRITICAL | B03/B04/B07/C01/C06 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-07](M07/WO-M07-07.md) — Medición contable de arrendamientos | M07 | Accounting | [WO-M07-02](M07/WO-M07-02.md), [WO-M06-10](M06/WO-M06-10.md) | Tras HARD; owner disjunto | CRITICAL | B03/B04/B07/C01/C06/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-08](M07/WO-M07-08.md) — Beneficios a empleados sin nómina completa | M07 | Accounting | [WO-M07-02](M07/WO-M07-02.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B07/B10/C01/C06/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-09](M07/WO-M07-09.md) — FX y diferencias de cambio por finalidad | M07 | Accounting | [WO-M07-02](M07/WO-M07-02.md), [WO-M05-02](M05/WO-M05-02.md), [WO-M06-05](M06/WO-M06-05.md) | Tras HARD; owner disjunto | CRITICAL | B03/B04/B07/C01/C05/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-10](M07/WO-M07-10.md) — COGS y VNR separados del costo operativo | M07 | Accounting | [WO-M07-02](M07/WO-M07-02.md), [WO-M03-05](M03/WO-M03-05.md) | Tras HARD; owner disjunto | CRITICAL | B03/B04/B05/B07/C01/C03 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-11](M07/WO-M07-11.md) — Auxiliares CxC/CxP y deterioro | M07 | Accounting | [WO-M07-02](M07/WO-M07-02.md), [WO-M04-02](M04/WO-M04-02.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B07/C01/C05 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-12](M07/WO-M07-12.md) — Patrimonio y resultados acumulados | M07 | Accounting | [WO-M07-02](M07/WO-M07-02.md), [WO-M06-07](M06/WO-M06-07.md), [WO-M06-08](M06/WO-M06-08.md) | Tras HARD; owner disjunto | CRITICAL | B03/B04/B07/C01/C06/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-13](M07/WO-M07-13.md) — Impuesto corriente/diferido según marco y régimen | M07 | Accounting | [WO-M07-02](M07/WO-M07-02.md) | Tras HARD; owner disjunto | CRITICAL | B03/B04/B07/C01/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-14](M07/WO-M07-14.md) — Apertura, ESFA y transición sustentada | M07 | Accounting | [WO-M07-02](M07/WO-M07-02.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B07/B10/C01/C02/D02 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-15](M07/WO-M07-15.md) — Cierre, reversión y hechos posteriores | M07 | Accounting | [WO-M07-02](M07/WO-M07-02.md), [WO-M07-03](M07/WO-M07-03.md), [WO-M07-04](M07/WO-M07-04.md), [WO-M07-05](M07/WO-M07-05.md), [WO-M07-06](M07/WO-M07-06.md), [WO-M07-07](M07/WO-M07-07.md), [WO-M07-08](M07/WO-M07-08.md), [WO-M07-09](M07/WO-M07-09.md), [WO-M07-10](M07/WO-M07-10.md), [WO-M07-11](M07/WO-M07-11.md), [WO-M07-12](M07/WO-M07-12.md), [WO-M07-13](M07/WO-M07-13.md), [WO-M07-14](M07/WO-M07-14.md), [WO-M07-20](M07/WO-M07-20.md), [WO-M07-21](M07/WO-M07-21.md), [WO-M07-22](M07/WO-M07-22.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B05/B07/B08/C01/C02/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-16](M07/WO-M07-16.md) — JournalTemplates, reglas y recurrencia a draft | M07 | Accounting | [WO-M07-02](M07/WO-M07-02.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B07/C01/C13/D01 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-17](M07/WO-M07-17.md) — AIService neutral y reservas de presupuesto | M07 | AIService | [WO-M03-09](M03/WO-M03-09.md), [WO-M01-07](M01/WO-M01-07.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B10/B12/B16/C10/C11/D01 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R1 |
| [WO-M07-18](M07/WO-M07-18.md) — Sugerencia contable a draft y RuleCandidate | M07 | Accounting | [WO-M07-17](M07/WO-M07-17.md), [WO-M07-16](M07/WO-M07-16.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B07/B10/B16/C01/C11/D01 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-19](M07/WO-M07-19.md) — Shadow Accountant en entorno aislado | M07 | Accounting | [WO-M07-18](M07/WO-M07-18.md), [WO-M01-08](M01/WO-M01-08.md), [WO-M07-14](M07/WO-M07-14.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B10/B13/B15/B16/C10/C11/D01 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-20](M07/WO-M07-20.md) — Anticipos y prepagos con consumo por período | M07 | Accounting | [WO-M07-02](M07/WO-M07-02.md), [WO-M05-05](M05/WO-M05-05.md), [WO-M04-02](M04/WO-M04-02.md) | Tras HARD; owner disjunto | CRITICAL | B03/B04/B07/C01/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-21](M07/WO-M07-21.md) — Inversiones e instrumentos: medición y nota | M07 | Accounting | [WO-M07-02](M07/WO-M07-02.md), [WO-M05-02](M05/WO-M05-02.md), [WO-M06-05](M06/WO-M06-05.md) | Tras HARD; owner disjunto | CRITICAL | B03/B04/B07/C01/C05/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M07-22](M07/WO-M07-22.md) — Partes relacionadas: evaluación y disclosure | M07 | Accounting | [WO-M07-02](M07/WO-M07-02.md), [WO-M06-07](M06/WO-M06-07.md), [WO-M06-08](M06/WO-M06-08.md) | Tras HARD; owner disjunto | CRITICAL | B03/B04/B07/C01/C06/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M08-01](M08/WO-M08-01.md) — Cuatro EEFF, mappings y comparativos | M08 | Accounting | [WO-M07-15](M07/WO-M07-15.md), [WO-M04-05](M04/WO-M04-05.md) | Tras HARD; owner disjunto | CRITICAL | B02/B04/B05/B08/B09/B15/C01/C02 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M08-02](M08/WO-M08-02.md) — Notas, paquete NPIF y aprobación formal | M08 | Accounting | [WO-M08-01](M08/WO-M08-01.md) | Tras HARD; owner disjunto | CRITICAL | B02/B08/B09/B10/C01 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M08-03](M08/WO-M08-03.md) — Comparador mensual oficial versus shadow | M08 | Accounting | [WO-M08-02](M08/WO-M08-02.md), [WO-M07-19](M07/WO-M07-19.md) | Tras HARD; owner disjunto | CRITICAL | B02/B08/B10/B16/C01/C11/D01 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R2 |
| [WO-M09-01](M09/WO-M09-01.md) — Perfil fiscal y TAX_RULE versionada | M09 | Tax | [WO-M01-06](M01/WO-M01-06.md), [WO-M02-01](M02/WO-M02-01.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R3 |
| [WO-M09-02](M09/WO-M09-02.md) — Determinaciones fiscales y reconciliación SIRE | M09 | Tax | [WO-M09-01](M09/WO-M09-01.md), [WO-M04-04](M04/WO-M04-04.md), [WO-M05-05](M05/WO-M05-05.md), [WO-M05-02](M05/WO-M05-02.md), [WO-M07-02](M07/WO-M07-02.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B08/C07/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R3 |
| [WO-M09-03](M09/WO-M09-03.md) — Workspace de obligaciones, libros y paquetes | M09 | Tax | [WO-M09-02](M09/WO-M09-02.md), [WO-M07-02](M07/WO-M07-02.md), [WO-M06-01](M06/WO-M06-01.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B08/B10/C08/C11 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R3 |
| [WO-M09-04](M09/WO-M09-04.md) — Mirror histórico y linaje de declaración externa | M09 | Tax | [WO-M09-01](M09/WO-M09-01.md), [WO-M03-01](M03/WO-M03-01.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B10/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R3 |
| [WO-M09-05](M09/WO-M09-05.md) — Conciliación de casillas y revisión de diferencias | M09 | Tax | [WO-M09-04](M09/WO-M09-04.md), [WO-M09-03](M09/WO-M09-03.md) | Tras HARD; owner disjunto | CRITICAL | B02/B03/B04/B08/C08 | PREPARED — NOT AUTHORIZED FOR EXECUTION | R3 |

## Responsabilidad de implementación

| Owner/lane | WOs |
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

Conteo por responsable principal de la PR, no reasignación de hechos: los coordinadores conservan participantes y propietarios en cada ficha. No hay Privacy ni Finance genérico. Todas las fichas permanecen pendientes de revisión independiente; ningún resultado funcional está PASSED.
