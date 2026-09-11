# Extracción de Wbpro hacia CasPro

Wbpro-ERP permanece READ-ONLY REFERENCE. No es dependencia de ejecución ni carpeta de trabajo. No se ha copiado código en esta fundación. Legacy queda fuera de lectura y modificación.

## Familias de reutilización

| Familia V1 | Clasificación | Criterio / destino |
|---|---|---|
| Separación de entidad y conceptos de dinero/stock | REUSE CONCEPT | Pasar a especificaciones propias, contrastando supuesto vs hecho |
| Invariantes sobre parciales, coste original, idempotencia y procedencia serial | REUSE CONCEPT | Conservar propiedad y contraejemplo; rediseñar mecanismo |
| Modelos ORM | PENDING REVIEW | Evaluar frente al modelo conceptual; no renombrarlos y asumir que encajan |
| Migraciones | DO NOT PORT | No hay datos CasPro que obliguen a reproducir historial de schema V1 |
| Services monolíticos y resolutores mutables | REIMPLEMENT FROM SPEC | Casos de uso/coordination explícitos; extraer solo reglas verificadas |
| Cálculos puros útiles | PORT WITH CHANGES | Solo tras comprobar dominio, precisión, licencia/procedencia, firma y ausencia de dependencias ocultas |
| UI | REUSE CONCEPT | Recuperar tareas y estados útiles; nuevo contrato visual/accesible, sin copiar bundles |
| Tests de reglas y regresión | REUSE CONCEPT | El escenario puede ser evidencia; comprobar que no afirma el defecto histórico |
| Test puro aislado | PORT WITH CHANGES | Solo si prueba contrato CasPro y no copia su implementación |
| Mega-fixtures y organización por cortes históricos | DO NOT PORT | Builders locales y categorías por propiedad |
| Clientes de integración | PENDING REVIEW | Revalidar contrato/versiones/autenticación; adaptador separado |
| Documentación actual | REUSE CONCEPT | Extraer decisión/fuente concreta; no importar aprobaciones ni duplicados |
| AGENTS/skills/commands | DO NOT PORT | Nuevo router, protocolo único y modelos configurables |
| Scripts/quality.py/perfiles repetidos | DO NOT PORT | Recuperar verificaciones puntuales útiles, no el pipeline redundante |

## Admisión de una pieza

Documentar: propiedad empresarial correcta; encaje en fronteras; deuda accidental; evidencia y limitaciones; coste estimado de portar vs reimplementar; costes futuros; origen/revisión y cambios necesarios. No usar inversión histórica como argumento a favor ni origen V1 como motivo de descarte automático.

Un portado sucede solamente dentro de una WO autorizada en CasPro, con diff y perfil propios. No ejecutar suites V1 para acreditar el portado. No hacer de una prueba anterior la fuente canónica de negocio: si contradice la spec se revisa, no se fuerza CasPro a reproducirla.

La auditoría fundacional previa fue estática. Sus carreras identificadas son contraejemplos a cubrir, no ejecuciones realizadas. En la generación inicial solo se volvió a la constitución actual. El Grand Master Program posterior autorizó una lectura más profunda de documentación vigente y la clasificó en [extracción de conocimiento](../evidence/wbpro-knowledge.md); no consultó legacy ni convirtió conclusiones contables/tributarias de Wbpro en normas CasPro.

Las rutas exactas de documentación actual consultada quedan en esa extracción. CasPro debe poder funcionar y especificarse sin acceso al repositorio Wbpro; las fuentes regulatorias externas sostienen cualquier afirmación normativa.
