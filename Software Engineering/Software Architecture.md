# Software Architecture
Es el conjunto de estructuras necesarias para razonar sobre el sistema, que comprende los elementos de software, las relaciones entre ellos y las propiedades de ambos. Es la parte *"gruesa"* del [[Diseño de sistemas|diseño]], con menor nivel de detalle pero definiendo la estructura general. La documentación de la arquitectura es prescriptiva y debe ser validada contra lo que se implementó.

La arquitectura actúa como "puente" entre los [[Requerimientos]] del sistema y su implementación. Es la que habilita la ejecución del [[Modelo de negocio|modelo de negocio]] para crear el mayor valor al cliente, minimizando costos y maximizando ingresos. No debe ignorar la complejidad de las relaciones entre los 4 componentes ([[Software Engineering/Fundamentals/Dominio|dominio]], [[Modelo de negocio|modelo de negocio]], [[Estructura organizacional|estructura organizacional]] y arquitectura de software en sí).

Una definición es:
>An architecture is the set of significant decisions about the organization of a software system, the selection of the structural elements and their interfaces by which the system is composed, together with their behavior as specified in the collaborations among those elements, the composition of these structural and behavioral elements into progressively larger subsystems, and the architectural style that guides this organization---these elements and their interfaces, their collaborations, and their composition. \[BRJ99\]

**Architectural investigation** involves identifying those [[Requerimientos#Requerimientos funcionales|functional]] and (especially) [[Requerimientos#Requerimientos no funcionales|non-functional requirements]] that have (or should have) a significant impact on the [[Diseño de sistemas|system design]], such as market trends, [[FURPS+#Performance|performance]], cost, [[FURPS+#Mantainability|maintainability]], and [[Variaciones protegidas|points of evolution]]. Broadly, it is requirements analysis with a focus on those requirements that have special influence on the major system design decisions.
**Architectural design** is the resolution of these forces and requirements in the design of the software, the hardware and networking, operations, policies, and so forth.
In the [[Unified Process|UP]], architectural investigation and design are together called **[[Architecture analysis|architectural analysis]]**.

# Actividades
- Crear el negocio del sistema.
- Comprender [[Requerimientos|requerimientos]]. En particular los [[Requerimientos#Atributos de Calidad|QA]].
- Crear o seleccionar la arquitectura.
- Documentar y comunicar la arquitectura.
- Analizar o evaluar la arquitectura.
- Asegurar la construcción del sistema sobre esa arquitectura.

# Beneficios
- Comunicación con los stakeholders.
- Análisis del sistema de manera temprana.
- Reutilización a gran escala y [[Patrones|patrones]].

## ¿Por qué necesitamos arquitectura de software?
- Permite un análsis temprano de las principales características del sistema a construir, como así también facilitar el manejo de la complejidad ante sistemas grandes.
- Un sistema podría cumplir la adecuación funcional y aún así tener problemas. Los [[Requerimientos#Requerimientos no funcionales|requerimientos no funcionales]] necesitan soporte desde la arquitectura.
- Frecuentemente no se hace foco o se analizan en detalle las propiedades o atributos del software que se desarrolloa.
- El diseño se va conformando por la suma de acciones aisladas y equipos desacoplados que no tienen una visión común del producto.
- Se genera [[Deuda técnica|deuda técnica]] sin el debido registro ni gestión (y también a veces con poca concienca).
- La [[Agile methodologies|agilidad]] mal aplicada relega la arquitectura.
- Facilita la comunicación entre los stakeholders durante todo el cilco de vida.
- Es un registro que se lleva desde el inicio del proyecto sobre las decisiones de diseño tomadas respecto del producto.
- Es una [[Abstracción|abstracción]] representada en un modelo reusable y transferible de un sistema, utilizado además como una prescripción para la implementación.

# Architectural Business Cycle (ABC)
Es el ciclo en el cual la arquitectura del sistema se define como consecuencia de una serie de influencias provenientes del [[#Contexto técnico|contexto técnico]], el [[#Contexto de negocios|contexto de negocios]], el [[#Contexto del proyecto|contexto del proyecto]] y el [[#Contexto profesional|contexto profesional]]. A su vez, la existencia de esta arquitectura afecta a dichos contextos, que posteriormente influirán en arquitecturas futuras y así sucesivamente. El ciclo puede describirse a partir de los siguientes tópicos:

## Contexto técnico
Las prácticas estándares de la industria y las técnicas de ingeniería de software prevalentes en la comunidad influencian fuertemente la arquitectura. A su vez, el contexto técnico incluye el cumplimiento de los atributos de calidad del producto. Por otro lado, la arquitectura afecta a los [[Requerimientos|requerimientos]] de los stakeholders al darle la oportunidad a éstos de obtener un sistema con una mayor madurez a futuro en cuanto a los [[Requerimientos#Atributos de Calidad|atributos de calidad]].

## Contexto de negocios
El sistema es creado principalmente a partir de la arquitectura para satisfacer las necesidades del modelo de negocios de la empresa que va a utilizar dicho sistema. A su vez, la arquitectura del sistema puede influenciar fuertemente el modelo de negocios y los objetivos de la empresa al brindar la posibilidad de abordar ciertos casos de una manera más eficiente y con un alcance mayor.

## Contexto del proyecto
El equipo de desarrollo debe crear un caso de negocios para el sistema, entender los requerimientos de la arquitectura que éste demande, diseñar, comunicar, documentar y analizar dicha arquitectura, implementarla y [[Verificación y validación|verificar y validar]] dicha implementación. A su vez, esta arquitectura prescribe una estructura para el sistema, particularmente las unidades o módulos de software que deben ser implementados u obtenidos de alguna manera para conformar dicho sistema. Estas unidades son la base para la estructura de desarrollo del proyecto, por lo que existe una influencia mutua entre la arquitectura y el proyecto de desarrollo.

## Contexto profesional
Tanto el diseño como la implementación de la arquitectura requieren habilidades y conocimientos que influirán en el resultado. A su vez, cada sistema y entorno tiene sus particularidades que requerirán que tanto el arquitecto como el equipo de desarrollo amplíen su conocimiento y habilidades a medida que van ganando experiencia.

# Dcoumentación de la Arquitectura de Software
Documentar una arquitectura de software es una cuestión de documentar las vistas relevantes y luego agregar información que se aplica a más de una vista.
Se produce el SAD ([[Software Architecture Document]]):
- Sirve principalmente para la educación, comunicación y análisis de la arquitectura.
- Se produce de forma iterativa junto a todo el trabajo de diseño.
- No es un documento monolítico difícil de leer.
- Debe estar orientado a las necesidades de información de cada stakeholder.
- UML por sí solo no hace a una buena documentación. Se puede hacer un mal uso del mismo.
- Siempre incluir comportamiento.