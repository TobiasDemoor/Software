El procesador es el recurso más utilizado demandado, dado que permite la ejecución de los procesos.

Un [[proceso]] es un **[[programa]] en ejecución**. Es la unidad de procesamiento del SO (la del usuario es la [[Tarea]]).

La taza o flujo de ejecución del proceso es la secuencia de instrucciones que se ejecutan para dicho proceso. No necesariamente se ejecutan de manera consecutiva, pueden existir bucles, ramas condicionales, etc., por lo que **no es posible saber a priori observando el código del programa cuál va a ser el flujo de ejecución del proceso**, dado que puede variar en tiempo de ejecución dependiendo de la información que dicha ejecución posea. Solo se puede saber cuando el proceso finaliza. NO HAY DOS PROCESOS IGUALES.

- Los procesos se identifican con un Process Id. (PId.)
- Un proceso ejecuta un código.
- El sistema operativo almacena información de la ejecución en la pila. Es una estructura de datos administrativa del SO que refiere al proceso y que le sirve para mantener toda la información de ejecución de ese proceso. 
- Procesa datos externos, los cuales deben ser almacenados en memoria.
- Proceso = Pid + Código + Pila + Datos + Atributos (indicadores de gestión).

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

## Atributos de un proceso
- Process Id. 
- TimeStamp de inicio (fecha y hora)
- Usuario que está ejecutando el proceso
- PC para saber la instrucción que se está ejecutando
- Punteros a las diferentes secciones de memoria.
- Prioridad relativa a otros procesos.
- Datos de contexto. (registros del procesador, entre otros)
- Estado de E/S, tal como dispositivos asociados al proceso, una lista de archivos usados por el proceso, etc.
- Información de uso de procesador.

## Creación de procesos 
- Lo crea el SO a solicitud de un usuario.
- Lo crea el SO en un sistema Batch, donde los procesos se van creando secuencialmente sin intervención del usuario.
- Lo crea otro proceso.
- Se crea para ofrecer un servicio, como, por ejemplo, la impresión.
- Procesos “hijos” (un proceso crea otro proceso y le cede el control) y “hermanos” (un proceso crea otro proceso a la par de si mismo y ejecutan concurrentemente, como el editor de Word con el corrector). El usuario siempre ve los conjuntos de procesos como uno solo y los llama tarea.

### *La creación de un proceso requiere*
1. Darle un Pid.
1. Crearle una entrada en la tabla de procesos.
1. Asignarle memoria al código (proceso de carga en memoria).
1. Crear su pila en memoria.
1. Cargar sus datos (crear su bloque de control de proceso).
1. Setear sus atributos.
1. Dejarlo “Listo” para ejecutar.

### *Process spawning*
Fenómeno que sucede cuando el SO crea un proceso a petición explícita de otro proceso.

## Finalización de procesos
### *Un proceso puede terminar*
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

### *La finalización de un proceso requiere*
1. Liberar todos los recursos asignados a él.
1. Liberar la memoria ocupada por el proceso.
1. Eliminar su entrada en la tabla de procesos (última acción).

## Estados de un proceso
Los estados de un proceso se refieren a la situación del proceso dentro del sistema de computación

- *Nuevo.* El proceso está siendo creado y tiene una entrada en la tabla, pero no tiene memoria asignada.
- *Listo.* El proceso está en condiciones de ocupar el procesador, pero se encuentra a la espera de la asignación del mismo. Son todos los que compiten por el procesador.
- *En ejecución.* El proceso está montado en el procesador avanzando en su flujo de operaciones.
- *Terminado.* El proceso se encuentra liberando sus recursos (etapa de finalización).
- *Bloqueado.* El proceso solicita una e/s y es bloqueado para que no ocupe tiempo muerto en el procesador. Para mejorar la eficiencia a la hora de reanudar un proceso que previamente ha sido bloqueado, existe una cola de procesos bloqueados por cada evento. De esta manera, el SO no debe recorrer toda la cola de procesos bloqueados preguntando a ver cuál de todos completó la operación por la cual fue bloqueado, sino que cuando el evento ocurre, la totalidad de la cola de procesos bloqueados referidos a ese evento pueden ser transferidos a la cola de procesos listos para ejecutar.

Si el despacho de procesos está dictado bajo un esquema de prioridades, sería conveniente tener una cola de procesos Listos para cada nivel de prioridad definido.

## **Process swaping: Procesos en suspensión**
El procesador trabaja a una velocidad extremadamente mayor que los dispositivos de E/S, por lo que no sería descabellado tener una situación en la cual el procesador se encuentre inactivo dado que todos los procesos que se encuentran en memoria estén a la espera de una operación de E/S. No es una solución viable expandir la memoria principal para manejar más procesos, dado que, en ese caso, los procesos solicitarían más memoria dado que hay mayor cantidad disponible. La solución es mover parte de todos los procesos desde la memoria principal a la memoria secundaria. Cuando ninguno de los procesos que se encuentran en memoria principal están en el estado Listo, el SO mueve uno de los procesos bloqueados a una cola de procesos suspendidos en la memoria secundaria. Luego, el SO trae a memoria un proceso de dicha cola de suspensión o uno nuevo que se encuentre listo para ejecutar. Como el swap es una operación de E/S de disco, puede empeorar el problema.
## **Estructuras de control del SO**
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
- Cualquier información necesaria para gestionar la [[memoria virtual]].

### Tablas de E/S
- Un dispositivo de E/S puede estar disponible o estar asignado a un proceso en particular.
- Almacena el estado de la operación de E/S.
- Posición de memoria principal que se está utilizando como origen o destino en la transferencia de E/S.

### Tablas de archivos
- Ofrecen información sobre la existencia de los archivos.
  - Posición en la memoria secundaria del [[archivo]].
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

## **Estado del procesador**
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

## **Context Switch**
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