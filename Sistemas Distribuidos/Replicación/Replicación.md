---
aliases: ["replicación", "redundancia", "réplicas"]
---
Hay dos motivos principales para replicar datos. Primero, los datos son replicados para incrementar la fiabilidad de un sistema. Si un sistema de archivos ha sido replicado puede ser posible continuar trabajando si una de las réplicas se cae simplemente trabajando con la otra réplica. También, manteniendo varias copias, es posible proveer protección contra la corrupción de datos.

La otra razón para replicar datos es la [[performance]]. La replicación para performance es importante cuando un [[Sistemas Distribuidos|sistema distribuido]] necesita [[Escalabilidad|escalar]] en términos de tamaño o en términos de área geográfica que cubre.

El precio de la replicación es tener que lidiar con los problemas de consistencia originados por dichas réplicas. Cuando una copia es modificada, dicha copia ahora es diferente al resto. Consecuentemente las modificaciones deben ser llevadas a cabo en todas las copias para asegurar la consistencia. El cómo y cúando se llevan a cabo dichas modificaciones determina el **precio de la replicación**.

Un posible trade-off que se debe analizar es que el mantener las copias sincronizadas puede exigir más ancho de banda de la red. Considere un proceso P que accede una réplica local N veces por segundo, mientras que la réplica misma es actualizada M veces por segundo. Suponiendo que una actualización refresca la versión anterior de la réplica. Si N << M, osea, el ratio acceso-actualización es muy pequeño, tenemos una situación donde muchas de las versiones actualizadas de la réplica local no serán accedidas por P, haciendo que todas las comunicaciones para esas versiones sea inútil. En ese caso, puede ser preferible no instalar una réplica local cerca de P, o aplicar una estrategia distinta para actualizar la réplica.

Un problema más serio es que el hecho de mantener múltiples copias consistentes puede generar problemas de escalabilidad graves. Intuitivamente una colección de copias es consistente cuando todas las copias son siempre iguales. Consecuentemente, cuando una operación de actualización es realizada sobre una copia, la actualización debería ser propagada a todas las copias antes de que una operación subsecuente tome lugar, sin importar en qué copia la operación es iniciada o realizada.

A este tipo de consistencia donde todas las copias siempre son iguales se le suele llamar **consistencia hermética** o **replicación sincrónica**. La idea clave es que una actualización es llevada a cabo en todas las copias como una sola operación atómica, o [[Transacciones|transacción]]. Desafortunadamente implementar transacciones involucrando un número elevado de réplicas distribuidas sobre una red grande es inherentemente difícil cuando al mismo tiempo se requiere rapidez.

Para poder sincronizar las réplicas surge la necesidad de que las réplicas se pongan de acuerdo en cuándo se debe llevar a cabo una actualización localmente. Por ejemplo, estas pueden necesitar decidir un orden global de operaciones ([[Sincronización]]). La sincronización global lleva mucho tiempo de comunicación, especialmente cuando las réplicas están muy distribuidas a través de una red WAN.

> Entonces arribamos a un dilema. Los problemas de **escalabilidad** pueden ser aliviados mediante **replicación** llevando a una mejor performance. Pero esta replicación suele requerir **sincronización global** lo que lleva a problemas de escalabilidad.

En muchos casos la única solución viable es relajar los **requerimientos de consistencia**. En otras palabras, si se relajan los requerimientos que las actualizaciones deben ser ejecutadas como operaciones atómicas, podemos evitar la sincronización global instantánea y por lo tanto ganar performance. El precio es que las copias no son iguales en todos lados.

## Modelos de consistencia centrados en datos
Tradicionalmente la consistencia fue discutida en el contexto de operaciones de lectura/escritura sobre datos compartidos, disponibles por medio de memoria compartida, una base de datos distribuida o un sistema de archivos. Aquí se usará el concepto **almacen de datos** o **data store** que abarca todos los anteriores. Un almacen de datos puede estar distribuido físicamente a través de varias máquinas. En particular se supone que cada proceso que puede acceder a datos del almacen tiene una copia local (o cercana) del almacen entero.

![[SSDD_replicación_data_store_1.png]]

![[Modelo de consistencia]]

A falta de un reloj global es difícil determinar precisamente que operación de escritura es la última. Como alternativa, necesitamos proveer otras definiciones, llevando a un rango de modelos de consistencia. Cada modelo efectivamente restringe los valores que una operación de lectura en un ítem puede retornar.

