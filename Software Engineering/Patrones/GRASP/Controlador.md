## Problema
¿Quén debe ser el responsable de gestionar un evnto de entrada del sistema ([[Operación de sistema|operación de sistema]])?

## Solución
Asignar la [[Responsabilidad|responsabilidad]] de manejar un mensaje de evento de entrada del sistema a una clase controladora que representa una parte del sistema.

El controlador es un objeto que no pertenece a la interfaz de usuario, y es responsable de recibir o manejar un evento del sistema, es decir, define un método para las [[Operación de sistema|operación de sistema]]. Es la vista quien llama al controlados, el controlador solo debe tener la [[Responsabilidad|responsabilidad]] de delegar acciones del sistema, no debe tener muchas responsabilidades adicionales.
Se puede utilizar un controlador para cada caso de uso del sistema, e modo que éste almacene información del estado del [[Use Case|caso de uso]] correspondiente. Es conveniente utilizar un controlador por caso de uso en el escenario donde si se implementara un solo controlador para todos los eventos, éste resulte con una baja [[Cohesión|cohesividad]].