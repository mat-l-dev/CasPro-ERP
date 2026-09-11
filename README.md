# CasPro ERP

**Fundación y especificación documental — 2026-09-10.** ERP interno diseñado primero para TILMUX S.A.C. La condición vigente y el cierre de Gate 1 se consultan en la [revisión](docs/review.md). Esta entrega contiene decisiones y contratos de diseño; no contiene software funcional, infraestructura desplegada ni evidencia de ejecución.

Empieza por el [índice](docs/index.md), el [producto](docs/product/charter.md) y el [registro de decisiones](docs/decisions/index.md). La [revisión fundacional](docs/review.md) identifica límites, refutaciones y decisiones humanas pendientes.

## Generación inicial y estado publicado

- Durante la generación inicial, la carpeta CasPro-ERP existía y estaba vacía, incluidos archivos ocultos; los archivos de la fundación se crearon entonces.
- Wbpro-ERP es una referencia de solo lectura, nunca una dependencia de ejecución. Se reutilizó la auditoría previa y se consultó selectivamente su constitución actual para distinguir hechos, decisiones y supuestos.
- No se copiaron paquetes, modelos, migraciones, pruebas ni instrucciones extensas de Wbpro. No se consultó legacy.
- La generación inicial no ejecutó tests, Docker, bases de datos, builds ni migraciones, ni creó servicios cloud, repositorios remotos o commits. Posteriormente, Gate 1 fue publicado en el [repositorio CasPro-ERP](https://github.com/mat-l-dev/CasPro-ERP). La [revisión](docs/review.md) registra el Foundation Amendment posterior y su comprobación Git.
- SUPERPROMPT 2 fue autorizado posteriormente y se concreta en la [especificación del primer circuito B2C](docs/specs/first-operational-circuit.md). El Grand Master Program posterior integra ese circuito con P2P, Accounting, Tax, Corporate, UX e IA en [cuatro roadmaps coordinados](docs/roadmap/program.md). Sus Work Orders siguen preparadas; implementación y ejecuciones requieren un nuevo encargo.

La arquitectura distingue principios aceptados de mecanismos provisionales por alcance en cada ADR. El monolito modular, la propiedad explícita y la coordinación transaccional no dan por validado RLS, las versiones, los parámetros numéricos o la operación. La fundación puede ser referencia canónica de esas decisiones y pendientes sin convertirlos en controles implementados.
