# Cambios fundacionales, gaps y decisiones pendientes

Este registro explica evidencia nueva posterior a Gate 1 sin reabrirlo por rutina. Las reglas vigentes viven en sus documentos propietarios.

## Cambios con evidencia

| OLD | NEW | WHY / EVIDENCE | IMPACT |
|---|---|---|---|
| Venta de bienes “recomendada”; servicios sin delimitar | TILMUX vende bienes; compra servicios/gastos no inventariables; no catálogo de servicios vendidos | Decisión del propietario | Charter, model, P2P |
| H1/HP1 decisión pendiente | B2C contado, pago íntegro antes de despacho, sin tolerancia silenciosa | Decisión del propietario | SP2 cobertura/dispatch |
| Costeo sin método final | Promedio ponderado móvil operativo; UNKNOWN no cero; devolución no vendible | Decisión HP3 + NPIF §11 | Inventory/Accounting |
| Contabilidad futura genérica | Arquitectura R2R, NPIF completa V1, PCGE/adaptador versionado y transición | NPIF completa, ERP benchmark, PCGE 2026 | Nuevos docs/roadmap; no código |
| Marco Wbpro asumía `<150`, RCNC 002-2021 y silencios NPIF | `≤150`, RCNC 003-2022; NPIF trata errores y moneda | Fuentes N001–N003 | No trasladar conclusiones Wbpro |
| PCGE 2019 como único horizonte | PCGE 2019 vigente; PCGE 2026 anticipable y obligatorio 2028 | RCNC 002-2026 | versión de plan independiente |
| Corporate sin owner CasPro | Corporate capability posee hechos societarios, sin app anticipada | Requisito y frontera legal real | boundaries/model/roadmap |
| IA solo ADR general | Servicio provider-neutral de candidatos con evaluación y puertos sin escritura | Requisito + investigación Hermes/DeepSeek | arquitectura AI/M06 pilot |
| UI neutral sin modos | LIGHT/DARK/SYSTEM, keyboard, saved views, split preview y document flow derivado | Requisito + HIG/WCAG/benchmark | UI; validación futura |
| WO-SP2-01 “siguiente” automático | WOs SP2 requieren regeneración después del freeze; programa completo decide secuencia | Mandato Grand Master | review/work-orders/roadmap |

## Clasificación vigente de pendientes

Este es el único registro de incógnitas/gates abiertos. Sustituye la clasificación de bloqueos del informe Astra anterior; no cambia hechos normativos ni declara pruebas ejecutadas. El estado global vive en [review](../review.md) y la readiness M01–M09 en [deep specs](../specs/index.md).

| Clase | Qué impide | Registros abiertos |
|---|---|---:|
| A — DESIGN FREEZE BLOCKER | Falta semántica de dueño, hecho, identidad, estado, reconocimiento, autorización, corrección, contrato público o frontera irreversible | **0** |
| B — IMPLEMENTATION VALIDATION GATE | Aceptar el mecanismo/alcance implementado sin el ensayo definido abajo | **16** |
| C — PRODUCTION / FEATURE ACTIVATION BLOCKER | Usar en datos reales la función/configuración afectada sin hechos, política o habilitación | **13** |
| D — DEFERRED / TRIGGERED | Iniciar una evolución opcional sin su trigger y nueva spec/WO | **6** |

Son 35 registros de trabajo agrupados, no un conteo de cada parámetro o pregunta profesional. La aceptación independiente del candidato es un requisito de gobernanza cuyo resultado se registra únicamente en [review](../review.md): no es una incógnita de diseño A ni evidencia de runtime B, y no cierra los gates B/C/D. Ni la tabla ni un ensayo B autorizan implementar.

A exige resolver antes de freeze: no se convierte en B una decisión semántica abierta. B congela hipótesis, evidencia y respuesta segura al fallo; no el mecanismo como ya probado. C admite preparar/implementar un contrato definido con fixtures y función desactivada; no inventa datos reales. Una respuesta real que exceda la superficie de política especificada abre amendment A antes de ampliar ese alcance.

## Cierres de diseño y contradicciones resueltas

