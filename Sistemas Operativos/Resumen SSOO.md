# Sistema de computación (SC)
![[Sistemas de Computación]]

# Sistema Operativo (SO)
![[Sistemas Operativos]]

## Interrupciones
Es el mecanismo mediante el cual el SO se entera que ha ocurrido un evento que es de su interés y que debe ser atendido.

Es la interrupción de un proceso debida a un factor externo al mismo y que se lleva a cabo de tal modo que el procesador pueda atender la demanda y reanudar luego la ejecución de dicho proceso.

### Interrupciones de hardware
#### *Sincrónicas*
Se producen con una determinada frecuencia. Por ejemplo, el reloj interrumpe a cada segundo para que el SO lo plasme en la pantalla.
#### *Asincrónicas*
Provocadas por dispositivos o fallas de hardware.

### Interrupciones de software
#### *Explícitas*
Llamadas al sistema. Un proceso solicita la utilización del hardware.
#### *Implícitas*
Desbordamiento aritmético, división por cero, intento de ejecutar una instrucción ilegal, referencia a una zona de memoria fuera del espacio de direcciones permitido al usuario.

### Tratamiento de la interrupción
Cuando el SO identifica una interrupción pendiente, se detiene la ejecución del proceso de usuario y se transfiere el control al SO.

El SO identifica la interrupción por un número que usa como subíndice en el vector de interrupciones para obtener la dirección del código de la interrupción y lo ejecuta.

El SO devuelve el control al proceso de usuario que reanuda su ejecución.

1. Un proceso o dispositivo causa una interrupción.
1. El procesador verifica si hay un pedido de interrupción pendiente y atiende la que corresponda.
1. Se almacenan los datos necesarios para continuar posteriormente la ejecución del proceso (registros de datos del procesador, PC, PSW, etc.).
1. El procesador carga el PC con la ubicación de entrada de la rutina de tratamiento de la interrupción correspondiente y comienza su ejecución. 
1. Cuando el proceso de interrupción se completa, se restauran los datos necesarios para retomar la ejecución del proceso que causó la ejecución y se continúa con la misma.
### Interrupciones múltiples
#### *Secuenciales*
Termina la ejecución de la rutina de atención una interrupción para luego atender la siguiente.
#### *Anidadas*
Interrumpe (dada las prioridades) una rutina de atención de una interrupción para atender la nueva interrupción.
### Prioridad de las interrupciones
Las interrupciones de prioridad más alta pueden hacer que las de prioridad más bajas tengan que esperar (No desalojo).

Hace que se interrumpa la rutina de tratamiento de prioridad más baja (desalojo – Tiempo Real)

Por ejemplo, cuando llega una interrupción desde la línea de comunicaciones, se necesita atender ésta rápidamente para hacer lugar a nuevas entradas.

## Modo dual de protección
Es un mecanismo de protección de los recursos del SC que implementa el sistema operativo (información, procesador, memoria y dispositivos de E/S) y debe tener soporte de hardware (bit de modo en el procesador).

- El *modo Kernel* es el estado del sistema operativo en el cual tiene acceso completo a todo el hardware y puede ejecutar cualquier instrucción. Aquí se van a incluir los servicios de uso más frecuentes.
- El *modo usuario* es el estado del sistema operativo en el cual solo un subconjunto de instrucciones es permitido, aquellas que no requieren acceso al hardware. Se recurre a llamadas al sistema para E/S.

### Instrucciones privilegiadas
Comprenden las llamadas al sistema. Son aquellas que requieren la manipulación del hardware.

### Instrucciones no privilegiadas
No requieren la manipulación del hardware, pueden ser ejecutadas por el proceso. Comprenden las instrucciones lógicas tales como “a+b”.

El sistema operativo debe resolver las instrucciones privilegiadas, mientras que debe solicitar a un tercero que resuelva las no privilegiadas.

Para que el procesador conozca el tipo de instrucción que se está ejecutando, existe el *Bit de Modo* para indicar que el proceso cargado en memoria es un proceso del sistema operativo (1), que por sí solo podrá resolver la instrucción, o bien es un proceso del usuario que requerirá una llamada al sistema para resolver ciertas instrucciones (0).


# **Procesos**
El procesador es el recurso más utilizado demandado, dado que permite la ejecución de los procesos.

## **Objetivo de gestión de SO**
1. Intercalar la ejecución de múltiples procesos para maximizar la utilización del procesador ofreciendo un tiempo de respuesta razonable pero siempre maximizando el uso del procesador, de modo de aprovechar de la mejor manera los tiempos muertos.
1. Asignar los recursos a los procesos de forma tal que dichos recursos son asignados, utilizados y liberados lo más rápido posible. 
1. Dar soporte a la comunicación entre procesos y la creación de procesos por parte del usuario.
1. Mejorar permanentemente los indicadores de desempeño.

## **Indicadores básicos de desempeño**
1. *% de uso efectivo del procesador.* Solamente se toma como tiempo efectivo el tiempo que el procesador estuvo atendiendo procesos DE USUARIO y no procesos del sistema operativo o de burocracia (operaciones de memoria, creación de procesos, etc.). Es un indicador del sistema de computación en general.

1. *Productividad.* Es un número que indica la cantidad de procesos terminados por unidad de tiempo. Es un indicador del sistema de computación en general.

1. *Tiempo de Turn around.* Tiempo completo de existencia del proceso sin preocuparnos por los estados que pasa el mismo durante su ciclo de vida. Es el tiempo desde que el proceso nace hasta que muere. Cada proceso tendrá su propio tiempo de Turn around. Es ideal analizar la media y la desviación estándar de este parámetro.

1. *Tiempo de espera.*  Tiempo que los procesos permanecen en las distintas colas ya sea para ser ejecutados o a la espera de un recurso. No se incluye el tiempo de E/S. 

1. *Tiempo de respuesta.* Mide el tiempo desde que el proceso es creado hasta que el usuario recibe algún síntoma de que el sistema lo está atendiendo, como, por ejemplo, una E/S.

# **Proceso**
Es un PROGRAMA EN EJECUCIÓN. Es la unidad de procesamiento del SO (la del usuario es la Tarea).

La taza o flujo de ejecución del proceso es la secuencia de instrucciones que se ejecutan para dicho proceso. No necesariamente se ejecutan de manera consecutiva, pueden existir bucles, ramas condicionales, etc., por lo que **no es posible saber a priori observando el código del programa cuál va a ser el flujo de ejecución del proceso**, dado que puede variar en tiempo de ejecución dependiendo de la información que dicha ejecución posea. Solo se puede saber cuando el proceso finaliza. NO HAY DOS PROCESOS IGUALES.

- Los procesos se identifican con un Process Id. (PId.)
- Un proceso ejecuta un código.
- El sistema operativo almacena información de la ejecución en la pila. Es una estructura de datos administrativa del SO que refiere al proceso y que le sirve para mantener toda la información de ejecución de ese proceso. 
- Procesa datos externos, los cuales deben ser almacenados en memoria.
- Proceso = Pid + Código + Pila + Datos + Atributos (indicadores de gestión).

### Atributos
- Process Id. 
- TimeStamp de inicio (fecha y hora)
- Usuario que está ejecutando el proceso
- PC para saber la instrucción que se está ejecutando
- Punteros a las diferentes secciones de memoria.
- Prioridad relativa a otros procesos.
- Datos de contexto. (registros del procesador, entre otros)
- Estado de E/S, tal como dispositivos asociados al proceso, una lista de archivos usados por el proceso, etc.
- Información de uso de procesador.

### Creación de procesos 
- Lo crea el SO a solicitud de un usuario.
- Lo crea el SO en un sistema Batch, donde los procesos se van creando secuencialmente sin intervención del usuario.
- Lo crea otro proceso.
- Se crea para ofrecer un servicio, como, por ejemplo, la impresión.
- Procesos “hijos” (un proceso crea otro proceso y le cede el control) y “hermanos” (un proceso crea otro proceso a la par de si mismo y ejecutan concurrentemente, como el editor de Word con el corrector). El usuario siempre ve los conjuntos de procesos como uno solo y los llama tarea.

#### *La creación de un proceso requiere*
1. Darle un Pid.
1. Crearle una entrada en la tabla de procesos.
1. Asignarle memoria al código (proceso de carga en memoria).
1. Crear su pila en memoria.
1. Cargar sus datos (crear su bloque de control de proceso).
1. Setear sus atributos.
1. Dejarlo “Listo” para ejecutar.

#### *Process spawning*
Fenómeno que sucede cuando el SO crea un proceso a petición explícita de otro proceso.

### Finalización de procesos
#### *Un proceso puede terminar*
1. De manera normal (instrucción END)
1. Anormalmente.
   1. *Tiempo límite excedido* (e/s o lo que sea)
   1. *No hay memoria disponible*. Por ejemplo, stack overflow o el proceso solicita más memoria de la que el sistema puede proveerle.
   1. *Violación de límites*. Por ejemplo, al intentar acceder a un área de memoria que no le corresponde.
   1. *Error de protección*. Por ejemplo, al intentar acceder a un recurso que no le corresponde o intentar escribir en un archivo de solo lectura.
   1. *Error aritmético*. Por ejemplo, una división por cero.
   1. *Tiempo máximo de espera superado*. En una cola de espera, por ejemplo.
   1. *Fallo de E/S*. Por ejemplo, tratar de leer una sección ilegal o dañada del disco.
   1. *Instrucción ilegal.*
   1. *Intervención del operador o del SO* (Deadlock).
   1. *Terminación del padre.*
   1. *Solicitud del padre.*

#### *La finalización de un proceso requiere*
1. Liberar todos los recursos asignados a él.
1. Liberar la memoria ocupada por el proceso.
1. Eliminar su entrada en la tabla de procesos (última acción).

### Estados de un proceso
Los estados de un proceso se refieren a la situación del proceso dentro del sistema de computación

- *Nuevo.* El proceso está siendo creado y tiene una entrada en la tabla, pero no tiene memoria asignada.
- *Listo.* El proceso está en condiciones de ocupar el procesador, pero se encuentra a la espera de la asignación del mismo. Son todos los que compiten por el procesador.
- *En ejecución.* El proceso está montado en el procesador avanzando en su flujo de operaciones.
- *Terminado.* El proceso se encuentra liberando sus recursos (etapa de finalización).
- *Bloqueado.* El proceso solicita una e/s y es bloqueado para que no ocupe tiempo muerto en el procesador. Para mejorar la eficiencia a la hora de reanudar un proceso que previamente ha sido bloqueado, existe una cola de procesos bloqueados por cada evento. De esta manera, el SO no debe recorrer toda la cola de procesos bloqueados preguntando a ver cuál de todos completó la operación por la cual fue bloqueado, sino que cuando el evento ocurre, la totalidad de la cola de procesos bloqueados referidos a ese evento pueden ser transferidos a la cola de procesos listos para ejecutar.

Si el despacho de procesos está dictado bajo un esquema de prioridades, sería conveniente tener una cola de procesos Listos para cada nivel de prioridad definido.




# **Process swaping: Procesos en suspensión**
El procesador trabaja a una velocidad extremadamente mayor que los dispositivos de E/S, por lo que no sería descabellado tener una situación en la cual el procesador se encuentre inactivo dado que todos los procesos que se encuentran en memoria estén a la espera de una operación de E/S. No es una solución viable expandir la memoria principal para manejar más procesos, dado que, en ese caso, los procesos solicitarían más memoria dado que hay mayor cantidad disponible. La solución es mover parte de todos los procesos desde la memoria principal a la memoria secundaria. Cuando ninguno de los procesos que se encuentran en memoria principal están en el estado Listo, el SO mueve uno de los procesos bloqueados a una cola de procesos suspendidos en la memoria secundaria. Luego, el SO trae a memoria un proceso de dicha cola de suspensión o uno nuevo que se encuentre listo para ejecutar. Como el swap es una operación de E/S de disco, puede empeorar el problema.
# **Estructuras de control del SO**
- Información sobre el estado actual de cada proceso y de cada recurso.
- El sistema operativo construye tablas de información sobre cada entidad que esté administrando. 
- PCBS (bloque de control de procesos) y Tabla de Procesos.

### Ubicación de los procesos
- *Un proceso incluye un programa o un conjunto de programas a ejecutar.*
  - Conjunto de ubicaciones de datos para las variables locales y globales.
  - Constantes definidas.
  - Pila

- *Bloque de control del proceso.*
  - Colección de atributos.

- *Imagen del proceso.*
  - Colección de programa, datos, pila y atributos.

