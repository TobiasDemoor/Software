Siempre que hay un recurso no compartible y un conjunto de procesos que compiten por él, el SO debe decidir qué [[proceso]] asignarlo. Recurre, entonces, a un planificador.

Solo se encargan de PLANIFICAR, pero no es el que materializa dicha planificación. Es decir, es el autor INTELECTUAL del uso de los recursos.

Los schedullers son módulos del SO que planifican el uso de un recurso, decidiendo a qué proceso se le asignará el recurso en base a un criterio determinado (algoritmo de schedulling). A su vez, interactúan con otro modulo responsable de la ejecución material de sus decisiones.

## Procesos y recursos
- Los procesos solicitan recursos al sistema y los liberan voluntariamente cuando ya lo utilizaron. 
  - El Proceso solicita un recurso (System Call).
  - El SO verifica la disponibilidad del recurso.
  - Si no está disponible, el proceso espera por el recurso (en la cola del recurso) hasta su disponibilidad.
  - Si está disponible, el SO lo asigna al proceso.
  - Cuando el proceso termina de usarlo, lo libera voluntariamente (System Call). LOS PROCESOS LIBERAN LOS RECURSOS.
- Los recursos pueden estar **disponibles** (sin estar utilizados) o bien **asignados** (siendo utilizados por un proceso que lo tiene asignado).
- Hay recursos **Compartibles** (pueden ser asignados a más de un proceso a la vez) y **NO Compartibles** (de uso exclusivo por parte de un proceso).
- En un Sistema de Computación puede haber varias **instancias o ejemplares** de un mismo tipo de recurso (ej. varias impresoras).
- Cuando un proceso solicita un recurso, lo hace en forma genérica (“necesito una impresora”) y el SO le asigna *cualquiera* de las instancias del mismo que esté disponible.
- Si un proceso solicita un recurso que no tiene instancias disponibles, queda bloqueado, esperando hasta que se le asigne una.
- El sistema operativo debe saber en qué estado (asignado o disponible) se encuentra un recurso, por lo que mantiene Tabla donde se registra si cada recurso está libre o asignado, y si está asignado, a qué proceso se le asignó.
- Existen **recursos reusables** (dispositivos de I/O, procesador, memoria principal y secundaria, etc.) cuyo uso no deteriora el recurso en sí, y existen otros que son **consumibles,** los cuales son creados y destruidos (interrupciones, señales, mensajes, información en los buffers de I/O. 
  - Por lo tanto, puede existir [[deadlock]] sin necesidad de implicar recursos de I/O. Por ejemplo, dos procesos se comunican y esperan recibir un mensaje del otro. Si un proceso envía un mensaje al otro, se queda en espera. El otro proceso envía el mensaje de respuesta y queda a la espera de otro mensaje. Si el mensaje de éste último se pierde, ambos procesos se quedan esperando una respuesta por parte del otro proceso.

### Scheduler de Memoria
El que materializa la planificación de este scheduler es Loader de memoria. Planifica principalmente la creación de procesos y la asignación de espacios de memoria y almacenamientos de datos. Es conocido también como Scheduler de Largo Plazo, dado que la frecuencia de creación de procesos es baja.

*Loader.* Es el módulo del SO que carga y descarga procesos de memoria. Sus funciones son las de leer los contenidos de un archivo ejecutable conteniendo las instrucciones del programa en memoria, para acto seguido dejar preparado el proceso para su ejecución.

### Scheduler de Procesador
Decide a qué proceso de los que se encuentra en la cola de “listos” le otorgará el procesador, y es el Dispatcher el que materialmente realiza dicha acción. Es también conocido como Scheduler de Corto Plazo, dado que los procesos son altamente interactivos. Es por esto que este scheduler influye directamente en la eficiencia del [[uso del procesador]].

*Dispatcher.* Es el módulo que ejecuta el context switch. Cada vez que se intercambia un proceso, primero se guardan los valores actuales del contexto de operación en el PCB. Luego, se carga el siguiente proceso tras establecer los valores del contexto con los del PCB del nuevo proceso.

### Scheduler de Dispositivo E/S
Similar al scheduler del procesador, pero con dispositivos físicos y el Driver (enviándole los comandos al controlador del dispositivo) es quien materialmente ejecuta las decisiones del scheduler del dispositivo de E/S. 

### Scheduler de mediano plazo
Algunos sistemas operativos implementan un scheduler intermedio, principalmente cuando se cree que en algunos casos es conveniente disminuir el grado de multiprogramación sacando procesos de la memoria principal. Se encarga de las funciones de swap de los programas dentro de la memoria principal, determinando cuándo están cargados completamente y cuándo parcialmente.

### Uso de prioridades
Consta de asignarle una prioridad a cada proceso, a partir de la cual el scheduler siempre elegirá un proceso de mayor prioridad antes que uno de menor prioridad para ser ejecutado. Para ello, se utilizan colas de prioridades, donde cada nivel de prioridad tendrá una cola de procesos para ser ejecutados, y el scheduler irá recorriendo cada una de ellas en orden descendente de prioridad a la hora de hacer una selección de un proceso. Un problema de un scheduling de prioridades puro es que los procesos de baja prioridad pueden no ser ejecutados por un largo período de tiempo si sucede que siempre hay un proceso de mayor prioridad. Esto puede producir que un proceso de larga duración sufra de inanición, lo cual puede solucionarse ascendiendo a un proceso a un nivel de prioridad más alto luego de un determinado tiempo de espera.

### Función de selección
Determina cuál proceso entre los que están en la cola de listos debe ser seleccionado para ser ejecutado. La función puede estar basada en prioridades, requerimientos de recursos, entre otros.

El **modo de decisión** especifica los instantes en el tiempo en los cuales la función de selección es utilizada.

- *No desalojo.* Una vez que el proceso está en ejecución, éste continuará hasta terminar o hasta que pase al estado bloqueado.
- *Desalojo.* El proceso en ejecución puede ser interrumpido y llevado a la cola de listos por el sistema operativo. Esto puede suceder basado en una interrupción de reloj o bien cuando un nuevo proceso arriba.

#### *First-Come-First-Served*
Cuando el proceso que se encuentra en ejecución deja de ser ejecutado, se elige el que más tiempo lleva esperando en la cola de listos para ser ejecutado en nueva instancia. Cuando llegan procesos cortos luego de otros que requieren de un tiempo de servicio más prolongado, el tiempo de turn around será extremadamente mayor al tiempo de servicio del proceso.

#### *Round Robin*
Limita el tiempo de ejecución de cada proceso a un determinado número de unidades de tiempo (quantum). Cuando ocurre la interrupción de reloj, el proceso que se encuentra en ejecución es llevado a la cola de listos, y se selecciona el siguiente proceso que se encuentra en espera mediante FCFS para ser ejecutado. 

El principal problema de esta técnica es la longitud del tiempo quantum a utilizar. Si el quantum es muy corto, entonces los procesos cortos serán interrumpidos rápidamente. Por esto, suele utilizarse un tiempo de quantum un poco más grande que el tiempo requerido para una interacción típica como un swap context o una función de un proceso, dado que, si el quantum fuese menor, la mayoría de los procesos requerirían al menos dos quantums. Por otro lado, si el quantum es extremadamente largo, Round Robin se comportará como un First-Come-First-Served.

Esta técnica es particularmente efectiva en un sistema de tiempo compartido o en un sistema de procesamiento de transacciones. Por otro lado, el uso de RR resulta en una ineficiencia en las operaciones de E/S. Por ejemplo, si un proceso es interrumpido por una operación de E/S antes de que se termine su tiempo de quantum, éste será llevado luego de ser atendida su solicitud de E/S al final de la cola de listos, teniendo que esperar que se ejecuten los quantums de todos los procesos que se encontraban después de él en un principio, resultando así en un tiempo de respuesta muy elevado. 

En algunos casos se utiliza un virtual RR que posee una cola auxiliar, en la cual son alojados los procesos que fueron bloqueados por una operación de E/S y finalizaron la misma, de modo que el scheduler luego los carga en el procesador y los deja continuar su ejecución con el tiempo restante que les quedaba del quantum cuando fueron bloqueados.

#### **Shortest Process Next – Shortest Job Next** (SJF)
Mediante esta técnica, se elige el proceso que menor tiempo esperado de servicio posea dentro de la cola de listos. Uno de los inconvenientes con esta técnica es que el programador debe poder estimar de antemano el tiempo de servicio que requerirá un proceso, cosa que no es fácil en la mayoría de los casos.

#### **Shortest Remaining Time** (SRJF)
Es una versión con modo de decisión preventiva de SPN. En este caso, el scheduler elegirá siempre el proceso que posea el menor tiempo procesamiento restante esperado. Cuando llega un nuevo proceso a la cola de listos, puede que tenga un tiempo remanente menor al del proceso que se encuentra en ejecución, por lo que el scheduler puede pasar a ejecutar otro proceso cuando un nuevo proceso pasa al estado de listo. Al igual que en SPN, el scheduler tiene que poseer una estimación del tiempo necesario de servicio para cada proceso.

Existen dos variantes: una con desalojo y otra sin el mismo, es decir, se espera hasta que el proceso actual finalice.

#### *Highest Response Ratio Next*
Cuando el proceso actual termine o sea bloqueado, el scheduler elegirá el proceso que posea la mayor tasa de respuesta, que se calcula como:

R=w+ss

Donde 

R = response ratio 

w = tiempo transcurrido esperando al procesador

s = tiempo esperado de servicio

#### *Prioridades*
Se selecciona el proceso con mayor prioridad. En caso de empate, el criterio de selección entre los procesos es igual al de FCFS. Puede suceder que los procesos de baja prioridad no sean ejecutados hasta mucho tiempo después del arribo.

Dos variantes: con desalojo o sin desalojo.

#### *Feedback*
Si no se posee información acerca de la longitud relativa de varios procesos, entonces no podemos utilizar ninguna de las técnicas anteriores (exceptuando RR). Otra forma de manejar estas situaciones, es penalizando a los procesos a partir de un cierto límite de tiempo de procesamiento.

Esta técnica utiliza un sistema basado en prioridades. Cuando un proceso entra por primera vez en el sistema, se sitúa en la cola de mayor prioridad. Una vez que está en ejecución y es interrumpido por primera vez, cuando vuelve al estado de listo, es situado en una cola de prioridad inferior. De esta manera, los procesos cortos finalizarán su ejecución de manera rápida, sin descender demasiado por la cadena de prioridades.

Cuando un proceso no puede descender más por la jerarquía de colas de prioridad, es devuelto a la cola que se encontraba hasta finalizar su ejecución.

#### *Fair-Share Scheduling*
Todos los algoritmos de planificación anteriormente explicados tratan la colección de procesos en estado listos como una sola “pileta” de procesos de donde se debe elegir el siguiente para ser ejecutado. Esta pileta puede ser reorganizada mediante un criterio de prioridades, pero siempre será homogénea.

El Fair-Share Scheduling consta de, en sistemas multiusuarios, dividir el uso del procesador en partes iguales en una determinada cantidad de usuarios o de grupos de usuarios, de modo que, si un usuario X requiere una cantidad extremadamente mayor de tiempo de procesador que un usuario Y, este hecho solo afecte usuario X, mientras que el usuario Y no es perjudicado.

### Efecto convoy
Se le denomina efecto convoy cuando el CPU se encuentra ejecutando un proceso que consumirá mucho más tiempo que los procesos que se encuentran en espera.

### Unix scheduling
El scheduler tradicional de [[UNIX]] emplea un feedback de multinivel utilizando round robin dentro de cada una de las colas de prioridad. Utiliza un desalojo adelantado de un segundo, es decir, si un proceso en ejecución no finaliza o no es bloqueado en un segundo, es desalojado del procesador. 

La prioridad que utiliza [[UNIX]] está basada en el tipo de proceso y la historia de ejecución del mismo. Esta prioridad es recalculada cada un segundo.

En orden de prioridad decreciente, los tipos de procesos son:

- *Swapper.*
- *Bloqueo del controlador de dispositivo de E/S.*
- *Manipulación de archivos.*
- *Dispositivo de control de E/S de caracteres.*
- *Procesos de usuario.*

Esta jerarquía debería proveer el uso más eficiente de los dispositivos de E/S. Dentro de la banda de los procesos de usuario, la historia de ejecución de los procesos tiende a penalizar a los procesos vinculados al procesador a expensas de los procesos vinculados con E/S.

Esta estrategia está orientada a sistemas de entornos interactivos de tiempo compartido.