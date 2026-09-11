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
| CRITICAL | Políticas NPIF, apertura y tratamiento RER aún no especificados | Accounting | catálogo de políticas y casos contables | contador | no / M07 / EEFF |
| CRITICAL | Momento/artefactos CPE y obligaciones SUNAT exactas | Sales/Tax | policy CPE externa | regulatory research | no / M04 parcial / venta segura |
| CRITICAL | Mutuo rotativo gratuito no validado | Corporate/Treasury/Tax/Accounting | contrato y tratamientos por hechos | legal+tax+accounting | no / M06 mutuo / desembolso |
| HIGH | Buffer/PUT Jumpseller y checkout race no demostrados | Inventory/Integration | gate de sandbox/CAS/reconciliación | técnica | no / publicación / sobreventa |
| HIGH | RLS sigue provisional | Access/DB | demostrar roles, policies y entry paths | ejecución | no / M01 / aislamiento |
| HIGH | Precisión/escalas y backdating cost no calibrados | Data/Inventory | parámetros y escenarios reales | técnica+contable | no / M03/M07 / márgenes/cierre |
| HIGH | Retención, RPO/RTO y restore DB+objects sin cifras | Operations/Documents | targets y prueba de restore | owner+ejecución | no / deploy / continuidad |
| HIGH | P2P tolerancias/compra directa/servicio/detracción | Procurement/Tax | deep spec | owner+professional | no / M05 / pagos seguros |
| HIGH | Statement format y evidencia BBVA no comprobados | Treasury | import/reconciliation spec | muestra sintética/real autorizada | no / M06 / control diario |
| MEDIUM | Corporate placement físico no decidido | Architecture | elegir cuando primer consumidor exista | arquitecto | no / M06 / no |
| MEDIUM | IA/VPS/proveedor sin recursos ni evaluación | AI | piloto sintético y benchmark | owner+technical | no / M06 optional / no |
| MEDIUM | Dispositivo operativo/densidad y browser matrix | UX | prueba de tareas con operadores | owner/research | no / UI / productividad |
| MEDIUM | Beneficiario final probablemente próximo | Corporate/Tax | verificar fecha RUC/activación y vencimiento | business evidence | no / expediente / compliance |

## Máximo cinco decisiones humanas agrupadas

1. Aprobar con contador el marco/elegibilidad inicial, políticas NPIF, presentación del RER y adopción PCGE 2019 vs anticipada 2026.
2. Aprobar con asesor legal/tributario/contable la estructura del mutuo antes de contrato o dinero.
3. Definir evidencia operativa mínima de cobro y formatos de extracto/cuentas reales para Treasury, sin exponerlos en Git.
4. Fijar artefactos/momento CPE y obligaciones SIRE/IGV/SPOT con profesional según RUC/operaciones reales.
5. Fijar RPO/RTO/retención y dispositivos objetivo antes del primer despliegue.
