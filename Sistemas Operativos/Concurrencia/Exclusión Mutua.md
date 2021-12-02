### Algoritmo de Dekker (Dijkstra)
- Solución por software
- Preguntar si puedo entrar a través de una variable
- **Problema:** espera activa, la manipulación de la variable turno no es atómica. Pregunta a cada rato, no se bloquea. Necesita ejecutarse para saber si puede o no continuar con su ejecución. Consume procesador. Puede suceder que dos procesos en dos procesadores distintos entren a la sección crítica a la vez.

### Inhabilitación de interrupciones
- El proceso no sería interrumpido
- Solamente es válido para sistemas monoprocesador
- Inhabilita las soluciones, posibles problemas.
- Los hardwares modernos proveen instrucciones que nos posibilitan modificar variables de forma atómica, es decir, de forma ininterrumpida.

### Semáforos
Es una variable entera con tres operaciones atómicas asociadas. Indica la cantidad de recursos libres que se disponen para otorgar al proceso que lo solicite. Cuando el contador del semáforo llega a 0, todos los recursos están siendo utilizados.

- *Init.* Inicializa el semáforo a un valor no negativo.
- *Wait - Solicitar.* Decrementa el contador del semáforo. Si luego de decrementar el semáforo, resulta que s<0,  el proceso se bloquea y se agrega a la lista de espera del semáforo.
- *Signal - Liberar.* Incrementa el valor del semáforo. Luego, si s≤0 desbloquea un proceso y lo saca de la lista.
- *El acceso a la variable semáforo no es atómico.*

- Las primeras implementaciones de semáforos se realizaron con **espera activa**, donde el proceso se queda preguntando hasta que se libera un recurso. Supone un gasto de tiempo de procesador. Es útil cuando se estima que la espera activa sea menor que el tiempo que conlleva un context switch.
- Las implementaciones con **espera pasiva** suponen bloquear los procesos que soliciten recursos cuando no hay disponibles y almacenarlos en una cola de espera para luego despertar alguno cuando se libera un recurso.
  - En las implementaciones que bloquean realmente a los procesos, cuando se bloquea uno de ellos, el scheduler de CPU debe escoger otro proceso para traer al procesador.
  - Cuando no hay recursos disponibles, el proceso se bloquea.
  - Cuando se libera un recurso, se debe desbloquear algún proceso.
  - No debe darse que dos procesos ejecuten wait y signal en el mismo semáforo al mismo tiempo (consistencia del contador del semáforo).

#### *Binarios*
Solo puede tomar valor 0 o 1. También conocidos como mutex locks.
#### *N-ario*
Puede tomar cualquier valor entero positivo.

#### *Posibilidad de Deadlock*
La implementación de un semáforo con una cola de espera puede dar a lugar una situación en la cual dos o más procesos esperan indeterminadamente para ser ejecutados por un evento que puede ser causado únicamente por otro proceso.

Supongamos dos procesos y dos semáfotos S y Q.  P0 ejecuta waitS y luego P1 ejecuta waitQ. Cuando P0 ejecute wait(Q), debe esperar a que P1 ejecute signal(Q) y pasará lo mismo cuando P1 ejecute waitS, debe esperar a que P0 ejecute signalS. [[Deadlock]].

Otro posible problema es la espera indefinida o muerte por inanición.

Suppose that a process interchanges the order in which the wait() and signal() operations on the semaphore mutex are executed, resulting in the following execution:

1. signal(mutex);
1. critical section
1. wait(mutex);

In this situation, several processes may be executing in their critical sections simultaneously, violating the mutual-exclusion requirement. This error may be discovered only if several processes are simultaneously active in their critical sections. Note that this situation may not always be reproducible.

Suppose that a process replaces signal (mutex) with wait (mutex). That is, it executes

1. wait(mutex);
1. critical section
1. wait(mutex);

In this case, a deadlock will occur.

### Monitor
Un monitor es un TDA que consta de uno o más procedimientos, una secuencia de inicio y datos locales. Sus características básicas son:

- Las variables locales sólo están accesibles para los procedimientos del monitor y no para procedimientos externos.
- Un proceso entra en el monitor invocando uno de sus procedimientos.
- Los programadores no deben escribir código de sincronización.
- Solo un proceso puede estar ejecutando en el monitor en un instante determinado. Cualquier otro proceso que haya invocado al monitor quedará suspendido mientras espera a que el monitor esté disponible.
- El monitor ofrece por sí solo exclusión mutua. Cuando se quiere proteger una estructura de datos compartida, puede colocarse la misma dentro de un monitor.
#### *Estrcutura*
- Cola de entrada de procesos.
- Datos locales.
- Variables de condición.
- Colas de condición.
- Procedimientos.
- Cola de urgentes.
- Código de inicio.
#### *Variables de tipo **condicion
Un monitor ofrece sincronización por medio de las variables de condición, a las que se accede a través de funciones:

- *cwait(c).* Suspende la ejecución del proceso que se llama bajo la condición c. El monitor pasa a estar disponible para ser usado por otro proceso. 
- *csignal(c)*. Reanuda la ejecución de un proceso suspendido por la condición c.

### Paso de mensajes
Ofrece a la vez sincronización y comunicación. Tiene la ventaja adicional de que puede ser implementado en sistemas monoprocesador con memoria compartida, sistemas multiprocesador y sistemas distribuidos.

Debe existir un link entre los procesos que se quieren comunicar entre sí. Solo puede existir un link entre un par de procesos.

Primitivas.

- *SEND(destino, mensaje).* Bloqueante (no continúa hasta que el mensaje es recibido) o no bloqueante. La idea es que no sea bloqueante.
- *RECEIVE(origen, mensaje).*  Bloqueante, no bloqueante o con comprobación de llegada. Es lo más natural esperar a recibir algo que se necesita. 
- *Ejemplo envío bloqueante y recepción bloqueante.* Dos procesos que necesitan entre sí para seguir ejecutándose.
- *Ejemplo envío no bloqueante y recepción bloqueante.* Un servidor se encuentra a la espera de recibir un mensaje.
- *Direccionamiento Directo.* En primitiva se incluye el proceso destino.
- *Direccionamiento indirecto.* En la primitiva se incluye un buzón o puerto destino. Permite un buzón compartido entre varios procesos.
  - *Se debe decidir si todos los procesos serán capaces de recibir el mensaje o solo lo recibirá el primero que lo atienda.*

Debe existir un buffer donde almacenar mensajes que aún no fueron recibidos por el proceso destino.

- *Cola de capacidad cero.* No puede haber mensajes esperando en ella. El emisor debe bloquearse hasta que se recibe el mensaje.
- *Capacidad limitada.* Pueden existir a lo sumo n mensajes en espera. Si la cola está llena, el emisor debe esperar hasta que haya un lugar para su mensaje.
- *Capacidad ilimitada.* El emisor nunca se bloquea.
