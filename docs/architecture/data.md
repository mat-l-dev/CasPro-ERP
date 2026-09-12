# Datos, precisión y evolución

Contrato de [ADR-006](../decisions/adr-006-data.md). Modelo empresarial: [domain/model](../domain/model.md).

## Primitivas

| Primitiva | Decisión | Consecuencia |
|---|---|---|
| Dinero | Decimal en aplicación y numeric en PostgreSQL; moneda obligatoria. PEN/USD iniciales a dos decimales de importe monetario | No float ni PostgreSQL money. JSON transmite importes como cadenas decimales + moneda |
| Cálculo | Decimal; 38 dígitos de precisión intermedia es un candidato PROVISIONAL, no una garantía de suficiencia | Cuantizar en fronteras definidas; rechazar NaN, Infinity, desbordamientos y pérdida de precisión no prevista por la política |
| Precio unitario | Hasta seis decimales como base técnica candidata | No confundir precio/coste unitario con importe de línea; calibrar con catálogo real |
| Cantidad | Decimal, hasta seis decimales, unidad explícita y paso permitido por SKU | Una unidad serial indivisible no admite fracciones; conversiones versionadas conservan unidad base |
| Tipo de cambio | Decimal hasta diez decimales como base candidata; origen, sentido, fecha y versión | Guardar importes original/convertido y redondeo; no sumar monedas ni recalcular historia con tasa actual |
| Redondeo | HALF_UP comercial propuesto; reparto con residuo exacto | Política comercial PROVISIONAL; reglas contables/fiscales específicas no se deducen de esta elección |
| Tiempo técnico | Instantes conscientes de zona, persistidos en UTC | Visualización America/Lima inicial; correlación no depende del reloj del navegador |
| Fechas empresariales | Fecha de operación, documento, contabilidad e impuesto son conceptos distintos | No derivar automáticamente todas del created_at ni intercambiarlas |

La precisión intermedia y las escalas de cantidades/precios/FX son parámetros candidatos; 38/6/6/10 no son defaults implementables por estar escritos aquí. Precio comercial, coste unitario, valor de stock e importe de liquidación son magnitudes diferentes: [Inventory](../specs/milestones/inventory-deep.md) propone 12 decimales de coste y 6 de valoración, sin contradecir los 6 de precio comercial. Ninguna presentación de dos decimales recorta el coste conservado. La política versionada declara escala por magnitud, frontera de cuantización, método y reparto de residuos; la última parcialidad consume el remanente exacto. Correcciones conservan la política histórica y producen deltas, no recálculo silencioso.

