Es una unidad de procesamiento de un nivel de granularidad menor que un [[Sistemas Operativos/Conceptos/Proceso|proceso]]. Un proceso se descompone en hilos de procesamientos. Un hilo es una unidad de trabajo que se puede expedir para su ejecución, y es ejecutada secuencialmente y de forma ininterrumpible. Un proceso multihilo es una secuencia de hilos que se ejecutan de manera concurrente.

#### Librería en la capa de usuario
Es menos costoso crear y destruir hilos, dado que consta únicamente de asignar espacio en memoria para configurar la pila de hilos.

Cambiar del contexto de un hilo al otro también es poco costoso. Se deben modificar únicamente los valores de los registros del CPU que hagan referencia a los datos del hilo. No hace falta limpiar el TLB ni nada por el estilo

Todos los hilos son mapeados a una sola entidad planificable (el proceso). Cada vez que se invoque una llamada al sistema bloqueante, el SO bloqueará el proceso entero, y por ende todos los hilos.

#### Proceso con un solo hijo
- Sin paralelismo de operaciones, llamadas al sistema bloqueantes.
- Un proceso no bloquea a los demás que colaboran con él.
- El kernel puede planificar cada hilo.
- Context switch costoso, dado que requiere cambiar del contexto de un proceso entero a otro.
- Cada proceso tiene su propio espacio de datos protegido por el SO.

#### Máquina de estado finito
- Paralelismo, llamadas al sistema no bloqueantes, interrupciones.
- Cuando llega una petición a un servidor de máquina de estado finito, el **hilo principal (y único)** examina la petición.
	- Si puede ser resuelta con alguna entrada en la cache, perfecto.
	- Si no, debe acceder al disco. Para no bloquear el proceso, el hilo inicia una operación de disco asíncrona y no bloqueante. Cuando esta operación finaliza, el sistema operativo notifica al hilo, y éste verifica el estado y continúa procesando la solicitud.
	- El envío de respuestas al cliente también es llevado a cabo mediante operaciones asíncronas.
	- El hilo debe almacenar los datos necesarios de la petición que le permitan retomar el procesamiento de la misma luego de la operación asíncrona.
- Gran performance y paralelismo de operaciones.
- Es difícil desarrollar y mantener las operaciones no bloqueantes

#### Múltiples hilos por proceso
Similar a la implementación en capa de usuario salvo que un hilo se puede bloquear sin bloquear todo el proceso y la asignación de hilos al procesador la lleva a cabo el SO.