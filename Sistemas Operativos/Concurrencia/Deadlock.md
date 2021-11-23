El **deadlock** o **interbloqueo** es un problema que afecta a [[Proceso|procesos]] concurrentes que utilizan recursos en un sistema.

Es una situación en el [[Sistemas de Computación]] donde un conjunto de procesos se encuentran bloqueados, cada uno de ellos esperando por un recurso que retiene otro proceso de ese conjunto.

Hay 4 condiciones simultáneas, necesarias y suficientes para que un deadlock ocurra:
1. [[Exclusión Mutua|Exculsión mutua]].
2. Retención y espera.
3. No apropiación.
4. Espera circular.

El **Deadlock** o **Interbloqueo** es un problema que afecta a *procesos* concurrentes que utilizan *recursos* en un sistema.

**Es una situación en el Sistema de Computación donde un conjunto de procesos se encuentran bloqueados, cada uno de ellos esperando por un recurso que retiene otro proceso de ese conjunto (quien lo está utilizando).**

Ningún proceso del conjunto puede avanzar en su ejecución, dado que todos están bloqueados en espera de un evento que debe ser determinado por otro proceso que también está bloqueado a la espera de un recurso.

Throughput tiende a cero, turn around y tiempo de espera tienden a infinito.

Un deadlock puede aparecer cuando se tiene un conjunto de procesos cada uno bloqueado en espera de un evento que sólo otro puede provocar. A esta situación se le conoce como *interbloqueo de comunicación*. Por ejemplo, en los sistemas de comunicaciones (como las redes), en donde dos o más procesos se comunican mediante el envío de mensajes. Un arreglo común es que el proceso A envía un mensaje de petición al proceso B y después se bloquea hasta que B envía de vuelta un mensaje de respuesta. Suponiendo que el mensaje de petición se pierde, A se bloquea en espera de la respuesta y B se bloquea en espera de una petición. Finalmente, se produce un deadlock.


### Condiciones para el Deadlock
Hay 4 condiciones simultáneas, necesarias y suficientes para que un Deadlock ocurra:

1. *Exclusión mutua.*
   1. Sólo un proceso puede usar un recurso cada vez. 
   1. Sólo los recursos no compartibles se ven involucrados en un Deadlock.

1. *Retención y Espera.*
   1. Un proceso solicita recursos no disponibles manteniendo asignados otros recursos (sin liberarlos). Espera por recursos que están en uso por otros procesos y por ende no libera los que tiene él asignados.
   1. Reteniendo algunos, espera por otros.
1. *No Apropiación.*
   1. Los recursos asignados no pueden ser arrebatados al proceso que los tiene; los libera voluntariamente (únicamente). Si no se diera esta condición, otros procesos podrían robar recursos a otros procesos.

1. *Espera circular.*
   1. Existe una serie de procesos en espera P0,  P1,  ... ,  Pn en la que todo Pi espera por un recurso retenido por Pi+1; y Pn espera por un recurso retenido por P0.
   1. Ejemplo: dos personas en una misma habitación quieren escribir una carta y necesitan papel, lápiz y luz.
      1. P1 tiene luz y lápiz, pero no tiene papel. P1 se encuentra a la espera de papel.
      1. P2 tiene luz y papel, pero no tiene lápiz. P2 se encuentra a la espera de lápiz.
      1. Ninguno de los dos continúa su tarea. Ambos mueren por inanición. Tiempo de turn arround tiende a infinito.


### Impresora – Caso puntual
El uso de colas (spooling) es una manera de lidiar con los dispositivos de E/S dedicados en un sistema de multiprogramación. Considere un dispositivo común que utiliza colas: una impresora. Aunque sería técnicamente sencillo dejar que cualquier proceso de usuario abriera el archivo de caracteres especial para la impresora, suponga que un proceso lo abriera y no hiciera nada durante horas. Ningún otro proceso podría imprimir nada (Deadlock).

En vez de ello, lo que se hace es crear un proceso especial, conocido como demonio, y un directorio especial llamado directorio de cola de impresión. Para imprimir un archivo, un proceso genera primero todo el archivo que va a imprimir y lo coloca en el directorio de la cola de impresión. Es responsabilidad del demonio, que es el único proceso que tiene permiso para usar el archivo especial de la impresora, imprimir los archivos en el directorio. Al proteger el archivo especial contra el uso directo por parte de los usuarios, se elimina el problema de que alguien lo mantenga abierto por un tiempo innecesariamente extenso.

El uso de colas no es exclusivo de las impresoras. También se utiliza en otras situaciones de E/S. Por ejemplo, la transferencia de archivos a través de una red utiliza con frecuencia un demonio de red. Para enviar un archivo a cierta parte, un usuario lo coloca en un directorio de la cola de red. Más adelante, el demonio de red lo toma y lo transmite.

## Representación de las asignaciones
### Grafo de asignación de recursos
Sirve para representar el estado de un sistema de asignación de recursos. Consta en un conjunto de vértices y aristas como todo grafo, pero el conjunto de vértices se encuentra dividido en dos tipos de nodos: Los nodos que representan procesos activos P y los nodos que representan todos los recursos del sistema diferenciándolos por su tipo R convención de Silberschatz.

