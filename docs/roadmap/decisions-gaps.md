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
| WO-SP2-01 “siguiente” automático | WOs SP2 siguen preparadas; programa completo decide secuencia y siguiente hito documental | Mandato Grand Master | review/work-orders/roadmap |

## Gap analysis

| Sev. | Gap y razón | Dominio / fuente actual | Decisión objetivo | Humano / research | Bloquea roadmap / implementación / operación |
|---|---|---|---|---|---|
| CRITICAL | Elegibilidad NPIF y RER son declaraciones no evidenciadas | Accounting/Tax | verificar documentos y aprobar perfiles por período | profesional + evidencia | no / Accounting+Tax / cierre y cumplimiento |
| CRITICAL | Políticas NPIF, apertura y RER especificadas como candidato, sin aprobación profesional de hechos | [M07](../specs/accounting-deep.md), [M08](../specs/reporting-goldens.md), catálogo NPIF | revisar elecciones, apertura y cifras esperadas; elegibilidad por período | contador | freeze global sí / M07 / EEFF |
| CRITICAL | Oportunidad CPE investigada, pero SEE/artefactos y perfil real no acreditados | [CPE](../specs/cpe-document-delivery.md), [Tax](../specs/tax-deep.md) | validar policy por operación y SEE; anticipos no esperan despacho | profesional+hechos | freeze global sí / M04 parcial / venta segura |
| CRITICAL | Mutuo rotativo gratuito investigado, sin hechos ni dictamen final | [memorando temprano](../research/mutuo-tax-corporate.md) | contrato, facultades y efectos por ambos sujetos; RTF no prueba neutralidad | legal+tax+accounting | freeze de modalidad sí / antes de autorizar financiación aunque UI sea M06 / desembolso |
| HIGH | Buffer/PUT Jumpseller y checkout race no demostrados | Inventory/Integration | gate de sandbox/CAS/reconciliación | técnica | no / publicación / sobreventa |
| HIGH | RLS sigue provisional | Access/DB | demostrar roles, policies y entry paths | ejecución | no / M01 / aislamiento |
| HIGH | Escalas, pool y revisión de costes tardíos propuestos, no aceptados/calibrados | [Inventory profundo](../specs/inventory-deep.md) | revisar replay por secuencia y puente a período cerrado; límites/volumen | técnica+contable | freeze de política sí / M03/M07 / márgenes/cierre |
| HIGH | Retención, RPO/RTO y restore DB+objects sin cifras | Operations/Documents | targets y prueba de restore | owner+ejecución | no / deploy / continuidad |
| HIGH | P2P candidato completo; tolerancia cero no explicada y excepciones requieren aceptación | [P2P profundo](../specs/procurement-deep.md) | aprobar tolerancias, compra directa y conformidad; SPOT por servicio | owner+professional | freeze de política sí / M05 / pagos seguros |
| HIGH | Conciliación especificada; formato BBVA y política de evidencia real no comprobados | [Treasury profundo](../specs/treasury-corporate-deep.md) | validar parser/import y duplicados reales; no inferir de CSV de otro banco | muestra sintética/real autorizada | no para contrato / adapter M06 / control diario |
| MEDIUM | Corporate placement físico no decidido | Architecture | elegir cuando primer consumidor exista | arquitecto | no / M06 / no |
| MEDIUM | IA/VPS/proveedor sin recursos ni evaluación | AI | piloto sintético y benchmark | owner+technical | no / M06 optional / no |
| MEDIUM | Dispositivo operativo/densidad y browser matrix | UX | prueba de tareas con operadores | owner/research | no / UI / productividad |
| HIGH | Cohorte de beneficiario final no determinada; calendario 2026 investigado | Corporate/Tax, N029 | verificar RUC/activación/ingresos y período/vencimiento real | business evidence | freeze de perfil sí / expediente / compliance |
| HIGH | Dataset PCGE2026 no tiene identidad binaria corroborada con PDF oficial descargado; 70992 duplicado editorialmente | [auditoría pcge-peru](../research/pcge-code-audit.md) | reconciliar origen/edición antes de adoptar 2026; no normalizar silenciosamente | técnica+contador | no para adapter neutral / catálogo2026 / contabilidad2026 |
| MEDIUM | Matriz62 tiene inventario completo; no lectura íntegra ni historia exhaustiva de cada texto | [matriz NIIF](../research/ifrs-applicability.md) | cotejar texto/fecha/elección cuando se active cada norma; no aplicarlas por estar listadas | research+profesional | no para NPIF si remisiones resueltas / marco futuro / cumplimiento futuro |
| HIGH | Falta revisión separada del candidato global | [gate profundo](../specs/deep-spec-index.md) | reviewer distinto sobre identidad exacta y cierre de contradicciones/políticas | revisión independiente | freeze global sí / todo código / no operación autorizada |

## Máximo cinco decisiones humanas agrupadas

1. Aprobar con contador el marco/elegibilidad inicial, apertura y políticas NPIF, presentación del RER, pool/precisión/costes tardíos y adopción PCGE 2019 vs anticipada 2026.
2. Aprobar con asesor legal/tributario/contable la estructura del mutuo antes de contrato o dinero.
3. Definir evidencia operativa mínima de cobro y formatos de extracto/cuentas reales para Treasury, tolerancias/compra directa/conformidad de Procurement y excepciones de autoaprobación, sin exponer datos privados en Git.
4. Fijar artefactos/momento CPE y obligaciones SIRE/IGV/SPOT/no domiciliados/beneficiario final con profesional según RUC/operaciones reales.
5. Fijar RPO/RTO/retención y dispositivos objetivo antes del primer despliegue.
