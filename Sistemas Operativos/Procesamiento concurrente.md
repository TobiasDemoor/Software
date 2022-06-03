- Dos procesos son concurrentes cuando se ejecutan de manera que sus intervalos de ejecución se solapan (multitarea pero no multiprocesamiento).
- Se denomina pseudoconcurrencia cuando la concurrencia es aparente al usuario, pero no se da efectivamente en el sistema. Por ejemplo, hay más procesos que procesadores y los procesos se intercambian el procesador en el tiempo.
- La concurrencia es real cuando efectivamente se ejecutan los procesos en paralelo, en distintos procesadores o núcleos.
 
## **Ventajas**
- *Compartir recursos físicos y lógicos.* Aprovechar los recursos de hardware limitados.
- *Acelerar los cálculos.* División de cálculos en procesos ejecutados en paralelo en múltiples procesadores.
- *Modularidad.* Facilita la programación, dividiendo las funciones del sistema en procesos separados.
- *Comodidad.* Facilita al [[usuario]] la posibilidad de realizar varias tareas a la vez.

## **Funciones del SO en cuanto a la concurrencia**
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
- *Filósofos que cenan.* Existen 5 filósofos que se juntan a pensar y comer. Hay una mesa redonda con 1 plato de comida en el medio, 5 sillas, 5 platos y 5 tenedores. Cada filósofo necesita de 2 tenedores para comer. Cuando un filósofo quiere comer entonces, los filósofos que se encuentren a su izquierda y a su derecha no deben encontrarse comiendo, de lo contrario no podrá tener sus dos cubiertos. Notar que si todos los filósofos piden comer y toman el tenedor a su derecha y quedan a la espera del tenedor a izquierda, entramos en [[Deadlock]].

- *Rendez-vouz.* 
## **Creación de procesos**
Durante su ejecución, un proceso puede crear varios procesos nuevos invocando llamadas al sistema. El proceso que crea es el **proceso padre**, y los creados se denominan **procesos hijos.** Los procesos mantienen el PID del proceso padre.

- *[[UNIX]].* Sentencia fork copia el espacio de direcciones del original, y ambos procesos (padre e hijo) continúan la ejecución juntos.
  - Genera dos ejecuciones concurrentes en un programa (nuevo proceso, mismo programa).
  - El nuevo proceso empieza en una instrucción etiquetada L.
  - *JOIN.* Permite recombinar varias ejecuciones paralelas en una sola. La rama que ejecuta primero la instrucción JOIN termina su ejecución. Para saber el número de ramas que se deben reunir se usa un parámetro con JOIN (una variable entera no negativa que se inicializa con el número de ejecuciones paralelas a reunir).
- *Win32.* CreateProcess y CreateThread. 
\*

## **Condiciones de concurrencia**
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

## **Interacciones entre procesos**
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



## **Sección Crítica**
La ejecución concurrente que requiere **cooperación** entre procesos necesita mecanismos de **sincronización** y/o de **comunicación**.

- La **sección crítica** es un segmento de código que manipula un recurso compartido y debe ser ejecutado de forma atómica. Son las partes del código que pueden alterar el resultado de la ejecución de otro proceso.
  - Se asocia a un recurso algún mecanismo de gestión de [[exclusión mutua]].
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

## **Exclusión Mutua**
![[Exclusión Mutua]]