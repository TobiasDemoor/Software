En términos generales, los requisitos son capacidades y condiciones con los cuales debe ser conforme el sistema y más ampliamente el proyecto. Para cada tipo se tienen [[Patrones|patrones]] especificos y probados.

# Functional
Por supueso que se debe considerar como un elemento curcial de la calidad del software el cumplimiento de los [[Requerimientos#Requerimientos funcionales|requerimientos funcionales]]. Dentro de este atributo entran las features, capabilities y la seguridad.

# Usability
Capacidad del producto de software para ser entendido, aprendido, usado y resultr atractivo, cuando se usa bajo determinadas condiciones. Aspectos:
- **Capacidad para reconocer su adecuación**: grado en el cual los usuarios pueden reconocer cuando un sistema es apropieado para sus necesidades.
- **Capacidad de aprendizaje**: grado en el cual un producto puede ser utilizado de manera más eficiente a medida que se aprende a utilizarlo.
- **Capacidad para ser usado**: grado en el cual un sistema tiene atributos que hacen que sea fácil de operar y controlar.
- **Protección contra errores de usuario**: grado en el cual un sistema protege a los usuarios de cometer errores.
- **Estética de la interfaz de usuario**: grado en el cual una UI es satisfactoria para el usuario.
- **Accesibilidad**: grado en el cual un producto o sistema puede ser usado por amplio rango de personas con capacidades distintas.
Dentro de este atributo entran los factores humanos, la ayuda a los usuarios y la documentación.

## [[Tácticas]]
- Separar interfaz de usuario del resto del sistema para que sea más fácilmente adaptable a lo que solicitan los usuarios.
	- [[Model-View-Controller]]
	- [[Layers]]
	- [[Client-Server]]
- Usuario
	- [[Command]]

# Reliability
Capacidad de un sistema o componente para desempeñar las funciones específicas, cuando se usa bajo condiciones y períodos de tiempo determinados. El mínimo del que podemos hablar es 99%, si un sistema no tiene alta disponibilidad, no puede ser confiable.
- Madurez: capacidad del sistema para satisfacer las necesidades de fiabilidad en condiciones normales.
- Disponibilidad: capacidad del sistema o componente de estar operativo y accesible para su uso cuando se requiere.
- Tolerancia a fallos: capacidad para operar según lo previsto en presencia de [[Fault, Failure|fallas]] de hardware y/o software.
- Capacidad de recuperación: capacidad para recuperar datos afectados y el estado del sistema ante [[Fault, Failure|fallos]] o interrupciones.
Dentro de este atributo entran la fecuencia de [[Fault, Failure|fallas]], la recoverability y la predictability.

## [[Tácticas]] para disponibilidad
- Detección de fallas
	- Ping/echo: se utiliza tanto para conocer los tiempos de respuesta como para saber si el módulo está vivo o no.
	- System Monitor: componente que monitorea el estado de varios módulos del sistema, idealmente los críticos. El monitor puede detectar una falla y orquestar el inicio de alguna otra táctica que se encargue de recuperar el sistema del estado de falla.
	- Exception Detection.
- Recuperación de fallas
	- Preparación y reparación
		- Redundancia activa: todos los nodos pertenecientes a un grupo deben protegerse, reciben y procesan inputs en paralelo, menteniendo un estado de sincronización constante.
		- Redundancia pasiva: sólo los módulos activos del grupo de protección procesan tráfico de inputs, y uno de ellos se encarga de enviar una actualización de estado a los demas nodos que se encuentran en estado pasivo.
		- Reintento: supone que el fallo en la transacción fue ocasional y el realizar dicha operación nuevamente puede solucionar dicho problema.
		- Spare
		- Exception Handling.
	- Reintroducción
		- Resincronización de estado
		- Rollback
- Prevención de fallas
	- [[Transacciones]]
	- Exception Prevention.

# Performance
Rendimiento del sistema. Dentro de este atributo entran los tiempos de respuesta, throughput, accuracy, availability y uso de recursos.

# Supportability
Dentro de este atributo entran adaptability, maintainability, internationalization y configurability.

## Mantainability
Capacidad del producto de software para ser modificado efectiva y eficientemente, debido a necesidades evolutivas correctivas o perfectivas: 
- **Modularidad**: grado en el que un sistema o programa de computadora se compone de componentes discretos de manera que un cambio en un componente tiene un impacto mínimo en otros componentes.
- **Reusabilidad**: grado en el que un activo se puede utilizar en más de un sistema o en la construcción de otros activos.
- **Analizabilidad**: grado de efectividad y eficiencia con el que es posible evaluar el impacto de un cambio en el sistema.
- **Modificabilidad**: grado en el que un producto o sistema puede modificarse de manera eficaz y eficiente sin introducir defectos o degradar la calidad del producto existente.
- **Testeabilidad**: grado de eficacia y eficiencia con el que se pueden establecer criterios de prueba para un sistema.

# +
El + implica:
- Implementación: lenguajes, software, hardware, etc.
- [[Interfaz]]: interacción con otros sistemas.
- Operaciones: gestión y administración.
- Empaquetamiento o deploy.
- Legales: licencias, etc.