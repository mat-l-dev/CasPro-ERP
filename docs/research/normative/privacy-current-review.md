# Perú — revisión acotada de datos personales

Corte: 2026-09-12. Pregunta F02: mínimos operacionales de atención, incidentes y recuperación; no dictamen de TILMUX. Fuentes oficiales consultadas; inferencias de diseño separadas en [contrato](../../security/personal-data-lifecycle.md). No trasplante de RGPD.

## Fuentes y vigencia

| Fuente primaria | Fecha/alcance comprobado | Límite |
|---|---|---|
| [Ley 29733, Congreso](https://leyes.congreso.gob.pe/documentos/leyes/29733.pdf) | Publicada 2011-07-03; principios, datos sensibles, derechos arts.18–23, obligaciones art.28 y autoridad | Su aplicación exige finalidad, base y contexto reales; no permiso de procesar por existir ERP |
| [DS 016-2024-JUS, publicación oficial alojada por Congreso](https://www3.congreso.gob.pe/Docs/DGP/DIDP/files/ds_016-2024-jus.pdf) | Publicado 2024-11-30; vigencia general 120 días calendario siguientes: 2025-03-31; sustituye DS 003-2013-JUS | Art.37 y disposiciones finales contienen implantación gradual del Oficial; art.76 tiene plazo especial. Procedimientos iniciados antes siguen régimen transitorio |

La fecha de entrada general se corrobora con la [comunicación oficial MINJUSDH del2025-03-31](https://www.gob.pe/institucion/minjus/noticias/1137398-nuevo-reglamento-de-proteccion-de-datos-personales-refuerza-el-consentimiento-de-usuarios-para-recibir-llamadas-publicitarias), además de la fórmula del reglamento.

Cómputo ordinario de «días» del reglamento: hábiles (definición III.8), salvo calendario/horas expresos. No transformar 48 horas en dos días hábiles. Portabilidad art.76: vigencia seis meses después de entrada general, ya transcurrida al corte; comprobar supuesto y viabilidad antes de prometer formato/transferencia.

## Derechos, acceso y conservación

Arts.6 y 18–23 de ley/reglamento según materia: informar responsable, finalidades, destinatarios, conservación, derechos y fuente indirecta pertinente; consentimiento válido cuando se exija, no como fundamento universal. Datos sensibles requieren condición y protección específica. Bloqueo definido en III.2 impide tratamiento, incluida visualización, durante la atención y conservación por responsabilidades aplicables.

Arts.66–71: encargado remite al responsable; atención simple y gratuita en privados, acreditación proporcional, respuesta aun sin datos. Art.69: información 8 días, acceso 20, rectificación/cancelación/oposición 10, desde el día siguiente a presentación. Requerimiento de información adicional art.70 dentro de 7 días; titular dispone 10 y la suspensión se documenta conforme al supuesto. Art.71 permite una ampliación justificada por plazo igual y aviso previo al vencimiento, excepto información. No reloj discrecional de workflow.

Arts.76 y 78–84: portabilidad condicionada; acceso sin vulnerar terceros; rectificar/incluir/actualizar con evidencia; solicitud de supresión implica bloqueo durante evaluación; registrar cumplimiento y traslado a receptores pertinente. Art.84 admite conservación por fundamento legal/contractual u otros supuestos previstos: no derecho automático a borrar todo ni retención universal indefinida. Original legal puede conservarse restringido; identidad de maestro, atributos y copia de presentación no son el mismo objeto.

Arts.31–33: contrato e instrucciones del encargado/subencargado, devolución/supresión conforme relación y obligaciones. Límite de dos años tras último encargo del art.31.2 tiene supuestos/excepciones propios: no se usa como plazo general del ERP.

## Decisión sobre incidentes

| Supuesto y artículo | Obligación legal comprobada | Evidencia operacional |
|---|---|---|
| 34.1: grandes volúmenes por cantidad/tipo o número de personas; O sensibles; O perjuicio evidente a derechos/libertades | Responsable notifica ANPD dentro de 48 horas de conocimiento. Retraso exige razones. Resolución interna no exime | Momento inicial, hechos/categorías/volumen aproximados, umbral, motivos y constancia |
| 34.2 | Identificar naturaleza/tipo y número aproximado de personas, contacto, consecuencias y medidas | Versión conocida al enviar; incertidumbres explícitas |
| 34.3–34.4: otros derechos del titular afectados | Comunicar al afectado dentro de 48 horas, lenguaje sencillo y medidas; excepción solo si no concurre afectación descrita y se resolvió totalmente | Decisión separada de ANPD; no excepción global por cifrado ni por recuperación |
| 34.5: entorno digital | Notificar además CNSD conforme marco de confianza digital | Evaluar canal/obligación aplicables, no inventar plazo distinto |
| 35: todos los incidentes | Documentar hechos, efectos y medidas, incluso sin obligación de notificar | Caso completo y revisión al llegar información nueva |
| 36: encargado conoce incidente | Comunicar inmediatamente al responsable | Hora de conocimiento/aviso, evidencia del proveedor, actualizaciones; no esperar peritaje final |

## Seguridad, responsables y activación

Art.37 exige Oficial en los supuestos tipificados de entidad pública, tratamientos de grandes volúmenes por cantidad/tipo o afectación de gran número de personas conforme a ese artículo, o actividades principales con datos sensibles. No universalmente a cualquier microempresa. Implementación progresiva de los supuestos privados37.1.2–3 por ventas: más de2300UIT un año, más de1700 hasta2300 dos, más de150 hasta1700 tres, hasta150 cuatro desde publicación. Validar hecho/supuesto y plazo concreto, sin asumir tamaño por marco contable.

Arts.43–44: verificar registro de bancos y comunicación del flujo transfronterizo según corresponda. Arts.46–48: privilegios/autenticación, trazabilidad de interacciones al menos dos años y revisión semestral de privilegios; documento de seguridad vigente, inventario, medidas físicas y de custodia. Art.51: copia al menos semanal salvo ausencia de actualización, y comprobación de integridad/recuperación. Targets C10 no pueden bajar del mínimo aplicable.

Inferencia de diseño: restaurar una copia no revoca una decisión posterior de bloqueo/supresión; diario independiente del rollback y barrera de reapertura evitan reexposición. No se atribuye a la ley un diseño específico de epoch/DB. Conservación exacta por clase, banco, encargados, transferencias, Oficial, personas responsables y validación profesional permanecen C06/C10/C11/C13; demostrar mecanismo B02/B10/B13/B15. Ninguna política real queda aprobada por este memo.
