---
name: caspro-ui
description: "Trabajar apariencia, accesibilidad, teclado y flujos de presentación CasPro; escalar cambios de significado o confirmación al dueño del negocio."
---

# caspro-ui

Lee el [protocolo](../../../.ai/README.md) y el [estado](../../../docs/review.md) si no están en contexto. Esta skill no concede permiso: implementación requiere WO regenerada y autorización explícita; hoy solo análisis/documentación del alcance encargado. No generar WOs reales en la misión de agentes. Docs poseen las reglas; ante contradicción detener el efecto afectado y escalar, sin editar el contrato silenciosamente.

## Entrada y contexto

Requiere tarea de usuario, superficie/estado, cambio esperado y alcance autorizado. Leer [UI](../../../docs/architecture/ui.md) y sección pertinente de la spec local si existe. Para color/espaciado solo contrato visual y artefacto afectado; no cargar Accounting, normativa ni historia. Ausencia de UI construida no se resuelve creando funcionalidad fuera del encargo.

## Procedimiento y opcionales

Identificar si el cambio es visual o modifica acciones/estados/capabilities. Un atajo de navegación/búsqueda requiere solo el contrato de UI; si prepara o confirma una acción de negocio, leer comando y [transacciones](../../../docs/architecture/transactions.md#preparar-y-ejecutar) del dueño y separar preparación de ejecución según contrato. Si cambia semántica, escalar al dueño/Architecture; no «arreglarla» en UI.

Leer [QA](../../../docs/quality/strategy.md) para evidencia proporcional; B09/C12 y acceso/efecto del [registro](../../../docs/roadmap/decisions-gaps.md) solo si aplican. Memo UX es opcional para rastrear un DDR, no fuente alternativa. No prometer a11y/teclado/rendimiento probado desde una maqueta ni ejecutar browser/build no autorizado.

## Salida / revisión

Antes/después visible, contexto utilizado, semántica conservada o cuestión escalada, evidencia/limitaciones. Revisión UX proporcional para apariencia; independiente de dominio/seguridad para confirmaciones, permisos o efectos críticos. Un atajo nunca aporta por sí mismo autorización de dinero/stock/envío.
