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

La precisión intermedia y las escalas de cantidades/precios/FX son parámetros PROVISIONAL; los valores 38/6/6/10 no se convierten en defaults implementables por estar escritos aquí. Su aceptación requiere rangos de operandos, longitud de acumulaciones, operaciones/conversiones previstas y fronteras de cuantización; después, evidencia ejecutable de extremos, residuos y rechazo de pérdida de precisión no autorizada. El rango monetario y el máximo de dígitos físico dependen de ese análisis. HALF_UP conserva su condición comercial provisional; no es regla fiscal. No se crean campos ORM ni se inventan límites para cerrar esta incertidumbre.

El suelo/techo de una fecha proviene del hecho o de una regla validada. No imponer que una recepción real ocurrió después de la fecha técnica de captura de una compra; puede haber registro tardío. Registrar tardíamente exige motivo y tratamiento de período cerrado. Un suelo fiscal no conocido permanece no definido, no inventado.

## Identidad y relaciones

- PK interna bigint para filas ordinarias: pequeña y compatible con Django. No se expone como autorización ni número comercial.
- UUIDv7 como ID público de agregados/documentos/eventos que deban circular entre módulos. No hace falta un segundo UUID en cada fila auxiliar. Python 3.14 lo proporciona sin dependencia adicional [S03](../decisions/sources.md).
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

## Reporting, imports y exports

Consultas paginadas con orden estable; keyset cuando el volumen lo justifique. Listas frecuentes deben tener filtros e índices asociados al acceso por entidad. Cálculo comercial reutiliza políticas del dueño; los informes pueden combinar contratos/proyecciones de lectura publicadas, nunca escribir tablas operativas.

CSV/Excel/PDF son formatos de salida, no bases paralelas. Procesar por lotes/streaming limitado; imports pasan por staging y validación, informe de errores y aplicación idempotente por fila/lote con semántica declarada. Nunca confirmar todo un archivo como efecto de subirlo. Neutralizar fórmulas en exportaciones de texto no confiable a hojas de cálculo.

Un reporte largo captura filtros, entidad, actor, versión/cursor de datos y fecha de corte; vuelve a comprobar permisos al descargar. Se genera fuera de transacciones operativas largas. Consistencia de snapshot entre páginas/chunks debe especificarse: repetir consultas bajo READ COMMITTED no da por sí solo un reporte histórico consistente. Sin data warehouse ni réplica inicial; aislar carga mediante límites y trabajo durable cuando aparezca consumidor.

La [arquitectura operativa](../operations/delivery.md) define migraciones, retención, backup y restore. El mero dump de PostgreSQL no incluye blobs ni todas las configuraciones externas.
