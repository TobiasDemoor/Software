# Requisito de software
Es una declaración que traduce o expresa una necesidad y sus restricciones y condiciones asociadas. Si se expresa en forma de lenguaje natural, la sentencia debe contener un sujeto, un verbo y un complemento. Un requisito debe indicar el sujeto del requisito (por ejemplo, el sistema, el software, etc.) y lo que se debe hacer. Especifica una función externa visible o atributo de un sistema. Deben declararse de un punto de vista completamente externo.

# Requerimientos funcionales
> “Son las declaraciones de los servicios que debe responder el sistema y de la manera en la que debe reaccionar a las entradas. **Describen lo que el sistema debe hacer**.” -(Sommerville, 2005)

La especificación de requerimientos funcionales debe estar completa y ser consistente:
* Completa: todos los servicios solicitados por el usuario deben estar definidos.
* Consistente: no debe tener definiciones contradictorias ni ambiguas.
* 
En la práctica esto es casi imposible en la gran mayoría de los proyectos, debido a las razones humanas (stakeholders).

# Requerimientos no funcionales
> “Son restricciones establecidas de algunas características o propiedades, que en general afectan a todo el sistema.” -(Sommerville, 2005)

Son más críticos que los requerimientos funcionales porque el incumplimiento de un requerimiento no funcional puede significar que el sistema entero sea inutilizable. Se dividen principalmente en dos tipos:

## Restricciones
También llamados constraints. Son variables de producto inalterables que vienen dadas por el contexto. Son decisiones ya tomadas por el cliente, por ejemplo:
- "La aplicación debe poder usarse desde un navegador web."
- "Para la persistencia se debe usar la versión de MySQL que usamos en la empresa."
- "El sistema debe codificarse en Java."

## Atributos de Calidad
Son las propiedades de un producto de software por medio de las cuales los stakeholders establecen y miden la calidad del producto. La funcionalidad es lo que debe hacer una sistema, para lo cual fue diseñado. Sin embargo, puede fallar al satisfacer otros requerimientos de calidad. Los atributos de calidad se logran a partir de las decisiones arquitectónicas sin perder de vista la funcionalidad deseada. Se puede encontrar una gran selección listados en la ISO 25010 junto con algunas [[Tácticas|tácticas]].
Se clasifican según [[FURPS+]].