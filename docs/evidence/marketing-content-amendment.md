# Marketing Content / Media Library — expediente del autor

**PENDING INDEPENDENT REVIEW.** Evidencia documental del autor; no aceptación independiente, ensayo ejecutado, política real aprobada ni autorización de código. **IMPLEMENTATION NOT AUTHORIZED. WORK ORDER DELTA NOT YET GENERATED.** [Review](../review.md) es la autoridad de fase.

## Origen y cierre separado de PR10

Requisito nuevo confirmado por el propietario: centro de contenido comercial con biblioteca profesional pequeña y carpetas administradas desde CasPro. **POST-FREEZE SCOPED SEMANTIC AMENDMENT**, no defecto retroactivo de F01–F07 ni de la regeneración anterior.

| Identidad / resultado | Evidencia verificable |
|---|---|
| PR #10 aceptado independientemente por resultado comunicado por propietario | HEAD `9fadf6569e98298d7db3a5fbd6bc53575adf4ff7`; tree `9189869d1495dd25a5d2d68d6874990348053618`; F-WO-01/F-WO-02 PASS |
| Precondiciones Phase A | PR OPEN/no merged, branch local/remota docs/regenerate-work-orders, HEAD/tree exactos, árbol limpio; main/origin/main `b27e5eeb280b8b654b18218a11181e9c4a8eb7b1` sin avance incompatible |
| Commit de estado único | `58b24e2c5f893053f25cc312920476c9530f9f20`; tree `a70215f850e062f7e7c0380c305acf9f2e933592`;4 archivos,15 adiciones/5 eliminaciones, solo review/índice WO/cabecera expediente/índice evidencia |
| Equivalencia del cierre | 84 fichas y contratos semánticos sin cambio frente al candidato aceptado; REQUEST CHANGES/FIXED pendientes preservados como historia. El expediente del autor no se reescribió como review independiente |
| Merge autorizado | [PR10](https://github.com/mat-l-dev/CasPro-ERP/pull/10) MERGED,2026-09-13T01:41:54Z, **MERGE COMMIT** `3f0dc782468c83749bcc08a2ad13f218d3889314`, tree `a70215f850e062f7e7c0380c305acf9f2e933592` idéntico al cierre editorial |
| Main de partida Phase B | HEAD `3f0dc782468c83749bcc08a2ad13f218d3889314`, tree `a70215f850e062f7e7c0380c305acf9f2e933592`; local/origin iguales y limpios. Rama integrada eliminada local/remota después de probar ancestro; nueva `docs/marketing-content-media-library` desde ese main |

PR #10 no se vuelve a modificar en fase B. La cabecera de specs/index aún decía “conjunto candidato pendiente” al inventariar esta fase: se sincroniza aquí junto a su nuevo routing Marketing, sin otro commit ni modificación de PR10; es una omisión editorial de routing del cierre, no cambio del baseline ni de sus fichas.

## Decisión y alcance

[Spec única](../specs/flows/marketing-content-media-library.md) contiene semántica completa. Opción **C**, pequeño dueño Marketing, porque campañas/revisiones/aprobaciones/usos son hechos independientes de custodia, Catalog y Sales. No app, módulo Privacy/Communications/Media paralelo, CMS/DAM genérico ni diseño gráfico. Documents conserva DocumentVersion/objetos/hashes/derivados/retención; Integrations transporte futuro; Access permisos/DataRestriction; Audit rastro; Operations incidente/restore. Dueño de finalidad Marketing no es autoridad jurídica: responsable acreditado/profesional decide, Documents custodia, Corporate coordina facultades.

| Familia de decisión | Resultado candidato / por qué |
|---|---|
| Organización | Root por entidad, carpetas con identidad estable, parent/nombre/revisión/ciclo; activo en una primaria + tags/campañas múltiples. Move/rename no toca bytes ni permisos; archive carpeta solo vacía; prevención de ciclos concurrentes |
| Activo y derechos | Asset estable → revisión editorial → referencias DocumentVersion. Estado técnico, aprobación por uso y publicación separados. RightsRevision + evidencia/destino/finalidad/vigencia; contracción actual prevalece. Dedupe no fusiona negocio |
| Custodia | PostgreSQL metadata, object storage bytes detrás del adapter existente. Original inmutable; derivados con hash/lineage/preset. Referencias Documents atómicas impiden purga concurrente o pérdida por reutilización |
| Campañas y marca | Campaña revisable agrupa productos/activos/copy/planes sin crear orden ni ad-network. Kit versiona logos/colores/tipografías/guidelines; no duplica licencias de font ni crea engine |
| Copy y precio | Texto plano con revisiones/aprobación por uso. Snapshot comercial fija fuente/revisión/precio/condiciones; no precio vivo en banner ni segundo Catalog |
| Plan y registro | Plan fija revisiones/representaciones/destino/ventana/responsable. MANUAL_EXTERNAL conserva tiempos/fuente/evidencia/ID externo y linaje acreditado; hecho sin autoridad se registra con advertencia, no aprobación retroactiva. Identidad incierta UNRESOLVED |
| Automatización futura | Marketing intención empresarial, Integrations attempt/HTTP; CONFIRMED/FAILED/UNKNOWN por evidencia de superficie. Reconciliar original, nunca retry ciego. API/media/tema no son una autoridad interna |
| Seguridad/privacidad | Quarantine, SVG raster, parsers sin red/límites, EXIF separado, proxy autenticado, no buckets públicos ni original por preview. Filtro antes de facetas/thumbnail. Restore normal READ+outbound OFF hasta diario posterior completo |
| Acceso | 17 IDs nuevos registrados,276 totales sin duplicados; dos roles específicos,23 humanos propuestos. Seis IDs Documents/support y privacy.execute reciben elegibilidad acotada a consumidores Marketing, sin expansión automática de OPERATIVOS. No ID de ejecución social ni principal técnico nuevo |
| Gobernanza | MARKETING_CONTENT descriptor/policy exactos; contexto P exige privacy.context.prepare AND marketing.policy.prepare AND configuration.prepare sobre misma entidad/P/scope. SoD de contenido SOD-12; no exención profesional por autofirma |
| Roadmap | M03+ paralelo después de Access/Audit/config/privacy M01, Catalog M02 y Documents/restore M03; no dependencia inversa de B2C/stock/Accounting. Núcleo CONFIRMED_BUILD; personas/políticas ACTIVATION_ONLY; social automático/IA/analytics OPTIONAL_FUTURE |

Research oficial con fuente/fecha y límites en [MC-S01–09](../research/marketing-content-providers.md): Meta distingue login/cuenta/superficie y container/resultados; Pages feed tiene programación, no universal para todas las superficies. Jumpseller expone imágenes de producto/página y tiene componentes de banners de tema distintos. Adobe/Odoo aportan patrones de revisiones/representaciones/metadata; no se importan sus permisos por defecto, purga automática o bloat. Fuente mutable se revalida antes del adaptador; no credenciales ni llamadas de tienda.

## Work order impact

**No se crean IDs, fichas, plantillas ni DAG nuevo.** Las84 WOs aceptadas siguen baseline válido de su alcance original; cero cuerpos modificados. Cobertura original87/87 y178 HARD acíclicos raíz WO-M01-01 no cambia. El nuevo mapa propone6 capacidades adicionales (93 total):87/93 cubiertas por WOs existentes;6 requieren delta después de aceptación y mandato posterior. No atribuirlas a títulos genéricos de WOs previas.

| Clasificación | Miembros / alcance exacto |
|---|---|
| UNCHANGED_EXISTING_WOS | 78 fichas: todas las84 salvo las6 listadas abajo. Incluye WO-M01-01 bootstrap, WO-M01-02 Audit, WO-M02-02 Catalog como prerrequisitos por contrato existente; stock/B2C/Treasury/Accounting/Tax no requieren Marketing |
| EXISTING_WOS_REQUIRING_FUTURE_DELTA | WO-M01-04: matrices de aislamiento/resource scope Marketing; WO-M01-05: dos plantillas/17 IDs/SoD-12; WO-M01-06: descriptor MARKETING_CONTENT; WO-M01-07: nueva finalidad/P/contexto y aplicación de restricción; WO-M03-01: formatos/derivados/referencias de custodia y conjunción original Marketing; WO-M03-03: manifiesto/restore sensible con derechos posteriores y nuevas relaciones. Seis contratos/evidencias se extenderán mediante delta posterior; las fichas actuales no son falsas para el alcance que aceptó PR10 y permanecen intactas |
| NEW_WOS_REQUIRED | Familias estimadas: biblioteca media/organización/revisiones/derechos; campañas/copy/kit de marca; calendario/registro manual externo. Decomposición/tamaño/IDs finales y HARD edges se decidirán solo al encargar WO delta del amendment aceptado |
| DEFERRED_WOS_ONLY_ON_TRIGGER | Adaptadores Meta por login/superficie y Jumpseller media/theme (incluye extensión de consumidor WO-M03-09 al trigger), IA de sugerencias y analytics/paid ads separados. D03 o D01 según efecto; ninguna ficha ni ejecución ahora |

El impacto es extensión de consumidores, sin declarar inválidas las garantías anteriores ni afirmar evidencia runtime. La independencia del nuevo incremento evita invalidación masiva y mantiene M01–M09. Conservar las seis fichas no significa que ya implementen Marketing: cobertura del delta sigue pendiente.

## Adversarial cases

Los40 escenarios del encargo se resolvieron **a nivel de contrato**, en [spec](../specs/flows/marketing-content-media-library.md). PASS documental del autor en cada fila; todas las pruebas ejecutables quedan REQUIRES LATER VALIDATION bajo gates pertinentes.

| Caso | Contraejemplo | Resultado definido |
|---|---|---|
| 01 | Banner V1 usado públicamente, luego V2 | V1/DocumentVersion y PublicationRecord permanecen; V2 nueva revisión, nunca overwrite |
| 02 | Rename de carpeta tras publicar | Cambia organización/nombre; IDs, hashes y publicaciones no cambian |
| 03 | Move de activo | Una primaria cambia bajo scopes origen/destino; no movimiento físico ni concesión de audiencia |
| 04 | Imagen en dos campañas | Dos vínculos versionados a revisión elegida; no copia del activo por campaña |
| 05 | Bytes idénticos, dos activos empresariales | IDs/derechos/retenciones independientes; dedupe Documents no fusiona |
| 06 | Revisión aprobada seguida de draft | Current puede señalar draft; no sustituye uso aprobado de revisión anterior |
| 07 | Campaña antigua referencia revisión vieja | Manifest/versiones preservados, no “última aprobada” dinámica |
| 08 | Precio Catalog cambia después del banner | Snapshot comercial antiguo permanece; nueva preparación revalida vigencia/contexto |
| 09 | Producto archivado y campaña histórica | Referencia protegida, sin cascade; histórico persiste y nuevo uso revisa vigencia |
| 10 | Campaña visible, activo no | Intersección por objeto/permiso antes de proyectar; no thumbnail/título/ID oculto |
| 11 | Counts/tags revelan activo oculto | Filtro previo a facetas/autocomplete/aggregates; sin conteos de placeholders ocultos |
| 12 | SVG malicioso | Cuarentena/validación; original nunca inline; raster aislado sin red, rechazo si peligroso |
| 13 | EXIF GPS | Inspección con acceso restringido; derivado de difusión elimina metadata según decisión; original no sobrescrito |
| 14 | Rostro o sitio cliente | P/contexto/finalidad/autoridad acreditados por uso; sin contexto, recepción mínima restringida o HOLD |
| 15 | Derechos sin evidencia | PENDING bloquea aprobación/difusión; file AVAILABLE no crea licencia |
| 16 | Hold legal/privacidad | Conservación restringida y restricciones actuales prevalecen; no purga ni difusión por aprobación vieja |
| 17 | Delete después de publicar | Archive/retire no destruyen hecho; purge solo por plan autorizado/retención/referencias, historia mínima preservada |
| 18 | Original ausente, thumbnail existe | Original MISSING; no nuevo uso/descarga original; derivado íntegro visible solo autorizado y rotulado |
| 19 | Hash/lineage de derivado inconsistente | Cuarentena y regeneración desde original íntegro; no usar derivado corrupto como prueba |
| 20 | Timeout Meta futuro | UNKNOWN, retener intención e identidad; consultar/reconciliar antes de nueva ejecución |
| 21 | Confirmación tardía de proveedor | Observación idempotente ligada al intento/cuenta original; no revive revisión sustituida ni crea nuevo envío |
| 22 | Publicación manual registrada después | Dos tiempos/fuente/registrador y responsable; MANUAL_EXTERNAL, ninguna ejecución CasPro inventada |
| 23 | Mismo activo Instagram y Facebook | Dos usos/canales y hechos independientes, cada uno con permisos/derechos/revisión |
| 24 | Plan nunca ocurrido | MISSED derivado de ventana y ausencia de observación; nunca PUBLICADO por calendario |
| 25 | Campaña archivada, posts públicos | Publicaciones externas permanecen; archivo no supone retirada remota |
| 26 | Imagen Jumpseller vieja tras nueva revisión | Mapping/observación sigue revisión usada; cambio interno no publica ni sustituye remoto |
| 27 | Copy2 aprobado, Copy3 draft | Manifest usa Copy2 hasta nueva revisión/aprobación explícita |
| 28 | IA propone texto sin humano | Draft/sugerencia, sin aprobación/publicación; ZERO AI inicial completo |
| 29 | Carpeta con50.000 activos | Paginación keyset/metadata, árbol por nivel, lazy thumbnails y límites; B15 mide, no claim de benchmark ejecutado |
| 30 | Restore anterior a restricción nueva | Diario posterior fuera del rollback, lecturas/outbound OFF hasta reaplicar derechos/restricciones/grants y reapertura independiente |
| 31 | Signed URL sobrevive revocación | Preview inicial usa proxy autenticado sin URL de objeto reutilizable; ruta heredada no revocable se suspende, ventana residual se registra. Bytes ya entregados no son recuperables |
| 32 | Activo de otra entidad | Denegación/FK pertenencia antes de lectura/vínculo; no dedupe/search cruzado |
| 33 | Original privado marcado público | Invariante de storage/serving deniega; incidente Access/Operations, retirar exposición y reconciliar sin declarar cero fuga previa |
| 34 | Derivado sin EXIF, original preservado | Dos hashes/objetos y lineage/preset; original restringido permanece, no se etiqueta sanitizado como original |
| 35 | Download original sin permiso | Requiere marketing.download_original AND marketing.view AND documents.view AND documents.download, misma audiencia/revisión |
| 36 | Requisito de canal cambia después de aprobar | Aprobación histórica intacta, readiness actual inválida; nueva representación/revalidación antes de efecto |
| 37 | Meta cambia scopes/API | Adapter HOLD/currentness por superficie/cuenta; no ampliar permiso ni continuar por viejo ACK |
| 38 | Upload Jumpseller falla, activo válido | Resultado externo FAILED/UNKNOWN separado, activo local no se invalida ni se borra |
| 39 | Aprobado Jumpseller, no social | Guardas de canal rechazan social; roles no expanden la aprobación |
| 40 | Derechos solo catálogo interno | Intersección de finalidad/canal/territorio/vigencia bloquea difusión social aunque exista permiso técnico |

Revisión adicional de concurrencia/autoridad: dos moves que formarían ciclo serializan en árbol; aprobación frente a retiro/contracción se ordena bajo A5/M25/G30; purge frente a attach usa D80 y referencias Documents transaccionales; nueva clave D no evade ID externo único; actor con dos roles no borra SoD; registrar hecho externo no requiere fingir aprobación retroactiva. Esos casos explican el mecanismo, no certifican PostgreSQL ni seguridad implementados.

## Gates y recomputación

[Matriz canónica](../roadmap/decisions-gaps.md#marketing-content-gates): **A0 / B16 / C13 / D6**, todos35 B/C/D OPEN, sin adición/cierre. Autor identifica0 nuevos gaps A: dueño, estados, identidad, corrección, autorización y fronteras están especificados. Revisión independiente puede refutar esta conclusión; no se convierte en A0 aceptado por la tabla.

B02/B03/B09/B10/B13/B15 cubren mecanismos nuevos; B12 transporte futuro; B16 IA futura y B14 equivalencia condicional. C06 por autoridad legal/privacidad/derechos concreta, C10 custodia/retención, C12 soporte real, C13 grants/configuración, C11 solo efecto/transferencia externa real. D03 futuros adaptadores/analytics/paid ads; D01 IA sugerente. B11 no se usa para imagen, C04 no para aprobación, D04 no para Brand Kit básico, D05 no para engagement y D06 no para calendario. No gate inventado por existir feature; no se distorsiona uno para conservar cifra.

## Inventario y delta documental

Fuentes inventariadas por frontera, sin cargar legacy/Wbpro: producto, ownership/ADR-001, datos/Documents, access/roles/configuración/CM0, integración, privacidad/threat/restore, UI/automatización/QA y programa/capabilities/gaps. F01–F07/normativa, skills/agentes y contratos de dinero/stock/Accounting/Tax no requieren corrección por este encargo.

Archivos de fase B (26):

- Nuevos: `docs/specs/flows/marketing-content-media-library.md` (contrato profundo); `docs/research/marketing-content-providers.md` (fuentes y límites); este expediente.
- Ownership/routing: `docs/architecture/boundaries.md`, `overview.md`, `data.md`, `integrations.md`, `ui.md`, `automation.md`.
- Autoridad: `docs/architecture/capability-registry.md`, `roles-delegation.md`, `configuration-governance.md`; `docs/specs/cross-cutting/command-matrix.md`. Configuración y CM0 se incluyen por necesidad real: finalidad nueva sin descriptor o lock root sin registro dejarían autorización/atomicidad ambiguas.
- Seguridad/operación: `docs/security/personal-data-lifecycle.md`, `threat-model.md`; `docs/operations/delivery.md`; `docs/quality/strategy.md`.
- Producto/roadmap: `docs/product/charter.md`; `docs/roadmap/capabilities.md`, `program.md`, `decisions-gaps.md`.
- Estado/navegación: `docs/review.md`, `docs/index.md`, `docs/specs/index.md`, `docs/evidence/index.md`, `docs/research/index.md`.

La spec concentra detalle; otras fuentes solo añaden ownership/autoridad/routing/placement o extensión local necesaria. Seis filas de elegibilidad de soporte y privacy.execute para MC10 se amplían explícitamente, no se renombran IDs ni se amplía OPERATIVOS. Los84 cuerpos/índice/DAG/coverage de WOs permanecen exactamente como en main del cierre; nueva cobertura se informa en roadmap/review/evidencia, no reescribe baseline aceptado.

## Comprobaciones y límites

Verificación estática ejecutada: **903 enlaces/anchors locales** en los26 archivos cambiados, sin errores; identidad/duplicación de capabilities (276 registrados,17 nuevos), consumidores y scopes; coincidencia ownership de spec/boundaries; referencias de gates B16/C13/D6, todas abiertas; integridad de las84 WOs,178 HARD y raíz única conservadas por comparación con main; diff exclusivamente Markdown dentro del alcance. Resultado final de las comprobaciones se fija en PR con HEAD/tree exactos después del commit; este documento no intenta contener su propio hash.

La matriz40/40 es autorrefutación documental. Pendiente: reviewer separado del candidato exacto; toda evidencia de runtime/RLS/locks/parser/restore/UI/carga/proveedor, políticas/datos/grants y futura WO delta. No tests de aplicación, builds, Docker, migraciones, llamadas a cuentas/proveedores, datos reales ni implementación. Preguntas al propietario: **0**.

**PASS — MARKETING CONTENT / MEDIA LIBRARY AMENDMENT READY FOR INDEPENDENT REVIEW** (veredicto del autor, sujeto a comprobación final y reviewer independiente).

**WORK ORDER DELTA NOT YET GENERATED. IMPLEMENTATION NOT AUTHORIZED.** Nuevo PR debe quedar OPEN, sin autorización de merge.