Muestra:

- Cuántas instancias hay de cada tipo de recurso.
- Los procesos activos en el sistema.
- Qué recursos (instancias) están asignados y a qué procesos.
- Qué procesos están bloqueados y por cuáles recursos.

#### *Construcción*
- *Círculos:*  Procesos.
- *Cuadrados:* Recursos.
- *Un arco* P→ R*  indica una solicitud aún no satisfecha (proceso bloqueado en espera del recurso). **REQUEST**
- *Un arco* R→ P  indica que ese recurso (instancia) está asignado a ese proceso. **ASSIGNMENT**
- *Ciclo en el grafo:* Posible deadlock. **Si cada recurso posee una sola instancia, entonces el ciclo implica un Deadlock.**

## Opciones de abordaje
1. Permitir la aparición de deadlocks y recuperarse cuando ocurran (Detección y Recuperación)
	1. Permitir que ocurra el Deadlock y luego salvarlo.
	2. Se requiere de un sistema de detección y de un mecanismo de recuperación.
2. Garantizar que nunca ocurran deadlocks
	1. Evitación: tratar de no caer nunca en un deadlock. Evitar una de las condiciones necesarias y suficientes.
	2. Prevención: diseñar el sistema de manera que nunca se cumpla alguna de las cuatro condiciones del deadlock.
3. Hacer caso omiso al problema
	1. Si hay deadlock, el usuario tiene que darse cuenta y resolverlo.


## Detección y recuperación
### Detección del deadlock
El interbloqueo se puede detectar comprobando si existe una secuencia de terminación de procesos (similar a la sec. segura). Es un proceso que consume recursos.

Sea L la lista de procesos del sistema y R el conjunto de recursos disponibles.

1. Buscar en L un proceso que puede continuar con los recursos disponibles en R.
1. Si no se encuentra ningún proceso, ir al paso 5.
1. Suponer que P termina (lo retiramos de L) y que libera los recursos que retiene (los añadimos a R).
1. Volver al paso 1.
1. Si L no está vacía, hay interbloqueo.

### Recuperación del deadlock
Un sistema que pretenda recuperarse del deadlock, debe invocar a un algoritmo de detección cuando lo considere oportuno (ej. periódicamente). Tener en cuenta la inanición y el reinicio infinito de un proceso (mato y lo vuelvo a instanciar infinitamente).

#### *Formas de intentar la recuperación:*
1. *Terminación de procesos.* 
   1. Matar todos los procesos implicados en el deadlock, que ya son conocidos por la detección.
2. Matar de a un proceso hasta romper el deadlock. ¿Cuál elegir?
      1. El que más recursos libere.
      2. El que menos tiempo lleve en ejecución. Si mato un proceso que lleva mucho tiempo, reiniciarlo será más costoso.
      3. Se debe llamar a un método de detección de deadlock inmediatamente después de matar un proceso para decidir si continuar con la terminación de procesos o no.
3. Retrocediendo la ejecución de algún proceso (rollback)
      1. Muy complicado de implementar y debe diseñarse los programas para que éstos puedan retroceder (implementar puntos de rollback, transacciones, etc.).

1. *Expropiación de recursos.*
   1. *Selección del proceso víctima.* ¿Qué recursos y de qué proceso se expropian? Se debe reducir el impacto general.
   2. *Retroceso.* Si expropiamos un recurso de un proceso, ¿Qué hacemos con ese proceso? Si el proceso no está preparado para rollback, estaríamos matando al proceso por completo.
   3. *Puede suceder, en un sistema que elija el proceso víctima como el que menos costo genere, que éste muera por inanición por ser siempre elegido como víctima.* Se puede solucionar llevando un contador y definiendo un número máximo de veces que el proceso puede ser elegido como víctima.
## Garantizar la no ocurrencia del deadlocks
### Evitación del deadlock (algoritmo del banquero)
- Se trata de conceder los recursos sólo cuando no representen un riesgo futuro de interbloqueo (los bancos dan préstamos solo cuando tienen garantía de que éstos serán pagados a futuro).
- Lo procesos han de declarar por anticipado la cantidad máxima de instancias de cada recurso que van a utilizar a lo largo de su vida.
- Sistema de computación en estado Seguro o Inseguro.
- Es un proceso costoso y difícil de implementar.
- Garantiza riesgo 0 de deadlock.
- Se necesitan varias estructuras de datos:
  - *Disponibles.* Vector que indica la cantidad disponible de cada recurso.
  - *Matriz de máximos.* Matriz que indique la cantidad máxima de instancias de cada recurso para cada proceso.
  - *Matriz de Alocación.* Indica la cantidad de cada recurso asignada a cada proceso.
  - *Matriz de necesidades.* Indica la cantidad de recursos restantes que cada proceso puede solicitar.

#### *Estado seguro*
Estado en el cual no hay riesgo inminente de deadlock. Un estado es seguro si en él podemos encontrar una **secuencia segura** con todos los procesos del sistema.

