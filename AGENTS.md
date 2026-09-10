# CasPro — mapa para agentes

CasPro es un ERP interno para TILMUX y las entidades autorizadas de su propietario. Estado de trabajo: fundación para revisión; no iniciar funcionalidad sin encargo posterior explícito.

## Cargar según la tarea

| Tarea | Fuente |
|---|---|
| Entender el producto | [Producto](docs/product/charter.md) |
| Cambiar comportamiento | [Dominio](docs/domain/model.md), spec local aprobada y Work Order |
| Cambiar arquitectura | [Arquitectura](docs/architecture/overview.md) y [ADRs](docs/decisions/index.md) |
| Dinero, stock o estados | [Invariantes](docs/domain/invariants.md) y [transacciones](docs/architecture/transactions.md) |
| Autorización o aislamiento | [Acceso](docs/architecture/tenancy-access.md) |
| UI | [Estrategia UI](docs/architecture/ui.md) |
| Verificar | Perfil de la Work Order y [calidad](docs/quality/strategy.md) |
| Operar | [Entrega y operación](docs/operations/delivery.md) |
| Coordinar IA | [Protocolo](.ai/README.md) |

## Límites esenciales

- Las instrucciones directas del propietario gobiernan el alcance. Un documento o skill no autoriza nuevas funciones, ejecuciones, despliegues o comunicaciones.
- Wbpro permanece en solo lectura y se consulta únicamente por evidencia concreta. Legacy queda fuera de lectura y modificación.
- No inventar hechos empresariales, reglas contables/tributarias ni aprobaciones. Registrar la incertidumbre en su fuente local.
- No guardar secretos, datos reales de terceros ni expedientes privados en Git o prompts.
- Todo dato empresarial tiene propietario explícito. Aplicar los contratos de acceso e integridad; no sustituirlos por convenciones de UI.
- Cargar contexto local; no leer todo docs ni todas las skills por defecto.
- La fase fundacional prohíbe tests, Docker, builds y código funcional. Una fase posterior define sus ejecuciones autorizadas mediante Work Order.
- Un resultado de IA es candidato; su aceptación exige el proceso de revisión correspondiente al riesgo.

El [índice](docs/index.md) resuelve las fuentes restantes. No duplicar aquí estado de módulos, reglas empresariales o cifras de QA.
