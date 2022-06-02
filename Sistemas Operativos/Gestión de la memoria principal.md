La memoria es uno de los recursos básicos del Sistema de Computación. Necesitamos gestionarla para hacer un uso eficiente de ella (que no haya memoria ociosa) y alojar la mayor cantidad de procesos posibles (grado de multiprogramación). **Esto mejora potencialmente el % de uso efectivo del procesador, dado que el mismo siempre tendrá procesos para ejecutar.**
**
La memoria principal y los registros del procesador son las únicas unidades de almacenamiento a las que el CPU puede acceder de manera directa. Para los registros, solo basta con un ciclo de reloj, mientras que para el acceso a memoria se requieren dos o más ciclos de reloj. Para solventar esta situación, se añaden memorias caché (más veloces que la principal) intermedias entre el procesador y la memoria principal, la cual actúa como buffer de memoria.

La administración de memoria central es la función del sistema operativo que lleva el registro de cuáles partes de la memoria están en uso, asigna memoria a los procesos cuando la precisan y los desaloja cuando terminan. Cuando se requiere que un sistema albergue más de un [[Sistemas Operativos/Conceptos/Proceso]] en memoria, se deben adoptar políticas de administración de la memoria, debiéndose implementar medidas de [[protección]] para que un proceso no viole el espacio asignado a otro y establecer criterios para asignar el espacio a los procesos a cargar.
## **Fragmentación**
Es la cantidad de memoria ociosa (no utilizada efectivamente), esté disponible o no.

- Si esa memoria no utilizada está asignada a un proceso, entonces solo él puede usarla. Si no la usa: **Fragmentación interna.** Ningún otro proceso la puede utilizar
- Si esa memoria no utilizada no está asignada a ningún proceso, entonces estará disponible para su uso: **Fragmentación externa.**
## **Indicadores**
- *Grado de multiprogramación (N) ↑*

- *Tamaño máximo del proceso (N) ↑*

- *Fragmentación interna (FI) ↓*

- *Fragmentación externa (FE) ↓*

Se deben verificar además los mecanismos de garantías de la protección, para evitar que un proceso no acceda a un área de memoria de otro proceso sin el permiso necesario. Permite garantizar el uso adecuado de los recursos.

## **Cuestiones a considerar**
El programador no sabe dónde se alojará el código de su programa en cada ejecución y tampoco conoce qué otros programas (código) residirán en la memoria en el momento de ejecución.

Es imposible, entonces, comprobar las direcciones absolutas de los programas, puesto que se desconoce la ubicación de ese código en la memoria principal.

## **Vinculación de direcciones**
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

## **Traducción de direcciones lógicas a físicas**
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

## **Intercambio**
El pasaje de procesos de memoria al dispositivo de almacenamiento secundario (backing store) se llama Swap Out.

El pasaje de procesos del dispositivo de almacenamiento secundario a la memoria se llama Swap in.

El conjunto de Swap Out y Swap In se lo conoce como Swapping.


## **Principios de gestión de la memoria**
### Principio de continuidad
Dice que un proceso debe cargarse contiguo en memoria (en direcciones consecutivas).
### Principio de completitud
Dice que un proceso debe cargarse completo en memoria.

## **Maquina desnuda**
En los principios de la computación, hasta 1960, no había [[sistemas operativos]]. La memoria era una sábana de celdas contiguas sin división física ni lógica.

No había soporte para la gestión de la memoria. El proceso debía controlar los dispositivos.

El programador, administrador y usuario eran la misma persona y era quien administraba los recursos.
## **Monitor Residente**
Fue el primer esquema de un gestor de acciones y recursos. Se encargaba del secuenciamiento de tareas, la gestión de los dispositivos y algunas rutinas que eran de uso recurrente. Debía conocer los dispositivos y saber cómo funcionaban.

Fue necesario dividir la memoria para evitar que el proceso de usuario no escribiera sobre el monitor residente: surge la cuestión de la protección y el Registro FENCE, el cual almacena la dirección base del proceso.

## **Swapping superpuesto**
Tiene como objetivo optimizar el tiempo de carga y descarga de los procesos (tiempo muerto). Se divide la memoria en tres regiones iguales. Mientras en una región está el proceso que se está ejecutando, en otra región está el proceso que se está descargando, y en la tercera región está el proceso nuevo, que se está cargando. (Similar a PIPE-LINE arquitectura de computadoras).

Siempre hay solo un proceso en ejecución: multiprogramación, pero monotarea.