### Tablas de procesos
¿Dónde está el proceso?

- *Atributos del proceso necesarios para su administración*
  - ID del proceso.
  - Estado del proceso.
  - Ubicación en la memoria. Dirección del código del programa.
  - Puntero al bloque de control.



### Tablas de memoria
- Guarda la asignación de memoria principal y secundaria a los procesos.
- Atributos de protección de bloques de memoria principal o virtual, como qué procesos pueden acceder a ciertas regiones compartidas de memoria.
- Cualquier información necesaria para gestionar la memoria virtual.

### Tablas de E/S
- Un dispositivo de E/S puede estar disponible o estar asignado a un proceso en particular.
- Almacena el estado de la operación de E/S.
- Posición de memoria principal que se está utilizando como origen o destino en la transferencia de E/S.

### Tablas de archivos
- Ofrecen información sobre la existencia de los archivos.
  - Posición en la memoria secundaria del archivo.
  - Estado actual.
  - Otros atributos.
- A veces, esta información es mantenida por el file system.


### Bloque de control de procesos (PCB)
Es una estructura creada y administrada por el SO. La utilidad más significativa de estos bloques de control es que contienen información suficiente para posibilitar la interrupción de un proceso en ejecución y luego retomar dicha ejecución como si nada hubiera pasado. Es una herramienta clave para el SO para administrar el multiprocesamiento.

- *Identificación de proceso.* Contiene toda la información de gestión del proceso que el SO necesita para administrar el proceso.
  - *Identificador de este proceso.*
  - *Identificador del proceso que creó a este proceso (el proceso padre).*
  - *Identificador del usuario que está ejecutando este proceso.*

- *Información del estado del procesador.*
  - *Registros visibles para el usuario.* Es aquél que puede hacerse referencia por medio del lenguaje de máquina que ejecuta el procesador. Normalmente, existen de 8 a 32 de estos registros, aunque algunas implementaciones RISC tienen más de 100. Cuando un proceso deja de usar el procesador, todos los valores de estos registros son almacenados en el PCB del proceso para continuar su ejecución posteriormente si fuese necesario.
  - *Registros de control y de estado.* Hay varios registros del procesador que se emplean para controlar su funcionamiento.
    - *Contador de programa.* Contiene la dirección de la próxima instrucción a leer.
    - *Códigos de condición.* Muestran el resultado de la operación aritmética o lógica más reciente (signo, cero, acarreo, igualdad, desbordamiento, etc.).
    - *Información de estado.* Incluye los indicadores de habilitación o inhabilitación de interrupciones y modo de ejecución.
  - *Punteros de pila.* Cada proceso tiene una o más pilas con criterio LIFO del sistema asociadas. Se utilizan para almacenar los parámetros y las direcciones de retorno de los procedimientos y de las llamadas al sistema. El puntero de pila siempre apunta a la cima de la pila.

- *Información de control del proceso.* 
  - *Información de planificación y de estado.* Esta es la información que necesita el sistema operativo para llevar a cabo sus funciones de planificación, es decir, es la información con la cual el scheduler decide. Los elementos típicos de esta información son los siguientes:
    - *Estado del proceso.* Define la disposición del proceso para ser planificado para ejecutar (en ejecución, listo, esperando, bloqueado).
    - *Prioridad.* Se puede usar uno o más campos para describir la prioridad de planificación de los procesos. En algunos sistemas se necesitan varios valores (por omisión, actual, la más alta permitida).
    - *Información de planificación.* Ésta dependerá del algoritmo de planificación utilizado. 
    - *Suceso.* La identidad del suceso que el proceso está esperando antes de poder reanudarse. Por ejemplo, el número de interrupción que identifica la operación que satisface la solicitud de E/S del proceso.
  - *Estructuración de datos.* Un proceso puede estar enlazado con otros procesos en una cola, anillo o alguna otra estructura.
  - *Comunicación entre procesos.* Puede haber varios indicadores, señales y mensajes asociados con la comunicación entre dos procesos independientes.
  - *Privilegios de los procesos.* A los procesos se les otorgan privilegios en términos de la memoria a la que pueden acceder y el tipo de instrucciones que pueden ejecutar. Además, también se pueden aplicar privilegios al uso de los servicios y utilidades del sistema.
  - *Gestión de memoria.* Esta sección puede incluir punteros a las tablas de páginas o segmentos que describen la memoria virtual asignada al proceso.
  - *Propiedad de los recursos y utilización.* Se pueden indicar los recursos controlados por el proceso, como los archivos abiertos. También puede incluir un historial de la utilización del procesador o de otros recursos.


# **Estado del procesador**
El estado del procesador está formado por el contenido de los registros del procesador. Cuando un proceso es desalojado del procesador, antes de cargar el siguiente proceso, se deben cargar los valores de los registros del procesador en el PCB del proceso correspondiente para luego poder retomar su ejecución.

- *Registros visibles para el proceso de usuario.*
- *Registros de control y de estado.*
- *Punteros de pila.*

### ¿Cuándo un proceso libera el procesador?
- *Interrupción de reloj.*  El proceso en ejecución ha consumido la fracción máxima de tiempo permitida.
- *Interrupción E/S.* El proceso realiza un system call.
- *Fallo de memoria.* La dirección de memoria se encuentra en la memoria virtual, por lo tanto, debe ser llevada a la memoria principal. El proceso se bloquea hasta que la página solicitada sea cargada en memoria.
- *Cepos.* Se ha producido un error. Puede hacer que el proceso que se estaba ejecutando pase al estado de Terminado.
- *Llamada del supervisor.* La operación de abrir un archivo (system call).




# **Context Switch**
Es el proceso mediante el cual se salva el contexto del procesador, incluyendo el contador de programa y otros registros. Es un proceso automático de volcado de información del PCB a los registros del procesador y viceversa en el proceso de carga y descarga de un proceso respectivamente.

1. Guardar el contexto del procesador, incluyendo PC y otros registros.
1. Actualizar el bloque de control del proceso que está en estado de ejecución. Esto incluye modificar el estado del proceso a otro.
1. Mover el bloque de control del proceso a la cola apropiada (listos, bloqueados, etc.).
1. Seleccionar otro proceso para su ejecución.
1. Modificar el PCB del proceso seleccionado. Esto incluye modificar su estado a Ejecutando.
1. Actualizar las estructuras de administración de memoria.
1. Restaurar el contexto del proceso seleccionado.

### ¿Cuándo realizar el Switch?
1. *Interrupción de reloj*. El SO determina que el proceso alcanzó el tiempo máximo de uso de procesador.
1. *Interrupción de E/S.* 
1. *Fallo de memoria.* El procesador encuentra una referencia a una palabra del programa que se encuentra en la memoria virtual y el SO debe cargar el bloque o página correspondiente en la memoria principal.
1. *System call.*
1. *El proceso termina por alguna razón.*

### Mode Switch
Si no hay ninguna interrupción pendiente, el procesador continúa la ejecución del proceso actual. Si existe una interrupción pendiente, el procesador prosigue de la siguiente manera:

1. Setea el PC en la posición inicial de la rutina de atención a la interrupción.
1. Switchea del modo de usuario al modo kernel dado que es probable que la rutina de atención posea instrucciones privilegiadas.

# **Ejecución del sistema operativo**
Dado que el sistema operativo es un conjunto de programas y es ejecutado por el procesador como cualquier otro programa, ¿Es el SO un proceso? ¿Quién y cómo lo controla?

La ejecución del SO puede darse por procesos que se encuentran dentro de:

1. *Núcleo (fuera de todo proceso de usuario).* Ejecuta el kernel del SO fuera de cualquier proceso. El SO tiene su propia región de memoria para utilizar, así como su propia pila del sistema para controlar llamados a procedimientos y retornos de los mismos. A su vez, el mismo se encarga de completar la función de guardar el entorno del procesador y proceder a cambiar a otro proceso. Es por ello que el concepto de proceso sólo se utiliza para programas de usuario. El código del SO se ejecuta como una entidad separada que opera en modo privilegiado.
1. *Ejecución dentro de los procesos de usuario.* Software del SO en el contexto de un proceso de usuario. Un proceso se ejecuta en modo privilegiado SÓLO cuando se ejecuta el código del SO. Cuando se produce una interrupción en el programa de usuario, el procesador realiza un Mode Switch al modo kernel y le pasa el control al SO, pero sin realizar un Process Switch.
# **Schedullers (Planificadores)**
Siempre que hay un recurso no compartible y un conjunto de procesos que compiten por él, el SO debe decidir qué proceso asignarlo. Recurre, entonces, a un planificador.

Solo se encargan de PLANIFICAR, pero no es el que materializa dicha planificación. Es decir, es el autor INTELECTUAL del uso de los recursos.

Los schedullers son módulos del SO que planifican el uso de un recurso, decidiendo a qué proceso se le asignará el recurso en base a un criterio determinado (algoritmo de schedulling). A su vez, interactúan con otro modulo responsable de la ejecución material de sus decisiones.

### Scheduler de Memoria
El que materializa la planificación de este scheduler es Loader de memoria. Planifica principalmente la creación de procesos y la asignación de espacios de memoria y almacenamientos de datos. Es conocido también como Scheduler de Largo Plazo, dado que la frecuencia de creación de procesos es baja.

*Loader.* Es el módulo del SO que carga y descarga procesos de memoria. Sus funciones son las de leer los contenidos de un archivo ejecutable conteniendo las instrucciones del programa en memoria, para acto seguido dejar preparado el proceso para su ejecución.

### Scheduler de Procesador
Decide a qué proceso de los que se encuentra en la cola de “listos” le otorgará el procesador, y es el Dispatcher el que materialmente realiza dicha acción. Es también conocido como Scheduler de Corto Plazo, dado que los procesos son altamente interactivos. Es por esto que este scheduler influye directamente en la eficiencia del uso del procesador.

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

#### *Shortest Process Next – Shortest Job Next **(SJF)
Mediante esta técnica, se elige el proceso que menor tiempo esperado de servicio posea dentro de la cola de listos. Uno de los inconvenientes con esta técnica es que el programador debe poder estimar de antemano el tiempo de servicio que requerirá un proceso, cosa que no es fácil en la mayoría de los casos.

#### *Shortest Remaining Time **(SRJF)
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
El scheduler tradicional de UNIX emplea un feedback de multinivel utilizando round robin dentro de cada una de las colas de prioridad. Utiliza un desalojo adelantado de un segundo, es decir, si un proceso en ejecución no finaliza o no es bloqueado en un segundo, es desalojado del procesador. 

La prioridad que utiliza UNIX está basada en el tipo de proceso y la historia de ejecución del mismo. Esta prioridad es recalculada cada un segundo.



En orden de prioridad decreciente, los tipos de procesos son:

- *Swapper.*
- *Bloqueo del controlador de dispositivo de E/S.*
- *Manipulación de archivos.*
- *Dispositivo de control de E/S de caracteres.*
- *Procesos de usuario.*

Esta jerarquía debería proveer el uso más eficiente de los dispositivos de E/S. Dentro de la banda de los procesos de usuario, la historia de ejecución de los procesos tiende a penalizar a los procesos vinculados al procesador a expensas de los procesos vinculados con E/S.

Esta estrategia está orientada a sistemas de entornos interactivos de tiempo compartido.


# File System
![[Sistemas de archivos]]

# Gestión de la memoria principal
La memoria es uno de los recursos básicos del Sistema de Computación. Necesitamos gestionarla para hacer un uso eficiente de ella (que no haya memoria ociosa) y alojar la mayor cantidad de procesos posibles (grado de multiprogramación). **Esto mejora potencialmente el % de uso efectivo del procesador, dado que el mismo siempre tendrá procesos para ejecutar.**
**
La memoria principal y los registros del procesador son las únicas unidades de almacenamiento a las que el CPU puede acceder de manera directa. Para los registros, solo basta con un ciclo de reloj, mientras que para el acceso a memoria se requieren dos o más ciclos de reloj. Para solventar esta situación, se añaden memorias caché (más veloces que la principal) intermedias entre el procesador y la memoria principal, la cual actúa como buffer de memoria.

La administración de memoria central es la función del sistema operativo que lleva el registro de cuáles partes de la memoria están en uso, asigna memoria a los procesos cuando la precisan y los desaloja cuando terminan. Cuando se requiere que un sistema albergue más de un proceso en memoria, se deben adoptar políticas de administración de la memoria, debiéndose implementar medidas de protección para que un proceso no viole el espacio asignado a otro y establecer criterios para asignar el espacio a los procesos a cargar.
# **Fragmentación**
Es la cantidad de memoria ociosa (no utilizada efectivamente), esté disponible o no.

