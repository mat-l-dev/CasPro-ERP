# SP2 — Perfiles de validación y gates habilitantes

Propietario: Quality con dueños de los contratos SP2. Alcance: selección de evidencia futura del primer circuito, subordinada a [calidad](../../quality/strategy.md), los [gates actuales](../../roadmap/decisions-gaps.md) y el [estado global](../../review.md). Se extraen sin cambio material los perfiles existentes de la baseline congelada; no son pruebas ejecutadas, nuevas WOs ni autorización. Las [seis WOs SP2](../../history/work-orders-sp2.md) conservan su identidad histórica y requieren regeneración.

## Perfiles de evidencia

Son selección de propiedades, no arquitectura quick/full/risk3 ni comandos del runner actual. Identidades de escenarios viven en [aceptación](operational-scenarios.md). Las WOs referencian estos perfiles y sus recortes explícitos. Se deduplica la unión de casos/configuraciones según QA; sin manifiesto/equivalencia demostrada no se reutiliza parcialmente por «módulo sin cambios».

| Perfil | Categorías y escenarios mínimos | Configuración/evidencia y límite |
|---|---|---|
| VP-SP2-01 | STATIC runtime/dependencias; UNIT: SP2-AC-108; CONTRACT de configuración/categorías | Colección UNIT aislada sin inicializar Django/DB/red; runtime/locks/runner identificados. No benchmark/budget inventado ni suite económica |
| VP-SP2-02 | STATIC permisos/inventario; INTEGRATION: SP2-AC-026–032; CONTRACT de entradas construidas; TRANSACTIONAL conexión/rollback; MIGRATION instalación/upgrade aplicable | PostgreSQL real con rol runtime no owner, A/B, contexto ausente; variantes de grants/policies maliciosas deben fallar. Artefactos de permisos efectivos/inventario/schema y revisión independiente |
| VP-SP2-03 | STATIC; UNIT normalización/validación pura; INTEGRATION maestros; CONTRACT DTO/errores; SP2-AC-016–018, 026–027 y C11/C12 en ramas de maestro | RLS de tablas nuevas; identidad/moneda/unidad/revisiones/retirada sin red. Mapping de canal se añade en VP-SP2-06, no fingirlo construido aquí |
| VP-SP2-04 | STATIC; UNIT + PROPERTY conservación de cantidad/coste de apertura/ajuste; INTEGRATION + TRANSACTIONAL: SP2-AC-024, 039, 046, 050 en alcance C13 | Posiciones/seriales y coste UNKNOWN; pruebas de ajuste concurrente y duplicación de origen. Donde interviene una reserva, escenario queda pendiente hasta VP-SP2-FLOW; no declarar pasado con R siempre cero |
| VP-SP2-05 | STATIC; UNIT + PROPERTY dinero exacto; INTEGRATION + TRANSACTIONAL: SP2-AC-051–052 en registro de cobro, 056, 064–065 en C17/C23 | C16/C17/C23 reales, duplicación/revisión/cuenta/evidencia. Aplicación/refund y SP2-AC-063 quedan pendientes hasta VP-SP2-FLOW; no construir modelos futuros para rellenar el perfil |
| VP-SP2-06 | STATIC; CONTRACT Jumpseller/correspondencias/observaciones; UNIT parser exacto/HMAC; INTEGRATION + TRANSACTIONAL: SP2-AC-002–015, 019–020, 031, 100–103/106 en recepción/lectura | Raw fixtures oficiales/sanitizadas, transporte controlado sin cuentas reales; generación/duplicados/paginación/429/firmas/conexión; las porciones C14/stock outbound de esos escenarios quedan pendientes, no PASSED |
| VP-SP2-FLOW (posterior) | STATIC + UNIT + PROPERTY + INTEGRATION + TRANSACTIONAL; SP2-AC-001–012 y 033–065 completos | Coordinación Sales/Inventory/Treasury real, intercalaciones y rollback con recursos comunes; perfil de tablas/entrypoints nuevos reutiliza VP-SP2-02 solo donde haya equivalencia |
| VP-SP2-DOC (posterior) | STATIC + CONTRACT + INTEGRATION + TRANSACTIONAL: SP2-AC-066–076 y 079–099; UNIT parsing/fingerprint/derivación; BROWSER tareas de aprobación/preview/HOLD | Object storage aislado/captura email, fixtures firmadas; env negativos sin envíos LOCAL/CI. Adaptador Resend se verifica por contrato controlado; activación externa es evidencia adicional autorizada |
| VP-SP2-OPS (posterior) | STATIC + CONTRACT + INTEGRATION: SP2-AC-021–025, 077–078, 109–110; BROWSER preview/confirm/search | Datos sintéticos completos/incompletos, macros/fórmulas, cortes consistentes y ausencia de fuga en conteos. No NFR genérico para rellenar categorías |
| VP-SP2-RECOVERY (posterior) | TRANSACTIONAL + MIGRATION + NON-FUNCTIONAL: SP2-AC-100–107 y 028–030/074/105 | Restore DB+objetos+roles/epoch en destino aislado, efectos desactivados; duración/pérdida medidas. No declarar RPO/RTO alcanzados antes de decidirlos/probarlos |

