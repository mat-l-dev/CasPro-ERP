---
name: caspro-ui
description: "Trabajar apariencia, accesibilidad, teclado y flujos de presentación CasPro; escalar cambios de significado o confirmación al dueño del negocio."
---

# caspro-ui

Consulta el [estado](../../../docs/review.md) para la fase vigente y aplica el [protocolo](../../../.ai/README.md#autoridad-y-autorización). Esta skill no concede permiso: implementación solo con fase habilitada y WO regenerada explícitamente autorizada, respetando todos sus límites. Preparar WOs también requiere autorización vigente. Docs poseen las reglas; ante contradicción, detener la parte afectada y escalar.

## Entrada y contexto

Requiere tarea de usuario, superficie/estado, cambio esperado y alcance autorizado. Leer [UI](../../../docs/architecture/ui.md) y sección pertinente de la spec local si existe. Para color/espaciado solo contrato visual y artefacto afectado; no cargar Accounting, normativa ni historia. Ausencia de UI construida no se resuelve creando funcionalidad fuera del encargo.

## Procedimiento y opcionales

Identificar si el cambio es visual o modifica acciones/estados/capabilities. Un atajo puramente visual usa el contrato de UI; navegación/búsqueda que revela datos requiere además el contrato de lectura del dueño. Si prepara o confirma una acción de negocio, leer comando y [transacciones](../../../docs/architecture/transactions.md#preparar-y-ejecutar) del dueño y separar preparación de ejecución según contrato. Si cambia semántica, escalar al dueño/Architecture; no «arreglarla» en UI.

Case Flow, vistas parciales, proyecciones stale y preview PDF/XML → [spec de flujo/preview](../../../docs/specs/cross-cutting/case-flow-preview.md), especialmente [disclosure antes del layout](../../../docs/specs/cross-cutting/case-flow-preview.md#proyección-seguridad-y-recuperación). Lectura/preview/download/export o cambio de permisos → [registro exacto](../../../docs/architecture/capability-registry.md); datos personales → [privacidad](../../../docs/security/personal-data-lifecycle.md). Verificar nodos/aristas/conteos ocultos, revalidación y permisos separados en esas fuentes; no añadir un motor ni autoridad al grafo.

Leer [QA](../../../docs/quality/strategy.md) para evidencia proporcional; B09/C12 y acceso/efecto del [registro](../../../docs/roadmap/decisions-gaps.md) solo si aplican. Memo UX es opcional para rastrear un DDR, no fuente alternativa. No prometer a11y/teclado/rendimiento probado desde una maqueta ni ejecutar browser/build no autorizado.

## Salida / revisión

Antes/después visible, contexto utilizado, semántica conservada o cuestión escalada, evidencia/limitaciones. Revisión UX proporcional para apariencia; independiente de dominio/seguridad para confirmaciones, permisos o efectos críticos. Un atajo nunca aporta por sí mismo autorización de dinero/stock/envío.