- Si esa memoria no utilizada está asignada a un proceso, entonces solo él puede usarla. Si no la usa: **Fragmentación interna.** Ningún otro proceso la puede utilizar
- Si esa memoria no utilizada no está asignada a ningún proceso, entonces estará disponible para su uso: **Fragmentación externa.**
# **Indicadores**
- *Grado de multiprogramación (N) ↑*

- *Tamaño máximo del proceso (N) ↑*

- *Fragmentación interna (FI) ↓*

- *Fragmentación externa (FE) ↓*

Se deben verificar además los mecanismos de garantías de la protección, para evitar que un proceso no acceda a un área de memoria de otro proceso sin el permiso necesario. Permite garantizar el uso adecuado de los recursos.
# **Cuestiones a considerar**
El programador no sabe dónde se alojará el código de su programa en cada ejecución y tampoco conoce qué otros programas (código) residirán en la memoria en el momento de ejecución.

Es imposible, entonces, comprobar las direcciones absolutas de los programas, puesto que se desconoce la ubicación de ese código en la memoria principal.
# **Vinculación de direcciones**
La vinculación de direcciones de instrucciones y datos a memoria, puede ocurrir en tres momentos distintos:

En tiempo de compilación. Si la región de memoria se conoce a priori, se puede generar el llamado código absoluto. Si la región cambia, se debe recompilar el programa.

En tiempo de carga. Se debe generar código relocalizable, dado que la memoria ya no se conoce en tiempo de compilación. 

En tiempo de ejecución. La vinculación se posterga hasta el tiempo de ejecución si el proceso puede moverse de un segmento de memoria a otro. Se necesita soporte de hardware para los mapas de direcciones (registros base y límite). La posición final de una referencia a memoria no se determina hasta que es referenciada en ejecución.

### Direcciones lógicas
Son las generadas por la CPU. También se denominan espacio virtual de direcciones. Son las direcciones vistas por el proceso.

### Direcciones físicas
Son las direcciones vistas por la unidad de memoria. Dirección real.

Las direcciones físicas y lógicas son las mismas en los esquemas de vinculación de tiempo de compilación y tiempo de carga.

Las direcciones físicas y lógicas difieren en el esquema de vinculación en el tiempo de ejecución. Se debe resolver el mapeo de virtual a físico.

### Referencias
Se deben traducir las referencias a la memoria encontradas en el código a las direcciones físicas reales.

- Direcciones al mismo código.
- Referencias a datos y a pila.

Es conveniente permitir el acceso de varios procesos a una misma zona de la memoria principal (compartida) en lugar de que cada proceso tenga su propia copia. Por ejemplo, si se tienen 8 documentos de Word abiertos, no vale la pena tener cargado el programa 8 veces en la memoria.


# **Traducción de direcciones lógicas a físicas**
La Memory Management Unit (MMU) es un dispositivo de HW que transforma las direcciones virtuales en direcciones físicas. A cada dirección generada por el proceso de usuario se le suma el valor del registro de relocalización del mismo (dirección base).

De esta manera, un programa usuario siempre hará referencia a direcciones lógicas, independizándose de las direcciones físicas de la memoria.

### Direccionamiento con reubicación
En un sistema con multiprogramación, la memoria principal generalmente es compartida por varios procesos. Cuando un proceso es quitado de la memoria y luego de un tiempo vuelve a ser cargado en la misma, lo más probable es que sea alojado en otro sector de la misma, por lo que sus registros base y límite serán distintos cada vez que sea cargado, es decir, se reubicará el proceso en un área diferente de la memoria.
#### *Dirección lógica*
Es una referencia a una posición de memoria independiente de la asignación actual de datos a la memoria. Se debe hacer un mapeo a física.
#### *Dirección relativa*
La dirección se expresa como una posición relativa a algún punto conocido.
#### *Dirección física*
Dirección absoluta en la memoria, generada por la MMU.

### Registros necesarios para el mapeo
#### *Registro base*
Se carga con la dirección física del inicio del proceso en la memoria.
#### *Registro límite*
Indica la dirección física final del proceso en la memoria.

Se suma el valor del registro base a la dirección relativa del código para obtener una dirección absoluta y compara con el valor del registro límite (protección). Si la dirección no está dentro de los límites, se genera una interrupción en el sistema operativo (error fatal).

La protección necesaria para que un proceso no pueda acceder a áreas de memoria fuera del rango admitido se realiza mediante un dispositivo de hardware que se encuentra en el CPU que toma los registros base, límite y la dirección y decide si ésta es correcta. Estos registros base y límite solo pueden ser modificados por el SO, precisamente por el Dispatcher, mediante una instrucción privilegiada especial, de modo que el SO puede cargar y descargar procesos del CPU a la memoria.
# **Intercambio**
El pasaje de procesos de memoria al dispositivo de almacenamiento secundario (backing store) se llama Swap Out.

El pasaje de procesos del dispositivo de almacenamiento secundario a la memoria se llama Swap in.

El conjunto de Swap Out y Swap In se lo conoce como Swapping.


# **Principios de gestión de la memoria**
### Principio de continuidad
Dice que un proceso debe cargarse contiguo en memoria (en direcciones consecutivas).
### Principio de completitud
Dice que un proceso debe cargarse completo en memoria.

# **Maquina desnuda**
En los principios de la computación, hasta 1960, no había sistemas operativos. La memoria era una sábana de celdas contiguas sin división física ni lógica.

No había soporte para la gestión de la memoria. El proceso debía controlar los dispositivos.

El programador, administrador y usuario eran la misma persona y era quien administraba los recursos.
# **Monitor Residente**
Fue el primer esquema de un gestor de acciones y recursos. Se encargaba del secuenciamiento de tareas, la gestión de los dispositivos y algunas rutinas que eran de uso recurrente. Debía conocer los dispositivos y saber cómo funcionaban.

Fue necesario dividir la memoria para evitar que el proceso de usuario no escribiera sobre el monitor residente: surge la cuestión de la protección y el Registro FENCE, el cual almacena la dirección base del proceso.

# **Swapping superpuesto**
Tiene como objetivo optimizar el tiempo de carga y descarga de los procesos (tiempo muerto). Se divide la memoria en tres regiones iguales. Mientras en una región está el proceso que se está ejecutando, en otra región está el proceso que se está descargando, y en la tercera región está el proceso nuevo, que se está cargando. (Similar a PIPE-LINE arquitectura de computadoras).

Siempre hay solo un proceso en ejecución: multiprogramación, pero monotarea.

### Ventaja
Se superponen los procesos de carga, descarga y ejecución (se ejecutan concurrentemente), entonces, se eliminan los tiempos muertos de procesador mientras se cargan y descargan los procesos. El procesador siempre está ocupado corriendo un proceso de usuario.
### Desventajas
El tamaño máximo del proceso se reduce a un tercio de la memoria física disponible para procesos de usuarios.

Además, se produce fragmentación interna en cada división.



# **Múltiples particiones de tamaño fijo (MFT)**
Si el proceso requiere una E/S en el modelo de Swapping, el procesador se queda esperando a que se complete dicha operación. Por ello, se desarrolló otra metodología que resulta de la evolución de la anterior.

En el modelo MFT, se divide la memoria en particiones o regiones de igual tamaño (fijo) que alojan diferentes procesos en ejecución (aparece la multitarea).

En cualquier partición libre puede cargarse cualquier proceso cuyo tamaño sea menor o igual que el tamaño de la partición.

- La cantidad y tamaño de particiones son declaradas al momento de generar el sistema.
- El uso de la memoria es ineficiente, cualquier programa, sin importar lo pequeño que sea, ocupará una partición completa, generando fragmentación interna.
- El tamaño máximo de proceso es el tamaño de la partición.
  - Las particiones pueden ser todas iguales o diferentes entre sí, pero su tamaño es fijo. Si son todas iguales, con una sola cola es suficiente para cargar los programas en memoria.
  - Si las particiones son diferentes, conviene implementar múltiples colas, para que cada proceso compita por la región en la que mejor ajusta y con mayor tamaño máximo, pero puede darse el caso de que un proceso pequeño esté esperando en la cola mientras existe una partición de mayor tamaño que esté en desuso.
# **Múltiples particiones de tamaño variable (MVT)**
- Se divide la memoria en particiones variables en número y longitud. 
- Al proceso se le asigna exactamente tanta memoria como necesite.
- Con el uso, se van produciendo varios huevos en la memoria **(Fragmentación Externa)**, pero no existe fragmentación interna.
- Se debe usar la **Compactación** para desplazar los procesos para que estén contiguos, de forma tal que toda la memoria libre quede junta en un solo bloque. Desventaja para sistemas operativos de tiempo real (piloto automático, por ejemplo). Este proceso genera un gran desperdicio de tiempo de procesador.
- El sistema operativo debe decidir qué espacio libre le asigna al proceso
- *Mejor ajuste (best fit):*
  - Elige el bloque de tamaño más próximo al solicitado.
  - Proporciona en general los peores resultados.
  - Asigna el hueco más pequeño para el proceso, garantizando que el fragmento que se deja es lo más pequeño posible y, por lo tanto, se debe compactar más frecuentemente.

- *Primer ajuste (first fit):*
  - Es el más rápido.
  - Puede tener varios procesos cargados en el extremo inicial de la memoria que es necesario recorrer cuando se intenta encontrar un bloque libre.
- *Peor ajuste (Worst fit):*
  - Asigna el bloque libre más grande. 
  - Minimiza la fragmentación externa.


# **Paginación**
- Se rompe el principio de continuidad de MFT.
- La memoria principal se encuentra dividida en trozos iguales de tamaño fijo **(Marco/Frame)** y cada proceso se divide en trozos de tamaño fijo **(Página/Page)**. Las páginas y los frames poseen el mismo tamaño fijo.
- El sistema operativo debe mantener una tabla de frames, la cual posee una entrada por cada frame de la memoria e indica si está libre u ocupado, y, si está ocupado, indica con qué página de qué proceso lo está.
- **El sistema operativo mantiene una tabla de páginas para cada proceso.**
  - Muestra la posición del marco de cada página del proceso.
  - La dirección de la memoria consta en un numero de página y un desplazamiento dentro de la misma.
- Todos los frames libres pueden ser ocupados: No hay fragmentación externa.
- Siempre hay fragmentación interna en el último frame asignado a cada proceso. En promedio, cada proceso posee una fragmentación interna en el último frame igual a la mitad del tamaño del mismo, por lo cual:
  - Cuanto más grande sea el tamaño del frame, habrá mayor FI.
  - El tamaño máximo del proceso que se puede correr es equivalente a toda la memoria física.
  - El N máximo es la cantidad de frames.
- Dos o más procesos pueden compartir una tabla de páginas, de forma que solo es necesario cargarla una única vez (procesos que comparten el código fuente puro, el cual no puede ser modificado en tiempo ejecución).

### Tabla de páginas
- Cada proceso tiene su propia tabla de páginas en su PCB. Es un arreglo de tipo integer, donde cada elemento guarda el frame correspondiente a la entrada, es decir, el elemento 0 tiene la posición de la página 0 (número de frame).
- El SO tiene una tabla propia cargada en registros asociativos (Hardware) donde se mapea la tabla de páginas del proceso actual, en tiempo de context Switch, para mayor performance.
  - El hecho de tener una tabla de páginas en hardware es útil para procesos cuya tabla de páginas sea pequeña. En otros casos, la tabla de páginas se almacena en la memoria principal, y se posee un registro que indica la dirección base de la misma. 
  - Al realizar un context Switch, en cuanto a la tabla de páginas, solo debe actualizarse este registro, por lo que se reduce el tiempo requerido, pero para acceder a la tabla de páginas se requiere acceder a memoria principal (más lenta, y requiere un acceso para obtener el número de frame y otro para ir al frame en sí).

Para solucionar este problema, se utiliza un buffer de traducción anticipada *(Translation Look-aside Buffer)* cuando se utiliza memoria virtual.


#### *Estructura de un nivel*
Tomando una dirección lógica en la que los primeros n bits son el número de página y los m restantes son el desplazamiento: 

1. Primero se extrae el número de página como los n bits más significativos de la dirección lógica. 
1. Se usa el número de página como un índice en la tabla de páginas del proceso para encontrar el número de frame, k.
1. La dirección física de comienzo del frame es k \* tamaño de página, y la dirección física del byte referenciado es ese número más el desplazamiento.