Las filas con recortes especifican subafirmaciones, no permiten marcar un escenario compuesto completo como pasado. Reporte identifica qué pasos/propiedades del ID están pendientes. Al integrar el flujo se ejecuta el escenario completo contra los propietarios reales. Casos UNIT no importan Django/ORM ni fixtures globales; tests de DB viven en categorías distintas con PostgreSQL y base aislada. No usar SQLite ni mocks como evidencia de locks/RLS. BROWSER se reserva a tareas humanas construidas, no toda política pura.

Resultado reutilizable: manifestar candidato/insumos, casos/subafirmaciones, parámetros/semillas, configuración efectiva, comandos reales y artefactos de ejecución. Las causas de invalidación y equivalencia se leen una vez en QA; aquí no existe otra excepción. Cambiar spec de comportamiento, gates, fixtures, permisos, parser, contratos o runner invalida su afirmación afectada. No budgets de segundos sin baseline; registrar colección/setup/call/teardown para decidir después.

## Gates habilitantes

| Gate | Momento / condición |
|---|---|
| RUNTIME | Cierre WO-SP2-01: compatibilidad/locks y separación de categorías demostradas, sin afirmar todos los mecanismos aceptados |
| ISOLATION | Cierre WO-SP2-02, antes de implementar operaciones sensibles de WO-SP2-03 en adelante. Evidencia runtime, inventario/policies/grants, negativas de configuración, conexión/rollback y frontera construida conforme ADR-005 |
| ISOLATION-EXTENSION | Cada nueva tabla/entrypoint requiere su evidencia antes de habilitarlo; gate anterior no cubre workers/imports/exports inexistentes. Fallo detiene ese alcance, no manager como sustituto silencioso de RLS |
| STOCK-PUBLISH | Antes de escritura de stock positiva desatendida; demostrar condiciones y carreras de [integraciones](../flows/jumpseller-external-work.md#stock-publication). No es parte cumplida por WO-SP2-06 inbound |
| EMAIL-ENV | Antes de habilitar transporte Resend; casos negativos LOCAL/CI/STAGING/HOLD/ambigüedad de VP-SP2-DOC y activación autorizada |
| OPERATION | Políticas HP aplicables, UI crítica, recuperación y circuito completo con evidencia; terminar esta spec o estas seis WOs no lo cierra |

RLS permanece PROVISIONAL en ADR-005 hasta revisión trazable de sus alcances demostrados. Si WO-SP2-02 falla, no se ejecutan las dependientes sensibles. Si una entrada posterior falla, se corrige o se eleva contradicción concreta; no se reabre toda la fundación ni se degrada aislamiento por conveniencia.
