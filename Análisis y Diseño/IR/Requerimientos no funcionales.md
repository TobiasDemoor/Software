# Requerimientos no funcionales
> “Son restricciones establecidas de algunas características o propiedades, que en general afectan a todo el sistema.” -(Sommerville, 2005)

Son más críticos que los requerimientos funcionales porque el incumplimiento de un requerimiento no funcional puede significar que el sistema entero sea inutilizable.
![[requerimientos_no_funcionales_1.png]]
Se dividen principalmente en dos tipos:

## Restricciones
También llamados constraints. Son variables de producto inalterables que vienen dadas por el contexto. Son decisiones ya tomadas por el cliente, por ejemplo:
- "La aplicación debe poder usarse desde un navegador web."
- "Para la persistencia se debe usar la versión de MySQL que usamos en la empresa."
- "El sistema debe codificarse en Java."

## Atributos de Calidad
Son las propiedades de un producto de software por medio de las cuales los stakeholders establecen y miden la calidad del producto. La funcionalidad es lo que debe hacer una sistema, para lo cual fue diseñado. Sin embargo, puede fallar al satisfacer otros requerimientos de calidad. Los atributos de calidad se logran a partir de las decisiones arquitectónicas sin perder de vista la funcionalidad deseada. Se puede encontrar una gran selección listados en la ISO 25010 junto con algunas [[Tácticas|tácticas]].
Se clasifican según [[FURPS+]].