### Consistencia continua
![[Consistencia continua]]

### Ordenamiento consistente de operaciones
Esta clase de modelos proviene del campo de la programación concurrente. Los siguientes modelos tratan con ordenar consistentemente las operaciones sobre información replicada y compartida.

#### Consistencia Secuencial
En los siguientes casos se usa una notación donde se representa el eje temporal como un eje horizontal que corre de izquierda a derecha. Se utiliza la notación $W_i (x)a$ para denotar que el proceso $P_i$ escribe un valor $a$ a un item de datos x. Similarmente usamos la notación $R_i (x)b$ para representar que el proceso $P_i$ lee x y el valor leido es b. También se asume que cada item tiene valor inicial NIL.

![[SSDD_consistencia_secuencial.png]]

La **consistencia secuencial** es un importante modelo de consistencia centrado en datos (definido por Lamport\[1979] en el contexto de memoria compartida para sistemas multiprocesador).  Un almacen de datos es secuencialmente consistente  si satisface la siguiente condición:

> El resultado de cualquier ejecución es el mismo que si las operaciones (de lectura y escritura) de todos los procesos efectuados sobre el almacén de datos se ejecutaran en algún orden secuencial y las operaciones de cada proceso individual aparecieran en esa secuencia en el orden especificado por su programa.

Esta definición significa que cuando los procesos corren concurrentemente, cualquier intercalación de operaciones es aceptable, pero **todos los procesos deben tener la misma intercalación de operaciones**.

