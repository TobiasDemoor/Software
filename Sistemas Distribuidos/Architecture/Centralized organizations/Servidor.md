### Servidor multihilo
El servidor usualmente se espera por una solicitud, la lleva a cabo y envía la respuesta. Una organización particularmente popular es en la cual se tiene un [[Thread|hilo]] llamado **dispatcher**, el cual lee requests entrantes y luego de examinarlas elige un **worker thread** que se encuentre suspendido y le entrega la request.

Una alternativa a esto sería correr un servidor como una gran máquina de estados de un solo hilo. Cuando se recibe una request, el hilo la examina. Si puede ser resuelta con el cache en memoria, se hace, si no, el hilo debe acceder a disco. Pero en vez de ejecutar una instrucción bloqueante, el hilo programa una operación de disco asincrónica la cual lo interrumpirá cuando esté completa (por medio del [[Sistemas Operativos|sistema operativo]]). Para lograr esto, el hilo debe almacenar el estado de la request y continuar a ver si hay otras requests entrantes.

Una vez que se complete la operación el SO notifica al hilo, el cual entonces buscará el estado de la request y continuará procesandola. Eventualmente se enviará una respuesta al cliente solicitante por medio de una llamada no bloqueante.

![[servidor_1.png]]