#### *Estructura jerárquica de dos niveles*
En los sistemas modernos, el espacio de direccionamiento lógico es muchísimo más grande que el espacio de direccionamiento físico de la memoria, por lo que las tablas de páginas son excesivamente grandes y deben ser paginadas. Ahora, si suponemos una dirección lógica de 32 bits de los cuales 20 referencian al número de página y 12 al offset, el número de página consta de un número de página (correspondiente a la tabla de páginas de la tabla de páginas del proceso) y un offset dentro de la misma.

### Direcciones
Cada dirección es expresada como:

- Un número de página que es usada como un índice para ingresar a la tabla de páginas y encontrar el número de frame donde está alojada esa página en memoria física. Como los frames son de tamaño fijo, puedo encontrar la dirección donde inicia la página.
- Un offset de página que es combinado con la dirección base para definir la dirección física de la referencia. 


### Tabla de páginas del SO
- Es de acceso rápido.
- Tiene una cantidad finita de entradas que se setean en el Context Switch
- ` `con la tabla de páginas del proceso que se carga en el procesador.
  - Cuando el proceso tiene menos páginas que la cantidad de entradas que la tabla del SO, se deben marcar las entradas inválidas que quedan en desuso.
  - Cuando un proceso tiene más páginas que las entradas de la tabla de del SO, se mantiene una parte de la tabla en memoria (la tabla de páginas del proceso debe ser paginada) y se incrementa el tiempo de acceso efectivo a memoria.
# **Segmentación**
- Se rompe el principio de continuidad de MVT.
- La memoria principal se la considera una sábana sin divisiones preestablecidas.
- Los procesos son divididos en segmentos según un criterio de unidad lógica definido por el usuario, cada uno con su tamaño (existe una longitud máxima de segmento).
- Los segmentos se van asignando en memoria en los huecos libres que haya, dispersos entre sí.
- El esquema de administración de memoria es más cercano a la vista de memoria del usuario.
- Un programa es una colección de segmentos.
  - Programa principal, procedimiento, función, librería, método, objeto, variables locales, pila, matrices, etc.



- No hay fragmentación interna en los segmentos. 
- El programador debe conocer el tamaño máximo de cada segmento.
- Todos los huecos libres se pueden ocupar: hay **fragmentación externa, pero es mínima** (compactación).
- La compactación es menos probable que en MVT, dado que es más fácil cargar un proceso divido en varios segmentos que en un solo bloque contiguo.
- La compactación es ininterrumpible e impredecible, dado que ocurre cuando existe espacio libre para un proceso, pero no se encuentra contiguo.

### Tabla de segmentos
Cada proceso tiene su propia tabla de segmentos en su PCB. Es un arreglo de dos campos, cada elemento guarda la dirección base del segmento y la dirección limite (direcciones lógicas respecto al programa). Es más grande que la tabla de páginas.

El SO tiene una tabla de segmentos en el contexto de operación del proceso donde se mapea la tabla de segmentos del proceso actual en tiempo de context Switch para mayor performance.

Todas las consideraciones hechas para paginación son válidas para la Segmentación en cuanto a la administración de la tabla de segmentos del SO, bit de validez, rebalse, etc.

### Direcciones
Cada dirección es expresada como:

- Un número de segmento que es usado como índice para ingresar a la tabla de segmentos y encontrar la dirección base del segmento en la memoria física.
- Un offset que es combinado con la dirección base del segmento para definir la dirección física de la referencia.

#### *Mapeo lógico a físico*
1. Se extrae el número de segmento de los n bits más significativos de la dirección lógica. 
1. Se utiliza el número de segmento como un índice en la tabla de segmentos del proceso para encontrar la dirección física del segmento.
1. Se compara el desplazamiento, expresado en los m bits menos significativos, con la longitud del segmento. Si el desplazamiento es mayor o igual a la longitud, la dirección es inválida. 
1. La dirección física deseada es la suma de la dirección física de comienzo del segmento más el desplazamiento.


# **Memoria Virtual**
Memoria virtual es una técnica de administración de memoria que permite la ejecución de procesos que no están completamente cargados en memoria (rompe el principio de completitud).

Todas las referencias a memoria serán direcciones lógicas que se traducirán dinámicamente a direcciones físicas durante la ejecución (realocación dinámica).

Un proceso puede dividirse en varias partes y no es necesario que todas estas partes estén en la memoria ppal. durante la ejecución. Es decir, no será necesario que estén todas las páginas o segmentos del proceso cargadas en memoria en tiempo de ejecución.

La memoria virtual es una memoria situada en disco (área de swap) y permite una multiprogramación más eficiente.

# **Ventajas**
- Se cargan sólo algunos fragmentos de cada proceso, solo los que son requeridos. Proceso de Swapping más eficiente. 
- Se pueden mantener más procesos en la memoria principal (Mayor a N).
  - Con tantos procesos en la memoria principal es muy probable que uno de los procesos esté en estado Listo en un instante determinado (menos tiempo ocioso).
- Es posible ejecutar procesos más grandes que el tamaño de toda la memoria principal. El tamaño máximo de proceso es prácticamente infinito (limitado por el almacenamiento secundario).

# **Fallo de acceso**
- El sistema operativo crea el proceso y comienza a cargarlo trayendo solo algunos pocos fragmentos de su código a memoria.
- El conjunto residente es la parte del proceso que está realmente en memoria principal.
- Si el procesador encuentra una dirección lógica que no está en la memoria principal (una referencia a memoria que no está en memoria principal), genera un Fallo de acceso a memoria*,** que provoca una interrupción.
- Un fallo de acceso es una referencia válida de un proceso a una dirección ausente en memoria.

### Rutina de atención de un fallo de acceso
Ante un fallo de acceso, el SO debe traer a memoria principal el fragmento de proceso que contiene la dirección lógica válida y ausente que provocó el fallo.

1. El SO emite una solicitud de lectura al disco donde está alojado el fragmento y pone el proceso en estado de *Bloqueado* por I/O.
1. El SO dispara otro proceso de usuario para que se ejecute mientras se realiza la operación de I/O.
1. Una vez que el fragmento requerido se ha traído a memoria principal (se emite una interrupción de satisfacción de I/O), se devuelve el control al SO y éste coloca el proceso afectado en estado Listo.

### Principio de cercanía de referencias
- Las referencias a los datos y al programa dentro de un proceso tienden a agruparse (cercanas) y se pueden dividir por locaciones. Cuando un proceso se encuentra en una de estas locaciones, las referencias que realizará muy posiblemente se encuentren en el entorno de esta locación. Por ejemplo, cuando se llama a una función, se define una nueva localidad, en la cual se encontrarán las instrucciones de la función, parámetros y un sub set de variables locales.
- Durante cortos períodos de tiempo se necesitarán sólo unos pocos fragmentos de un proceso.
- Sería posible entonces hacer predicciones inteligentes sobre qué fragmentos de un proceso se necesitarán en un futuro cercano, de modo de minimizar los posibles fallos de acceso.
- El principio de cercanía sugiere que los esquemas de memoria virtual pueden funcionar eficazmente.


# **Técnicas de gestión de Memoria virtual**
### Soporte de hardware necesario para la gestión
- Tiene que existir un soporte adicional y específico de hardware para implementar paginación/segmentación por demanda.
- El SO debe incluir un software (en kernel) para gestionar el movimiento de páginas o segmentos entre memoria secundaria y principal.
- El SO debe implementar algorítmica específica adicional para lograr un uso eficiente de la memoria usando estas técnicas.

### Segmentación por demanda
- Similar a Segmentación pura, pero no todos los segmentos del proceso están cargados en la memoria principal.
- Los segmentos se van trayendo a memoria principal cuando se los demanda.
- Fallo de acceso = fallo de segmento.
- Valen los mismos principios de gestión que en la paginación por demanda. 
- Facilita la compartición entre procesos (es más probable compartir segmentos que procesos)
- La referencia sigue siendo por un par (Segmento, Desplazamiento).
- La Tabla de segmentos es más cara (más ancha).

### Paginación por demanda
- Similar a Paginación pura, pero no todas las páginas del proceso están cargadas en la memoria principal.
- La totalidad de las páginas del proceso están en memoria Secundaria.
- Las páginas se van trayendo a la memoria principal cuando se las demanda o requiere.
- Fallo de acceso = fallo de página.
- Cada proceso tiene asignados un conjunto de frames para operar.
- Algunas páginas del proceso están en memoria principal.
- Página que no se requiere, no se carga nunca.
- A medida que se van produciendo fallos de página, el SO va cargando las páginas que el proceso requiere en los frames que tiene asignados, conforme las va solicitando (swap in).
- Cuando un proceso tiene todos sus frames asignados ocupados y produce un fallo de página, se requiere el reemplazo de alguna de las páginas cargadas por la nueva requerida.
- En el reemplazo, primero se debe descargar (swap out) la página que será reemplazada (página víctima). Se debe actualizar en la memoria secundaria la página descargada.

#### *Indicadores*
- Cada fallo de página significa un proceso de Swapping que cuesta caro (tiempo de transferencia).
- Además, el proceso current pierde el procesador (context Switch) hasta recuperar la página que requiere (tiempo de Bloqueado por I/O) y recién ahí vuelve a estado Listo.
- Por lo tanto, hay que minimizar la Cantidad de fallos de páginas** y la **Tasa de Fallos de página (cantidad de FdP en el tiempo).

#### *Páginas limpias y sucias*
- La descarga de la página víctima a reemplazar requiere actualizar su imagen en la memoria secundaria.
- Si la página víctima no se modificó, (página limpia) no es necesario descargarla ni actualizarla. Se realiza solo una swap in y se pisa la página víctima. Un swap menos.
- Se requiere ahora otro bit de control en la tabla de páginas, el Dirty Bit**,* que indica si la página fue modificada luego de ser cargada en memoria.

#### *Tablas de páginas*
- Cada proceso tiene su tabla de páginas en su PCB.
- Cada entrada de la tabla contiene el número de frame correspondiente en la memoria principal.
- Se necesita agregar un bit adicional a cada entrada para indicar si la página está presente en memoria principal o no. (Present/Absent bit).
- La tabla completa de páginas completa puede ocupar una cantidad enorme de memoria principal.
  - Las tablas se almacenan en la memoria virtual
- Cada referencia genera, entonces, dos accesos a la memoria virtual:
  - *Uno para obtener la entrada de la tabla de páginas correspondiente.*
  - *Otro para obtener el dato deseado.*
- Baja performance.


#### *Tabla de páginas del SO - TLB*
- La tabla del SO suele estar en HW, por lo que posee un tamaño limitado de entradas.
- Se utiliza el Translation Lookaside Buffer, a modo de caché de entradas de tabla de páginas. 
  - Es una memoria de caché rápida que contiene entradas de la tabla de páginas del proceso usadas recientemente o con mayor frecuencia. 
  - Cada entrada al TLB consiste en un par clave-valor. El TLB contiene solo unas pocas entradas de la tabla de páginas del proceso. 
  - Cuando se quiere acceder a una página mediante una dirección virtual, el procesador primero consulta el TLB (aunque en realidad suelen consultarse las memorias caché a la vez que las secundarias y se toma la respuesta que llegue primero). Si se produce un fallo de caché, el proceso debe ir a buscar la entrada a la tabla de páginas en memoria secundaria y cargarla en el TLB.
  - Una vez obtenida la entrada, se corrobora que la página esté cargada en la memoria.
  - Si está presente, se ejecuta la referencia.
  - Si está ausente, se produce un fallo de página.

#### *Tamaño de página – Consideraciones*
- Cuanto menor sea el tamaño de página, menor será la cantidad de fragmentación interna, y menor el tiempo de Swapping.
- Cuanto menor sea la página, mayor será el número de páginas que se necesitan por proceso (más entradas en la tabla de páginas).
- Esto puede significar que una gran parte de las tablas de páginas de los procesos activos deben estar en la memoria virtual (mayor cantidad de fallos de páginas).

#### *Políticas de asignación de frames*
- *Equitativa.* Asigna a todos los procesos la misma cantidad de frames. A procesos pequeños pueden sobrarle frames mientras que a los procesos grandes le pueden faltar.
- *Proporcional.* Se asigna a cada proceso la parte proporcional de frames de la memoria principal, en función de su tamaño.  Menor cantidad de fallos de página.
- *Existe una cantidad mínima de frames para que el proceso pueda ejecutar una instrucción de assembler completa. En caso de fallar en el medio de la ejecución de una instrucción (al decodificar un operando, por ejemplo) se deberá ejecutar la instrucción desde el inicio luego de solventar el page fault.*
- *En principio, cuanto mayor es la cantidad de frames asignados a un proceso, menor debería ser la cantidad de fallos de página.*