#### Consistencia Causal
El modelo de **consistencia causal** representa una flexibilización de la consistencia secuencial en que hace la distinción entre eventos que son potencialmente relacionados causalmente y los que no (la causalidad se puede representar mediante un [[Relojes Lógicos#Relojes Vectoriales|reloj vectorial]]).

Considerando una interacción simple donde un proceso P1 escribe el valor de datos $x$. Y luego P2 lee $x$ y escribe $y$. Aquí la lectura de $x$ y la escritura de $y$ son potencialmente causalmente relacionados, dado que el cálculo de $y$ puee haber dependido del valor de $x$ leido por P2.

Por otro lado si dos procesos espontáneamente y simultáneamente escriben dos items de datos distinto, no están relacionados causalmente. A las operaciones que no están relacionadas causalmente se las llama **concurrentes**.

Para que un almacen de datos se considere causalmente consistente, es necesario que cumpla la siguiente condición:

> Escrituras que potencialmente están relacionadas por la causalidad, deben ser vistas por todos los procesos en el mismo orden. Las escrituras concurrentes pueden verse en un orden diferente en diferentes máquinas.

![[SSDD_consistencia_causal.png]]

#### Operaciones de agrupamiento
Muchos modelos de consistencia están definidos al nivel de operaciones de lectura y escritura. Este nivel de granularidad se debe a razones históricas: estos modelos se desarrollaron inicialmente para sistemas de multiprocesador de memoria compartida, y en realidad se implementaron al nivel de hardware.

Esta granularidad en muchos casos no coincide con la granularidad provista por aplicaciones. Lo que vemos es que la concurrencia entre programas compartiendo información es generalmente controlada mediante mecanísmos de sincronización para [[Exclusión mutua distribuida|exclusión mutua]] y [[Transacciones]].

Lo que ocurre dentro de un programa es que se opera sobre los datos por una serie de operaciones de lectura y escritura protegidas contra el acceso concurrente. Osea, se transforma una serie de operaciones en una unidad de ejecución atómica, por lo tanto, elevando el nivel de granularidad.

### Consistencia Eventual
![[Consistencia eventual]]

## Modelos de consistencia centrados en el cliente
Los **modelos de consistencia centrados en el cliente** apuntan a proveer una vista consistente a nivel sistema del almacén de datos. Para el siguiente análisis se consideran almacenes de datos que se caracterízan por el ausencia de actualizaciones simultáneas, o que cuando estas ocurren, se supone que pueden ser resueltas fácilmente. La mayor parte de las operaciones son de lectura de datos. Estos almacenes ofrecen un modelo de consistencia débil, tal como la consistencia eventual. Introduciendo modelos de consistencia centrados en el cliente resulta que muchas inconsistencias se pueden ocultar de una manera relativamente sencilla.

![[SSDD_modelos_de_consistencia_centrados_en_el_cliente.png]]

Eventualmente los almacenes de datos consistentes generalmente funcionan bien dado que los clientes siempre acceden a la misma réplica. Sin embargo surgen inconveneintes cuando se accede a diferentes réplicas a lo largo del tiempo. Por ejemplo, si un cliente se conecta a una réplica en un momento, realiza operaciones de actualización y luego accede al sistema a través de otra réplica, si los cambios no se han propagado a dicha réplica el cliente notará un estado inconsistente.

El problema anterior puede ser resuelto incorporando **consistencia centrada en el cliente**. En esencia esto provee la garantías *para un solo cliente* con respecto a la consistencia de los accesos al almacen de datos por este cliente. No se proveen garantías en lo que respecta al acceso por parte de clientes diferentes.

### Lecturas monotónicas
Se dice que un almacén de datos provee **consistencia de lecturas monotónicas** si se cumple la siguiente condición:

> Si un proceso lee el valor de un elemento de datos x, cualquier operación de lectura sucesiva sobre x que haga ese proceso devolverá siempre el mismo valor o un valor más reciente.

En otras palabras la consistencia de lecturas monotónicas garantiza quee una vez que un proceso ha visto un valor de x, nunca verá una versión anterior de x.

Usando una notación similar a la de modelos de consistencia centrada en datos, la consistencia de lecturas monotónicas puede ser representada gráficamente. En vez de mostrar procesos sobre el eje vertical se muestran almacenes de datos locals. Una operación de lectura o escritura es indexada por el proceso que ejecutó la operación. $W_2(x_1;x_2)$ indica que el proceso $P_2$ es responsable de producir la versión $x_2$ que sigue de la $x_1$. Así mismo, $W_2(x_1|x_2)$ denota que el proceso $P_2$ produce la versión $x_2$ concurrentemente a la versión $x_1$ (por lo tanto potencialmente introduciendo un conflicto write-write).

![[SSDD_lecturas_monotonicas.png]]

### Escrituras monotónicas
En muchas situaciones es importante que las operaciones de escritura sean propagadas en el orden correcto a todas las copias del almacén. Esta propiedad es expresada en la **consistencia de escrituras monotónicas**. En un almacén consistente en escrituras monotónicas se cumple la siguiente condición:

> Una operación de escritura hecha por un proceso sobre un elemento x se completa antes que cualquier otra operación sucesiva de escritura sobre x realizada por el mismo proceso.

Más formalmente, si tenemos dos operaciónes de escritura sucesivas $W_k(x_i)$ y $W_k(x_j)$ por un mismo proceso $P_k$, entonces, sin importar donde se ejecuta $W_k(x_j)$, también tenemos $WS(x_i;x_j)$. Por lo tanto, completar una operación de escritura significa que esa copia en donde se ha realizado una operación sucesiva refleja el efecto de una operación de escritura previa por el mismo proceso, sin importar donde fue iniciada esta operación. En otras palabras, la operación de escritura en una copia de x es llevada a cabo solo si esa copia ha sido actualizada por medio de alguna operación de escritura previa por el mismo proceso, lo cual puede haber ocurrido en cualquier otra copia de x. Osea la nueva operación debe esperar que la anterior termine.

![[SSDD_escrituras_monotonicas.png]]

### Lea sus escrituras
Se dice que un almacén de datos provee **consistencia de lea sus escrituras**, si se cumple la siguiente condición:

> El efecto de una operación de escritura hecha por un proceso sobre un elemento de datos x siempre será visto por una operación de lectura sucesiva sobre x hecha por el mismo proceso.

En otras palabras, una operación de lectura siempre es completada antes de una lectura sucesiva por el mismo proceso, sin importar donde esa lectura toma lugar.

La asusencia de consistencia lea sus escrituras se suele exprimentar cuando se actualiza un documento Web y luego se lo quiere acceder. El problema es que usualmente estos documentos suelen estar cacheados de manera que no ese tengan que pedir al servidor Web. Consecuentemente, cuando se actualiza la página WEb el usuario no verá los efectos.

## Manejo de réplicas
Un problema clave de cualquier sistema distribuido que soporta replicación es decidir dónde, cuándo y por quién deben ser colocadas estas réplicas y subsecuentemente qué mecanismos se usarán para mantenerlas consistentes. El problema de la ubicación puede ser dividido en dos subproblemas: el que consisten en ubicar **servidores de réplica** y el de ubicar el **contenido**.

### Replicación y ubicación de contenido
Cuando se trata de replicación y ubicación de contenido, hay tres tipos distinguibles de réplicas.

![[SSDD_replicacion_y_ubicacion_de_contenido.png]]

#### Réplicas permanentes
Las réplicas permanentes se pueden considerar el conjunto inicial de réplicas que constituyen el almacén de datos distribuido. En muchos casos el número de réplicas permanentes es reducido. Considerando el ejemplo de un sitio web, su distribución suele presentarse de dos maneras. El primer tipo es en el que el archivo que constituye el sitio es replicado sobre un número limitado de servidores en una ubicación única.

Al segundo tipo se le llama **mirroring**. En este caso un sitio web es copiado a un número limitado de servidores llamados **mirror sites**, los cuales se encuentran distribuidos geográficamente a través de [[Internet]]. en muchos casos, los clientes simplemente eligen uno de los varios mirros sites de una lista ofrecida a ellos.

#### Réplicas iniciadas por el servidor
En contraste a las réplicas permanentes, las réplicas iniciadas por el servidor son copias de un almacén de datos que existe para mejorar la [[performance]], y  creadas por la iniciativa del dueño del almacén de datos.

#### Réplicas iniciadas por el cliente
Un tipo importante de réplica es la iniciada por un cliente. Estas se suelen conocer como **(client) caches**. En esencia un cache es almacenamiento local utilizado por un cliente para temporalmente persistir una copia de datos que ha solicitado. En principio su manejo es dejado completamente en manos del cliente. Los client caches son usados solamente para mejorar los tiempos de acceso.

### Distribución de contenido
El manejo de réplicas también trata con la propagación de contenido actualizado a los servidores de réplicas relevantes.

#### Estado versus operaciones
Un problema de diseño relevante concierne a qué es lo que se va a propagar. Básicamente se tienen tres posibilidades:
- Propagar solamente una notificación de la actualización.
- Transferir los datos de una copia a otra.
- Propagar la operación de actualización a otras copias.

Propagar una notificación es lo que hacen los **protocolos de invalidación**. En estos, se les informa a las otras copias que se ha llevado a cabo una actualización y que su información ya no es válida. En estos se puede notificar qué parte es invalidada. Su ventaja principal es su bajo consumo de ancho de banda. Estos modelos son convenientes cuando se tiene un bajo ratio lectura/escritura (solo se actualiza una réplica inválida cuando se requiere y se ahorran actualizaciones inútiles).

La segunda alternativa es transferir los datos. Esto es útil cuando el ratio lectura/escritura es alto, en ese caso la posibilidad de que una actualización sea efectiva (osea es leida) antes de que llegue la siguiente es alta.

La tercer alternativa es en vez de transmitir los datos transmitir las operaciones obre estos. Esta alternativa se suele llamar **replicación activa**, y asume que cada réplica es representada por un proceso capaz de "activamente" manter los datos asociados al día llevando a cabo operaciones. Su mayor beneficio es que las actualizaciones usualmente pueden ser propagadas con un costo de ancho de banda bajo, siempre y cuando que el tamaño de los parámetros asociados con la operación sean relativamente pequeños.

#### Protocolos pull versus push
Otro problema de diseño es si las actualizaciones son pulled o pushes. En un **modelo basado en push**, también referido como **protocolo basado en servidor**, las actualizaciones son propagadas a las otras réplicas sin que esas réplicas lo soliciten. Esto se suele usar con las réplicas iniciadas por el servidor.

Por el contrario en los **modelos basados en pull** un cliente o servidor solicita a otro servidor que le envíe las actualizaciónes que tenga pendientes. Estos modelos también son llamados **protocolos basados en cliente**, y suelen ser usados por los client caches.

| Cuestión                  | Basado en push                                             | Basado en pull                   |
| ------------------------- | ---------------------------------------------------------- | -------------------------------- |
| **Estado en el servidor** | Lista de réplicas, clientes y cache                        | Ninguno                          |
| **Mensajes enviados**     | Actualiza (y posteriormente trae la actualización después) | Sondea y actualiza               |
| **Tiempo de respuesta**   | Inmediato (o busca el tiempo de actualización)             | Busca el tiempo de actualización | 

#### Web Cache
![[Web cache]]