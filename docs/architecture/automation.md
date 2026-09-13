# Plantillas y automatización tipada

Contrato transversal de transporte/observabilidad; cada dueño conserva comando completo, hechos, aprobación y política. [Configuración](configuration-governance.md) posee revisión/ImpactManifest/activación; [transactions](transactions.md) posee atomicidad y jobs. [Accounting](../accounting/templates-automation-shadow.md) concreta el único nuevo consumidor económico de este delta. Investigación: [AF-S01–13](../research/automation-flow-ai-benchmark.md). Fase: [review](../review.md). No WorkflowEngine, Rule DSL, motor low-code, settings dump ni autorización runtime en esta misión.

## Familias de plantillas

Descriptor común: ID, familia/owner, entidad/alcance, revisión inmutable, vigencia, estado, aprobador, esquema de variables permitido, preview, referencias de política/evidencia, hash y usos. Payload validado por tipo/dueño; compartir descriptor no comparte autoridad ni tablas de negocio. Copiar plantilla produce DRAFT nuevo con procedencia; cambios no alteran documentos/asientos ya emitidos.

| Familia | Dueño / contenido permitido | Salida y frontera |
|---|---|---|
| AccountingJournalTemplateRevision | Accounting posee semántica, revisión y aplicación: roles/cuentas, líneas y variables tipadas | Borrador validable; Documents solo representa un artefacto si se solicita, nunca interpreta ni aplica la plantilla contable |
| DocumentTemplate | Documents con dueño de contenido; layout y placeholders conocidos | Derivado versionado; no original legal/CPE por sí mismo |
| CommercialTemplate | Sales; términos/estructura de cotización/contrato dentro de política | Borrador comercial, aprobación propia |
| EmailTemplate | Dominio del acto aprueba contenido/audiencia; Documents posee representación, versión y render del mensaje | Mensaje preparado; envío requiere intención/autorización específica, no permiso por editar plantilla |
| ImportMappingTemplate | Dueño del import; columnas, tipos y mapeos explícitos | Preview/import por comandos autorizados; nunca escritura SQL libre |
| SiteFormTemplate | Sales posee requisito de sitio y aplicabilidad; Documents posee TemplateRevision/render; flujo de visita/instalación captura valores autorizados | Formulario no decide obligación legal/cliente ni autoriza trabajo; cambio conserva paquetes y originales anteriores |
| ReportTemplate | Dominio del informe posee definición, fórmulas, filtros/columnas y aprobación; Documents posee representación/render del artefacto | Lectura/export autorizado; plantilla visual no redefine mayor, impuesto ni EEFF |
| AIRequestTemplate | Accounting para AI-TPL-ACCOUNTING-CLASSIFY; schema/políticas/minimización | Solicitud/sugerencia o interpretación shadow, nunca mandato oficial |

Variables monetarias Decimal/moneda, fechas con semántica, referencias de origen y cuentas aplicadas; sin JavaScript, Python, SQL, fórmulas abiertas ni texto IA interpretado como código. Campos desconocidos rechazan. Herencia dinámica de plantillas y edición de lógica desde UI no se incorporan.

Separación F03: contenido y aplicabilidad permanecen en el dominio; Documents conserva mecánica de plantilla documental, versión y render; la superficie consumidora captura/usa valores y la entrega conserva su intención independiente. DocumentTemplate exige el dueño del acto para texto y uso, además de Documents para representación. «Communications», «Reporting» y «Operations» en superficies no crean módulos ni propietarios empresariales. AccountingJournalTemplateRevision es una regla/plantilla contable de Accounting, no una plantilla documental trasladada a Documents. Un dominio puede solicitar otro render, nunca mutar la historia inmutable del anterior.

## Modos y riesgo

Amendment [Marketing Content](../specs/flows/marketing-content-media-library.md): BrandKit/copy/versiones pertenecen al pequeño dueño Marketing; Documents conserva representaciones binarias y render. Templates/backgrounds son activos revisados, sin motor gráfico ni scripts. Su calendario inicial solo planifica y registra hechos MANUAL_EXTERNAL; no ejecución automática por llamarlo calendario. Funciona con ZERO AI; sugerencias futuras D01/B16 nunca aprueban ni publican, adaptadores de publicación D03/B12/C11 requieren otro contrato/mandato. Los modos Accounting de esta fuente no se heredan por Marketing.

El modo se resuelve y muestra **antes** de llamar a IA. Regla determinística conocida gana sobre consulta ambigua; fuente faltante no se inventa para satisfacer una plantilla.

| Modo | Resultado / autoridad |
|---|---|
| MANUAL | Humano prepara y confirma comandos ordinarios |
| TEMPLATE_DRAFT | Uso explícito de revisión de plantilla genera borrador |
| RULE_AUTO_DRAFT | Regla tipada aprobada reconoce hecho y prepara borrador |
| SCHEDULED_DRAFT | Ocurrencia respaldada por fuente real prepara borrador |
| EVENT_AUTO_DRAFT | Evento durable conocido prepara borrador, deduplicado |
| RULE_AUTO_EXECUTE | Solo comando determinístico expresamente aprobado y mandato vigente; OFF inicial |
| AI_SUGGEST | Respuesta candidata; aceptación humana a DRAFT |
| SHADOW_AI_EXECUTE | Interpretación/post/reversa solo dentro del ledger experimental aislado |