### Ventaja
Se superponen los procesos de carga, descarga y ejecución (se ejecutan concurrentemente), entonces, se eliminan los tiempos muertos de procesador mientras se cargan y descargan los procesos. El procesador siempre está ocupado corriendo un proceso de usuario.
### Desventajas
El tamaño máximo del proceso se reduce a un tercio de la memoria física disponible para procesos de usuarios.

Además, se produce fragmentación interna en cada división.

## **Múltiples particiones de tamaño fijo (MFT)**
Si el proceso requiere una E/S en el modelo de Swapping, el procesador se queda esperando a que se complete dicha operación. Por ello, se desarrolló otra metodología que resulta de la evolución de la anterior.

En el modelo MFT, se divide la memoria en particiones o regiones de igual tamaño (fijo) que alojan diferentes procesos en ejecución (aparece la multitarea).

En cualquier partición libre puede cargarse cualquier proceso cuyo tamaño sea menor o igual que el tamaño de la partición.

- La cantidad y tamaño de particiones son declaradas al momento de generar el sistema.
- El uso de la memoria es ineficiente, cualquier programa, sin importar lo pequeño que sea, ocupará una partición completa, generando fragmentación interna.
- El tamaño máximo de proceso es el tamaño de la partición.
  - Las particiones pueden ser todas iguales o diferentes entre sí, pero su tamaño es fijo. Si son todas iguales, con una sola cola es suficiente para cargar los programas en memoria.
  - Si las particiones son diferentes, conviene implementar múltiples colas, para que cada proceso compita por la región en la que mejor ajusta y con mayor tamaño máximo, pero puede darse el caso de que un proceso pequeño esté esperando en la cola mientras existe una partición de mayor tamaño que esté en desuso.

## **Múltiples particiones de tamaño variable (MVT)**
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

## **Paginación**
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
- El SO tiene una tabla propia cargada en registros asociativos (Hardware) donde se mapea la tabla de páginas del proceso actual, en tiempo de context Switch, para mayor [[performance]].
  - El hecho de tener una tabla de páginas en hardware es útil para procesos cuya tabla de páginas sea pequeña. En otros casos, la tabla de páginas se almacena en la memoria principal, y se posee un registro que indica la dirección base de la misma. 
  - Al realizar un context Switch, en cuanto a la tabla de páginas, solo debe actualizarse este registro, por lo que se reduce el tiempo requerido, pero para acceder a la tabla de páginas se requiere acceder a memoria principal (más lenta, y requiere un acceso para obtener el número de frame y otro para ir al frame en sí).

Para solucionar este problema, se utiliza un buffer de traducción anticipada *(Translation Look-aside Buffer)* cuando se utiliza [[memoria virtual]].


#### *Estructura de un nivel*
Tomando una dirección lógica en la que los primeros n bits son el número de página y los m restantes son el desplazamiento: 

1. Primero se extrae el número de página como los n bits más significativos de la dirección lógica. 
1. Se usa el número de página como un [[Índice]] en la tabla de páginas del proceso para encontrar el número de frame, k.
1. La dirección física de comienzo del frame es k \* tamaño de página, y la dirección física del byte referenciado es ese número más el desplazamiento.



#### *Estructura jerárquica de dos niveles*
En los sistemas modernos, el espacio de direccionamiento lógico es muchísimo más grande que el espacio de direccionamiento físico de la memoria, por lo que las tablas de páginas son excesivamente grandes y deben ser paginadas. Ahora, si suponemos una dirección lógica de 32 bits de los cuales 20 referencian al número de página y 12 al offset, el número de página consta de un número de página (correspondiente a la tabla de páginas de la tabla de páginas del proceso) y un offset dentro de la misma.

### Direcciones
Cada dirección es expresada como:

- Un número de página que es usada como un índice para ingresar a la tabla de páginas y encontrar el número de frame donde está alojada esa página en memoria física. Como los frames son de tamaño fijo, puedo encontrar la dirección donde inicia la página.
- Un offset de página que es combinado con la dirección base para definir la dirección física de la referencia. 


### Tabla de páginas del SO
- Es de acceso rápido.
- Tiene una cantidad finita de entradas que se setean en el Context Switch con la tabla de páginas del proceso que se carga en el procesador.
  - Cuando el proceso tiene menos páginas que la cantidad de entradas que la tabla del SO, se deben marcar las entradas inválidas que quedan en desuso.
  - Cuando un proceso tiene más páginas que las entradas de la tabla de del SO, se mantiene una parte de la tabla en memoria (la tabla de páginas del proceso debe ser paginada) y se incrementa el tiempo de acceso efectivo a memoria.

## **Segmentación**
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