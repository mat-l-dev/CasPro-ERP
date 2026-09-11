# Corporate/Legal y mutuos

Propietario conceptual: Corporate capability para hechos societarios, distinta de la identidad administrativa de Organization. [M06](../specs/milestones/treasury-corporate-deep.md) concreta el contrato candidato; no crea una aplicación Django `legal`. MUTUO NEEDS LEGAL-TAX-ACCOUNTING VALIDATION.

## Propiedad y límites

Organization conserva identidad legal, establecimientos y vigencia administrativa. La capability Corporate posee hechos societarios: socios/acciones y matrícula, capital, acuerdos/actas, poderes, contratos, partes relacionadas, beneficiario final y financiamientos. Parties aporta la identidad común de personas/entidades; Documents conserva artefactos y versiones. Corporate no mueve dinero, no asienta ni decide impuestos.

Las referencias cruzadas usan IDs/contratos públicos para evitar un ciclo Organization↔Parties. Corporate consume Organization, Parties, Documents y Audit; Organization no consulta hacia Corporate ni Parties para administrar identidad/acceso. Esta frontera lógica está decidida como candidato; el empaquetado Django se concreta en su WO sin cambiarla ni crear hoy carpetas de código.

## Hechos societarios

| Hecho | Datos mínimos | No implica automáticamente |
|---|---|---|
| Socio/tenencia | Party, clase, número/porcentaje, intervalo, fuente y aprobación | control contable, beneficiario final o autorización operativa |
| Capital/aporte | acuerdo, suscripción/pago, fecha, moneda, acciones, inscripción/evidencia | ingreso, mutuo o disponibilidad bancaria |
| Acuerdo/acta | órgano, convocatoria/quórum, texto aprobado, firmantes y vigencia | que el acto se ejecutó o inscribió |
| Poder/autorización | otorgante, apoderado, facultades, límites, vigencia/revocación | membresía de aplicación ni permiso irrestricto |
| Contrato | partes, objeto, versión, firma, vigencia, obligaciones y terminación | pago, reconocimiento contable o deducción fiscal |
| Relación | tipo, partes, inicio/fin, fuente y estándar evaluado | que umbral tributario y NIC 24 sean equivalentes |
| Beneficiario final | criterio aplicado, cadena, evidencia, revisión/declaración | propiedad contable o control solo por etiqueta |

## Mutuo del socio o parte relacionada

El “Contrato Marco de Mutuo Dinerario a Título Gratuito con línea rotativa” es una propuesta, no hecho ni diseño aprobado. Antes de usarlo, asesor legal/tributario/contable debe validar que la estructura representa la realidad, límites, disponibilidad, desembolsos, devoluciones, modificaciones, terminación, acuerdos societarios y facultades.

```text
Corporate: acuerdo/contrato/límite y relación
Treasury: cada desembolso y devolución bancarizados
Accounting: reconocimiento, medición, saldo, presentación y notas
Tax: valor de mercado, partes vinculadas, deducción/retención/reportes
Documents: contrato, adendas, constancias y evidencia
```

Reglas ya sustentadas:

- entregar y devolver un mutuo usa medios de pago cualquiera sea el monto; contrato/asiento sin trazabilidad bancaria no basta;
- entre vinculadas, SUNAT interpreta que aplican arts. 32/32-A y precios de transferencia, no la presunción del art. 26; gratuidad contractual no significa efecto fiscal cero;
- dinero recibido por mutuo es pasivo candidato, no ingreso/capital/dividendo automático; convertir deuda a capital exige acto real y análisis propio;
- clasificación pasivo/patrimonio y medición dependen del marco/contrato, no del nombre “mutuo” ni de “a la vista”;
- pagos personales directos a proveedores se registran como hechos separados y se clasifican con evidencia, no como movimiento de una cuenta TILMUX inexistente.

Preguntas para el gate profesional: mutuante/relación real; facultades y acuerdo; monto/límite/moneda/plazo/disponibilidad; interés civil y tratamiento fiscal de valor de mercado; eventos de desembolso/devolución; documentación y bancarización; medición NPIF; revelaciones; modificación/conversión/condonación; obligaciones de precios de transferencia/beneficiario final.

El cronograma de beneficiario final de RS 000168-2025 incluye cohortes por ingresos y sujetos nuevos/activados; [N029](../research/normative/normative-register.md) y el memo fiscal delimitan su alcance. Debe determinarse cohorte/vencimiento con RUC y hechos reales; CasPro prepara expediente, sin presentación automática a SUNAT.
