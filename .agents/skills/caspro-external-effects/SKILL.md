---
name: caspro-external-effects
description: "Analizar o preparar adaptadores Jumpseller, proveedores, CPE/Documents y correo CasPro con control de efectos externos; no decidir pago, impuesto o estado empresarial desde el canal."
---

# caspro-external-effects

Lee el [protocolo](../../../.ai/README.md) y el [estado](../../../docs/review.md) si no están en contexto. Esta skill no concede permiso: implementación requiere WO regenerada y autorización explícita; hoy solo análisis/documentación del alcance encargado. No generar WOs reales en la misión de agentes. Docs poseen las reglas; ante contradicción detener el efecto afectado y escalar, sin editar el contrato silenciosamente.

## Entrada y contexto por efecto

Requiere proveedor/capacidad, dirección inbound/outbound, entorno, dueño solicitante, actor y alcance autorizado. Leer [integraciones](../../../docs/architecture/integrations.md), [CM0](../../../docs/specs/cross-cutting/command-matrix.md#cm0), [gaps](../../../docs/roadmap/decisions-gaps.md) y solo la rama pertinente:

- Jumpseller/webhook/publicación/trabajo durable: [flow externo](../../../docs/specs/flows/jumpseller-external-work.md), ficha del comando y dueño Sales/Inventory participante.
- CPE/archivo/correo: [CPE/Documents](../../../docs/specs/flows/cpe-document-delivery.md); Sales o Procurement posee el expediente, Documents archivo/entrega. Tax se añade solo por interpretación fiscal.
- Otro provider: puerto/contrato del dueño; verificar documentación oficial actual para capacidad/versiones/autenticación que la tarea requiera. Nueva capability fuera de contrato va a Architecture antes de implementación.

## Procedimiento / límites

Separar observación, intención preparada, autorización del comando, llamada y resultado confirmado/ambiguo conforme a la ficha. No derivar pago de PAID remoto ni confirmar negocio desde un callback. No copiar secretos, cuentas ni destinatarios reales a Git/prompts. Ante respuesta incierta, seguir reconciliación/replay autorizado; no reintentar ciegamente para obtener verde.

B10/B11/B12 y C07/C11, acceso/retención y otros gates se seleccionan por efecto desde el registro. Una instrucción «automático» no autoriza email/publicación, acceso de proveedor o acción económica. Sin mandato y gates, solo análisis/preparación expresamente permitidos; no emitir CPE ni activar integración. No usar herramientas conectadas reales como prueba documental.

## Salida / revisión

Capacidad/entorno/owner, ruta/comando, fuentes oficiales cuando usadas, incertidumbres, efectos retenidos y evidencia de contrato. Reviewer independiente de contratos/seguridad y dueño del efecto; validación profesional si validez fiscal. No confundir conexión que responde con operación autorizada.
