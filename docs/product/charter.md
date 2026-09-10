# Producto y alcance

CasPro administra la operación de TILMUX S.A.C. con cifras explicables y separación por entidad legal. Primero resuelve compras, mercadería, venta, cobro, entrega, devolución, evidencia y cierre. No se diseña como plataforma comercial multi-país ni como SaaS público.

## Qué sabemos y qué no convertimos en hecho

| Base | Tratamiento en CasPro |
|---|---|
| El propietario pide un proyecto nuevo y una fundación previa al software | Mandato de esta fase |
| Wbpro describe TILMUX constituida, operación centrada en bienes y trabajo con un operador | Contexto interno reutilizable; no acredita RUC, régimen, cuentas ni operaciones reales |
| Venta de bienes como foco inicial | Alcance recomendado; servicios vendidos fuera de la primera especificación |
| Varias entidades del ecosistema del propietario | Separación desde el inicio, sin activar entidades ficticias ni consolidación automática |
| Contabilidad interna completa como objetivo previo | Se conserva como objetivo de producto; el alcance requerido al primer uso se ratifica en H1 de la revisión |
| Régimen, marco contable, capital, mutuos, casillas y supuestos tributarios | PENDING DOMAIN/REGULATORY VALIDATION; ninguna decisión dudosa de V1 se hereda como norma |

Un usuario puede actuar para varias entidades mediante membresías. Mathew persona natural, TILMUX, otra sociedad y cualquier RUC personal nunca representan la misma propiedad empresarial. Un depósito del socio no se clasifica automáticamente como capital, ingreso o dividendo.

## Primera capacidad empresarial objetivo

Un circuito pequeño y completo: identificar bienes/contrapartes → comprar y recibir → vender y preparar evidencia → cobrar/aplicar → entregar → devolver bienes y/o dinero con sus consecuencias → conciliar y explicar el cierre. Su especificación completa será posterior. Garantía comercial e importaciones comerciales se activan por necesidad y encargo, no por existir en V1.

El Foundation Amendment del propietario incorpora Jumpseller como primer canal ecommerce real de TILMUX: pedidos entrantes y publicación del stock disponible calculado por CasPro. Incorpora también archivo privado en Documents y entrega documental por email mediante Resend, empezando con AUTO_WITH_APPROVAL. El [contrato de integraciones](../architecture/integrations.md) delimita autoridad, automatización y capacidades externas comprobadas; estos proveedores iniciales están elegidos, sus conexiones no están implementadas ni validadas.

Los primeros meses incluyen bandeja de pendientes/excepciones y discrepancias del canal, ajustes con motivo/auditoría, búsqueda global autorizada, importación CSV/Excel con validate → preview → confirm y coste/margen bruto básico trazable. Se resuelven mediante los propietarios existentes, sin CRM completo ni motor general de workflows. Preservar hechos para Accounting no equivale a haber construido el cierre contable requerido en H1.

Los recorridos deben tolerar parcialidades, anulaciones, reintentos y errores del operador. El saldo bancario, el dinero aplicado, el valor entregado y la obligación comercial son hechos distintos. El panel los muestra por su nombre y con su origen.

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
