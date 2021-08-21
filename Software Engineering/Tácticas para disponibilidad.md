### Detección de fallas
- Ping/echo: se utiliza tanto para conocer los tiempos de respuesta como para saber si el módulo está vivo o no.
- System Monitor: [[Component|componente]] que monitorea el estado de varios módulos del sistema, idealmente los críticos. El monitor puede detectar una falla y orquestar el inicio de alguna otra táctica que se encargue de recuperar el sistema del estado de falla.
- Exception Detection.
### Recuperación de fallas
- Preparación y reparación
	- Redundancia activa: todos los nodos pertenecientes a un grupo deben protegerse, reciben y procesan inputs en paralelo, menteniendo un estado de sincronización constante.
	- Redundancia pasiva: sólo los módulos activos del grupo de protección procesan tráfico de inputs, y uno de ellos se encarga de enviar una actualización de estado a los demas nodos que se encuentran en estado pasivo.
	- Reintento: supone que el fallo en la transacción fue ocasional y el realizar dicha operación nuevamente puede solucionar dicho problema.
	- Spare
	- Exception Handling.
- Reintroducción
	- Resincronización de estado
	- Rollback
### Prevención de fallas
- [[Transacciones]]
- Exception Prevention.