#### *Políticas de carga inicial de páginas*
- *Pre paginación.* Al inicio del proceso se cargan algunas de sus páginas en los frames asignados. Se cargan las iniciales y las que poseen mayor probabilidad de ser referenciadas en el corto plazo.
- *Paginación por demanda estricta/pura.* Se cargan las páginas a medida que se van referenciando. Página que no es referenciada, nunca es cargada.

#### *Criterios de reemplazo de páginas*
- *Criterio local.* Se reemplaza una víctima del conjunto de frames asignado al proceso.
- *Criterio global.* Se reemplaza una página del conjunto total de frames de la memoria, sin importar a qué proceso esté asignado.
- Ante la necesidad de reemplazar alguna página, se debe elegir cuál reemplazar tratando de elegir aquella que menor efecto tenga en la tasa de fallo de páginas.
- No todas las páginas son víctimas candidatas. Hay algunas “páginas bloqueadas” que comprenden las del kernel, estructuras de control, buffers de I/O, etc. La propia página que realiza la referencia tampoco puede ser reemplazada obviamente. El bloqueo se consigue asociando un bit de bloqueo a cada marco, el cual indica si es posible que la página sea reemplazada o no.

### Algoritmos de selección de página víctima
#### *FIFO*
- Se reemplaza la página que ha estado más tiempo cargada en memoria.
- Requiere agregar un Timestamp de tiempo de carga en la TP para las páginas presentes, que se actualiza en cada swap in.
- Es muy fácil de implementar.
- Estas páginas pueden necesitarse de nuevo en el corto plazo. Mayor cantidad de fallos de página.

##### Anomalía de Belady
*Cuando aplicamos un algoritmo FIFO de reemplazo, puede pasar que, al incrementar los frames asignados a un proceso, en vez de reducir su cantidad de fallos de página, los incremente.*

#### *Más usada (MU) - Menos usada (LU)*
- Se reemplaza la página que ha sido más o menos usada desde que se cargó. 
- En caso de MU, se piensa que la más usada no volverá a ser referenciada a corto plazo, y la menos usada es la más propensa a ser referenciada dado que es probable que recién haya sido cargada en memoria.
- Requiere agregar un contador de referencias en la TP para las páginas presentes, que se actualiza en cada vez que se referencia.
- Es fácil de implementar.
- El mayor o menor uso de las páginas no tiene que ver con su uso futuro.

#### *Algoritmo Optimal* 
- Selecciona para reemplazar la página que tiene que esperar una mayor cantidad de tiempo hasta que se produzca la siguiente referencia a la misma.
- Es imposible de implementar porque requiere que el SO tenga conocimiento de las referencias futuras… y el futuro es impredecible.
- Sirve como referencia para benchmarking.

#### *Menos usada recientemente (LRU)*
- Reemplaza la página de memoria que no ha sido referenciada hace más tiempo.
- Debido al principio de cercanía, esta sería la página con menor probabilidad de ser referenciada en el corto plazo.
- Requiere agregar un Timestamp de tiempo de última referencia en la TP para las páginas presentes en memoria, que se actualiza en cada referencia.

### Procedimiento de reemplazo de página
1. Fallo de página.
1. Se salva el estado del proceso por la interrupción (registers, condition code, instruction counter).
1. Se bloquea la página que hace la referencia.
   1. *Si hay frames asignados libres*: se asigna uno.
   1. *Si no hay frames asignados libres*: se determina el conjunto de víctimas candidatas (CVC).
      1. Si la política de reemplazo es local, entran en el CVC sólo las páginas del proceso cargadas en memoria.
      1. Si la política de reemplazo es global, entran en el CVC todas las páginas cargadas en memoria (de todos los procesos).
   1. Se reduce el CVC al conjunto de páginas limpias (si las hubiera).
   1. Se aplica el algoritmo para elegir la página víctima dentro de las que integran el CVC (FIFO, LRU, etc.)
1. Swap Out de la página víctima (si fuera sucia).
1. Swap in de la página ausente referenciada.


### Hiperpaginación
- Cuando tenemos una cantidad fija de frames asignados, reemplazo local y alta tasa de falla de páginas, decimos que estamos en Hiperpaginación, que es circunscripta al proceso en cuestión.
- El SO expulsa una página de un proceso, justo antes de ser usada. 
- El procesador consume más tiempo intercambiando páginas del proceso que ejecutando instrucciones de usuario.

### Trashing
- Sucede que un proceso produce un fallo de página en una instrucción, y se utiliza un criterio de reemplazo global, de modo que dicho proceso comienza a sacarle frames a otros procesos, pero a su vez, esos procesos necesitan de esos frames, por lo que luego también generarán fallos de página y comenzarán a sacarle frames a otros procesos. Por lo tanto, mientras se releva la página referenciada, se carga otro proceso que también produce un fallo y así sucesivamente.
- En un Trashing, el % de Uso efectivo del procesador tiende a 0, el Tiempo de Turnaround y de espera de los procesos tiende a infinito, la Productividad cae a 0 y el % de uso de los dispositivos de I/O está al 100%.
- Provoca que el SO ocupe su tiempo en context switch y swapping más que en ejecutar instrucciones de procesos de usuarios.
- Como la productividad del procesador y el tiempo efectivo del mismo disminuye, el scheduler de Memoria aumenta el grado de multiprogramación, inyectando procesos al Sistema.
- Cuantos más procesos inyecta, menor es el % de Uso efectivo del procesador, hasta que llega a 0. 
- Para solventar esto, se establece un valor máximo para el grado de multiprogramación, de modo que al superarse el mismo se entiende que el proceso entró en Trashing, por lo cual, para aumentar el % de uso del procesador, se debe decrementar el grado de multiprogramación. Con esta técnica, cuando un proceso entra en trashing, no se le permite sacar frames a otros procesos.



# **Segmentación paginada**
La paginación tiene una serie de ventajas sobre la segmentación tales como la eliminación de fragmentación externa y la posibilidad de implementar algoritmos sofisticados y eficientes para la gestión de swapping de páginas, dado que éstas son de tamaño fijo. Por otro lado, la segmentación también tiene lo suyo: permite gestionar estructuras crecientes de datos, modularidad entre los mismos, y brinda soporte para el uso compartido de segmentos y la protección de los mismos (solo lectura para code segment, lectura-escritura para ds, etc.).

Por otro lado, en los sistemas modernos, el espacio de direcciones lógicas es sumamente mayor en tamaño al espacio de direcciones físicas, por lo que los programas y los segmentos del usuario pueden ser mucho más grandes que la memoria. Es por ello, que los segmentos pueden no caber en la memoria principal. Una solución a este problema es paginar los segmentos.
### Estructuras necesarias
En una estructura de segmentación paginada, el espacio de direcciones del usuario se encuentra dividido en segmentos definidos por el mismo, por lo cual se requiere una tabla de segmentos. A su vez, cada segmento está dividido (por el SO) en una cantidad de páginas de tamaño definido, por lo que se necesita una tabla de páginas para cada segmento. 

Cuando un proceso particular está corriendo, un registro mantiene la dirección de comienzo de la tabla de segmentos para ese proceso:

- Cuando se presenta una dirección lógica, el procesador utiliza el número de segmento para hallar la entrada en la tabla de segmentos del proceso y así encontrar la tabla de páginas para ese segmento. 
- Luego, el número de página de la dirección lógica es usado para ingresar a en la tabla de páginas del segmento y buscar el número de frame correspondiente. 
- Por último, se combina el número de frame con el offset para ingresar a la memoria física.




Segundo Parcial
# **Entrada/Salida**
# **¿Qué es un dispositivo de entrada/salida?**
Un dispositivo de E/S es todo aquel dispositivo que sea externo al entorno de ejecución puro (Procesador + memoria, es lo mínimo que necesita un proceso para ejecutarse). Es utilizado por el procesador y los procesos para comunicar información al entorno.
### Ejemplos
Teclado, mouse, pantalla. Clásicos.

Discos de almacenamiento, tarjetas de red, placas de video también lo son.

# **Clasificación de Tanenbaum**
### Dispositivos de bloques
- Todos aquellos cuya mínima unidad de tratamiento de datos es un bloque de tamaño fijo. Por ejemplo, discos rígidos, pendrives, etc.
- Bloques referenciados y direccionados unívocamente.
- Cada operación es independiente de las demás.

### Dispositivos de carácter
- Mínima unidad de tratamiento de datos: carácter (byte).
- No hay forma de referenciarlos ni son direccionables.
- Operan con flujos de caracteres sin importar la estructura.
- Por ejemplo, teclado envía caracteres y ni a él ni al sistema le interesan referenciarlos como tal. Otros ejemplos son el mouse, la impresora, la placa de red.

# **Clasificación de Stallings**
### Legibles por humanos
Adecuados para dialogar con las personas (teclados, mouse, monitor, impresora).

### Legibles por máquina
Adecuados para dialogar con máquinas electrónicas, pero no con humanos (disco rígido, pendrive). El SO abstrae el disco rígido y uno llega a pensar que se comunica con el mismo, pero no.

### Comunicación
Adecuados para dialogar con otros dispositivos que están a largas distancias (placa de red, módem).

# **Diferencias según su naturaleza – Stallings**
### Velocidad de transferencia de datos
Los dispositivos que dialogan con el ser humano suelen ser más lentos, dado que se debe limitar a la percepción de los sentidos humanos. Un claro ejemplo es la pantalla, que debe mostrar figuras que sean distinguibles por el humano, el humano no puede diferenciar 30 cuadros en un mismo segundo, por lo que hay mucha redundancia. Además, el ser humano hace foco en una cierta parte de la pantalla.

### Aplicación
Según el uso que se le dé a cada dispositivo será el software necesario para operar en él. Un disco puede ser utilizado para almacenar archivos en un file-system o actuar como espacio para memoria virtual (configuración totalmente distinta). Distinto software estará asociado, pero el hardware es el mismo.

### Conjunto de operaciones
#### *Solo lectura*
Mouse, teclados.
#### *Solo escritura*
Impresora.
#### *Lectura/escritura*
Discos rígidos, pendrives.

### Unidad de transferencia
Los datos pueden ser transferidos mediante un stream de bytes o caracteres (teclado, ratón) o en bloques (discos de E/S).

### Complejidad de control
- Cuantas más operaciones pueda desempeñar, mayor es el control. 
- Los dispositivos de lecto-escritura suelen tener más complejidad de control. 
- Ejemplo: La impresora posee una interfaz de control más sencilla que el disco rígido.

### Representación de los datos
- Diferentes esquemas de codificación son usados por cada dispositivo.
- Diferente manejo de los datos entre los dispositivos. Cada dispositivo almacena a su manera.

### Condiciones de error
#### *Críticos*
Ejemplo: lectura de un bloque defectuoso. Pérdida de información en un disco. No hay solución sin backup.
#### *No críticos*
Ejemplo: no tiene papel la impresora. Puede continuarse con la impresión solucionando el problema.


# **Objetivos del SO frente a los dispositivos de E/S**
### Rendimiento (Maximizar la eficiencia)
Debido a la notable diferencia de velocidad entre el procesador y los dispositivos de I/O.
### Independencia del dispositivo (abstracción del hardware)
Capacidad del sistema operativo de brindar una visión lógica simplificada de los dispositivos de E/S hacia los usuarios, procesos y otros componentes el sistema.
# **Capas del esquema de Entrada/Salida**
### Proceso de usuario
Se realiza una llamada al sistema a través de una interrupción de E/S. Por ejemplo, guardar un documento.

### Scheduler de I/O
Se encarga del manejo de la cola y el control de las operaciones de E/S. Además, maneja las interrupciones recolectando el estado de los dispositivos y reportando el mismo. Interactúa con el módulo de E/S.

### Módulo de E/S del SO
Es un software independiente del dispositivo.  Trata con dispositivos lógicos, sin conocer los detalles para controlar realmente el dispositivo. Maneja operaciones básicas de E/S requeridas por los procesos de usuario, tales como open, close, read y write.
#### *Funciones*
- *Nombramiento de los dispositivos.* Utilizar cadenas de caracteres amigables asociando los nombres lógicos a los físicos (por medio de tablas).
- *Resolver errores.* Los que no se resolvieron hasta ese nivel (ejemplo bloque defectuoso). Debe traducir los códigos de error del controlador del dispositivo.
- *Control de concurrencia.* Asignar y liberar los dispositivos de uso exclusivo o dedicado. Ejemplo: dos procesos quieren transmitir por la placa de red al mismo tiempo.
- *Protección.* Evita que procesos utilicen dispositivos indiscriminadamente. 
- *Seguridad.* Controles de acceso.
- *Control de flujo de operaciones.* Buffering y spooling.

