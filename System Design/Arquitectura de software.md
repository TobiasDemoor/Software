Es el conjunto de estructuras necesarias para razonar sobre el sistema, que comprende los elementos de software, las relaciones entre ellos y las propiedades de ambos. Es la parte *"gruesa"* del [[Diseño de sistemas|diseño]], con menor nivel de detalle pero definiendo la estructura general. La documentación de la arquitectura es prescriptiva y debe ser validada contra lo que se implementó.
La arquitectura actúa como "puente" entre los [[Requerimientos]] del sistema y su implementación

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

# Modelos
- [[Diagrama de despliegue]]
- [[Diagrama de módulos]]

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