- {P1,  P2,  ...,  PN} es una **secuencia segura** si los recursos que Pi puede pedir en el peor caso se pueden atender con lo que hay disponible más los recursos retenidos por todos los procesos Pj, j\<i
- Sólo concedemos recursos si el estado resultante tras la petición es seguro. El sistema simula que le está prestando el recurso al proceso y se asegura que el estado en el que queda el sistema de computación sea un estado seguro.
- Si el nuevo estado no es seguro, el proceso queda bloqueado aunque existan recursos suficientes para atender la petición.
#### *Secuencia segura*
- Nos ponemos en el peor caso del sistema: que todos los procesos soliciten al mismo tiempo el máximo de recursos a los que tiene derecho.
- El primer proceso de la secuencia es uno que podría finalizar en ese peor caso, con los recursos disponibles en el sistema.
- El segundo proceso es uno que puede finalizar con lo que hay disponible más los recursos que liberaría el primer proceso.
- De la misma forma, los siguientes procesos pueden finalizar con los recursos que han liberado los anteriores en la secuencia.
- Y si todos los procesos pueden terminar, es que no hay o no habrá deadlock. Podemos satisfacer la petición con seguridad.

### Prevención del deadlock
Se trata de eliminar la aparición de alguna de las cuatro condiciones necesarias para el Deadlock, dado que **son necesarias y suficientes**.

- *Exclusión mutua.* Depende de la naturaleza del recurso, así que esta condición no se puede eliminar.

- *Romper retención y espera. Hay que garantizar que un proceso no pueda quedar bloqueado si retiene algún recurso. ¿Cómo conseguirlo?
  - El proceso tiene que pedir todos sus recursos de una vez, p.ej. antes de empezar a ejecutarse. De esta manera el proceso nunca se bloqueará por espera de un recurso.
    - *Efecto negativo*. Muchos recursos retenidos, pero no usados. Puede suceder que, dependiendo del flujo de ejecución, no utilice uno o más de uno de los recursos que tiene asignado. **Mayor consumo de recursos.**
  - Un proceso sólo puede solicitar recursos cuando no tiene ninguno asignado. Cuando un proceso solicita un recurso, debe liberar todos los que tiene asignados y pedir ahora en una nueva transacción los recursos que acaba de liberar y el nuevo que quiere obtener. Si todos los recursos no están disponibles, no se le asigna ninguno, pero no queda reteniendo ninguno. Espera, pero no retiene.
    - *Efecto negativo:* puede ocurrir que tengamos que liberar un recurso y volver a pedirlo para poder solicitar otros recursos.
  - En ambos casos: inanición. Un proceso se queda con todos los recursos y los demás procesos tendrán que esperar.

- *No expropiación. Permitir que el SO desasigne recursos a un proceso bloqueado.
  - Si un proceso se bloquea por un recurso, los recursos retenidos quedan a disposición de los procesos activos
  - El proceso bloqueado tiene ahora que esperar por todos los recursos.
  - Penaliza a los procesos que necesitan muchos recursos.
  - Es posible seguir este protocolo en recursos cuyo estado se puede guardar fácilmente y después restaurarse (registros de CPU, espacio de memoria donde la posibilidad de rollback existe, etc.). Generalmente no puede aplicarse a recursos tales como impresoras y unidades de cinta, no puedo interrumpir una impresión, dado que sería abortar completamente el proceso.

- *Espera circular. Se puede evitar forzando un orden en la petición de los recursos.
  - Cada recurso tiene asignado un número de orden.
  - Los recursos se deben pedir en orden ascendente.
  - Aconsejable: que el orden de petición de los recursos se establezca según el orden de uso normal de los recursos de un sistema. Establecer una jerarquía de recursos (impresora, memoria, escáner). Primero se debe pedir jerarquía 1 y luego 2 y 3 etc. No se puede solicitar un recurso de un orden menor de jerarquía. 
  - Obliga a definir una jerarquía que a priori se desconoce.
  - *Efectos negativos:*
    - Se limita la libertad de escritura de código. El programador debe conocer la jerarquización de los recursos para realizar las peticiones y debe pedirlos sí o sí de esa manera, aunque la secuencia del código no sea la ideal.
    - Se puede inducir a una mala utilización de los recursos. 
    - Un cambio en la categorización implicaría que todos los procesos que corren a partir de un código escrito con otra categorización quedan obsoletos.

### Algoritmo del Avestruz (Hacer caso omiso al deadlock)
Agachar la cabeza y no hacer nada. El usuario debe intervenir y decidir cómo sale del deadlock.

Depende de la frecuencia de ocurrencia de un deadlock y del costo que implica recuperarse del deadlock. En un sistema con miles de procesos, el algoritmo del banquero es infinitamente costoso por la cantidad de procesos.

Solo se justifica la prevención de deadlocks en sistemas mono propósito o autogestionados, como pueden ser los embebidos o un satélite.

Por ejemplo, en Windows, cuando una tarea no responde y es indicado (Windows detecta el deadlock pero no lo resuelve) y tenemos que ir nosotros a matar la tarea al administrador de tareas. 