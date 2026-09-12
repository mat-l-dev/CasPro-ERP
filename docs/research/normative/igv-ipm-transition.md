# IGV/IPM — transición de componentes

Corte 2026-09-12; F05. Pregunta: mantener total sintético correcto y seleccionar componentes por hecho/vigencia cuando Tax/aduanas/layout los necesitan. No cambia G1 ni crea motor tributario.

## Fuentes y conciliación

| Fuente oficial | Evidencia verificada y límite |
|---|---|
| [SUNAT, TUO IGV capítulo V PDF, art.17, página6](https://www.sunat.gob.pe/legislacion/igv/ley/capitul5.pdf) | Reproduce modificación por tercera DCM Ley32387, publicación 2025-06-16; cuarta DCF condiciona aspectos cuantitativos al incremento gradual art.2 desde 2026-01-01. El texto14% es destino de transición, no tasa inmediata para2026 |
| [SUNAT orientación vigente, Concepto/Tasa](https://orientacion.sunat.gob.pe/3053-concepto-tasa-y-operaciones-gravadas-igv-empresas) | Tabla explícita2026–2029 con IPM/IGV y total18%; confirma lectura operacional de ley |
| [Congreso, Ley32387 consolidada](https://leyes.congreso.gob.pe/Documentos/2021_2026/ADLP/Texto_Consolidado/32387-TXM.pdf) | Localizado texto oficial indexado de publicación y art.2; descarga íntegra falló en esta consulta. No se declara lectura íntegra; el pasaje legal aplicable se comprobó en PDF SUNAT anterior |
| [SUNAT HTML antiguo capítulo V](https://www.sunat.gob.pe/legislacion/igv/ley/capitul5.htm) | Conserva15% condicionado al DL1347 y texto anterior16%; omite Ley32387. Fuente desactualizada para esta transición, no prevalece sobre PDF actualizado y orientación |

La reproducción municipal usada por el audit original no es fundamento principal de esta corrección. Se verificó directamente fuente normativa publicada por SUNAT y orientación operativa; publicación de Ley32387 no significa que todos sus números finales rijan en2025.

## Tabla aplicable al supuesto general gravado

| Desde incluido | Hasta excluido | IGV | IPM | Total |
|---|---|---:|---:|---:|
| 2026-01-01 | 2027-01-01 | 15.5% | 2.5% | 18% |
| 2027-01-01 | 2028-01-01 | 15% | 3% | 18% |
| 2028-01-01 | 2029-01-01 | 14.5% | 3.5% | 18% |
| 2029-01-01 | Sustitución legal aplicable | 14% | 4% | 18% |

Para el supuesto general previo,16%+2% es antecedente, no constante universal. No inferir tasa para inafectos/exonerados/exportaciones ni regímenes especiales por esta tabla; selección del hecho y norma en C08/C07. Importación conserva base/tributos aduaneros y crédito/deducción aplicables: no reemplazar liquidación DAM por total comercial.

## Consumo y versiones

Reutilizar la regla tributaria versionada, fuente/efectividad y revisión del perfil definidos por Tax. Selección por entidad, propósito/consumidor, naturaleza y fecha legal del hecho/período, base y revisión de fuente. Persistir versión, componentes realmente usados, total y linaje; fecha de importación del archivo o de emisión del reporte no sustituye fecha legal del hecho. Hueco/solapamiento o norma posterior no reconciliada → HOLD fiscal, sin elegir tasa más reciente por comodidad.

Tax/imports/aduanas/layouts y reconciliaciones que demandan desglose conservan ambos componentes. Sales que solo necesita total usa el resultado autorizado18%, sin inventar campos fiscales o dividir con constantes. Accounting no reposta por cambio de etiqueta o desglose sin nuevo hecho. Corrección histórica crea revisión con norma aplicable al hecho; nunca reescribe original con regla vigente hoy. Nueva ley se registra y supersede por período, no extrapolando una fórmula de incremento.

B04/B08/B14 requieren posteriormente casos2026, fronteras2027/2028/2029, total igual con split distinto, import con desglose, venta con total, corrección histórica y fuente posterior. Revisión editorial:15.5+2.5=15+3=14.5+3.5=14+4=18. Ningún test ejecutado. C08/C07 retienen clasificación real, layout, oportunidad y criterio profesional. G1 continúa válido y sin cambios.