#### *Buffering*
Técnica que permite superponer la carga de datos a memoria con la ejecución del proceso. Podemos hacer algo con el proceso mientras voy cargando a memoria la información que necesito para este u otro proceso.

Dispone de un espacio de memoria principal para regular el intercambio de datos entre los procesos y los dispositivos de E/S, impidiendo pérdidas de información por desbordes o bajas de performance por insuficiencia de datos.

Por ejemplo, antes era más notoria la espera de carga del video. 


#### *Spooling*
Técnica que permite superponer la descarga de datos de memoria con la ejecución del proceso. 

Dispone de un espacio en memoria secundaria como un buffer de almacenamiento persistente para reducir la espera cuando los procesos transfieren datos a dispositivos periféricos.

Por ejemplo, cuando enviamos a imprimir un documento, Word envía este archivo a una zona de spooling en la memoria secundaria, de la cual otro proceso (el de la impresora en este caso) levantará el archivo para imprimirlo. Mientras tanto, el usuario puede seguir utilizando Word.


### Driver
Transforman las operaciones genéricas que le pasa el SO en comandos específicos que el controlador interpreta. Es software específico del dispositivo, pero posee la capacidad de hablar de manera genérica con el SO.

### Controlador - Adapter
Transforman los comandos a flujos de bits y los entregan al dispositivo y al bus del sistema. Es hardware que se comunica directamente con los buses de datos del dispositivo. 

### Dispositivo
Ejecuta físicamente la operación que el controlador le solicitó.


# **Evolución de las técnicas de E/S**
### E/S programada
El procesador envía un mandato de E/S, a petición de un proceso, a un dispositivo de E/S; a continuación, ese proceso realiza una espera activa hasta que se complete la operación antes de continuar.  El procesador pregunta periódicamente si la E/S finalizó, ocupando tiempo de procesador. Usualmente los bloques no podían viajar todos juntos por el bus de datos, por lo que una vez cargados en el buffer del disco de E/S, debían ser solicitados de a un fragmento de datos a la vez.


### E/S dirigida por interrupciones
El procesador emite un mandato de E/S a petición de un proceso. Si la solicitud de E/S requiere suspender el proceso, este se suspende y se carga otro proceso en el procesador para ser ejecutado. Luego, el proceso actual es interrumpido por el mismo módulo de E/S cuando la solicitud haya sido satisfecha. En esta técnica, todavía se debía recuperar la información bloque a bloque, por lo que se debía interrumpir cada vez que se requiera transferir un fragmento, por lo que el procesador está altamente implicado en el control de la operación de E/S.

### Entrada Salida por Acceso Directo a Memoria (DMA)
Un módulo de DMA controla el intercambio de datos entre la memoria principal y el dispositivo de E/S. El procesador manda una petición de transferencia de un bloque de datos al módulo de DMA y resulta interrumpido sólo cuando se haya transferido el bloque completo. De esta manera, las operaciones de E/S son resueltas por el DMA y no por el procesador. Se optimiza el tiempo ocioso.

#### *Módulos de E/S*
Los módulos de E/S se convierten en un procesador independiente con un set de instrucciones específicamente pensadas para operaciones de E/S. De esta manera, el procesador central le indica al módulos o canal de E/S que ejecute un programa de I/O en memoria principal, de modo que el CPU ya no tiene que intervenir ni ocupar tiempo en estas operaciones. 

Más adelante, se incorporaron a estos módulos de E/S una memoria local propia, de form a que se pueda controlar una gran cantidad de dispositivos de E/S de manera independiente, con mínima intervención del CPU.



#### *Funcionamiento de la técnica*
Cuando el procesador desea leer o escribir un bloque de datos, emite un comando al módulo de DMA con la siguiente información:

- Tipo de operación (R/W).
- Dirección del dispositivo de E/S involucrado.
- Dirección inicial de memoria a leer o escribir.
- La cantidad de palabras a leer o escribir.

Luego, el procesador continúa con otro proceso. El DMA se encarga de transferir el bloque directamente de la memoria palabra por palabra sin necesidad de utilizar el procesador. Cuando la transferencia se completa, el DMA envía una señal de interrupción al procesador. De esta manera, el procesador solo está involucrado en el inicio y el fin de las operaciones de E/S



Por otra parte, el DMA utiliza el bus de datos del sistema para comunicarse con los dispositivos de I/O, y lo realiza mediante una E/S programada para cada palabra que transfiere. Esto implica dos ciclos de bus por cada palabra del bloque que se lea o escriba. Para solucionar este problema, varios sistemas implementan un bus de E/S que conecta los dispositivos directamente con el DMA, de modo que éste no interfiere en el bus del sistema para transferir palabras, sino únicamente para recibir comandos para iniciar una operación de E/S y para enviar la interrupción que indique el fin de la misma.


# **Discos Rígidos**
### ¿Por qué optimizar su rendimiento?
- La capacidad de proceso ha aumentado un 40% cada año, mientras que el rendimiento de los discos rígidos solo ha mejorado un 50% durante la última década. 
- Los discos RIGIDOS llegaron a un límite mecánico.
- En todo sistema la velocidad más lenta es la más determinante. 
- Son un cuello de botella.

### Estructura de un disco
A nivel lógico, es un arreglo de bloques consecutivos.

- *Pistas.* Círculos concéntricos sobre el plato donde se sitúa la cabeza lectora.
- *Cilindro.* Conjunto de pistas alineadas verticalmente en los distintos platos. Proyección en vertical de las pistas entre todos los platos.
- *Sector.* Subdivisión dentro de las pistas.
- *Bloque.* Mínima unidad de almacenamiento utilizada por el disco. Intersección pista/sector.
- *Cabezal.* Dispositivo que efectúa la lectoescritura.
- *Brazo.* Extensión mecánica que ubica el cabezal.

### Tiempo de lecto escritura (tiempo de acceso a datos)
Tacceso=Tbusqueda+Tlatencia+Ttransferencia

#### *Tiempo de búsqueda*
Tiempo de seek. Tiempo que tarda el cabezal lector en desplazarse desde la pista en la que está a la que corresponde leer.

Tbúsqueda=Tarranque+Tdesplazamiento

- El *tiempo de arranque* es el tiempo que tarda el cabezal en acelerar hasta llegar a una velocidad constante.
- Tdesplazamiento=Tcilindro\*Ncilindros El único tiempo mejorable por el sistema operativo. Es el tiempo que tarda en recorrer las pistas.

#### *Tiempo de latencia*
Tiempo que tarda el plato en girar para colocar el inicio del sector correspondiente debajo de la cabeza lectora.

Se estima como un promedio entre el mejor tiempo (cuando el cabezal se encuentra justo arriba del sector) y el peor tiempo (cuando el cabezal tiene que esperar toda una vuelta del plato para estar arriba del sector).

Tlatencia=Trotación2
#### *Tiempo de transferencia*
Tiempo que se tarda en leer el sector. 

Ttransferencia=Nbloques\*TrotacionMbloquescilindro= TrotacionSectores por pista

# **Algoritmos de scheduling de disco**
### FCFS
Primera solicitud en llegar, primera en ser satisfecha.

- *Ventaja.* El más justo desde el punto de vista del orden de llegada. Simple de implementar.
- *Desventaja.* Al no poder atender desordenadamente, una secuencia intercalada sobre anillo y orilla puede ocasionar demasiado movimiento en el brazo (que se pidan leer secuencialmente sectores muy lejanos).



### Shortest Service Time First puro
Primero la lectura más cercana, aquella que requiera el menor movimiento del brazo del disco desde su posición actual.

- *Ventaja.* Elimina el problema de exceso de desplazamientos del brazo, disminuye el tiempo de búsqueda. 
- *Desventaja.* Posibles solicitudes sin atender durante largos períodos de tiempo.

### SCAN
El brazo barre de anillo a orilla y satisface todas las peticiones que se encuentren en la ruta hasta que llega a la pista final del plato y realiza el recorrido en sentido contrario.

- *Ventaja:* No tiene las desventajas ni de FCFS ni de SSTF. Movimiento simple del brazo. 
- *Desventajas.* Una solicitud que cae por detrás del lector debe esperar 2 recorridos de la superficie atendiendo solicitudes (ida y vuelta). Cuando no hay más solicitudes hasta llegar a la orilla igual el brazo recorre los cilindros restantes.

### C-SCAN
Ídem SCAN, pero solo lee en un sentido y vuelve sin leer.

- *Ventaja sobre SCAN.* Como máximo se espera 1 recorrido de superficie leyendo.

### C-LOOK
Misma lógica que C-SCAN, pero no llega a la orilla sino a solicitud más cercana a ella, y luego vuelve.

### N-step-SCAN and FSCAN
Con las técnicas de SSTF, SCAN, C-SCAN y C-LOOK, si un proceso realiza continuamente en una pista, pueden monopolizar el dispositivo entero repitiendo peticiones en esa misma pista. 

N-step-SCAN segmenta la cola de peticiones de disco en sub colas de longitud N. Estas sub colas son procesadas una a la vez, usando SCAN. Mientras una cola está siendo procesada, las peticiones nuevas deben ser añadidas a otra subcola. 

Si existen menos de N peticiones al finalizar el SCAN, entonces todas son procesadas con el siguiente SCAN. 

Si N es muy grande, se asimila a SCAN.

Si N=1, se a simila a FIFO.

FSCAN es una política que utiliza dos sub colas. Cuando empieza el SCAN, todas las peticiones se encuentran en una sola cola, mientras la otra se encuentra vacía. Durante el SCAN, todas las nuevas peticiones son almacenadas en la otra cola.

# RAID
![[RAID]]

# Seguridad
- **“Seguridad”** es un concepto muy amplio, que va más allá de la informática. 
- Es un concepto instalado en la sociedad y está íntimamente relacionado con los riesgos. 
- **Seguridad es ausencia de riesgos.** Una medida de confiabilidad del Sistema de Computación (SC) relacionada, fundamentalmente a la garantía de la integridad del propio SC y de la capacidad de discriminar el acceso al mismo.
- Cuando decimos que una ciudad es segura o insegura, estamos hablando de una “medida” o “grado” de la ciudad en relación a los riesgos a los que uno se expone viviendo en ella. Riesgo, por ejemplo, de que te maten o te roben en la ciudad. 
- La seguridad es una medida de confiabilidad del sistema (en general, en sentido amplio).
  - Incluso el sistema “ciudad”, “casa”, “persona” tiene su medida en términos de seguridad. 
  - Así, podemos pensar en los riesgos en una casa e implementar mecanismos para mitigarlos. Por ejemplo: puerta con llave, alarma, rejas, un vigilante en la puerta, etc.
  - **Todos estos mecanismos intentan que nadie no autorizado entre a la casa.**
- Cuantos más mecanismos de seguridad tengamos, “más seguridad” tendremos menos riesgo.
- Los mecanismos de seguridad suman su efecto más que linealmente.
- La seguridad es una medida de confiabilidad que está dada por la suma de los efectos potenciales de los mecanismos de seguridad implementados (dado por el “eslabón más débil de la cadena”).
  - **Cualquier “amenaza” u oportunidad que no consideremos o no abordemos con nuestros mecanismos de seguridad constituye una “vulnerabilidad” para el objeto en cuestión.**
- El humano es el responsable de la seguridad. Decide qué riesgos quiere correr y cuánta seguridad quiere.
- La seguridad es una inversión.
# **Mecanismos a priori y a posteriori**
Hay mecanismos de seguridad que actúan a **priori** (alarma, puerta con llave, sistema antimisiles, etc.) que tratan de evitar el incidente de inseguridad.

Hay otros mecanismos que actúan a **posteriori** (seguro contra incendios), tratando de reparar el efecto ocasionado por el incidente.

Con todos ellos llegamos a cierto punto o nivel, **la garantía o “seguridad total” no existe. El riesgo siempre está. Tratamos de minimizarlo.**

# **Seguridad en sistemas de computación**
### Integridad
Cuando hablamos de **integridad**, nos referimos a la capacidad del sistema para hacer aquello para lo que está previsto (**funcionalidad**) y que esté disponible para hacerlo (**disponibilidad**).