| Antes | Cierre candidato y fuente |
|---|---|
| Devolución a proveedor todavía “por especificar” en invariantes | [INV06](../specs/milestones/inventory-deep.md) y [invariantes](../domain/invariants.md): promedio del pool y crédito comercial separados |
| Precio a6 decimales vs coste a12 parecían reglas incompatibles | [Data](../architecture/data.md): magnitudes/fronteras distintas, residuos exactos; capacidad numérica B04, parámetros reales C03 |
| Pool y replay parecían alternativas todavía sin elegir | [Inventory](../specs/milestones/inventory-deep.md): granularidad y secuencia definidas; cambiarlas exige amendment; prueba B05 |
| Balance G1 podía cuadrar sin demostrar origen | [G1](../specs/acceptance/reporting-goldens.md): hechos/componentes, posting, mayor y membresía/fórmulas; ejecución B07–B08 |
| DDR-09/11 y continuidad sensible incompletos | [UI](../architecture/ui.md), [Transactions](../architecture/transactions.md#preparar-y-ejecutar): causa/owner/resolución, preparación, incertidumbre y revocación; [12 DDR](../evidence/ux-reconciliation.md) cerrados en diseño |
| Aprobación de cifras, RUC, mutuo o prototipo bloqueaba toda arquitectura | Contrato tipado definido vs aplicabilidad/activación C; ningún valor real queda aprobado por este cambio |
| Catálogo PCGE confundido con política/marco | [M07](../specs/milestones/accounting-deep.md): representación B07; procedencia2026 C02; adopción/vigencia C01 |
| WOs anteriores tratadas como listas para ejecutar | [WOs](../history/work-orders-sp2.md): NEEDS REGENERATION AFTER FREEZE; no ejecución |

<a id="implementation-gates"></a>
## B — Ensayos futuros de implementación

Cada WO concreta el fixture/candidato/configuración y evidencia de los gates pertinentes. Una negativa de seguridad, integridad o cumplimiento falla el alcance aunque otras pruebas pasen; no se omite para obtener un PASS.

| ID / owner / momento | Hipótesis | Ensayo acotado | Criterio de pase | Respuesta al fallo |
|---|---|---|---|---|
| B01 Architecture/Operations — primer runtime | Versiones, driver, conexión/pool, agrupación Workspace/Corporate y dependencias soportan contratos | Instalación/upgrade reproducible, conexión real y carga mínima por paquete | Locks reproducibles, APIs soportadas, ownership sin ciclos, versiones identificadas | Ajustar mecanismo compatible; si cambia frontera, amendment; no negocio sensible sobre runtime fallido |
| B02 Access/Security — antes de aceptar cada entrada sensible | RLS, roles, contexto, capabilities, MFA/revocación y FK compuesta impiden acceso cruzado | PostgreSQL real: web/admin/worker/import/export/search, dos entidades, ausencia/mala configuración/contexto reutilizado, is_staff, revocación y referencias cruzadas | Cero acceso/efecto no autorizado; denegación segura; cobertura de cada nueva tabla/entrada | Bloquear alcance sensible; corregir sin bypass manager/superuser ni relajar RLS; revalidar entradas afectadas |
| B03 Dueños de comandos — integración crítica | CM0 extendido conserva dinero/stock/hecho/auditoría/intención bajo concurrencia | Intercalaciones cobro compartido, refund/despacho, creación de raíces, cierre, fallo audit, deadlock, misma clave distinto contenido | Un efecto por intención, rollback completo, sumas exactas, orden sin inversión y retry acotado | Corregir implementación/orden con análisis de todos los consumidores; no retries ciegos ni locks omitidos |
| B04 Data/Inventory — antes de aceptar tipos y cálculos | Rango y precisión elegidos representan operandos y residuos sin pérdida no autorizada | Documentar límites, extremos, acumulaciones, FX, parcialidades, último agotamiento y overflow contra cálculo independiente de mayor precisión | Error dentro de frontera de cuantización declarada, totales conservados, rechazo fuera de rango; cero truncamiento silencioso | Ampliar representación o rechazar rango explícito; cambio de significado abre A; no redondear para pasar |
| B05 Inventory/Accounting — valoración y backfill | Hechos/revisiones y cortes completos reproducen coste sin omisiones ni duplicación | UNKNOWN, late cost con Q0/retornos, conteo vs movimiento, backdating, commit tardío, backfill con manifiesto y nueva ejecución | Mismos miembros/deltas exactos; no MAX-ID como única completitud; cantidad/coste/historia coherentes; corte cerrado preservado | Detener valoración/paquete afectados, conservar hechos, corregir algoritmo/manifest; no fabricar coste0 |
| B06 Procurement/Treasury — match y banco | Asignaciones N:M, signos, anticipos y payability conservan remanentes | Fixtures PO10/recepción6/facturas4+4, servicios sin stock, supplier return45/crédito60, banco N:M, duplicados idénticos legítimos, parser sintético | Ninguna doble asignación ni caja por match; moneda/cuenta exactas, residuo explicado y error reproducible | Corregir parser/coordinación; mantener HOLD/propuesta; no tolerancia implícita ni ajuste para cuadrar |
| B07 Accounting — aceptar posting y catálogo | Interpretación tipada y versión de catálogo producen una contribución económica activa | G1 y casos A01–09: otra policy/misma fuente, reversión doble, cierre concurrente, apertura sin soporte, cuenta retirada/namespace interno; adapter2019/2026 | Cuenta/postabilidad autorizadas, cada hecho/componente una vez, auxiliares=GL, historia intacta; fixture no es regla oficial | Bloquear posting/regla afectados; corregir con linaje; no suspense automático ni homologación por código |
| B08 Accounting/Documents — aceptar informes | Cuatro EEFF+notas derivan del mayor/cortes con linaje real | G1 completo y G2–G7, omitir/duplicar fuente manteniendo balance, fórmula circular, cambio de mapping/paquete, render tardío | Importes/membresías exactos, reconciliación de cada estado, EFE bruto, notas sustentadas, HTML/PDF mismo snapshot; sin plugs | Bloquear paquete final, corregir fuente/mapping, preservar versiones; no editar total/PDF para cuadrar |
| B09 UX/Quality — primera tarea y cada componente crítico | Estructura permite completar tareas con teclado/lector/zoom/temas | Venta, P2P, conciliación, cierre, EEFF y error/timeout/revocación; 320px, zoom, foco modal/swap, LIGHT/DARK/SYSTEM, usuario representativo | Tarea completa sin ratón cuando procede; sin foco perdido/oculto, significado solo por color ni acción económica accidental; criterios WCAG2.2AA aplicables satisfechos | Corregir interacción/tokens/paneles; suspender aceptación de UI afectada; no declarar conformidad por screenshot |
| B10 Security/UI/Documents — superficies de entrada | CSP/CSRF, no history sensible, upload privado y preview/import/export resisten entradas hostiles | HTMX/full request, contenido/archivo malicioso, cuarentena, URL/caché revocadas, fórmulas CSV, cambio de maestro tras preview | Sin ejecución/fuga ni aprobación por archivo; permisos actuales; preview obsoleto rechaza y conserva evidencia | Bloquear superficie; corregir parser/render/cache; no externalizar documento privado ni relajar CSP |
| B11 Integrations/Inventory — canal y publicación positiva | Inbox íntegro/revisiones protegen lectura; publicación positiva puede satisfacer su protocolo de carrera | HMAC/conexión, duplicado/desorden/ABA, paginación, aceptación seguida de revisión externa; sandbox checkout concurrente/CAS/fencing reales | Inbound no cambia hechos internos; generaciones correctas. Publicación positiva solo pasa con evidencia del protocolo frente a carrera, ACK no basta | Corregir inbound si falla. Si solo falla publicación positiva, desactivarla; mapping/propuesta/aceptación local continúan con sus gates |
| B12 Integrations/Documents — efectos/recovery | Intención durable/epoch y callbacks tardíos evitan nueva ejecución ciega | Caída antes/después commit/envío, timeout, ventana del proveedor vencida, restore, callback tras corrección | Hecho original preservado; resultado incierto consulta/conciliación; callback no reactiva revisión sustituida; no duplicación por retry | Detener efecto afectado, HOLD y conciliación manual; no promesa exactly-once externa |
| B13 Operations/Security — restore | Manifiesto DB+objetos+roles+secretos permite recuperación segura | Restaurar en destino aislado, objetos/clave faltante, efectos externos desactivados y reconciliación antes de reactivar | Cobertura íntegra o faltantes explícitos, acceso negativo correcto; duración/pérdida medidas frente a C10 | No autorizar producción/restore incompleto; corregir copias/plan, nunca activar efectos para “probar” |
| B14 Quality — reutilizar evidencia | Selección parcial detecta cambios relevantes sin acreditar otro candidato | Manifiesto transitivo y mutaciones de spec/permisos/fixtures/parser/runner; comparar selección con evidencia completa pertinente | Invalidación de cada afirmación afectada; reproducción y trazabilidad; ningún PASS heredado sin equivalencia | Ampliar selección/repetir solo alcance invalidado; no falsificar equivalencia ni presupuestos |
| B15 Architecture/Operations — consumidor de carga real | Paginación/snapshot/trabajo durable y límites sostienen carga sin cambiar autoridad | Dataset sintético representativo, consulta por entidad, workers concurrentes, recuperación y carga app/DB | Sin consultas sin alcance, pérdida de trabajo ni snapshot mezclado; baseline medido, presupuesto de WO justificado | Ajustar índices/límites/backend dentro del contrato; no microservicio o caché autoritativa por defecto |
| B16 AI/Security — solo piloto activado por D01 | Asistencia mejora una tarea sin acceso/escritura indebidos | Corpus sintético, inyección en documentos, comparación manual, calidad/coste/latencia y procedencia | Cero escritura/confirmación autónoma/fuga; umbral de utilidad definido antes del piloto y cumplido | Desactivar piloto y conservar flujo manual; no agente con nuevas facultades |

<a id="activation-gates"></a>
## C — Activación real, por función

| ID / owner | Falta verificar/aprobar | Qué puede construirse con fixtures | Qué permanece desactivado / momento |
|---|---|---|---|
| C01 Accounting + contador / DH1 | Elegibilidad/marco/edición por período, ESFA y comparativos, elecciones NP-01–18/estimaciones/RER en EEFF, plan2019 vs adopción2026/fecha | Libro, reglas tipadas, auxiliares, transición, ledger, reportes y adapter versionado | Libro/política/paquete oficial sin expediente real aprobado; antes de apertura/primer reconocimiento dependiente/cierre |
| C02 Accounting + mantenedor dataset / DH1 | Procedencia binaria/editorial PCGE2026 y tratamiento trazado del 70992 duplicado | Adapter que representa ambas versiones y pruebas con identidad declarada | Dataset2026 en libro real hasta reconciliación; hash distinto no invalida semánticamente todo el catálogo |
| C03 Inventory + owner/contador / DH1–DH3 | Costes admisibles/repartos, unidades/rangos reales y cuantización comercial/contable/fiscal por magnitud | Promedio/pool/replay definidos, UNKNOWN y parámetros candidatos con B04 | Operación valorada/política cuantizada afectada antes de uso; cambiar pool/método exige amendment, no simple parámetro |
| C04 Procurement/Access + propietario / DH3 | Evidencia de compra directa/conformidad, aprobadores, tolerancias justificadas y autoaprobación explícita | PO/recepción/conformidad/match/HOLD/payability y permisos | Liberación/anticipo/pago real sin política y responsable; ausencia de evidencia no se convierte en diferencia tolerada |
| C05 Treasury + propietario / DH3 | Cuentas/monedas, evidencia mínima de dinero y muestra BBVA autorizada/formato/locale/campos reales | Núcleo bancario neutral, importador sintético, conciliación N:M y manual | Parser bancario/cuenta/cobro real dependientes hasta muestra y conciliación aprobadas; no API bancaria ficticia |
| C06 Corporate + legal/tax/contador / DH2 | Facultades, sujetos/vínculo/residencia, contrato, moneda/plazo/interés, comparabilidad y consecuencias de mutuo | Estados, evidencia, instrumentos, registro de fondos ocurridos pendientes y prohibición de autoingreso/capital | Nuevo contrato/desembolso/capitalización afectado antes de financiar; no bloquea M01–M05 sin financiación |
| C07 Sales/Procurement/Tax + profesional / DH4 | RUC/SEE/certificados/artefactos/canales válidos y oportunidad CPE por operación | Expedientes múltiples, anticipos, validación/vínculos/correcciones y entrega preparada | Emisión/adquisición/entrega fiscal real dependientes; CPE puede preceder despacho, operación real no espera UI M09 |
| C08 Tax + contador / DH4 | RER/IGV/SIRE/RVIE/RCE/SPOT/retenciones/percepciones/no domiciliados, cohortes/cronograma/valores reales | Perfiles/reglas con vigencia, determinación y registros, puente libro→fiscal→declarado→pagado | Determinar/aprobar/presentar/pagar obligación real sin perfil/fuente/hechos; ND se resuelve antes de contratar/pagar servicio |
| C09 Corporate/Tax + profesional / DH4 | Cohorte/obligación beneficiario final y personas/control efectivos con evidencia | Expediente, relaciones y captura de constancia | Declaración/calendario real antes de su vencimiento; no inferir por ser SAC |
| C10 Operations/Documents + propietario/profesional / DH5 | RPO/RTO, retención por clase, legal hold, presupuesto/plan/región y custodia de claves/copia de objetos | Backup/restore/purga restringida con fixtures y B13 | Primer despliegue, destrucción empresarial o compromiso de recuperación hasta targets/política y ensayo; ningún plazo legal inventado |
| C11 Integrations + propietario | Cuentas/credenciales/destinatarios, entornos, protocolo de stock y aprobación de efectos externos | Puertos/transportes controlados, inbound/mapping/propuestas y modo manual | Cada integración/efecto real por separado; stock positivo exige B11, email B12; activar inbound no autoriza outbound |
| C12 UX/Operations + operador / DH5 | Dispositivos/navegadores/tecnología asistiva y tareas reales soportadas | UI accesible con matriz candidata y B09 | Uso operativo soportado hasta prueba pertinente; no bloquea especificar ni construir shell |
| C13 Access/Masters + propietario / DH3 | Entidades, identidad/capacidades/aprobadores iniciales, fuentes/unidades y datos de maestros/apertura reales | Bootstrap, altas/versiones/importación y aislamiento sintéticos | Habilitar cuentas/maestros/apertura real hasta autorización y revisión de datos; sin datos privados en Git |

<a id="deferred"></a>
## D — Pendientes con trigger explícito

| ID / owner | Pendiente | Trigger y siguiente decisión |
|---|---|---|
| D01 AI/Architecture | Proveedor, recursos VPS/LLM y piloto opcional | Tarea repetitiva con beneficio esperado y autorización; fijar corpus/umbral B16/coste. Flujo manual completo permanece válido |
| D02 Accounting/Tax | Aplicación de otros marcos/ediciones, lectura íntegra por trigger de matriz62, NIIF18/19/20 y revisiones futuras | Cambio acreditado de marco/elegibilidad, fecha de vigencia o transacción; revisar texto oficial y caso antes de activar. Un hecho aplicable al primer libro pasa a C01/C08 ahora, no se oculta en M10 |
| D03 Product/Architecture | Nuevos canales/entidades/capabilities M10, escalado y distribución; WhatsApp Business, crédito B2B/contraentrega y compromiso sin reserva | Caso/necesidad y autorización concretos; research actualizado por canal/efecto; crédito/COD tienen diseño profesional propuesto ahora, pendiente de aceptación y política comercial real versionada, activación expresa y WO autorizada. Compromiso sin reserva y demás canales conservan necesidad de spec/amendment antes de ampliarlos. Sin trigger no activar WhatsApp ni despacho sin cobertura íntegra. B2B prepago está aceptado como incremento explícito posterior M04, no se mantiene diferido genéricamente |
| D04 UX/Architecture | Grid avanzada/isla de otro framework, branding y visuales opcionales | Tarea demuestra insuficiencia del patrón inicial; comparar CSP/licencia/a11y/beneficio; no cambiar dominio. Valores de componentes iniciales se validan en B09 |
| D05 Sales/Inventory/Accounting | Analítica adicional de rentabilidad, costes indirectos o nuevos KPIs | Encargo explícito y definición de bases/repartos/linaje antes de ampliarla; no difiere margen básico SP2 ni G1 ya especificados |
| D06 Product/dueño de caso | Automatización de SLA/escalamiento o workflow genérico de Inbox | Necesidad operativa repetida y política aprobada; nueva spec. Inbox inicial solo proyecta dueño/causa/acción y seguimiento |

## Impacto del amendment B2B/financiación — aceptado

No nuevos IDs ni cierres: **A0 / B16 / C13 / D6** se conservan. La ampliación semántica fue aceptada por revisión independiente según [review](../review.md); conservar conteos no cierra gates. [Matriz/casos](../evidence/b2b-financing-amendment.md) y contratos de [B2B](../specs/flows/b2b-commercial-dossier.md), [financiación](../specs/flows/financing-events-statements.md) y [C40](../specs/flows/cpe-document-delivery.md#c40) son el delta de alcance de los gates siguientes.

| Gates existentes | Extensión de hipótesis / efecto bloqueado y trigger |
|---|---|
| B02–04/B10 | Nueva entrada OC/cotización, referencias/archivos privados, revisiones y asignaciones concurrentes; antes de aceptar esa implementación |
| B06 | Pago por tercero consume una vez obligación/fuente; reembolso/amortización y estado mensual reproducible; probar doble asignación, reversión tras reembolso y omisión que conserva saldo; antes de aceptar financiación/liquidación |
| B07/B08 | Correlación evita duplicar pasivo/gasto/caja y estado mensual no repostea; pago personal fuera de EFE propio; antes de consumir/publicar esos componentes |
| B09 | Navegación B2B/financiación, naturaleza/pendientes y aprobación accesibles; antes de aceptar UI afectada |
| B12 | C40 compite con envío, no inventa callback ni permite original duplicado; cambio proveedor no reinicia historial; antes de aceptar transporte/recuperación |
| C04/C05/C06/C08 | Para pago por cuenta/reembolso: obligación/evidencia/acuerdo/facultades, naturaleza y sustento fiscal; C06 valida también alcance probatorio/firma del estado y tratamiento de pagos directos. Antes del efecto real pertinente, no del registro de hechos ocurridos como pendientes |
| C07/C08/C10/C11/C13 | CPE/traslado/impuestos, conservación, transporte real y actores/maestros; B2B comercial puro no adquiere un gate profesional universal |
| D03 | WhatsApp futuro: necesidad y research de capacidades/políticas vigente al activar. Crédito/contraentrega: demanda real y política/spec aprobadas; sin resolver bloquea esa modalidad, no B2B prepago |

Todo efecto de implementación sigue además fase habilitada y WO autorizada. Esta modificación no aprueba valores, contratos, cuentas, destinatarios ni reglas fiscales reales.

## Máximo cinco grupos humanos y profesionales

DH1–DH5 son agrupaciones de preguntas de activación, no aprobación solicitada ahora ni sustitución de HP1–HP5. Referencias históricas H1–H5 en [review histórico](../history/reviews.md) no son IDs actuales. No se pide al propietario decidir locks, tablas, librerías ni cómo probar RLS.

<a id="dh1"></a>
### DH1 — Contabilidad, apertura y valoración

| Hechos necesarios / pregunta concreta | Opciones permitidas / fuente | Qué cambia / clase / cuándo |
|---|---|---|
| Ingresos/UIT/ejercicios, supervisor, marco anterior y comienzo real: ¿es elegible NPIF, qué edición/remisión y fecha ESFA/comparativo corresponden? | Marco acreditado con [N001–N004](../research/normative/normative-register.md); NPIF si procede, otro marco mediante su contrato/trigger; no RER=SAC=NPIF | Perfil/apertura/paquete; C01, antes de activar libro y presentar primer período |
| Activos/vidas/residuales, obligaciones/estimaciones, contratos/divisas y política de error: ¿qué inputs y tratamiento aplican a cada NP-01–18, incluida clasificación RER y supletoriedad? | [Catálogo NPIF](../accounting/npif-policy-catalog.md) y M07: elección sustentada dentro de superficie tipada; fuera de ella amendment | Regla/estimación/mapeo y notas reales; C01/C03, antes del reconocimiento dependiente. No bloquea mecanismo contable |
| ¿Qué plan y fecha adopta TILMUX y qué evidencia editorial resuelve2026/70992? | 2019 vigente o adopción anticipada2026 permitida; [auditoría PCGE](../evidence/pcge-code-audit.md) y N011. Representar ambos no elige uno | Plan aplicado C01; dataset2026 C02 antes de uso. No inventar70902 ni concluir corrupción por hash |
| Facturas/fletes/descuentos/unidades y rangos: ¿qué costes y cuantizaciones reales se aprueban? | Promedio operativo/pool ya especificados, fronteras [Data](../architecture/data.md); política fiscal independiente | Valores/políticas reales C03; antes de operación dependiente. Ingeniería prueba suficiencia B04; profesional no diseña tipos DB |

<a id="dh2"></a>
### DH2 — Financiación antes de contrato o dinero

Hechos: prestamista/prestatario, vinculación, residencia, poderes, origen/destino, moneda, línea/plazo, interés/gratuidad, devoluciones y garantías. Pregunta a legal/tax/contador: ¿es jurídicamente válida la modalidad, quién firma, qué reconocimiento, valor de mercado/comparabilidad, efectos por ambos sujetos y evidencia periódica exige? Opciones: modalidad documentada aprobada, términos corregidos o no financiar; “gratuito” no significa neutral. Fuente: [memorando y límites RTF](../research/normative/mutuo-tax-corporate.md), N017–N019 y hechos nuevos. Cambia contrato/policy/expendiente, **C06 antes de primer contrato/desembolso**; no bloqueo general M01–M05. Fondos ya ocurridos se preservan como pendientes; no se borran por incumplir aprobación.

<a id="dh3"></a>
### DH3 — Operación, responsables y evidencia bancaria

| Hechos / pregunta | Opciones / fuente | Cambio / clase / cuándo |
|---|---|---|
| Roles/personas, compras y conformidades: ¿quién autoriza cada efecto, qué evidencia basta y qué diferencias se aceptan con motivo? | [P2P](../specs/milestones/procurement-deep.md): match exacto, excepción autorizada o HOLD; compra directa justificada. Autoaprobación identificada o doble aprobación real, sin inventar segunda persona | C04/C13; antes de habilitar usuarios/liberar/anticipar/pagar reales; no redefine N:M ni dueño |
| Cuenta/moneda, comprobantes y muestra privada BBVA: ¿qué confirma dinero y cómo se interpreta cada fecha/signo/referencia? | [Treasury](../specs/milestones/treasury-corporate-deep.md): confirmación por evidencia aprobada, importación validada o vía manual; estado canal no prueba cobro | C05, antes de parser/cuenta/cobro real; B06 prueba parser con fixture autorizado, no pedir columnas ficticias |
| Entidades/unidades/identidades/stock inicial reales: ¿qué fuente y responsable los aprueban? | [Maestros](../specs/milestones/runtime-masters.md), [Inventory](../specs/milestones/inventory-deep.md): preview y revisión o rechazo | C03/C13, antes de importar/abrir realmente; conserva UNKNOWN donde permitido |

<a id="dh4"></a>
### DH4 — Cumplimiento según operaciones reales

| Hechos / pregunta al profesional | Opciones / fuente | Cambio / clase / cuándo |
|---|---|---|
| RUC/SEE, venta/anticipo/entrega/corrección y documentos disponibles: ¿qué artefacto/momento y canal son válidos? | [CPE](../specs/flows/cpe-document-delivery.md), N009 y [Tax](../specs/milestones/tax-deep.md); política por hecho o no activar operación sin cumplimiento | C07; antes de la primera operación afectada, no después de construir M09 |
| Régimen/ingresos/actividad, RUC/cohorte, servicio/bien, proveedores/vínculo/residencia: ¿qué RER/IGV/SIRE/SPOT/ND y vencimientos aplican? | [Registro](../research/normative/normative-register.md), N021/N024–N028; aplicar/no aplicar con fundamento o pendiente que bloquea obligación | C08; antes de determinar/declarar/pagar; servicio ND antes de contratar/pagar cuando lo exija la regla |
| Cadena de propiedad/control, RUC/activación/ingresos: ¿qué cohorte, beneficiarios y fecha de declaración corresponden? | N029 y [Corporate](../corporate/architecture.md); declaración requerida o no aplicable sustentada | C09; antes de vencimiento real, con expediente privado fuera de Git |

<a id="dh5"></a>
### DH5 — Continuidad y operación soportada

Hechos: criticidad/pérdida tolerable, costo del paro, clases documentales y obligaciones de conservación, presupuesto/región/custodios, dispositivos y tareas del operador. Preguntas: ¿qué RPO/RTO y retención/legal hold se comprometen, y en qué entornos se usará CasPro? Opciones: targets medibles con plan/copia/restore que los cumpla o despliegue pendiente; matriz soportada demostrada o adaptación antes de uso. Fuentes: [Delivery](../operations/delivery.md), [Data](../architecture/data.md), [UI](../architecture/ui.md); asesor valida plazos legales reales, ingeniería mide B09/B13/B15. Cambia configuración/soporte operativo, **C10/C12 antes del primer despliegue/uso**, no todo código.

## Cobertura de pendientes dispersos

Las menciones PROVISIONAL/PENDING/REQUIRES LATER VALIDATION en fuentes locales conservan su límite de aceptación. Su clase se resuelve aquí, no por la palabra aislada:

| Fuente / conjunto | Registros que absorben sus pendientes materiales |
|---|---|
| ADR002/003/005/006/007/008/009/010/011, Architecture, Security, Operations | B01–B04, B10–B16; C10–C13; D01/D03/D04 |
| M01/M02: runtime/acceso/audit/documentos/maestros/importación | B01–B04/B10/B13–B15; C10/C12/C13 |
| SP2/CM0, Inventory, P2P, Treasury, hechos/backfill | B03–B06/B09–B12/B15; C03–C07/C11/C13; D05 |
| Accounting/NP-01–18/G1–G7/PCGE | B04/B05/B07/B08; C01–C03; D02 |
| Tax/CPE/Corporate y registro N001–N029 | B06–B08/B10/B12; C01/C06–C09; D02 cuando no aplicable aún |
| Matriz62/delta NIIF y textos no leídos íntegros | D02 por norma/trigger; si hechos iniciales la activan, C01/C08 exige resolución antes de uso |
| Blueprint/DDR y UI | DDR cerrados en [memo](../evidence/ux-reconciliation.md); B09/B10, C12, D04/D06 |
| Audit/review/programa/WOs/skills | Clasificación anterior sustituida por este registro; resultado de aceptación independiente en review; WOs a regenerar; skills posteriores, sin ejecución ahora |

Una omisión o contradicción semántica descubierta por reviewer se registra como A con contraejemplo, dueño y contrato afectado. Cero A es conclusión de este cierre documental, no garantía de ausencia de errores ni aceptación independiente.

## Impacto profesional propuesto — validación y activación

Se conservan **A0 / B16 / C13 / D6**, sin cerrar ni añadir IDs. Elección de fórmula A resuelta por delegación del propietario, no bloqueador A pendiente. La propuesta del autor está pendiente de revisión independiente; cualquier contraejemplo semántico real abre A, no se oculta como parámetro C.

| Gates | Hipótesis/activación extendida y respuesta al incumplimiento |
|---|---|
| B02/B03/B04/B05 | Nuevas entradas por entidad, H27/exposición, transferencias/kit/corte, oferta/award y costo tardío, precisión/FX. Sin conservación/aislamiento bloquear alcance y corregir, sin tolerancia implícita |
| B06/B07/B08 | Proveedor-banco revisado, cuota/card/caja/renta, mapping efectivo, auxiliares/GL, formatos/cortes/libros y presentación externa. Sin linaje/estructura válida no aceptar salida final |
| B09/B10/B12/B13/B15 | Flujos/compare/drilldown, PDF/upload/firma/custodia, límites/cuotas/restore DB+objetos, callbacks/readiness caducada y export sensible. Fallo mantiene HOLD/quarantine o integración desactivada |
| C01/C03 | Fórmula promedio NPIF uniforme, método fiscal previo, costos importación/ajustes, unidades, reconocimiento entrega+instalación y alquiler/préstamo según marco. Antes de apertura/operación dependiente |
| C04/C05/C13 | Aprobadores/descuentos/directa/award, cuenta proveedor/mapping, instrumento/límites/caja/custodios, catálogo/perfiles/sedes reales. Antes de alta/aprobación/pago operativo afectado |
| C06 | Poderes/contratos/firma suficiente, tenencia/licencias aplicables, requisitos laborales/HSE por actividad y plazos/canal de reclamos. Antes del acto real correspondiente; no pide dictamen por toda cotización ordinaria |
| C07/C08 | SKU/origen/restricción/DAM/levante, CPE/oportunidad, marco/régimen/libro/layout/SIRE/FX/ND/CDI/CRF/MLI/beneficios y crédito. Fuentes contradictorias retienen efecto fiscal afectado hasta resolución; no falso dato ni tasa0 |
| C10/C11 | Original/derivados/firma/copia objetos/custodia/retención y puertos de firma/intake/FX; antes de datos o envío real, no provider elegido por herramienta |
| D03 | Crédito/COD diseñados, activación posterior por demanda/política/aceptación; compromiso sin reserva, WhatsApp, RMA/servicio independiente y consignación/producción nuevos siguen trigger. Imports/RFQ/multialmacén confirmados salen de incógnita funcional, sin nuevo gate |

La matriz no acredita políticas reales ni ensayos. Aceptación documental y autorización de ejecutar siguen review/WO; operación real exige además gates pertinentes.
