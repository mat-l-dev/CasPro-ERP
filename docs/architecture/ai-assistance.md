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

### Revalidación concreta al 2026-09-11

La [tabla DeepSeek](https://api-docs.deepseek.com/quick_start/pricing/) identifica `deepseek-flash`→V4.1-Flash y `deepseek-v4-pro`→V4-Pro-0813, contexto1M y máximo de salida384K, JSON/tools. En hora pico, USD por millón entrada sin caché/salida: Flash0.30/1.20; Pro1.32/3.96; fuera de pico la mitad. Los alias Flash antiguos ya sirven otro modelo: registrar alias **y versión efectiva**, no prometer reproducibilidad por alias. Ejemplo aritmético propio:1000 sugerencias de1000 tokens de entrada+200 de salida costarían0.54/2.112 USD respectivamente en pico, sin caché/reintentos/impuestos. No es presupuesto medido ni recomendación de enviar datos privados.

[JSON mode](https://api-docs.deepseek.com/guides/json_mode/) no demuestra conformidad con el esquema CasPro ni corrección factual: validar tipos, campos, IDs autorizados, límites y abstención; salida inválida se rechaza con fallback manual. Las condiciones contractuales de retención, entrenamiento, residencia y DPA permanecen **PENDING VALIDATION** antes de usar datos empresariales; no inferir privacidad de un endpoint compatible.

[OCI Always Free](https://docs.oracle.com/en-us/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm) consultado ahora anuncia A1 Arm2 OCPU/12GB totales,1500 OCPU-h y9000GB-h/mes, y200GB de volumen; no usar la cifra histórica4/24 sin comprobar contrato. Puede faltar capacidad en región y reclamarse instancia ociosa. No se ha comprobado disponibilidad en una cuenta del propietario ni provisionado nada. Es candidato a laboratorio prescindible, no continuidad de ERP ni GPU gratuita garantizada.

Estimación de ingeniería, no benchmark: pesos8B a4bits ocupan unos4GB antes de runtime/KV/cache;12GB podría alojar una cuantización pequeña con contexto acotado, pero CPU Arm/latencia/compatibilidad deben medirse. Pesos671B a4bits necesitan unos335.5GB solo en pesos: que MoE active37B no permite cargar solo37B. API evita ese hardware pero introduce coste/datos externos. Modelo Hermes8B conserva su licencia Llama; Hermes Agent MIT es orquestador, no esos pesos.

Alternativa mínima para M06: reglas/heurísticas sin LLM, coste de inferencia cero y explicación determinista, con menor cobertura semántica. Piloto siguiente compara ese baseline con una API y un modelo pequeño local fijados,100 casos sintéticos iniciales con ambiguos/negativos y20 ataques de documento/instrucción. Son tamaños de diseño del piloto, no evidencia estadística de precisión. Se mide abstención, falsos matches, calibración, latenciaP50/P95, memoria y coste por caso; ningún score habilita escrituras. Criterio de seguridad: cero ejecución de instrucciones de documento y cero referencias fuera de alcance; para calidad, el humano debe poder revisar cada propuesta y el piloto puede concluir REJECT.

Registrar inputs minimizados y explicación verificable, nunca razonamiento privado. Desactivar memoria/aprendizaje cruzado, skills dinámicas, shell, conectores de escritura y red no autorizada para cualquier host de agentes que se evalúe. Preferencia arquitectónica para este caso acotado: adapter directo antes de desplegar Hermes Agent completo; es CASPRO DECISION candidata por menor superficie, no crítica a su calidad general.

Antes de piloto: inventario real CPU/RAM/GPU/disco/red/persistencia; clasificación de datos; DPA/retención/localización si API; licencia exacta; versión y hashes; aislamiento de red/secretos; timeout/circuit breaker; presupuesto; schema con abstención; dataset y baseline; prueba adversarial de prompt injection/documentos; recuperación y apagado. El primer piloto recomendado, después de tener hechos, es **sugerencia de conciliación bancaria offline/sintética**, sin tools de escritura.