### Control de acceso
Cuando hablamos del **Control de Acceso**, nos referimos a la capacidad de verificar que solamente acceda al sistema quien está autorizado para ello.

### Dimensión ambiental.
- Tanto la integridad como el control de acceso a un Sistema de Computación van más allá del sistema propiamente dicho. Tienen que ver, antes que nada, con aspectos ambientales. Por ejemplo, si instalamos el pc del servidor en la vereda.
- Esta dimensión tiene que ver con el acceso y cuidado de la integridad del sistema en su conjunto desde el punto de vista físico.
- En esta dimensión se incluyen inundaciones, problemas eléctricos, robos, etc.
- La seguridad es relativa al contexto. El contexto supone ciertos riesgos.
- La seguridad en general y, muy particularmente, en la dimensión ambiental *es un problema y responsabilidad estrictamente humana. El SO no es responsable del ambiente.*

### Dimensión de las aplicaciones
- Las aplicaciones, en tiempo de ejecución, pueden causar problemas de seguridad, atentando contra la integridad del sistema (caballos de troya, virus, gusanos, malware, por ejemplo).
- El SO debe, por sí o por terceros, implementar mecanismos de seguridad que mantengan la integridad del SC ante el potencial accionar de las aplicaciones (antivirus, firewalls, etc.).

### Dimensión del control de acceso de usuarios
- El SO debe brindar mecanismos efectivos que garanticen el acceso al Sistema de Computación exclusivamente de los usuarios habilitados al efecto.
- Dimensión más relevante.
- La responsabilidad por la seguridad, aún en estos aspectos, es siempre de gerenciamiento; siempre humana.
- **La administración de la seguridad NO ES responsabilidad del SISTEMA OPERATIVO (que solo debe proveer los medios o mecanismos),** sino que** es el administrador el que instala y actualiza antivirus (o no) y define el uso contraseñas de acceso (o no) u otros mecanismos brindados por el SO.
- **El nivel de seguridad de un sistema siempre es producto de una decisión humana.**

# **Gestión de la seguridad**
### Plano político
En el **plano político** se definen los grandes objetivos de la gestión (igual que en los ministerios gubernamentales).

- El plano político tiene que ver con el **qué** queremos lograr:
  - Reducir la desnutrición infantil.
  - Garantizar el acceso físico al sistema exclusivamente al personal habilitado.
  - Evitar incidentes que atenten contra la integridad del Sistema.
  - Disponer de los resguardos actualizados cada 24 horas.
  - Recuperar el sistema en menos de 24 horas ante un incidente.
- Decidimos dónde queremos pararnos en términos de seguridad. 
- Qué riesgo estamos dispuestos a correr y qué riesgos no. 
- Se definen los costos.
- El nivel de seguridad se define en la política en base a:
  - El efecto del riesgo (en caso de ocurrir). Cuánto prestigio se pierde si no se tiene en cuenta, pérdida de confiabilidad, etc.
  - Probabilidad de ocurrencia del riesgo.
  - El valor de la información en juego.
  - Costo de la política (no solo en $, sino también en usabilidad del sistema, etc.). Suele ser determinante.
- La Gerencia General decide la política dependiendo del análisis conjunto de estos factores y de la relación inversión vs. riesgo final. Luego, le ordena a la Gerencia de Sistemas que diseñe e implemente los mecanismos necesarios para garantizarla.
- Siempre en el plano de los mecanismos se deben prever algunos que actúen a priori (preventivos) y otros que actúen a posteriori (remediales), de forma tal de garantizar que ante un error en la prevención (todo puede fallar), el sistema se pueda recuperar

### Plano de los mecanismos
En el **plano de los mecanismos** se definen los instrumentos o medios que contribuirán a cumplir con la política definida.

- El plano de los mecanismos tiene que ver con el **cómo** vamos a lograr la política definida.
- Se pueden definir varios mecanismos que actúan concurrentemente y contribuyen a una política. 
- Es una relación N a 1. (N mecanismos – 1 Política).

### Plano de implementación
En el **plano de la implementación** se concretan los instrumentos o mecanismos definidos, por medio de una serie de decisiones y acciones concretas.

- Se llevan los mecanismos a la realidad.
- Puede haber cientos de alternativas para implementar un mismo mecanismo (deben cumplir el mismo objetivo).

# **Autenticación de acceso**
Para el **Control de Acceso** implementa la identificación y autenticación, que permite definir usuarios (en tiempo de registro de los mismos) e identificarlos y autenticarlos (en tiempo de acceso de los mismos al SC).
### Registro de usuarios
- Dar de alta usuarios y contraseñas en la tabla de usuarios (enrolamientos).
- La contraseña (como mecanismo de autenticación) que el usuario elige a la hora de su registro es encriptada por el sistema para su almacenamiento.

fk=kregistrada

- Se pueden registrar varios medios de autenticación (huella dactilar, iris del ojo, ADN, etc.). Mientras más mecanismos o medios de autentificación tengamos, la certeza que tenemos de que el usuario que pretende ingresar es quien dice ser es mucho mayor. 
- Se recomienda usar funciones unidireccionales (hash). No es conveniente que exista una función inversa a la función que encripta los medios de autenticación.

### Identificación de usuarios
Poder saber cuál es el usuario registrado que pretende ingresar al SC.
### Autenticación
Poder verificar si realmente el usuario que pretende ingresar al SC es quien dice ser (contraseña).

### Secuencia de acceso
1. Se solicita el nombre de usuario.
1. Se solicita la contraseña al usuario.
1. Se aplica la función de encriptación a la contraseña.
1. Se autentica.
   1. Se valida la existencia del usuario en la tabla.
   1. Se comparan los hashes de las contraseñas.
1. Se permite el acceso o no. No es conveniente indicar en qué fallo el login (si en usuario o en contraseña)

### Integridad
- El SO debe proveer mecanismos para garantizar la integridad del SC (firewalls) y delega a terceros la administración de la seguridad.
- Queda en manos del administrador de la seguridad, la incorporación de otros instrumentos preventivos al efecto que sean compatibles con el SC y no disminuyan el rendimiento notablemente.
- Como dijimos, no hay conjunto de mecanismos capaz de GARANTIZAR la seguridad total. 
- **El único mecanismo que puede brindar garantías de recuperación del SC cuando todos los mecanismos preventivos fallan, es el BACK UP.**
- El resguardo de la información del SC es clave a la hora de definir una política.









# **Protección**
- Cuando hablamos de *Seguridad*, hablamos de una medida de confiabilidad del Sistema de Computación (SC) relacionada, fundamentalmente a la garantía de la integridad del propio SC y de la capacidad de discriminar el acceso al mismo.
- Una vez que el usuario ingresó al SC (incluso habiendo cumplido adecuadamente la identificación y autenticación) tiene acceso a los recursos (e instancias de recursos) del SC para realizar sus operaciones, por medio de procesos. No todos los usuarios tienen los mismos permisos de acceso a los diferentes recursos. Aquí interviene la **PROTECCIÓN.**
- El rol de la protección es el de proveer un mecanismo para reforzar las políticas que gobiernan un recurso.

Cuando hablamos de **PROTECCIÓN**, nos referimos a un problema interno del SC, y tiene que ver con la capacidad de administrar los permisos de acceso y de uso de los recursos del SC por parte de los procesos.

- *Garantizar la Protección de un SC es administrar, conforme la política establecida, los privilegios que los procesos tienen sobre los recursos (e instancias) del SC.*
- Un sistema es una colección de procesos y recursos (hardware o software).
- Los recursos básicos (4) tienen una granularidad muy grande para ser susceptibles de asignar privilegios. Incluso si hablamos de instancias.
- Un proceso no puede tener tal o cual privilegio sobre “la información” como recurso, dado que es un recurso muy amplio y es conveniente asignar privilegios según una unidad menor (carpeta o archivo o celda de un archivo, por ejemplo). Si un proceso tuviese privilegios sobre un dispositivo de E/S por ejemplo, podría manipular TODA la información que maneje dicho dispositivo.
- Si la granularidad la hacemos muy fina, nos quedamos con una unidad de asignación de privilegios muy pequeña y, entonces, la asignación de privilegios es interminable.

# **Principio del mínimo privilegio**
A cada programa, usuario o sistema se le otorga los privilegios justos y necesarios para realizar sus tareas. Por ejemplo, si a un guardia se le asigna una llave para abrir solamente la habitación que debe cuidar, si pierde la llave entonces el daño es pequeño.
# **Objeto**
Un **Objeto** es cualquier componente del SC (hardware o software) que pueda ser identificado unívocamente (puede ser tanto un dispositivo, un directorio, un archivo, un archivo de datos, una fila dentro del archivo de datos, una columna o una celda, según convenga). Se le puede aplicar privilegios de acceso a un objeto.
### Cada Objeto tiene: 
- Un nombre único que lo identifica (Object Id.)
- Un conjunto de operaciones que puede realizar un proceso sobre él. Este conjunto está limitado por el objeto. Por ejemplo, una impresora se limita a imprimir.
- Si el administrador del SC puede definir los Objetos del mismo, tiene la flexibilidad necesaria para manejar la protección y definir las operaciones permitidas. 
### Derecho de acceso (Access Right, AR)
Es el permiso o privilegio que tiene un proceso para realizar una operación sobre un objeto.

### Estructura de un Dominio
- Un **Dominio** es un conjunto de procesos con iguales privilegios (derechos de acceso) sobre los mismos objetos.
- Decimos que el proceso opera en un dominio.
- Asociación *proceso-dominio*
  - *Estática.* El conjunto de objetos disponibles para un proceso es fijo durante la vida del proceso.
  - *Dinámica.* El proceso puede cambiar de dominio durante la ejecución
#### *Formas de definir un dominio*
- *Por usuario.* Cada usuario podría es un dominio. El cambio de dominio implica un cambio de usuario.
- *Por proceso.* Cada proceso es un dominio. El cambio de dominio ocurre cuando un proceso envía un mensaje a otro y espera una respuesta.
- *Por función-método.* El conjunto de objetos que pueden ser accedidos corresponde a las variables locales definidas en el procedimiento. El cambio de dominio ocurre cuando se invoca una función.* 

### Perfiles de usuario
- Los usuarios que comparten privilegios sobre determinados recursos se definen persistentemente en grupos denominados Perfiles.
- Procesos de usuarios que comparten un Perfil conforman, por defecto, un Dominio.
- Un Dominio de protección define un conjunto de objetos junto con sus derechos de acceso.




# **Matriz de protección de acceso**
Es un modelo o mecanismo que permite especificar distintas políticas, y definir e implementar un control estricto (tanto para asociación estática como dinámica) de los privilegios de acceso. 

Usualmente, es el usuario quien define los AR para un objeto. Por ejemplo, cuando un usuario crea un archivo, puede definir los accesos de R/W para los distintos dominios.
### Elementos de la matriz de acceso:
- Filas (Dominios).
- Columnas (Objetos).
- Celdas (AR que los procesos del dominio tienen sobre el objeto).
- Es 3D, dado que cada celda puede contener más de un AR (read/write/execute, etc.).

- La Matriz de acceso es un mecanismo flexible y autoprotegido. La misma matriz y los mismos dominios pueden ser objetos.
- Puede expandir la protección dinámicamente: Permite que determinados dominios agreguen o eliminen AR, es decir, existen dominios que tienen privilegios sobre otros dominios. 
- Al permitir cambios controlados de los valores de la matriz, se requieren operaciones especiales: 
  - *Owner de un objeto.* Cuando un dominio tiene el acceso de owner sobre un objeto, un proceso que se ejecute en ese dominio puede modificar los accesos que los demás dominios u objetos posean sobre ese objeto.
  - *Copy AR de un objeto a otro*. Por ejemplo, si D1 tiene un AR de read\* (el asterisco indica que puede copiarse) sobre el archivo F2, un proceso ejecutándose en el dominio D1 puede copiar ese AR a cualquier otra entrada referida a F2. Puede suceder que, si se copia el AR a otra entrada de F2, no se transfiera la copiabilidad, es decir, se copia AR y no AR\*. Existe la variante de cortar y pegar.




- *Control.* Si un dominio Di tiene control sobre otro dominio Dj, entonces Di puede modificar los accesos del dominio Dj (usualmente solo eliminar, no agregar).
 
- Transferencia de AR de un dominio a otro.
- Cuando un proceso quiere cambiar de un dominio a otro, se debe tratar a los dominios como un objeto. Un proceso del dominio D1 puede cambiar al dominio D2 si (D1, D2) contiene switch.


