# Deep specs y gate documental global

Propietario: Architecture con dueños de dominio. Mandato [ADR-012](../decisions/adr-012-global-documentation-freeze.md). **Candidato M01–M09 entregado para revisión; ningún hito está FROZEN ni autorizado para código.** Las specs SP2 mantienen contratos precisados; las siguientes amplían y resuelven fronteras del programa. IDs de specs/comandos no implican clases/tablas anticipadas. [Cierre/readiness](../research/astra-master-audit.md) distingue contenido, aceptación y evidencia.

## Matriz de cobertura

| Hito | Contrato local profundo | Contenido de cierre documental |
|---|---|---|
| M01 | [Runtime/access/audit/operations](runtime-masters.md) | Runtime fijable, bootstrap, aislamiento/revocación, documentos privados, recuperación y ensayo habilitante |
| M02 | [Maestros e importación](runtime-masters.md) | Identidades/referencias/versiones, servicio comprado separado, preview invalidable y corrección |
| M03 | [Inventory/costeo](inventory-deep.md), [Treasury SP2](sales-stock-treasury.md), [integraciones](integrations.md) | Apertura/UNKNOWN, secuencia de valoración, dinero confirmado y propuesta externa |
| M04 | [B2C profundo](inventory-deep.md), [CPE](cpe-document-delivery.md), [hechos](economic-facts.md) | HP1–HP5, correcciones coordinadas, oportunidad CPE/adquisición externa, preservación para Accounting |
| M05 | [Procure-to-Pay](procurement-deep.md) | Mercancía/servicios, PO/recepción/conformidad/factura, match/hold, anticipo, devolución y payability |
| M06 | [Conciliación bancaria y Corporate](treasury-corporate-deep.md) | Import/duplicado/N:M/reversión, financiación/actos/relaciones y gate profesional temprano |
| M07 | [Accounting](accounting-deep.md) y [políticas NPIF](../accounting/npif-policy-catalog.md) | Interpretación, PCGE aplicado, posting/revisión, ledger, subcontroles, cierre y apertura |
| M08 | [Paquete financiero y goldens](reporting-goldens.md) | Cuatro estados+notas, comparativos, transición, integridad y drill-through |
| M09 | [Tax Perú](tax-deep.md) | Perfiles/vigencias, base fiscal, CPE/IGV/SIRE/SPOT, no domiciliados, registros/conciliación |

Las nueve filas tienen contrato candidato. SPECIFIED describe contenido, no aceptación: conservan gates profesionales y ejecutables expresos. El [contrato transversal](economic-facts.md) es obligatorio y extiende el orden de CM0 para P2P, conciliación, valoración y libros. Capabilities/programa conservan propósito, dependencias y roles, sin duplicar estados de comandos.

## Criterios de revisión transversal

1. Cada dato/estado/dinero/stock tiene un único dueño; referencias interempresa quedan rechazadas en servicio y persistencia.
2. Todo hecho relevante anterior a M07 puede consumirse una sola vez con trazabilidad, sin reconstruirlo desde el estado final mutable.
3. Ninguna norma se infiere de cuenta PCGE, ejemplo de guía o código Wbpro; fuente/edición/vigencia/marco/hechos son explícitos.
4. Refund/despacho, pago/cambio de proveedor, factura/recepción, costo tardío/cierre, posting/cierre y restore/replay tienen desenlace definido.
5. No hay FROZEN si un pendiente cambia reconocimiento, política legal, dato obligatorio o autorización. Experimentos declaran ensayo acotado y fallo.
6. Evidencia corresponde al candidato/afirmación; revisión estática no acredita PostgreSQL, RLS, CPE externo ni reportes ejecutables.
7. El paquete financiero cubre capabilities aplicables del primer año; no se difieren PPE/devengos/provisiones sin evaluar hechos.
8. UI explica origen/acción/corrección sin detalles técnicos innecesarios; búsqueda/drill-through respetan permisos.
9. Investigación/aprobación de financiación preceden al desembolso; implementación tardía no posterga ese control.
10. Reviewer separado y aprobación humana/profesional son hechos registrados, no roles ficticios de una misma respuesta.

## Handoff de futura WO

Leer AGENTS → estado global → tarjeta de hito → spec local/dependencias concretas → perfil de evidencia. Sol orquesta y conserva candidato; implementador/reviewer son distintos; Astra interviene en arquitectura, dinero/stock, Accounting/Tax/Legal, seguridad o contraejemplo transversal. WO fija archivos permitidos/prohibidos, datos sintéticos, incertidumbre y escalación. Si falta una política, no la inventa ni pide al propietario elegir detalles técnicos.

No generar skills finales mientras GLOBAL FREEZE siga abierto. Familias futuras del programa son propuesta, no instalación ni autorización de agentes autónomos.
