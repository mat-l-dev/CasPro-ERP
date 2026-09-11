# Origen del repositorio y publicación inicial

HISTORICAL EVIDENCE. Período: Foundation, Gate 1, Amendment, SP2 y Grand Master, hasta 2026-09-11. Este registro se extrae del README de la baseline `dbb1224d99f4dbdac61da25daf32f1fed872b4fa` para conservar la procedencia sin mezclarla con el estado diario. Fuentes vigentes: [producto](../product/charter.md), [estado global](../review.md) y [arquitectura](../architecture/overview.md).

## Generación inicial y estado publicado

- Durante la generación inicial, la carpeta CasPro-ERP existía y estaba vacía, incluidos archivos ocultos; los archivos de la fundación se crearon entonces.
- Wbpro-ERP es una referencia de solo lectura, nunca una dependencia de ejecución. Se reutilizó la auditoría previa y se consultó selectivamente su constitución actual para distinguir hechos, decisiones y supuestos.
- No se copiaron paquetes, modelos, migraciones, pruebas ni instrucciones extensas de Wbpro. No se consultó legacy.
- La generación inicial no ejecutó tests, Docker, bases de datos, builds ni migraciones, ni creó servicios cloud, repositorios remotos o commits. Posteriormente, Gate 1 fue publicado en el [repositorio CasPro-ERP](https://github.com/mat-l-dev/CasPro-ERP). La [revisión](reviews.md) registra el Foundation Amendment posterior y su comprobación Git.
- SUPERPROMPT 2 fue autorizado posteriormente y se concreta en la [especificación del primer circuito B2C](../specs/flows/first-operational-circuit.md). El Grand Master Program integra ese circuito con P2P, Accounting, Tax, Corporate, UX e IA en [cuatro roadmaps coordinados](../roadmap/program.md). Sus seis Work Orders son insumos históricos pendientes de regeneración después del freeze y la investigación de skills; implementación y ejecuciones requieren un nuevo encargo.

La arquitectura distingue principios aceptados de mecanismos provisionales por alcance en cada ADR. El monolito modular, la propiedad explícita y la coordinación transaccional no dan por validado RLS, las versiones, los parámetros numéricos o la operación. La fundación puede ser referencia canónica de esas decisiones y pendientes sin convertirlos en controles implementados.