Riesgo LOW: proyección/recordatorio sin efecto económico; MEDIUM: borrador; HIGH: propuesta económica con materialidad/revisión; CRITICAL: publicación oficial o efecto externo. Clasificación no concede permisos. RULE_AUTO_EXECUTE no se activa por número de aceptaciones ni al aprobar plantilla: requiere regla finita registrada, validación profesional, política/mandato separado por entidad/alcance/importe/frecuencia/vigencia y evidencia B03/B07, C01/C13 y gates del efecto. Posting oficial siempre ejecuta A03 completo con identidad de servicio autorizada; nunca cuenta/provider/AI/shadow con permiso de post. Sugerencia IA aceptada por humano puede seguir luego el posting humano normal, sin heredar una ruta automática. Pagos, CPE, firma, banco y envíos conservan sus propios mandatos; Centro no autoriza todo por un toggle.

## Recurrencia, concurrencia y cambios

Recurrencia describe fuente económica real (contrato/renta, activo/depreciación, cobertura de prepago, devengo de interés), calendario, timezone IANA, inicio/fin, fecha de reconocimiento, condiciones y revisión. El reloj no crea un gasto ni repite cobro ya satisfecho. OccurrenceKey estable `(entity, source obligation, coverage period, component)` **sin revisión de regla** evita volver a consumir el mismo hecho al editar calendario/plantilla. Intentos y versiones de interpretación son distintos de ocurrencia económica. Repetición sin fuente suficiente queda HOLD.

Guardar hora local + zona + instante UTC resuelto. Hora ambigua DST: primera ocurrencia cronológica, registrar offset; hora inexistente: siguiente instante válido con aviso y evidencia de ajuste. Esto resuelve ejecución técnica, no cambia fecha económica del dueño. No usar zona del navegador. Catch-up después de pausa o atraso requiere preview de pendientes y confirmación bajo mandato; no descarga masiva silenciosa de asientos. Período cerrado retiene propuesta; no mover a hoy ni reabrir automáticamente. Expiración de mandato/política y scheduler atrasado aplican POLICY_ACTIVATION_PENDING/STALE antes del efecto según configuración.

AutomationRun conserva regla/plantilla/política/revisiones, fuente/corte, modo, occurrenceKey, intentId, actor original y ejecutor, mandato/alcance, estado, intento, tiempos, resultado, efectos/refusals y razón. Lease durable con timeout y deduplicación del comando final, no confiar en que un cron se ejecute una sola vez. Antes de efecto: reautorizar Access, verificar epochs/vigencia/ImpactManifest y revisión esperada bajo el orden de locks de CM0; no sostener locks durante HTTP/IA. Cambio de regla tras draft lo marca para revisión/diff; no edita silenciosamente lo que el humano modificó. Retry técnico acotado candidato3, backoff/circuit breaker; un resultado externo incierto se reconcilia antes de reintentar, nunca asumir que timeout es no ejecución.

## Centro, observabilidad y simulación

Automation Center reúne descriptores registrados por dueño: nombre/propósito, familia, entidad/scope, modo/riesgo, responsable, revisión efectiva/propuesta, último/próximo run, por qué aplicó/no aplicó, fuente/corte, mandato/expiración, resultado/efectos, duración, retry, evidencia y enlace a editar/aprobar en el dueño. Listar no concede ejecución. Vistas «requiere atención», «pausadas», «próximas», «fallos» y «coste» explican causas; sin constructor visual de procesos. Scheduler/control técnico no posee configuración contable.

Métricas por entidad/familia: lag de fuente/cola, pending/failed/abstained, duplicados evitados, intentos inciertos, mandatos expirados, cambios de política, overrides y coste. Run verde no acredita efecto correcto; enlaces al resultado y al historial del dueño. Logs no guardan prompts privados ni credenciales; redacción y retención POL26/POL21. Prueba/evaluación vincula revisión y dataset, cobertura y limitaciones; historial no desaparece al desactivar regla.

Dry-run usa manifiesto congelado histórico autorizado o sintético, reloj/política/revisión explícitos y destino de evaluación aislado. Puertos/credenciales de escritura canónica y egress de efectos deshabilitados; producir propuestas/diffs, no mutar hechos, períodos, Documents originales ni intenciones de envío. Simulación no llama el mismo commit real con bandera confiada al UI. Activar exige volver a evaluar datos actuales, no reutilizar autorización vieja del replay. Casos desconocidos, contradicciones y contrajemplos son resultados, no errores que IA rellene.

Coste IA se gobierna en [Accounting](../accounting/templates-automation-shadow.md#proveedores-coste-y-datos): presupuesto por entidad/propósito, reservas concurrentes, límites diarios/mensuales/tokens, timeout y fallback manual. Sin proveedor, continúan plantillas/reglas determinísticas autorizadas. M01 implementaría solo primitives de jobs/audit/Access cuando se autorice; familias aparecen con sus dominios, M07 plantillas/rules/IA/shadow y M08 comparación. Ninguna WO se genera aquí.
