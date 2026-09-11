# SP2 — Primera tranche y Validation Profiles

Contrato: [.ai/work-order](../../.ai/work-order.md), [roles](../../.ai/README.md) y [QA](../quality/strategy.md). Se preparan exactamente seis WOs, **no ejecutadas ni autorizadas para implementación por este documento**. La misión actual solo especifica/valida documentos y publica su rama. No SUPERPROMPT 3 implícito.

## Dependencias y alcance de la tranche

`WO-SP2-01 → WO-SP2-02 → WO-SP2-03 → WO-SP2-04 / WO-SP2-05 → WO-SP2-06`.

Primero una aplicación/runner identificables, luego acceso demostrado, maestros, hechos iniciales de stock/dinero y recepción durable real de propuestas. WO-SP2-04 y WO-SP2-05 comparten contrato de acceso pero tienen propietarios distintos; no obliga a ejecutarlas en paralelo. WO-SP2-06 consume sus contratos de lectura sin confirmar venta/dinero por webhook.

Esta tranche permite empezar sin crear todos los modelos económicos en un solo PR. C14/C15/C18–C22, publicación positiva, CPE/archivo/envío y operación transversal están especificados; se encargarán después de aceptar estos cimientos con evidencia. No se crean ahora más WOs, tablas para esas funciones o paquetes vacíos. Haber terminado seis WOs no significará haber cerrado la vertical slice ni estar listo para producción.

## Perfiles de evidencia

