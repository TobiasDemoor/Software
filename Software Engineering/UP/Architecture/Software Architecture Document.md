In addition to the UML package, class, and interaction diagrams, another key artifact in the [[Unified Process|UP]] [[Design Model]] is the SAD. It describes the big ideas in the [[Software Architecture|architecture]], including the decisions of [[Architecture analysis|architectural analysis]]. Practically, it is a learning aid for developers who need to understand the essential ideas of the system.
Therefore, it should be written with this audience and goal in mind: What do I need to say (and draw in the UML) that will quickly help someone understand the major ideas in this system?

# Architectural views
1. **Logical architecture**
	- Organización conceptual del software en términos de las [[Layers|capas]], subsistemas, paquetes, [[Framework|frameworks]], clases e interfaces más importantes.
	- Muestra realización de [[Use Case|casos de uso]] sobresalientes (como diagramas de interacción) que ilustran aspectos claves del sistema.
2. **Process architecture**
	- Procesos e hilos. Sus responsabilidades, colaboraciones y su la alocación de elementos lógicos a ellos.
3. **Deployment architecture** describe el sistema en terminos de la alocación de procesos a unidades de procesamiento y la configuración de red. Resume la topología del sistema, comunicaciones y mapeo de los elementos ejecutables a nodos de procesamiento, es un término similar a arquitectura de sistema.
	- Deployment físico de procesos y [[Componente|componentes]] a nodos de procesamiento y la configuración red física entre los nodos.
	- Una vista al Deployment Model visualizado con [[Deployment Diagram|deployment diagrams]].
4. **Data architecture**
	- Vista general del esquema de datos persistentes, el esquema de mapeo de objetos a datos persistentes, el mecanismo de mapeo de objetos a [[Bases de Datos|base de datos]], procedimientos almacenados en la [[Bases de Datos|base de datos]] y triggers.
5. **Use case architecture**
	- Resumen de los [[Use Case|casos de uso]] con mayor significancia arquitectónica y sus [[Requerimientos no funcionales|requerimientos no funcionales]].
	- Una vista al Use-Case Model, expresado en texto y visualizado con use case diagrams.
6. **Implementation architecture**
	- Es un descripción resumida del conjunto de deliverables relevantes y las cosas que crean los deliverables (cómo el codigo fuente).
	- *In contrast to the other UP models, which are text and diagrams, this "model" is the actual source code, executables, and so forth. It has two parts: 1) deliverables, and 2) things that create deliverables (such as source code and graphics). The Implementation Model is all of this stuff, including web pages, DLLs, executables, source code, and so forth, and their organization—such as source code in Java packages, and bytecode organized into JAR files*
	- Una vista al Implementation Model, expresado en texto y visualizado mediante Package Diagram y [[Component Diagram]].

# Contenido
- Caracterísiticas del producto
- [[Requerimientos funcionales|Requerimientos funcionales]]
- [[Requerimientos no funcionales|Requerimientos no funcionales]]
- [[Requerimientos no funcionales#Restricciones|Restricciones]]
- Decisiones arquitectónicas y de diseño
- Modelos de vistas
- Descripción del comportamiento
- Las [[Interfaz|interfaces]] entre los [[Componente|componentes]]
- Trazabilidad entre elementos.