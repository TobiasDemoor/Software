---
aliases: ["memoria virtual"]
---
Memoria virtual es una técnica de administración de memoria que permite la ejecución de procesos que no están completamente cargados en memoria (rompe el principio de completitud).

Todas las referencias a memoria serán direcciones lógicas que se traducirán dinámicamente a direcciones físicas durante la ejecución (realocación dinámica).

Un [[proceso]] puede dividirse en varias partes y no es necesario que todas estas partes estén en la memoria ppal. durante la ejecución. Es decir, no será necesario que estén todas las páginas o segmentos del proceso cargadas en memoria en tiempo de ejecución.

La memoria virtual es una memoria situada en disco (área de swap) y permite una multiprogramación más eficiente.

## **Ventajas**
- Se cargan sólo algunos fragmentos de cada proceso, solo los que son requeridos. Proceso de Swapping más eficiente. 
- Se pueden mantener más procesos en la memoria principal (Mayor a N).
  - Con tantos procesos en la memoria principal es muy probable que uno de los procesos esté en estado Listo en un instante determinado (menos tiempo ocioso).
- Es posible ejecutar procesos más grandes que el tamaño de toda la memoria principal. El tamaño máximo de proceso es prácticamente infinito (limitado por el almacenamiento secundario).

## **Fallo de acceso**
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


## **Técnicas de gestión de Memoria virtual**
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
- Baja [[performance]].


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
- Para solventar esto, se establece un valor máximo para el grado de multiprogramación, de modo que al superarse el mismo se entiende que el proceso entró en Trashing, por lo cual, para aumentar el % de [[uso del procesador]], se debe decrementar el grado de multiprogramación. Con esta técnica, cuando un proceso entra en trashing, no se le permite sacar frames a otros procesos.



## **Segmentación paginada**
La paginación tiene una serie de ventajas sobre la segmentación tales como la eliminación de fragmentación externa y la posibilidad de implementar algoritmos sofisticados y eficientes para la gestión de swapping de páginas, dado que éstas son de tamaño fijo. Por otro lado, la segmentación también tiene lo suyo: permite gestionar estructuras crecientes de datos, modularidad entre los mismos, y brinda soporte para el uso compartido de segmentos y la protección de los mismos (solo lectura para code segment, lectura-escritura para ds, etc.).

Por otro lado, en los sistemas modernos, el espacio de direcciones lógicas es sumamente mayor en tamaño al espacio de direcciones físicas, por lo que los programas y los segmentos del usuario pueden ser mucho más grandes que la memoria. Es por ello, que los segmentos pueden no caber en la memoria principal. Una solución a este problema es paginar los segmentos.
### Estructuras necesarias
En una estructura de segmentación paginada, el espacio de direcciones del usuario se encuentra dividido en segmentos definidos por el mismo, por lo cual se requiere una tabla de segmentos. A su vez, cada segmento está dividido (por el SO) en una cantidad de páginas de tamaño definido, por lo que se necesita una tabla de páginas para cada segmento. 

Cuando un proceso particular está corriendo, un registro mantiene la dirección de comienzo de la tabla de segmentos para ese proceso:

- Cuando se presenta una dirección lógica, el procesador utiliza el número de segmento para hallar la entrada en la tabla de segmentos del proceso y así encontrar la tabla de páginas para ese segmento. 
- Luego, el número de página de la dirección lógica es usado para ingresar a en la tabla de páginas del segmento y buscar el número de frame correspondiente. 
- Por último, se combina el número de frame con el offset para ingresar a la memoria física.
