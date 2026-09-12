# M01–M02 — Runtime, acceso, recuperación y maestros

Estado: **SPECIFIED — candidato / PENDING EXECUTABLE VALIDATION**. Arquitectura: [tecnología](../../architecture/technology.md), [acceso](../../architecture/tenancy-access.md), [operación](../../operations/delivery.md). Hereda [contrato profundo](../cross-cutting/economic-facts.md). M01 entrega infraestructura mínima comprobable; M02 identidades y catálogos. Ninguno autoriza código ahora.

## M01: límite verificable

Python 3.14 con GIL, Django 6.1, PostgreSQL 17 y psycopg 3 son combinación candidata. WO fija parches soportados y dependencias exactas, registra compatibilidad y lock; no sustituye una rama silenciosamente. PostgreSQL 15+ es mínimo de Django 6.1, no la selección CasPro. Supabase se limita a PostgreSQL; Data API deshabilitada, rol runtime sin ownership/BYPASSRLS/superuser, rol de migración separado. Conexión directa o pool de sesión; pool transaccional requiere ensayo explícito de contexto y cursores. Django Auth posee sesión y credenciales.

MFA: candidato acotado django-allauth, TOTP + códigos de recuperación de un uso; sin social login, registro público ni headless inicial. Antes de aceptar dependencia: compatibilidad de versión exacta con Django/Python, licencia, CSRF/session fixation, recuperación, limitación de intentos, cifrado de secreto TOTP con clave fuera de DB, rotación y restore. Si no pasa, reabrir elección de identidad con Astra; no inventar MFA propio ni desplegar sin el control acordado. Las [fuentes oficiales](https://docs.allauth.org/en/latest/mfa/introduction.html) describen capacidad, no prueban esta configuración.

| Caso / capacidad / clase | Lecturas y locks | Escritura / resultado / fallo y corrección |
|---|---|---|
| Bootstrap / operador de despliegue / D | Estado de instalación, identidad de bootstrap I→A; secreto fuera del repositorio | Crear primer administrador y entidad autorizada una vez; cierre irreversible del bootstrap público. Repetición devuelve identidad sin contraseña. Instalación ya inicializada rechaza segunda raíz. Recuperación es procedimiento auditado, no endpoint secreto permanente |
| Conceder/revocar / access.manage / V | Concesión y capacidad delegable A; sesión/mandato vigentes | Nueva revisión de concesión y auditoría; prohibida autoescalación fuera del mandato. Revocación impide nuevas autorizaciones según frontera de commit del contrato de acceso; no promete retirar un efecto externo ya enviado |
| Cambiar entidad activa / usuario / V | Membresía vigente A; recursos aún no consultados | Nuevo contexto de solicitud, sin copiar permisos; tabs y jobs conservan entidad explícita. Recurso previo de otra entidad responde sin revelar existencia |
| Preservar archivo privado / documents.ingest / D | Metadatos/propuesta autorizada I→D en finalización | Upload temporal privado, límite/tipo/antimalware fuera de TX; hash y versión sellada al finalizar, bytes pendientes nunca elegibles. Reintento verifica hash. Fallo deja artefacto técnico rastreable; no borra evidencia empresarial |
| Descargar evidencia / documents.view / R | Permiso sobre dueño y versión; no basta conocer UUID | URL breve privada o streaming autenticado, auditoría pertinente; revocación impide emitir nuevo acceso, vencimiento limita enlace ya emitido. No links públicos permanentes |
| Restaurar / operador autorizado / D operacional | Manifest de backup, claves y entorno aislado; exclusión operacional de escritores y workers | Restaurar DB+objetos+roles/configuración; cotejar manifest/hashes, RLS y referencias; replay deshabilitado hasta resolver efectos UNKNOWN. No tráfico real en ensayo |

Acceso UI/admin/jobs/imports/CLI/export debe entrar por contexto verificado. Identidad global puede autenticar, pero datos empresariales siempre tienen entidad. Transacción usa contexto local que no contamina siguiente solicitud del pool. El servicio comprueba pertenencia y la persistencia impide referencias cruzadas. No usar señales Django como única auditoría: operaciones masivas o cascadas pueden no ejecutarlas.

## Operación, auditoría y recuperación

Separar ledger económico, auditoría crítica y logs técnicos. Auditoría append-only para runtime; actor, propósito, versión y correlación, sin secretos ni expedientes completos en logs. Capacidad técnica de administrador DB se trata mediante credenciales/revisión/backup, no afirmación de inmutabilidad absoluta. Acceso a secretos se limita por proceso; rotación no reinterpreta hechos.

Un backup útil incluye DB consistente, objetos referenciados y sus versiones, claves recuperables por canal separado, roles/extensiones/configuración y manifest. El punto de recuperación declara qué objetos y confirmaciones abarca; DB recuperada con blob ausente no pasa. HP5 impide eliminación empresarial automática. Retención de temporales técnicos se distingue de evidencia y requiere política; no usar una tarea de limpieza universal. RPO, RTO, retención, región y presupuesto siguen decisión humana [DH5](../../roadmap/decisions-gaps.md#dh5); el ensayo futuro mide contra valores aprobados, nunca “restore OK” sin objetivo.

Pruebas habilitantes M01: PostgreSQL real para RLS/FKs/roles y pooling; revocación concurrente; recuperación MFA y pérdida de factor; fijación de sesión/CSRF; límites de upload y contenido activo; restore aislado con un blob faltante detectado; redacción de logs. UI accesible de login/cambio de entidad/error/factor, foco visible y teclado. No necesita colas o conectores sin consumidor, ni E2E completo de ventas.

## M02: identidades y versiones

Party identifica persona/organización; los roles cliente/proveedor/socio no crean duplicados por sí solos. Identificador fiscal requiere país/tipo/valor normalizado y estado de verificación; no inventar RUC a consumidores anónimos. Un nombre o cuenta bancaria no demuestra identidad. Relación entre pagador y cliente se acredita en Treasury/Corporate, no mediante merge silencioso de Party.

SKU vendible inicial es un bien. Catalog posee bienes; Procurement posee conceptos de servicios comprados y líneas no inventariables, sin crear un SKU de servicio vendido. Una unidad de servicio no entra al kardex. Unidad base y política de serial son contratos del SKU; tras movimientos no se cambian para reinterpretar cantidades históricas. Unidades alternativas requieren conversión exacta/versionada. Lotes se activan por trazabilidad real; no columna obligatoria vacía para todos.

| Caso / capacidad / clase | Reads / locks | Writes / pre-post / corrección |
|---|---|---|
| Crear/editar Party (C11) / parties.manage / D o V | Identidad normalizada y coincidencias I→M | Alta única o revisión; homónimos no merge automático. Cambio de identidad legal con historia requiere revisión separada; snapshots previos permanecen |
| Crear/editar SKU (C12) / catalog.manage / D o V | Código, unidad, clase, uso I→M | Unicidad por entidad; desactivar impide nuevos usos, no oculta movimientos. Cambio incompatible después de uso se hace con SKU nuevo y relación documentada |
| Mapping externo (C12) / catalog.map / V | Conexión, identidad remota y maestro K→M | Correspondencia versionada, un destino inequívoco por versión; cambio invalida previews y publicación pendiente. No modifica pedidos ya aceptados |
| Preparar import / dominio.import / D | Archivo sellado, formato/versión y masters I→B→M | Preview con filas, errores y hashes del input/políticas/revisiones. Parser fuera de TX; ninguna fila empresarial confirmada |
| Aceptar import (C25) / dominio.import + permisos de efectos / D | B→M y recursos del comando destinatario en orden global | Releer fingerprint/revisiones. M02 acepta un lote acotado atómicamente; tamaño máximo a medir. Fraccionar exige lotes hijos explícitos y reporte de éxito parcial, no timeout con estado ambiguo |
| Corregir import / mismo dueño / D | Lote original y efectos confirmados | Nueva intención y comandos de corrección; nunca reemplazar archivo original ni borrar efectos por quitar una fila del CSV |

Previews no conceden permisos ni congelan autorización. CSV con fórmulas se presenta/exporta como texto; entradas y PDFs son datos no confiables. UX muestra duplicados probables, cambios antes/después, filas rechazadas y motivo; no puede “aceptar todo” si queda identidad dudosa. Lecturas buscables/paginadas preservan permisos y muestran desactivados cuando explican historia.

Salida M02: escenarios de homónimo, identificador duplicado concurrente, mapping cambiado después de preview, import repetido, referencias entre entidades, servicio enviado a Inventory rechazado, archivo alterado, unidad incompatible y desactivación con historia. UNIT para normalización; DOMAIN para reglas; PostgreSQL para unicidad/atomicidad; un E2E del preview→confirmación. Nada autoriza duplicar estas reglas en UI.

## Handoff y gates

M01: Astra architect/checkpoint de seguridad; Sol orquesta; implementador de WO y reviewer independiente. M02: misma estructura, Astra ante identidad/pertenencia o cambio de contrato. Entradas canónicas son este documento y sus enlaces, CM0 y tarjeta del [programa](../../roadmap/program.md). Permitido elegir nombres internos/fixtures/índices demostrables; prohibido cambiar autenticación, propiedad, retención, identidad o semántica de import sin ADR/spec. Salida documental exige revisión separada; salida ejecutable posterior exige evidencia del candidato exacto y cierre de [DH5](../../roadmap/decisions-gaps.md#dh5) antes de operación.

## Incremento profesional M02 propuesto

**Propuesta pendiente de revisión independiente**, conforme a review. [Catalog/sedes](../flows/catalog-sites-warehouses.md): departamentos/perfiles/UOM/identificadores/kits, sedes distintas de almacenes; [sourcing](../flows/sourcing-imports.md): proveedor/evaluación y cuenta aprobada por Treasury. [Documents](../flows/records-signatures-site-packs.md): originales/firma/custodia como consumidores posteriores. No adelanta movimientos a M02.
