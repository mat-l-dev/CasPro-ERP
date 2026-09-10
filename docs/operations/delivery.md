# Entrega, operación y recuperación

Diseño de [ADR-010](../decisions/adr-010-delivery.md). No se provisionó infraestructura ni se ejecutó Docker/build/CI. Render + Supabase es una topología candidata, sujeta a presupuesto, región y validación.

## Entornos y artefacto

LOCAL usa datos sintéticos y DB dedicada cuando la fase lo autorice; CI usa PostgreSQL aislado; STAGING reproduce roles/schema/configuración relevante; PRODUCTION usa credenciales y datos separados. Ningún entorno de pruebas apunta a la DB de negocio. Settings comparten código y cambian por configuración validada, no por parches personales.

Runtime futuro: proceso Django WSGI persistente con servidor de producción, proxy/TLS de plataforma y assets compilados. No ASGI/servidor async por reflejo; reconsiderar si hay conexiones prolongadas o carga que lo necesite. Worker es proceso separado del mismo artefacto al aparecer trabajo durable. Suelo inicial de infraestructura: aplicación + DB + almacenamiento privado cuando haya Documents; sin broker ni Kubernetes.

Construir imagen OCI una vez, con runtime y assets, publicar por digest y desplegar ese mismo digest en staging/producción. Un contenedor favorece la salida a VPS, pero no se necesita Docker durante esta fase documental. Node 24 LTS/npm solo en build; Python/uv/lock y librerías fijados; ejecución sin privilegios y sin secretos dentro de capas de imagen.

Render soporta imágenes por digest. Selección regional candidata: Virginia para app y DB, verificando conectividad real entre proveedores y latencia desde Perú; estar en la misma región no crea una red privada común [S16](../decisions/sources.md). Conexión TLS verificada, permisos y restricciones de red acordes al plan. No fijar capacidad de máquinas sin datos de carga.

## CI/CD y supply chain

GitHub Actions como orquestador: PR no confiable sin secretos, permisos mínimos por job, Actions por SHA completo, locks revisados, escaneo de secretos/vulnerabilidades y revisión de nuevas dependencias. Nueva dependencia runtime requiere necesidad, mantenimiento, licencia, alternativa, superficie de seguridad y coste de actualización. No aprobarla solo porque el código generado la importa [S19](../decisions/sources.md).

OIDC y credenciales breves donde el proveedor lo soporte; no presumirlo para Render. Si hacen falta tokens, limitar alcance, caducidad/rotación y uso por entorno. El despliegue productivo tiene identidad y aprobación empresarial explícita; un merge no es un permiso de presentar documentos o mover dinero.

Un release futuro registra: commit/árbol exacto, locks, digest, conjunto de migraciones, esquema de configuración esperado, evidencias usadas, fecha, actor y resultado por entorno. Configuración sensible conserva nombres/versiones o referencias al secreto, nunca valores. El manifiesto operativo indica lo realmente desplegado, incluyendo un rollback.

El plan de validación y cualquier reutilización obedecen al contrato canónico de [calidad](../quality/strategy.md). El release registra la evidencia aplicable al candidato y al artefacto realmente desplegable; generar otro informe no exige otra ejecución. Prohibidos checkout latest + instalación libre y pasadas repetidas solo para generar informes.

## Migraciones

| Caso | Política |
|---|---|
| Instalación limpia | Base nueva identificada, esquema/roles/políticas creados desde cero; jamás inferir limpieza porque migrate terminó |
| Upgrade | Probar desde el último release soportado con volumen/datos representativos |
| Schema compatible | Expand primero; código compatible con transición; contract después de retirar todos los consumidores anteriores |
| Data migration | Lotes acotados, checkpoints, idempotencia, observación y reconciliación; no transacción gigante no medida |
| Cambio destructivo | Ventana, backup recuperable y aprobación explícita; incluir efecto sobre RLS/FKs/consumidores |
| Rollback | Aplicación anterior solo si entiende schema/datos actuales; rollback de aplicación no implica rollback de DB |

Credencial de migración separada; ejecución única coordinada, no al arranque de cada réplica. Release declara orden expand → despliegue → backfill/migrate → validación → contract. Una caída durante la migración tiene estado y procedimiento de reanudación. No se escriben migraciones reales en esta entrega.

## Backup y disaster recovery

DB: combinar capacidades de backup/PITR contratadas con exportación/restauración portable cuando proceda. Objects: copia/versionado y manifiesto independientes; secretos/roles/configuración/artefactos también se recuperan. Los backups de DB de Supabase no incluyen blobs de Storage y no restauran automáticamente passwords de roles personalizados [S20](../decisions/sources.md).

Retención y frecuencia deben cubrir RPO/RTO elegidos por el propietario, más requisitos documentales verificados. No hay números inventados en esta fase. Copias cifradas, acceso separado de producción y credenciales de recuperación disponibles de forma controlada. No declarar recuperabilidad sin restore probado.

Drill futuro: restaurar en destino aislado → recrear roles/configuración segura → verificar schema/políticas y pertenencia → comprobar integridad de dinero/stock/objetos referenciados → reconciliar cursor de eventos/jobs → registrar duración/pérdida posible. Desactivar efectos externos durante restore/replay: recuperar una outbox no debe volver a enviar un pago o una notificación indiscriminadamente.

Mover a PostgreSQL managed/VPS cambia endpoint, roles, extensiones permitidas, TLS, backup y responsabilidades; no exige reescribir dominio. Mover plataforma Supabase completa añade servicios y objetos distintos. Comparar fuente/destino y ensayar restore antes de prometer portabilidad operativa.

## Observabilidad y salud

| Señal | Uso |
|---|---|
| Audit | Quién actuó, entidad, recurso, transición, motivo y origen; retención empresarial |
| Logs | Diagnóstico estructurado con correlación/release, sin PII ni secretos innecesarios |
| Metrics | Errores/latencia, saturación/conexiones DB, bloqueos, retries, antigüedad/backlog de jobs y fallos financieros agregados |
| Traces | Añadir en fronteras lentas/difíciles mediante interfaz portable OTLP cuando aporte diagnóstico; no instrumentar todo |

Liveness comprueba proceso capaz de atender, no proveedores externos. Readiness comprueba configuración esencial, conectividad/versión de DB y compatibilidad del release, con timeouts acotados; no realiza escrituras económicas. SUNAT/email/Jumpseller son degradables mientras las tareas locales sigan siendo válidas. Si un flujo necesita evidencia externa, ese flujo se bloquea de forma explícita, no necesariamente todo el ERP.

Storage caído degrada las tareas que necesitan evidencia; un flujo que no pueda confirmar sin ella debe esperar. Worker atrasado se observa mediante antigüedad y errores, no por responder 200 en la web. Estado verde de salud no demuestra integridad de negocio.

## Capacidad e incidentes

Baseline con distribución realista de SKUs, movimientos, años, documentos por contraparte y usuarios; usar datos sintéticos representativos, no diez filas. Medir consultas/N+1, páginas críticas, exportaciones, informes financieros y kardex. Paginación, límites y jobs antes de réplicas/warehouse. La suma de conexiones de web+worker+migración no puede agotar el límite contratado.

Runbooks futuros mínimos: desplegar/revertir, migrar/reanudar, restaurar/reconciliar, rotar credencial, atender discrepancia financiera y activar continuidad. Cada uno declara responsable, entrada, impacto, condición de éxito y evidencia. No se generan runbooks gigantes antes de elegir infraestructura y RPO/RTO.
