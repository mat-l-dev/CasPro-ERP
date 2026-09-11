# Producto y alcance

CasPro administra la operación de TILMUX S.A.C. con cifras explicables y separación por entidad legal. Primero resuelve compras, mercadería, venta, cobro, entrega, devolución, evidencia y cierre. No se diseña como plataforma comercial multi-país ni como SaaS público.

## Qué sabemos y qué no convertimos en hecho

| Base | Tratamiento en CasPro |
|---|---|
| El propietario pide un proyecto nuevo y una fundación previa al software | Mandato de esta fase |
| Wbpro describe TILMUX constituida, operación centrada en bienes y trabajo con un operador | Contexto interno reutilizable; no acredita RUC, régimen, cuentas ni operaciones reales |
| Venta de bienes como foco inicial | Alcance confirmado; los servicios vendidos quedan fuera y los servicios/gastos comprados entran por Procurement sin SKU de stock |
| Varias entidades del ecosistema del propietario | Separación desde el inicio, sin activar entidades ficticias ni consolidación automática |
| Contabilidad interna y estados financieros completos | Objetivo del programa: cuatro estados, notas, comparativos y trazabilidad; NPIF es el candidato inicial sujeto a elegibilidad y validación profesional |
| RER como régimen inicial declarado por el propietario | Hipótesis empresarial pendiente de ficha RUC/acogimiento y reglas vigentes; no convierte tasas, casillas o tratamientos heredados en norma |
| Capital, mutuos y otros supuestos societarios/tributarios | PENDING DOMAIN/REGULATORY VALIDATION; ninguna conclusión dudosa de V1 se hereda como norma |

Un usuario puede actuar para varias entidades mediante membresías. Mathew persona natural, TILMUX, otra sociedad y cualquier RUC personal nunca representan la misma propiedad empresarial. Un depósito del socio no se clasifica automáticamente como capital, ingreso o dividendo.

## Programa empresarial objetivo

La secuencia completa es: plataforma aislada y recuperable → maestros → stock/dinero/pedido durable → primera venta B2C → compra a pago → control financiero/corporate → ledger y cierre → EEFF NPIF → operación tributaria preparada. El [programa maestro](../roadmap/program.md) coordina esas entregas; ninguna fila autoriza código. Garantía comercial, importaciones comerciales y servicios vendidos se activan por necesidad y encargo.

El Foundation Amendment del propietario incorpora Jumpseller como primer canal ecommerce real de TILMUX: pedidos entrantes y publicación del stock disponible calculado por CasPro. Incorpora también archivo privado en Documents y entrega documental por email mediante Resend, empezando con AUTO_WITH_APPROVAL. El [contrato de integraciones](../architecture/integrations.md) delimita autoridad, automatización y capacidades externas comprobadas; estos proveedores iniciales están elegidos, sus conexiones no están implementadas ni validadas.

Los primeros meses incluyen bandeja de pendientes/excepciones y discrepancias del canal, ajustes con motivo/auditoría, búsqueda global autorizada, importación CSV/Excel con validate → preview → confirm y coste/margen bruto básico trazable. Se resuelven mediante los propietarios existentes, sin CRM completo ni motor general de workflows. Preservar hechos para Accounting no equivale a haber construido el cierre contable requerido en H1.

El primer circuito comercial vende únicamente bienes y exige pago íntegro confirmado antes de cualquier despacho. Los pagos parciales pueden registrarse, pero no habilitan despacho. Inventory usa promedio ponderado móvil para el coste operativo; un coste no sustentado permanece `UNKNOWN`, y toda devolución de cliente entra inicialmente como no vendible hasta revisión. Accounting conserva separadamente valoración financiera, VNR, deterioro y cierre.

Los recorridos deben tolerar parcialidades, anulaciones, reintentos y errores del operador. El saldo bancario, el dinero aplicado, el valor entregado y la obligación comercial son hechos distintos. El panel los muestra por su nombre y con su origen.

**Delta de producto propuesto — B2B y financiación:** el [amendment semántico](../evidence/b2b-financing-amendment.md), pendiente de revisión independiente, añade venta B2B general de bienes como incremento posterior a M04. [Sales](../specs/flows/b2b-commercial-dossier.md) posee cotización/OC cliente/revisión aceptada y expediente; tipo de cliente y condiciones de pago se separan. Inicialmente B2B conserva prepago íntegro antes de cualquier despacho; crédito y contraentrega siguen trigger D03. No se limita a un adjunto ni exige OC/cotización para toda venta.

M06 concreta [hechos individuales de financiación](../specs/flows/financing-events-statements.md), pagos personales por cuenta de la empresa, reembolsos separados de principal y estado mensual derivado. El contrato gratuito rotativo sigue propuesta bajo C06. Documents permite entrega por Resend opcional, otro adaptador futuro o registro externo conocido; WhatsApp Business permanece diferido D03/M10. Estas ampliaciones no aceptan el amendment ni habilitan código, WOs o operación real.

## Non-goals iniciales

- ERP genérico, plugins, multi-país, consolidación/intercompany automática, marketplace y personalización por cliente.
- SPA integral, móvil/offline, microservicios, data warehouse y motor general de reglas.
- Emitir, presentar o enviar CPE a SUNAT desde CasPro, incluso mediante una acción manual de su UI. El operador emite fuera de CasPro mediante SOL u otra vía externa autorizada; CasPro adquiere/importa, vincula/verifica y entrega documentos dentro de capacidades comprobadas. Tampoco ordena transferencias bancarias automáticas. Publicar stock en Jumpseller y entregar email son efectos externos incluidos expresamente; ampliar esos efectos exige nuevo mandato.
- CRM completo, otros canales ecommerce y frameworks multicanal. Conservar referencias neutrales mínimas no habilita especificar MercadoLibre/TikTok ni crear sus carpetas.
- Acceso de clientes/proveedores y ventas de servicios, hasta tener necesidad autorizada.
- Copiar el historial de datos, migraciones o supuestas aprobaciones de Wbpro.

## Qué significa éxito

El operador puede explicar una cifra hasta su documento y hecho original; ninguna operación individual o concurrente crea dinero/stock ficticio; una corrección conserva la historia pertinente; la aplicación puede restaurarse y desplegarse con identidad verificable.

Esta fundación habilita revisión. No habilita operación empresarial real. El [registro humano](../review.md) distingue alcance, aceptación de riesgo, presupuesto y validación profesional.
