# Arquitectura de IA asistida

Propietario: plataforma de asistencia, con decisiones finales en cada dominio. Estado: PROVISIONAL / RESEARCHED; no hay proveedor, modelo, VPS ni runtime elegido. La IA no es fuente de verdad.

## Frontera

```text
caso de uso autorizado → redacción/minimización → AIService
 → ProviderAdapter(modelo/versión) → salida estructurada sin permisos
 → validaciones deterministas → candidato explicable → decisión humana/dominio
 → auditoría + evaluación
```

`AIService` centraliza políticas, presupuesto, timeout, redacción, esquemas, provenance y observabilidad. Un adaptador puede usar API o inferencia propia; ningún dominio importa SDK/modelo. El modelo recibe solo datos necesarios y nunca credenciales, documentos completos por defecto o acceso DB. Sus tools son lecturas acotadas/candidatos; comandos que cambian dinero, ledger, stock, pagos, períodos, CPE, impuestos o envíos están fuera de su autoridad.

## Casos y riesgo

| Caso | Riesgo | Salida permitida | Control |
|---|---|---|---|
| Resumir/extractar documento ya autorizado | MEDIUM | campos+citas+incertidumbre | esquema, límites, revisión contra original |
| Clasificar gasto/cuenta | HIGH | candidatos y razones | política determinista y aprobación Accounting |
| Matching documental | MEDIUM/HIGH | candidatos, coincidencias/diferencias | no vincular ni verificar automáticamente |
| Conciliación bancaria | HIGH | ranking/confianza/contraevidencia | humano confirma; dinero preexistente |
| Explicar discrepancia/EEFF | MEDIUM | explicación con links a fuentes | cálculo proviene de sistema, no del LLM |
| Búsqueda semántica | MEDIUM | resultados autorizados | filtro de entidad/permisos antes y después |
| Anomalías | MEDIUM/HIGH | alerta reproducible | baseline/version/evaluación; sin bloqueo automático |
| Crear/modificar hechos críticos | PROHIBITED AUTONOMOUS ACTION | ninguna | puerto inexistente para el modelo |

## Evidencia por inferencia

Registrar caso, propósito, actor/entidad, inputs referenciados y redacciones, prompt/plantilla, modelo/proveedor/versión, parámetros, tools, output original/esquema, latencia/coste, validaciones, confianza/razones/contraevidencia, decisión humana y resultado posterior. No usar cadenas de pensamiento privadas como requisito de auditoría. Retención y reuso de prompts/outputs respetan sensibilidad del dato.

El dataset de evaluación usa ejemplos sintéticos o anonimizados aprobados, incluye positivos/negativos/ambiguos y mide falso positivo, falso negativo, abstención, schema validity, citas, coste y latencia. Un cambio de modelo, prompt, tool, política, esquema, redacción o distribución invalida comparabilidad hasta rerun. Siempre existe fallback determinista/manual.

## Candidatos investigados

**Hermes es ambiguo.** A la fecha hay al menos Hermes Agent de Nous Research y modelos Hermes. Hermes Agent es un host/agente MIT con tools, memoria, skills, gateways, automatización y múltiples proveedores; por su amplitud aumenta superficie de supply chain, secretos y acciones. La documentación promete VPS económicos, no prueba que el VPS gratuito del propietario tenga RAM/CPU/GPU, persistencia, aislamiento o disponibilidad. Hermes 3 8B deriva de Llama 3.1 y su model card usa licencia Llama 3, no MIT. Ninguno se selecciona como componente CasPro sin threat model, versión fijada, SBOM, sandbox, pruebas de tool calling y recursos medidos. Fuentes: [Hermes Agent](https://github.com/NousResearch/hermes-agent), [seguridad de ejecución](https://github.com/NousResearch/hermes-agent/blob/main/website/docs/user-guide/features/code-execution.md), [Hermes 3 8B](https://huggingface.co/NousResearch/Hermes-3-Llama-3.1-8B).

**DeepSeek tampoco es una sola decisión.** API, modelo y pesos/licencias se versionan por separado. La documentación actual ofrece modelos V4 con JSON/tools y contexto grande, pero precios/nombres son volátiles. DeepSeek-V3 local tiene 671B parámetros totales/37B activos y el ejemplo oficial usa paralelismo multi-GPU, impropio de un VPS gratuito común; modelos/quantizaciones menores necesitan evaluación separada. Código V3 es MIT, pesos V3 tienen licencia propia con restricciones. Fuentes: [API y precios actuales](https://api-docs.deepseek.com/quick_start/pricing), [V3/recursos](https://github.com/deepseek-ai/DeepSeek-V3), [licencia del modelo](https://github.com/deepseek-ai/DeepSeek-V3/blob/main/LICENSE-MODEL).

Alternativas se compararán por calidad en dataset CasPro, structured output/tool reliability, español, contexto, residencia/retención de datos, licencia, coste, latencia, rate limits, observabilidad, soporte y portabilidad. Ninguna marca recibe ventaja por popularidad.

## Gate de proveedor/VPS

Antes de piloto: inventario real CPU/RAM/GPU/disco/red/persistencia; clasificación de datos; DPA/retención/localización si API; licencia exacta; versión y hashes; aislamiento de red/secretos; timeout/circuit breaker; presupuesto; schema con abstención; dataset y baseline; prueba adversarial de prompt injection/documentos; recuperación y apagado. El primer piloto recomendado, después de tener hechos, es **sugerencia de conciliación bancaria offline/sintética**, sin tools de escritura.