El contrato congela Decimal, rechazo explícito de entradas no representables, conservación del total y separación cálculo/presentación/liquidación. La futura WO documenta límites de operandos/acumulaciones y demuestra extremos y error acotado antes de aceptar una representación física ([B04](../roadmap/decisions-gaps.md#implementation-gates)). Puede ampliar precisión/almacenamiento sin alterar importes empresariales aceptados; si exige cambiar política, unidad, pool o reconocimiento, requiere amendment de diseño. HALF_UP sigue candidato comercial a aprobar antes de operación; ninguna regla fiscal se deduce de él ([C03](../roadmap/decisions-gaps.md#activation-gates)). No se crean campos ORM ni límites ficticios.

El suelo/techo de una fecha proviene del hecho o de una regla validada. No imponer que una recepción real ocurrió después de la fecha técnica de captura de una compra; puede haber registro tardío. Registrar tardíamente exige motivo y tratamiento de período cerrado. Un suelo fiscal no conocido permanece no definido, no inventado.

## Identidad y relaciones

- PK interna bigint para filas ordinarias: pequeña y compatible con Django. No se expone como autorización ni número comercial.
- UUIDv7 como ID público de agregados/documentos/eventos que deban circular entre módulos. No hace falta un segundo UUID en cada fila auxiliar. Python 3.14 lo proporciona sin dependencia adicional [S03](../research/technical-sources.md).
- UUIDv7 revela orden temporal aproximado; no sirve como secreto o token de acceso. No determina orden causal de eventos; existe revisión/secuencia por agregado.
- Correlativos comerciales y números fiscales tienen espacio propio por entidad, tipo y serie según la norma/política aplicable. Ninguna clave global impone accidentalmente la regla tributaria de numeración.
- Claves externas: proveedor + cuenta/instalación + entidad + ID externo. Se conservan opacas. Un mensaje de otra conexión nunca cambia de empresa por traer un campo tenant_id.
- Identidad de intención cuando se requiera deduplicación: entidad + operación + clave, con ámbito de principal/mandato cuando el caso lo necesite. Alcance, fingerprint, retención y tratamiento de conflictos se especifican conforme al [contrato de idempotencia](transactions.md); no se exige una clave adicional a toda lectura o escritura por su método HTTP.

Las FKs empresariales deben impedir referencias entre entidades: identidad del objetivo más pertenencia forman la restricción cuando procede. La traducción exacta de restricciones compuestas al ORM/migraciones es REQUIRES LATER VALIDATION. No sustituirla por un test de formulario ni usar primitivas internas no soportadas del ORM.

No prohibir toda FK entre módulos por estética: se admite sobre una clave pública estable, con contrato y eliminación protegida. Sí se prohíbe usarla para navegar/escribir estructuras privadas o generar cascadas entre propietarios.

## Datos originales, derivados y JSON

Modelo relacional para dinero, aplicaciones, stock, membresías, estados y sus vínculos. JSON solo para payload externo/versionado o detalle variable con esquema, tamaño y consumidor definidos; no reemplaza relaciones ni columnas críticas.

Los snapshots conservan lo necesario para reproducir una decisión: identidad fiscal usada, bases/importes, política vigente y evidencia. No copiar perfiles enteros. Cada proyección publica origen, versión/cursor y momento de actualización; una proyección atrasada de reporte no autoriza una transición crítica.

Maestros y borradores pueden modificarse con concurrencia optimista y auditoría proporcional. Historia económica y auditoría crítica usan restricciones de escritura y reversión explícita. Datos temporales, sesiones, exportaciones caducadas y contenido rechazado pueden purgarse conforme a retención aprobada; no heredar «nunca borrar nada» universalmente.

## Archivo documental existente

Documents conserva PDF, XML y otros artefactos privados; object storage conserva bytes y PostgreSQL identidad/entidad, metadata, procedencia, hash, versión, retención y relaciones autorizadas con hechos empresariales. Una versión disponible no se sobrescribe: corrección o representación nueva conserva relación con su origen. Tipo declarado, contenido detectado, origen de adquisición/generación y condición original/representación son explícitos. Un XML reconstruido por CasPro jamás se etiqueta XML original; hash comprueba integridad, no autenticidad. El expediente y su estado comercial siguen en Sales/Procurement.

Preview rápido de PDF mediante contenido o representación derivada autorizada, cacheada por entidad/artefacto/versión con caducidad; descargar o previsualizar exige permisos actuales. Sin buckets públicos ni visores externos que reciban documentos privados por defecto. Cuarentena/análisis preceden disponibilidad; [integraciones](integrations.md) gobierna carga no atómica, huérfanos y links breves. Proveedor de storage, límites/tiempos de preview y retención concreta son PROVISIONAL hasta condiciones de operación; no se inventan plazos legales.

## Reporting, imports y exports

Consultas paginadas con orden estable; keyset cuando el volumen lo justifique. Listas frecuentes deben tener filtros e índices asociados al acceso por entidad. Cálculo comercial reutiliza políticas del dueño; los informes pueden combinar contratos/proyecciones de lectura publicadas, nunca escribir tablas operativas.

CSV/Excel/PDF son formatos de salida, no bases paralelas. La importación CSV/Excel sigue validate → preview → confirm: staging con archivo/versión y errores, vista de cambios propuestos y confirmación explícita mediante comandos del dueño. Declarar atomicidad/fallos por fila o lote y deduplicación según efecto; confirmar revalida permisos y revisiones, y cambios relevantes invalidan el preview. Nunca ejecutar macros/fórmulas del archivo ni confirmar negocio por subirlo. Procesar con límites; neutralizar fórmulas en exportaciones de texto no confiable a hojas de cálculo.

Un reporte largo captura filtros, entidad, actor, versión/cursor de datos y fecha de corte; vuelve a comprobar permisos al descargar. Se genera fuera de transacciones operativas largas. Consistencia de snapshot entre páginas/chunks debe especificarse: repetir consultas bajo READ COMMITTED no da por sí solo un reporte histórico consistente. Sin data warehouse ni réplica inicial; aislar carga mediante límites y trabajo durable cuando aparezca consumidor.

Los informes permiten preview temporal o snapshot PDF persistido en Documents con origen, corte y versión de cálculo. Un preview no es automáticamente evidencia retenida; un snapshot es representación generada, no documento original externo. Coste y margen bruto básico usan la fórmula ya especificada en [SP2: lecturas](../specs/flows/first-operational-circuit.md): ingresos comerciales de mercadería netos de descuentos/ajustes atribuibles menos coste de las unidades incluidas, misma moneda/corte, base de impuestos declarada y cargos ajenos separados. No etiquetar neto de impuestos si no se pueden separar con evidencia. Coste faltante/provisional queda visible y no se trata como cero ni como margen definitivo. Preservar líneas, costes, ajustes y hechos fuente permite Accounting futuro; no crea asientos ni determina reconocimiento contable.

La analítica adicional de rentabilidad con gastos indirectos o nuevos KPIs se difiere hasta su encargo ([D05](../roadmap/decisions-gaps.md#deferred)); no difiere el margen básico SP2 ya definido. El resultado contable y margen de G1 tienen definición propia en [reporting](../specs/acceptance/reporting-goldens.md); no se deducen del indicador comercial.

La [arquitectura operativa](../operations/delivery.md) define migraciones, retención, backup y restore. El mero dump de PostgreSQL no incluye blobs ni todas las configuraciones externas.

## Originales, perfiles y exportación profesional

**Propuesta pendiente de revisión independiente**, conforme a review. [Catalog](../specs/flows/catalog-sites-warehouses.md) define atributos tipados por familia, conversiones efectivas y evidencia por modelo. [Documents](../specs/flows/records-signatures-site-packs.md) define bytes originales inmutables fuera de PostgreSQL, derivados con hash propio, custodia, cuotas y copia de objetos separada. [Tax/import-export](../specs/flows/tax-workspace-books.md) exige schema/preview/revalidación/manifest y formato oficial por obligación, sin overwrite de hechos.
