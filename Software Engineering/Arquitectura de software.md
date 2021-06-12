Es el conjunto de estructuras necesarias para razonar sobre el sistema, que comprende los elementos de software, las relaciones entre ellos y las propiedades de ambos. Es la parte *"gruesa"* del [[Diseño de sistemas|diseño]], con menor nivel de detalle pero definiendo la estructura general. La documentación de la arquitectura es prescriptiva y debe ser validada contra lo que se implementó.
La arquitectura actúa como "puente" entre los [[Requerimientos]] del sistema y su implementación
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
- Reutilización a gran escala y patrones.

## ¿Por qué necesitamos arquitectura de software?
- Permite un análsis temprano de las principales características del sistema a construir, como así también facilitar el manejo de la complejidad ante sistemas grandes.
- Un sistema podría cumplir la adecuación funcional y aún así tener problemas. Los [[Requerimientos#Requerimientos no funcionales|requerimientos no funcionales]] necesitan soporte desde la arquitectura.
- Frecuentemente no se hace foco o se analizan en detalle las propiedades o atributos del software que se desarrolloa.
- El diseño se va conformando por la suma de acciones aisladas y equipos desacoplados que no tienen una visión común del producto.
- Se genera [[Deuda técnica|deuda técnica]] sin el debido registro ni gestión (y también a veces con poca concienca).
- La [[Agile methodologies|agilidad]] mal aplicada relega la arquitectura.
- Facilita la comunicación entre los stakeholders durante todo el cilco de vida.
- Es un registro que se lleva desde el inicio del proyecto sobre las decisiones de diseño tomadas respecto del producto.
- Es una abstracción representada en un modelo reusable y transferible de un sistema, utilizado además como una prescripción para la implementación.

# Modelos
- [[Deployment Diagram]]
- [[Diagrama de módulos]]