Son selección de propiedades, no arquitectura quick/full/risk3 ni comandos del runner actual. Identidades de escenarios viven en [aceptación](acceptance.md). Las WOs referencian estos perfiles y sus recortes explícitos. Se deduplica la unión de casos/configuraciones según QA; sin manifiesto/equivalencia demostrada no se reutiliza parcialmente por «módulo sin cambios».

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
| STOCK-PUBLISH | Antes de escritura de stock positiva desatendida; demostrar condiciones y carreras de [integraciones](integrations.md#stock-publication). No es parte cumplida por WO-SP2-06 inbound |
| EMAIL-ENV | Antes de habilitar transporte Resend; casos negativos LOCAL/CI/STAGING/HOLD/ambigüedad de VP-SP2-DOC y activación autorizada |
| OPERATION | Políticas HP aplicables, UI crítica, recuperación y circuito completo con evidencia; terminar esta spec o estas seis WOs no lo cierra |

RLS permanece PROVISIONAL en ADR-005 hasta revisión trazable de sus alcances demostrados. Si WO-SP2-02 falla, no se ejecutan las dependientes sensibles. Si una entrada posterior falla, se corrige o se eleva contradicción concreta; no se reabre toda la fundación ni se degrada aislamiento por conveniencia.

## WOs preparadas

Campos comunes, incorporados a las seis WOs: **Authorization/Mode:** PREPARED, ejecución pendiente de un nuevo encargo humano que autorice la WO concreta; las pruebas indicadas son futuras. **Files forbidden:** Wbpro/legacy completos, otras specs/reglas por conveniencia, módulos fuera de alcance, cuentas/credenciales reales, infraestructura/cloud/CI y efectos externos no autorizados. **Review:** candidato exacto, reviewer separado del implementador conforme .ai; refutación de riesgo indicada. **Return format:** efecto logrado, diff/archivos, comandos y evidencia realmente ejecutados con identidad/manifiesto, criterios/subafirmaciones pendientes/fallidas, impactos y veredicto; no PASSED supuesto ni cambio unilateral de spec. Cada fila siguiente completa esos campos, no los sustituye.

<a id="wo-sp2-01"></a>
### WO-SP2-01 — Runtime y calidad mínima

| Campo | Encargo preparado |
|---|---|
| WO-ID / Goal | WO-SP2-01; runtime Django mínimo instalable y selección de evidencia aislada, sin negocio |
| Canonical spec | [Alcance](first-operational-circuit.md), [tecnología](../architecture/technology.md), [QA](../quality/strategy.md), ADR-002/009 |
| Context required | Esas secciones + AGENTS; no cargar specs CPE/Inventory para bootstrap |
| Files expected | Futuros pyproject.toml/uv.lock y configuración mínima necesaria en src/caspro/config; tests de configuración/UNIT aislados y documentación breve de uso real. Solo directorios con archivos que tengan consumidor |
| Required behavior | Instalar/runtime fijados, configuración falla explícitamente si incompleta; seleccionar UNIT sin importar Django/DB, distinguir categorías y producir identidad de evidencia |
| Invariants | Ningún secreto/default productivo, lockfiles reales y entorno identificado; no declarar una puerta inexistente pasada |
| Acceptance criteria | SP2-AC-108 y revisión de instalación/configuración reproducible del alcance; incompatibilidad bloquea fijar combinación como validada |
| Validation Profile | VP-SP2-01; gate RUNTIME; dependencias/versiones fijadas solo tras evidencia |
| Security impact | Sin secretos/DB de negocio/red productiva; ejecución futura en entorno aislado |
| Data/migration impact | Ninguna tabla empresarial/fixtures de ERP; migraciones de framework solo si runtime realmente las necesita y la WO se autoriza |
| Documentation impact | Registrar instalación/selección de evidencia realmente disponible, no copiar estrategia QA |
| Explicit non-goals | CI, Docker, builds UI, componentes vacíos, módulos empresariales, proveedores e implementación de WOs siguientes |
| Review específico | Runtime/configuración y guardia negativa de UNIT; no auditoría monetaria inexistente |

<a id="wo-sp2-02"></a>
### WO-SP2-02 — Workspace mínimo y gate de aislamiento

| Campo | Encargo preparado |
|---|---|
| WO-ID / Goal | WO-SP2-02; después WO-SP2-01, identidad/selección de entidad/membresía y aislamiento ejecutable habilitante |
| Canonical spec | [Workspace/C00](first-operational-circuit.md#c00), [acceso](../architecture/tenancy-access.md), ADR-001/005 y [CM0](command-matrix.md#cm0) |
| Context required | Separación Identity/Organization/Access, excepciones globales mínimas y gate ISOLATION; no cargar circuito entero |
| Files expected | Futuros modules/workspace y audit mínimos con APIs/queries/migraciones reales; config de roles/contexto y pruebas PostgreSQL/entrypoints construidos; sin modelos económicos de ejemplo |
| Required behavior | C00, bootstrap administrativo acotado, selección solo entre membresías; perfil/establecimientos empresariales protegidos, denegar sin contexto/capacidad y materializar lecturas antes de salir de transacción |
| Invariants | Denegación por defecto, runtime no owner/BYPASS, SET LOCAL transaccional, pertenencia/FKs e inventario explícito de excepciones globales |
| Acceptance criteria | SP2-AC-026–032; introducir tabla desprotegida/policy permisiva/rol indebido debe impedir aceptación; restore de configuración de roles dentro del alcance demostrable |
| Validation Profile | VP-SP2-02, gate ISOLATION; entradas no construidas se declaran pendientes y se cubren en extensión, no se simulan implementadas |
| Security impact | Identidad/sesión/permisos/PII global mínima; auditoría de concesión/revocación; sin is_staff económico |
| Data/migration impact | Primeras tablas Workspace/Audit necesarias, instalación limpia/upgrade aplicable, grants/policies efectivos y restricciones reproducibles; no tenant implícito de sesión |
| Documentation impact | Evidencia habilitante/limitaciones de acceso y revisión de alcance ADR-005 si realmente se demuestra; no cambiarlo a ACCEPTED por terminar código |
| Explicit non-goals | Dinero/stock/CPE, roles jerárquicos genéricos, perfiles empresariales globales, Supabase Auth o cloud |
| Review específico | Independiente de seguridad/integridad; sin PASS de aislamiento no se implementan WOs sensibles siguientes |

<a id="wo-sp2-03"></a>
### WO-SP2-03 — Maestros Parties y Catalog

| Campo | Encargo preparado |
|---|---|
| WO-ID / Goal | WO-SP2-03; después ISOLATION, crear/consultar/corregir Party y Product/SKU mínimos de la slice |
| Canonical spec | [Parties/Catalog y C11/C12](first-operational-circuit.md), [modelo](../domain/model.md), [datos](../architecture/data.md) |
| Context required | Maestros/snapshots/identidades, acceso y contratos públicos; no Resend/colas |
| Files expected | Futuros modules/parties y catalog con APIs/queries/constraints/migraciones y pruebas propias/consumidores de acceso; config solo al conectar los módulos reales |
| Required behavior | Identidad tipada/contactos/versiones, SKU/unidad/paso/estado y precio con base explícita; no fusión por email, no stock en Catalog |
| Invariants | Entidad explícita, números exactos/revisión optimista, precio nuevo no reescribe hechos históricos |
| Acceptance criteria | SP2-AC-016–018, 026–027; ramas de maestro C11/C12. Snapshot de venta se verifica como contrato de datos, no se fabrica modelo Sales todavía |
| Validation Profile | VP-SP2-03 + ISOLATION-EXTENSION de nuevas tablas; reglas numéricas sin rangos aprobados rechazan configuración incompleta |
| Security impact | PII Party y ámbito de maestros; sin CRM/Customer duplicado ni fuga de búsqueda |
| Data/migration impact | Tablas/constraints solo del maestro construido; relación externa se materializa con consumidor en WO-SP2-06, no columnas por proveedor |
| Documentation impact | Contratos/campos efectivos y límites, enlazados a spec; no nuevas reglas comerciales |
| Explicit non-goals | Import CSV completo, mapping remoto activo, pricing engine, Stock/Treasury, pantallas masivas/CRM |
| Review específico | Integridad/identidad y aislamiento, independencia de estados comerciales |

<a id="wo-sp2-04"></a>
### WO-SP2-04 — Apertura e inventario base

| Campo | Encargo preparado |
|---|---|
| WO-ID / Goal | WO-SP2-04; después WO-SP2-03, posiciones/movimientos de apertura y ajustes trazables, sin venta aún |
| Canonical spec | [Inventory/C13](sales-stock-treasury.md#c13), [cantidades/coste](sales-stock-treasury.md), [matriz](command-matrix.md) |
| Context required | P/N/A, apertura, serial/posesión y coste de origen; cláusulas de reservas como contrato a respetar cuando exista su consumidor |
| Files expected | Futuros modules/inventory con APIs/queries/migraciones y pruebas de posición/apertura/ajuste/serial/coste; sin tablas Sales ficticias |
| Required behavior | C13 de apertura/ajuste/condición, identidad de origen única, cantidades/costes y UNKNOWN explicables, lectura de disponibilidad de posiciones |
| Invariants | Stock no negativo, no duplicar apertura con otra clave; no float; no recalcular coste total desde unitario redondeado |
| Acceptance criteria | Casos de VP-SP2-04 para inventario base y nuevas carreras de apertura/ajuste; R es cero porque no hay consumidor de reserva construido, no afirmar probados escenarios de reserva |
| Validation Profile | VP-SP2-04 + extensión de aislamiento; promedio móvil/UNKNOWN/retorno no vendible provienen de HP3, mientras posiciones/buffer/publicación exigen su gate propio |
| Security impact | Capacidad opening/adjust, motivo/evidencia y auditoría crítica; sin edición directa del saldo |
| Data/migration impact | Movimientos/posiciones/seriales/costes necesarios, no Procurement/recepciones inventadas ni tablas futuras de compromisos |
| Documentation impact | Límites de apertura y existencia construida; reservas permanecen especificadas hasta su WO con Sales real |
| Explicit non-goals | Procurement, reservas sin consumidor, publicación de stock, valoración fiscal, motores de picking y CSV completo |
| Review específico | Contraejemplo de apertura duplicada/ajuste concurrente, conservación y coste desconocido |

<a id="wo-sp2-05"></a>
### WO-SP2-05 — Cuenta y cobro confirmado

| Campo | Encargo preparado |
|---|---|
| WO-ID / Goal | WO-SP2-05; después WO-SP2-03, registrar cuenta y cobro con evidencia sin crear dinero desde canal |
| Canonical spec | [Treasury/C16](sales-stock-treasury.md#c16), [C17](sales-stock-treasury.md#c17), [C23](sales-stock-treasury.md#c23) y [dinero](../domain/invariants.md) |
| Context required | HP2, cuentas/propuestas/referencias/confirmación, datos exactos y auditoría; no construir objetivos de Sales inexistentes |
| Files expected | Futuros modules/treasury mínimos con APIs/queries/migraciones y pruebas de cuenta/propuesta/cobro; Documents solo contrato de referencia a evidencia, sin archivo funcional anticipado |
| Required behavior | Cuenta tipada, propuesta que no suma dinero, confirmación humana con referencia/evidencia suficiente y U íntegro sin aplicar; dedupe por referencia además de request |
| Invariants | Importe positivo/moneda/entidad/cuenta compatibles; N real confirmado, A=0 en esta tranche; observación PAID no es cobro |
| Acceptance criteria | VP-SP2-05 en cuenta/cobro; evidencia puede ser referencia externa registrada por operador según HP2, no exige construir Storage para confirmar la existencia de un comprobante bancario |
| Validation Profile | VP-SP2-05 + extensión RLS/constraints; propiedades de sumas/aplicaciones diseñadas no se declaran integración ejecutada todavía |
| Security impact | Separar propose/confirm/manage_account; confirmar exige fuente/motivo y autoridad propia; no transferencias/banco |
| Data/migration impact | Cuenta, propuesta y movimiento confirmado; sin tablas vacías de obligaciones/asientos o proyecciones Sales |
| Documentation impact | Evidencia real del núcleo construido y límites; aplicación/refund quedan para coordinación posterior completa |
| Explicit non-goals | Aplicación/refund funcionales sin Sales/caso autorizado, conciliación bancaria automática, Accounting/Tax, integración de pagos, UI de tesorería completa |
| Review específico | Referencia duplicada/confirmación concurrente/error de evidencia; no confundir alcance construido con ciclo financiero cerrado |

<a id="wo-sp2-06"></a>
### WO-SP2-06 — Jumpseller inbound y propuesta durable

| Campo | Encargo preparado |
|---|---|
| WO-ID / Goal | WO-SP2-06; después WO-SP2-03/04/05, recibir/reconciliar pedidos y mostrar propuesta pendiente con referencias locales |
| Canonical spec | [C01–C04/C06–C10](integrations.md), [resolución comercial](sales-stock-treasury.md), [C11/C12 mapping](first-operational-circuit.md) y matriz |
| Context required | Contratos de conexión/HMAC/Decimal/orden/generaciones, estados de propuesta, maestros y lectura de stock/dinero; no cargar CPE/email |
| Files expected | Futuros integrations/jumpseller, caso observado de modules/sales, correspondencias neutrales Parties/Catalog y backend worker simple solo para refresh/procesamiento; pruebas de frontera/rol/recuperación; UI mínima de pendiente si se autoriza en esta WO |
| Required behavior | Inbox antes de 2xx; firma y entidad correctas, deduplicación por recurso/identidad, lecturas paginadas/individuales con generaciones, mapping explícito y resolución de propuesta; ninguna venta/reserva/dinero por webhook |
| Invariants | Una identidad externa→un caso; traducción exacta sin float, no estado importado=true universal, no llamada HTTP bajo DB lock; cuenta activa solo tras validación autorizada |
| Acceptance criteria | VP-SP2-06 en inbound/lecturas/propuesta; SP2-AC-051 sin dinero, 100–103 en recuperación de lectura. UI de pendiente muestra causa/capacidad si está incluida, sin falso resolved |
| Validation Profile | VP-SP2-06 + gate de extensión a webhooks/workers; BROWSER solo si hay tarea humana construida. Sin escrituras a tienda, cuentas privadas o email real durante validación ordinaria |
| Security impact | Raw body/firma/secretos por conexión, principal limitado, replay/PII y SSRF; permisos públicos sin SDK en dominio |
| Data/migration impact | Inbox/jobs/casos/mappings con consumidores reales; no Sales aceptada, reserva/T o motor de workflows anticipados |
| Documentation impact | Publicar shapes/errores y evidencia de capacidades realmente demostradas; STOCK-PUBLISH sigue pendiente, igual que gate de operación |
| Explicit non-goals | C14/aceptación, entrega física, escritura de stock, Resend/SUNAT, devolución, CRM/otros canales y framework de colas universal |
| Review específico | Refutar replay, headers no firmados, A→B→A, página perdida y generación tardía; comprobar que webhook PAID no puede crear dinero |

Estas seis WOs quedan como insumos preparados de M01–M04 y deben reordenarse o dividirse durante el freeze de cada hito del [programa maestro](../roadmap/program.md). **WO-SP2-01** continúa siendo la primera dependencia técnica candidata, pero este archivo ya no constituye por sí solo la recomendación de ejecución siguiente. Ninguna WO se ejecuta por estar preparada; cada una requiere autorización, candidato/base Git y evidencia de dependencias, sin copiar una etiqueta PASS fuera de su contrato de equivalencia.
