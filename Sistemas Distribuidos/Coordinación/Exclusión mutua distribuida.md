Los algoritmos de exculsión mutua [[Sistemas Distribuidos|distribuidos]] pueden clasificarse en dos categorías distintas. Con las **token-based solutions** la [[Mutual exclusion|exclusión mutua]] se logra pasando un token entre [[Proceso|procesos]]. Solo hay un token disponible y quien lo tenga tiene permitido el acceso al recurso compartido. Cuando finaliza, el token es pasado al siguiente proceso. La principal desventaja de estas soluciones es como actuar cuando se pierde un token (por ejemplo, si el proceso poseedor crashea).

Una alternativa es un **permission-based approach**. En este caso, un proceso que requiere acceso a un recurso primero solicita permiso a otros procesos. Hay muchas maneras de llevara cabo esta alternativa, algunas son las siguientes.

### Algorítmo centralizado
Una forma de lograr la exclusión mutua en sistemas distribuidos es simular lo que ocurre en un sistema mono-procesador. Se elige un proceso como coordinador y cuando un proceso requiere acceso al recurso compartido envía una solicitud. El coordinador luego se encarga de gestionar los permisos. La principal ventaja de este aproach es su simpleza.

El diseño centralizado tiene algunas desventajas. El coordinador es un punto único de falla con todo lo que esto implica. En un sistema grande el tener un único coordinador puede tornarse en un cuello de botella. Para seleccionar al coordinador existen [[algoritmos de elección]].

#### Solución basada en token
En esta solución el coordinador tiene un [[Token|token]] para cada recurso, cuando un proceso solicita hacer uso del recurso se le entrega el token y cuando lo libera debe retornar el token al coordinador. Así se asegura la exclusión mutua en el uso del recurso.

### Algorítmo distribuido
Para esta solución se requiere un ordenamiento total de los eventos del sistema (utiliza los [[Relojes  Lógicos#Relojes lógicos de Lamport|relojes lógicos de Lamport]]). El algorítmo es el siguiente. Cuando un proceso quiere acceder a un recurso compartido, construye un mensaje conteniendo el nombre del recurso, su pid y el tiempo (lógico) actual. Envía este mensaje a todos los otros procesos (conceptualmente incluyendose a si mismo). El envío de mensajes se supone fiable (no se pierde ningún mensaje).

Cuando un proceso recibe un mensaje de solicitud de otro proceso, la acción que toma depende de su estado respecto al recurso. Hay tres casos distinguibles:
* Si el receptor no está accediendo al recurso y no quiere acceder al recurso, envía un OK al solicitante.
* Si el receptor tiene acceso al recurso, simplemente no respone. Sino que almacena la solicitud en una cola.
* Si el receptor quiere acceso al recurso también pero no lo tiene todavía, compara el timestamp del mensaje recibido con el contenido en el mensaje que envío al resto. El más bajo gano. Si el mensaje recibido tiene un timestamp menor simplemente envía un OK. Si el mensaje propio tiene un timestamp menor, el receptor no responde y almacena el pedido en una cola.

Luego de enviar las solicitudes de acceso el proceso espera que todos respondan. Tan pronto como todos los OK son recibidos puede acceder al recurso. Cuando termina envia mensajes de OK a todos los procesos en su cola y los elimina de la cola.

El principal inconveniente con este algorítmo es que tiene N puntos de falla, ya que el silencio de cualquier proceso será interpretado (incorrectamente) como negación de permiso, por lo tanto bloqueando todos los intentos siguientes de acceder a algún recurso compartido. Se puede patchear de la siguiente manera, cuando se recibe una solicitud el receptor siempre envía una respuesta, sea concediendo o denegando el permiso. Cuando se pierde o la solicitud o la respuesta el solicitante reintenta hasta recibir una respuesta o hasta que se concluye que el receptor está muerto. Luego de que el permiso es denegado el solicitante debe bloquearse esperando el envio del OK.