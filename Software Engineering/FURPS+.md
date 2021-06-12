En términos generales, los requisitos son capacidades y condiciones con los cuales debe ser conforme el sistema y más ampliamente el proyecto. Para cada tipo se tienen [[Patrones|patrones]] especificos y probados.

# Functional
Por supueso que se debe considerar como un elemento curcial de la calidad del software el cumplimiento de los [[Requerimientos#Requerimientos funcionales|requerimientos funcionales]]. Dentro de este atributo entran las features, capabilities y la seguridad.

# Usability
Capacidad del producto de software para ser entendido, aprendido, usado y resultr atractivo, cuando se usa bajo determinadas condiciones. Aspectos:
- Capacidad para reconocer su adecuación.
- Capacidad de aprendizaje.
- Capacidad para ser usado.
- Protección contra errores de usuario.
- Estética de la interfaz de usuario.
- Accesibilidad.
Dentro de este atributo entran los factores humanos, la ayuda a los usuarios y la documentación.

# Reliability
Capacidad de un sistema o componente para desempeñar las funciones específicas, cuando se usa bajo condiciones y períodos de tiempo determinados. El mínimo del que podemos hablar es 99%.
- Madurez: capacidad del sistema para satisfacer las necesidades de fiabilidad en condiciones normales.
- Disponibilidad: capacidad del sistema o componente de estar operativo y accesible para su uso cuando se requiere.
- Tolerancia a fallos: capacidad para operar según lo previsto en presencia de [[Fault, Failure|fallas]] de hardware y/o software.
- Capacidad de recuperación: capacidad para recuperar datos afectados y el estado del sistema ante [[Fault, Failure|fallos]] o interrupciones.
Dentro de este atributo entran la fecuencia de [[Fault, Failure|fallas]], la recoverability y la predictability.

## Tácticas
- Excepciones y manejo de errores (Exception Detection, Exception Handling, Exception Prevention).
- Patrones de redundancia:
	- Recuperación de fallas
		- Preparación y reparación
			- Redundancia activa
			- Redundancia pasiva
			- Spare
		- Reintroducción
			- Resincronización de estado
			- Rollback
	- Prevención de fallas
		- [[Transacciones]]

# Performance
Rendimiento del sistema. Dentro de este atributo entran los tiempos de respuesta, throughput, accuracy, availability y uso de recursos.

# Supportability
Dentro de este atributo entran adaptability, maintainability, internationalization y configurability.

## Mantainability
Capacidad del producto de software para ser modificado efectiva y eficientemente, debido a necesidades evolutivas correctivas o perfectivas: 
- Modularidad.
- Reusabilidad.
- Analizabilidad.
- Capacidad para ser modificado.
- Capacidad para ser probado.

# +
El + implica:
- Implementación: lenguajes, software, hardware, etc.
- Interfaz: interacción con otros sistemas.
- Operaciones: gestión y administración.
- Empaquetamiento o deploy.
- Legales: licencias, etc.