- Establecida la política de protección, el Administrador del SC debe configurar la Matriz (Mecanismo) para llevar adelante la política.
- La matriz, como objeto, debe ser protegida y debe asegurarse el uso correcto de la misma.
- El SO debe proveer los medios para implementar la matriz como mecanismo general de administración de la protección. 
- Hay diversas formas de implementar esta matriz, dependiendo del SO.
# **Implementaciones de la matriz de acceso**
### Tabla global
- La matriz se implementa como una tabla global en memoria.
- Es dinámica, muy grande y 3D (cada celda posee varios AR).
- Muy cara y difícil de administrar.
- Es rala (baja densidad de datos).
- Cada ocasión en la que un proceso quiere realizar una acción sobre un objeto, el SO debe acceder a la tabla para verificar si la operación requerida está permitida en su dominio.

### Listas de control de acceso (ACL)
- La matriz se puede descomponer en columnas. Tantas listas como objetos haya en el SC.
- Para cada objeto, una lista de control de acceso enumera los usuarios y sus derechos de acceso permitidos.
- Cada lista de objeto (ACL) tiene elementos del tipo dupla: **(*Dominio, AR).
- No se utiliza espacios muertos para guardar valores nulos de la matriz.
- Si quiero filtrar los AR de un dominio, tengo que recorrer las listas de todos los objetos (costoso). Es sencillo desde la perspectiva del objeto, no así del dominio.

















### Listas de capacidades (CL)
- Descomposición por filas de la matriz de acceso. Tantas listas como dominios haya en el SC.
- Especifica los objetos y las operaciones autorizadas para un proceso que opera en ese dominio.
- Cada lista de capacidades (CL) tiene elementos del tipo dupla: (Objeto, AR).
- Cada elemento de la lista se llama “capacidad”.
- Las CL son mantenidas y protegidas por el sistema operativo. Si todas las capacidades de un objeto están protegidas, entonces el objeto también lo está.















### Bits de protección - Unix
- Es una implementación para Archivos, generalizable a otros objetos.
- Consiste en agregar un atributo de 9 bits por archivo, que indican si el Dueño, Grupo u otros usuarios pueden Leer, Escribir o Ejecutar el archivo (Unix).

### ACL vs CL
- La ACL se corresponde con necesidades del usuario. Se carga cuando un proceso de un dominio solicita una operación sobre el objeto. Muchas listas cortas.
- La CL se utiliza para localizar información del proceso. Se carga cuando nace un proceso del dominio y quiere acceder a un objeto (debe tener la capacidad para realizar la acción). Pocas listas largas.
- La mayoría de los SSOO utilizan una combinación de ACL y CL. Cuando un proceso intenta a acceder por primera vez a un objeto, se busca en la lista de acceso. Si el acceso es denegado, ocurre una interrupción. Si el acceso es concedido, se crea y se asigna una capacidad al proceso para futuros accesos más rápidos. Luego del último acceso, se destruye la capacidad. Esta estrategia se utiliza en los sistemas MULTICS.

# **Seguridad y protección**
- La Seguridad y la Protección son dos aspectos complementarios en un SC que el ser humano debe administrar.
- En ambos casos, las definiciones en términos de política y administración son cuestiones propias de un profesional de la informática.
- El SO solo brinda herramientas para facilitar la administración.
- Se deben definir políticas que garanticen un equilibrio entre Seguridad y Protección en base al fin pretendido.


# Procesos y recursos
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
  - Por lo tanto, puede existir deadlock sin necesidad de implicar recursos de I/O. Por ejemplo, dos procesos se comunican y esperan recibir un mensaje del otro. Si un proceso envía un mensaje al otro, se queda en espera. El otro proceso envía el mensaje de respuesta y queda a la espera de otro mensaje. Si el mensaje de éste último se pierde, ambos procesos se quedan esperando una respuesta por parte del otro proceso.

# Deadlocks
![[Deadlock]]

# **Procesamiento concurrente**
- Dos procesos son concurrentes cuando se ejecutan de manera que sus intervalos de ejecución se solapan (multitarea pero no multiprocesamiento).
- Se denomina pseudoconcurrencia cuando la concurrencia es aparente al usuario, pero no se da efectivamente en el sistema. Por ejemplo, hay más procesos que procesadores y los procesos se intercambian el procesador en el tiempo.
- La concurrencia es real cuando efectivamente se ejecutan los procesos en paralelo, en distintos procesadores o núcleos.
# **Ventajas**
- *Compartir recursos físicos y lógicos.* Aprovechar los recursos de hardware limitados.
- *Acelerar los cálculos.* División de cálculos en procesos ejecutados en paralelo en múltiples procesadores.
- *Modularidad.* Facilita la programación, dividiendo las funciones del sistema en procesos separados.
- *Comodidad.* Facilita al usuario la posibilidad de realizar varias tareas a la vez.

# **Funciones del SO en cuanto a la concurrencia**
- El SO debe proporcionar servicios de creación y terminación de procesos (llamadas al sistema, Windows es createProcess/createThread).
- El SO debe ser capaz de seguir los procesos activos (PCB).
- El SO debe asignar y quitar varios recursos a los procesos activos. Por momentos, múltiples procesos quieren acceder al mismo recurso. Estos recursos incluyen:
  - *Tiempo de procesador.*
  - *Memoria.*
  - *Archivos.*
  - *Dispositivos de E/S.*
- El SO debe ser capaz de proteger los datos y los recursos físicos asignados a un proceso ante interferencias involuntarias de otros.
- Los resultados de un proceso deben ser independientes de la velocidad relativa a la que se realiza la ejecución de otros procesos concurrentes.
### Race Condition
Sucede cuando múltiples procesos o hilos leen y escriben datos de manera que el resultado final depende del orden de ejecución de las instrucciones de dichos procesos.

### Problemas típicos.
- *Productor – Consumidor.* Existen procesos que crean datos y los colocan en una zona o recurso compartido y otros que consumen dichos datos. Debe accederse de manera atómica al buffer de modo que no se solapen acciones. Se debe impedir que un productor no pueda agregar datos al buffer si está lleno y que el consumidor no remueva datos si está vacío.
- *Lectores – Escritores.* s Hay un área de datos compartida por un número de procesos. Hay un número de procesos que solo leen del área de datos (lectores) y un número de procesos que solo escriben en el área de datos (escritores). Las condiciones que se deben satisfacer son las siguientes:
  - Todos los lectores pueden leer a la vez.
  - Solo un escritor a la vez puede escribir en el área compartida.
  - Si un escritor está escribiendo, entonces no se puede leer.
- *Filósofos que cenan.* Existen 5 filósofos que se juntan a pensar y comer. Hay una mesa redonda con 1 plato de comida en el medio, 5 sillas, 5 platos y 5 tenedores. Cada filósofo necesita de 2 tenedores para comer. Cuando un filósofo quiere comer entonces, los filósofos que se encuentren a su izquierda y a su derecha no deben encontrarse comiendo, de lo contrario no podrá tener sus dos cubiertos. Notar que si todos los filósofos piden comer y toman el tenedor a su derecha y quedan a la espera del tenedor a izquierda, entramos en Deadlock.

- *Rendez-vouz.* 
# **Creación de procesos**
Durante su ejecución, un proceso puede crear varios procesos nuevos invocando llamadas al sistema. El proceso que crea es el **proceso padre**, y los creados se denominan **procesos hijos.** Los procesos mantienen el PID del proceso padre.

- *UNIX.* Sentencia fork copia el espacio de direcciones del original, y ambos procesos (padre e hijo) continúan la ejecución juntos.
  - Genera dos ejecuciones concurrentes en un programa (nuevo proceso, mismo programa).
  - El nuevo proceso empieza en una instrucción etiquetada L.
  - *JOIN.* Permite recombinar varias ejecuciones paralelas en una sola. La rama que ejecuta primero la instrucción JOIN termina su ejecución. Para saber el número de ramas que se deben reunir se usa un parámetro con JOIN (una variable entera no negativa que se inicializa con el número de ejecuciones paralelas a reunir).
- *Win32.* CreateProcess y CreateThread. 
\*

# **Condiciones de concurrencia**
- Aseguran que la ejecución concurrente brinde los mismos resultados que la ejecución secuencial. 
- Se debe determinar el conjunto de lectura y de escritura de una sentencia.
  - RSi=a1, a2, … , an  conjunto de lectura Si (variables de las cuales toma el valor para realizar alguna instrucción).
  - WSi=b1, b2, … ,  bn conjunto de escritura Si (variables que modifica).
- **Condiciones que se deben cumplir para asegurar la correcta ejecución concurrente de dos sentencias** S1 **y** S2**:**
  - RS1∩W(S2)= ∅  
  - WS1∩RS2= ∅  
  - WS1∩WS2= ∅  

### Representación mediante grafos
- Un grafo de precedencias es un grafo acíclico orientado cuyos nodos corresponden a sentencias individuales.
- Un arco de un nodo Si al nodo Sj significa que la sentencia Sj puede ejecutarse sólo cuando ha acabado Si

# **Interacciones entre procesos**
Podemos clasificar la interacción de los procesos mediante el grado de conocimiento de la existencia los unos de los otros.
### Independientes
- No conocen de la existencia de los otros. No tienen intenciones de trabajar juntos.
- Dos procesos son independientes cuando sus estados no son compartidos (no comparten ni secciones de memoria ni nada).
- **Competencia** por los recursos.
- Ejecución concurrente **determinística (diagrama de Gantt la describe)**
  - Reproducible
  - Puede detenerse y reiniciarse sin efecto adversos

### Cooperativos
Ejecución con un resultado no predecible (**no determinística**)
#### *Indirectamente conscientes unos de otros*
- Estos son procesos que no necesariamente se conocen entre sí por sus ID pero comparten el acceso a un objeto en común.
#### *Directamente conscientes unos de otros*
- Existen procesos que son capaces de comunicarse entre sí con los process ID y están destinados a trabajar juntos en alguna actividad.



# **Sección Crítica**
La ejecución concurrente que requiere **cooperación** entre procesos necesita mecanismos de **sincronización** y/o de **comunicación**.

- La **sección crítica** es un segmento de código que manipula un recurso compartido y debe ser ejecutado de forma atómica. Son las partes del código que pueden alterar el resultado de la ejecución de otro proceso.
  - Se asocia a un recurso algún mecanismo de gestión de exclusión mutua.
  - Solamente un proceso puede estar simultáneamente en la sección crítica de un recurso.
### La solución al problema de la sección crítica debe cumplir tres requisitos:
- Exclusión mutua**.* Solamente se permite que un proceso se ejecute en la sección crítica.
- Progreso**.* No debe ser posible que un proceso que solicite acceso a una sección crítica (se encuentra en la sección de entrada) sea postergado indefinidamente. Cuando ningún proceso esté en una sección crítica, cualquier proceso que solicite su entrada lo hará sin demora. El proceso que entre en la sección crítica no debe estar ejecutando en su “remainder section”.
- Espera limitada**.* Existe un límite, o límite, en el número de veces que otros procesos pueden entrar en sus secciones críticas después de una ha realizado una solicitud para ingresar a su sección crítica y antes de eso se concede la solicitud.

- *Cuando un proceso sale de la sección crítica, debe avisar y notificar a los demás.*
- *Los procesos no deben retener el recurso de la sección crítica.*
- No se pueden hacer suposiciones sobre la *velocidad relativa* de los procesos ni el número de procesadores.
- Un proceso permanece en su sección crítica durante un *tiempo finito.*

### Enfoques para manejar las secciones críticas en un SO
- *Kernel con desalojo.* Permite que un proceso sea desalojado cuando está corriendo en modo kernel. Mejor para sistemas operativos de tiempo real. Más complejo de implementar, se debe sincronizar el acceso a los datos del kernel.

- *Kernel sin desalojo.* No permite que un proceso sea desalojado cuando está corriendo en modo kernel. Un proceso en modo kernel solo dejará el procesador si sale del modo kernel, si es bloqueado o deja voluntariamente el control del cpu. Estos kernels están libres de condiciones de competencia en las estructuras de datos del kernel, dado que solo un proceso está activado en modo kernel a la vez (no lo deja salir hasta que cambie el modo).

# **Exclusión Mutua**
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

Supongamos dos procesos y dos semáfotos S y Q.  P0 ejecuta waitS y luego P1 ejecuta waitQ. Cuando P0 ejecute wait(Q), debe esperar a que P1 ejecute signal(Q) y pasará lo mismo cuando P1 ejecute waitS, debe esperar a que P0 ejecute signalS. **Deadlock.**
**
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














