# Auditoría de pcge-peru 0.2.0

Corte 2026-09-11. Evidencia de código y ejecución **de la librería externa**, no de CasPro. Se usó un checkout temporal independiente y sin modificaciones; no se ejecutó Wbpro. El permiso excepcional para estas pruebas no habilita tests, builds ni implementación de CasPro.

## Identidad comprobada

| Evidencia | Resultado |
|---|---|
| Repositorio/tag | [pcge-peru v0.2.0](https://github.com/mat-l-dev/pcge-peru/tree/v0.2.0) |
| Tag anotado / commit resuelto | `3963267e01a759675f25f181277575a36fb8ccbe` / `ade8ea1505c0841a586a7e310314e76df623fe20` |
| Versión y runtime | 0.2.0; Python `>=3.14,<3.15`; sin dependencias de ejecución declaradas |
| Licencia de código | Apache-2.0; no convierte documentos oficiales de terceros en propiedad de la librería |
| Publicación | Release 2026-09-10 16:29:25 UTC; [metadatos PyPI](https://pypi.org/pypi/pcge-peru/0.2.0/json) comprobados |
| Wheel | `pcge_peru-0.2.0-py3-none-any.whl`; SHA-256 `f0a102dc178998dbff34673e77c21b100f772fa237ad99f22e3e2263da5eafc0` |
| sdist anunciado en PyPI | SHA-256 `a7330a6487d033dc35e4d3651269ba70880eb5741700debd3444c047afa98f54`; no se construyó una distribución |
| Correspondencia wheel/tag | Los archivos `pcge/` del wheel descargado en memoria coinciden con el tag tras normalizar finales de línea; no se instaló el wheel |
| Pruebas | **413 passed**, 4.52 s, CPython 3.14.6, pytest y jsonschema; bytecode/cache desactivados, temporales fuera del checkout; estado Git limpio al terminar |

Se leyeron la API exportada, loader, catálogo, modelos, enums, excepciones, metadata, procedencia y anomalías; pruebas representativas de contratos y workflows de distribución. Ejecutar la suite completa no equivale a revisar línea a línea cada test ni a certificar exactitud legal de cada cuenta.

## Contratos y límites reales

`available_versions()` devuelve `('2019', '2026')`. `load_catalog(version)` exige una cadena explícita admitida; no hay selección implícita de “latest”. La carga comprueba JSON estricto, claves/tipos, duplicados, versión del esquema, fechas, conteo, hash de entries y relaciones jerárquicas. Distingue errores de tipo de `PCGEDataError`. No aceptar una versión desconocida sustituyéndola silenciosamente por otra.

El catálogo valida códigos de 1 a 6 dígitos, padres existentes y prefijos exactos, duplicados y ciclos. `get` devuelve `None` para ausencia; indexación lanza `KeyError`; navegación devuelve tuplas y la búsqueda normaliza acentos/capitalización. Los seis dígitos documentales no implican un sexto nivel PCGE: su `pcge_level` es `None`. `anomalies_for` puede mencionar un código excluido: ausencia en el catálogo no prueba ausencia en el PDF.

Las entradas, metadata, procedencia y anomalías son valores congelados. **El objeto catálogo no es profundamente inmutable**: contiene diccionarios privados mutables. Una sonda aislada en memoria sustituyó `_entries` y produjo desacuerdo entre el conteo y la pertenencia de una cuenta. No es un ataque remoto ni un defecto de las consultas públicas; refuta tratar el catálogo como una frontera de seguridad inmutable.

El hash de entries detecta discrepancias con el `source.json` empaquetado, no autentica al editor ni coteja por sí mismo el PDF oficial. El loader no descarga ni valida `source_sha256` contra ese PDF; tampoco demuestra que toda selección editorial/anomalía represente correctamente la norma. El constructor manual puede omitir metadata: no sirve como camino de activación de un catálogo oficial en CasPro.

## Inventario de datos y diferencia estructural

| Campo | 2019 | 2026 |
|---|---|---|
| entries / códigos de seis dígitos | 1,757 / 20 | 1,636 / 12 |
| Anomalías / esquema / revisión | 10 / 1 / 1 | 1 / 1 / 1 |
| SHA-256 entries | `fc70e43b94d0718373ab3b9f81202731e5295ededf0df75231a2ffb3c2beec04` | `70d6cb7dfc501a1306a0e934df48409f70e83ffae033676b49f297d9cbeaf43a` |
| SHA-256 PDF declarado por paquete | `ec0ca9d36cd2f5cdb6d14ecb45a6e510879df929372fdb033bc2df88329eb9f2` | `48c568ca196c68348743dda96c55c38593b0437ce732a4c5d77d7c9aca896b19` |
| Tramo documental declarado | PDF 21–62, impreso 20–61 | PDF 19–52, impreso 17–50 |

Comparación reproducida sobre ambos catálogos: **376 códigos eliminados, 255 añadidos, 1,381 comunes, 273 nombres distintos entre los comunes**. Estas cantidades describen datos; no constituyen una tabla de equivalencias contables ni permiten migrar saldos por coincidencia de código.

Anomalías 2019 identificadas por el paquete: `27233`, `30221-30224`, `33404`, `38472-38474`, `38352`, `63432`, `683351`, `6882-68812-68813`, `70111-70112`, `NOMENCLATURE-61-85-88`. No ocultarlas en la UI del administrador del plan.

Para 2026, el paquete documenta `70992` dos veces: PDF p.48/impresa 46 bajo `7090` (“Relacionadas”), excluida, y PDF p.49/impresa 47 bajo `7099` (“Contrato consultoría TI”), conservada. La extracción del PDF oficial adquirido confirma ambas apariciones y no contiene `70902`. **No inventar `70902`**, editar el dataset ni inferir que esa elección editorial ya está aprobada para uso empresarial.

El [PDF PCGE 2026 publicado por MEF](https://cdn.www.gob.pe/uploads/document/file/10596059/8559200-plan-contable-general-empresarial-pcge-2026.pdf?v=1788969391), 203 páginas, descargado el 11-09-2026, tiene SHA-256 **`5eebb29c5159770a8d6eb3ab77a6cd167a8e9c53e2e7bd7c15b7d61868a50ef1`**, distinto del PDF declarado por el paquete. Esto prueba distinta identidad binaria; no prueba por sí solo diferencias semánticas ni corrupción. **PENDING VALIDATION**: identificar la revisión documental usada por el editor y comparar el tramo fuente antes de activar el catálogo para producción. No sustituir silenciosamente el hash esperado. El hash del PDF 2019 declarado por el paquete tampoco se presenta aquí como cotejado contra una descarga oficial. Suite, fidelidad de extracción y autoridad normativa son verificaciones distintas.

## Decisión CasPro: adapter, no motor contable

**CASPRO DECISION — diseño candidato**: Accounting posee un adapter que carga exclusivamente por `load_catalog`, fija versión de paquete, dataset, esquema/revisión y hashes esperados; expone valores de consulta sin filtrar objetos mutables internos. Guardar la identidad exacta del catálogo con cada versión de plan y asiento. Error de integridad/versionado bloquea activación; nunca cae a un plan vacío o actualizado automáticamente.

El catálogo oficial es referencia de códigos/nombres/jerarquía/procedencia. CasPro conserva separadamente cuentas empresariales, estado habilitado, fechas, moneda/dimensiones, tipo de imputación, reglas de posting y mapas de EEFF. Una cuenta que existe no es necesariamente imputable; la jerarquía no decide reconocimiento, tributo, saldo normal o presentación. Extensiones empresariales tendrán namespace/procedencia propios, no se harán pasar por dataset oficial.

Los asientos guardan snapshot de la denominación y vínculo con la versión usada. Una actualización genera propuesta de correspondencias revisable, detecta cuentas usadas eliminadas/renombradas, permite relaciones uno-a-varios justificadas y nunca reescribe asientos emitidos. Cambio de catálogo no cambia automáticamente marco contable, política ni ejercicio.

**Recomendación provisional para target 2027**: conservar 2019 como opción vigente sin adopción anticipada; evaluar 2026 para un inicio nuevo solo con aprobación explícita de su adopción anticipada y políticas alineadas. La obligatoriedad de 2026 desde 2028 no convierte 2026 en default legal de 2027. La comparación demuestra trabajo de migración real; no demuestra que adelantarlo sea siempre más barato. Resolver elección antes de congelar el plan inicial M07, no pedir al operador cotidiano elegir versiones.

## Evidencia futura exigible al adapter

Contrato con versiones admitidas y entradas ausentes; rechazo de hash/revisión inesperados; protección de aislamiento entre planes de entidades; plan con cuenta oficial de seis dígitos; anomalía excluida y cuenta empresarial distinta; replay de asiento con catálogo anterior; migración uno-a-varios y conciliación de apertura; instalación real en el runtime fijado por M01. La suite externa se reutiliza con su identidad; no se repite para inflar QA ni acredita esos contratos de CasPro.
