El servicio de transporte se implementa mediante un **protocolo de transporte** entre las dos entidades de transporte. En ciertos aspectos, los protocolos de transporte se parecen a los protocolos de enlace de datos, ambos se encargan del control de errores, la secuenciación y el control de flujo, entre otros aspectos.

Sin embargo, existen diferencias considerables entre los dos, las cuales se deben a disimilitudes importantes entre los entornos en que operan ambos protocolos. En la capa de enlace de datos, dos enrutadores se comunican de forma directa mediante un canal físico, ya sea cableado o inalámbrico, mientras que, en la capa de transporte, ese canal físico se sustituye por la red completa. Esta diferencia tiene muchas implicaciones importantes para los protocolos.

![[entorno_protocolos_de_transporte.png]]

### Direccionamiento
Cuando un proceso de aplicación (por ejemplo, un usuario) desea establecer una conexión con un proceso de aplicación remoto, debe especificar a cuál se conectará. El método que se emplea por lo general es definir direcciones de transporte en las que los procesos puedan escuchar las solicitudes de conexión. En Internet, estos puntos terminales se denominan **puertos**. Usaremos el término genérico **TSAP (Transport Service Access Point)** para indicar un endpoint específico en la capa de transporte. Así mismo, los puntos terminales análogos en la capa de red (es decir, direcciones de capa de red) se llamen **NSAP (Network Service Access Point)**. Las [[direcciones IP]] son ejemplos de NSAP.

Los procesos de aplicación, tanto clientes como servidores, se pueden enlazar por sí mismos a un TSAP para establecer una conexión a un TSAP remoto. Estas conexiones se realizan a través de puntos NSAP en cada host, como se muestra. El propósito de tener puntos TSAP es que, en algunas redes, cada computadora tiene un solo NSAP, por lo que se necesita alguna forma de diferenciar los múltiples puntos terminales de transporte que comparten ese punto NSAP.

![[direccionamiento_tsap_nsap.png]]

### Establecimiento de una conexión
El proceso de establecer una conexión suena fácil, pero en realidad es sorprendentemente complicado. A primera vista parecería suficiente con que una entidad de transporte enviara tan sólo un segmento CONNECTION REQUEST al destino y esperara una respuesta CONNECTION ACCEPTED. El problema ocurre cuando la red puede perder, retrasar, corromper y duplicar paquetes. Este comportamiento causa complicaciones serias.

Imagine una red que está tan congestionada que las confirmaciones de recepción casi nunca regresan a tiempo, y cada paquete expira y se retransmite dos o tres veces. Suponga que la red usa datagramas en su interior y que cada paquete sigue una ruta diferente. Algunos de los paquetes podrían atorarse en un congestionamiento de tráfico dentro de la red y tardar mucho tiempo en llegar. Es decir, se pueden retardar en la red y reaparecer mucho después, cuando el emisor piense que se han perdido y haya retransmitido el paquete. Entonces puede llegar este paquete duplicado al receptor y causar estragos si no se controla.

Este problema se puede atacar de varias maneras, ninguna de las cuales es muy satisfactoria. Una es usar direcciones de transporte desechables. En este enfoque, cada vez que se requiere una dirección de transporte, se genera una nueva. Cuando una conexión es liberada, se descarta la dirección y no se vuelve a utilizar. Así, los paquetes duplicados con retardo nunca encuentran su camino hacia un proceso de transporte y no pueden hacer ningún daño. Sin embargo, esta estrategia dificulta la conexión con un proceso.

Otra posibilidad es dar a cada conexión un identificador único (es decir, un número de secuencia que se incremente con cada conexión establecida) elegido por la parte iniciadora y puesto en cada segmento, incluyendo el que solicita la conexión. Después de liberar cada conexión, cada entidad de transporte puede actualizar una tabla que liste conexiones obsoletas como pares (entidad de transporte de igual, identificador de conexión). Cada vez que entre una solicitud de conexión, se puede verificar con la tabla para saber si pertenece a una conexión previamente liberada.

Por desgracia, este esquema tiene una falla básica: requiere que cada entidad de transporte mantenga una cierta cantidad de información histórica durante un tiempo indefinido. Esta historia debe persistir tanto en la máquina de origen como en la de destino. De lo contrario, si una máquina falla y pierde su memoria, ya no sabrá qué identificadores de conexión ya han utilizado sus iguales.

Más bien, necesitamos un enfoque diferente para simplificar el problema. En lugar de permitir que los paquetes vivan eternamente dentro de la red, debemos idear un mecanismo para eliminar a los paquetes viejos que aún andan vagando por ahí. Con esta restricción, el problema se vuelve algo más manejable.

El tiempo de vida de un paquete puede restringirse a un máximo conocido mediante el uso de una (o más) de las siguientes técnicas: 
1. Un diseño de red restringido. 
2. Colocar un contador de saltos en cada paquete. 
3. Marcar el tiempo en cada paquete.

La primera técnica incluye cualquier método que evite que los paquetes hagan ciclos, combinado con una manera de limitar el retardo, incluyendo la congestión a través de la trayectoria más larga posible (ahora conocida). Es difícil, dado que el alcance de las interredes puede variar, desde una sola ciudad hasta un alcance internacional. El segundo método consiste en inicializar el contador de saltos con un valor apropiado y decrementarlo cada vez que se reenvíe el paquete. El protocolo de red simplemente descarta cualquier paquete cuyo contador de saltos llega a cero. El tercer método requiere que cada paquete lleve la hora en la que fue creado, y que los enrutadores se pongan de acuerdo en descartar cualquier paquete que haya rebasado cierto tiempo predeterminado. Este último método requiere que los relojes de los enrutadores estén sincronizados ([[Sincronización]]), lo que no es una tarea fácil, además, en la práctica un contador de saltos es una aproximación suficientemente cercana a la edad.

Al limitar los tiempos de vida de los paquetes, es posible proponer una manera práctica y a prueba de errores para rechazar segmentos duplicados con retardo. La base de esta propuesta es que el origen etiquete los segmentos con números de secuencia que no se vayan a reutilizar durante T segundos. El periodo T y la tasa de paquetes por segundo determinan el tamaño de los números de secuencia. De esta manera, sólo un paquete con un número de secuencia específico puede estar pendiente en cualquier momento dado. Aún puede haber duplicados de este paquete, en cuyo caso el destino debe descartarlos. Sin embargo, ya no se da el caso en que un duplicado con retardo de un paquete pueda vencer a un nuevo paquete con el mismo número de secuencia y que el destino lo acepte.

Para resolver el problema de una máquina que pierde toda la memoria acerca de su estado tras una falla, una posibilidad es exigir a las entidades de transporte que estén inactivas durante T segundos después de una recuperación. El periodo inactivo permitirá que todos los segmentos antiguos expiren, por lo que el emisor podrá empezar de nuevo con cualquier número de secuencia. Sin embargo, en una interred (interconexión de redes) compleja el periodo T puede ser grande, por lo que esta estrategia no es muy atractiva.

En cambio se propone equipar cada host con un reloj. Los relojes de los distintos hosts no necesitan estar sincronizados. Se supone que cada reloj tiene la forma de un contador binario que se incrementa a sí mismo a intervalos uniformes. Además, la cantidad de bits del contador debe ser igual o mayor que la cantidad de bits en los números de secuencia. Por último, y lo más importante, se supone que el reloj continúa operando aunque el host falle.

Cuando se establece una conexión, los k bits de menor orden del reloj se usan como número de secuencia inicial de k bits. Por tanto cada conexión comienza a numerar sus segmentos con un número de secuencia inicial diferente.

Una vez que ambas entidades de transporte han acordado el número de secuencia inicial, se puede usar cualquier protocolo de ventana deslizante para el control de flujo de datos. Este protocolo de ventana encontrará y descartará exactamente los paquetes duplicados después de que éstos hayan sido aceptados.

El método basado en reloj resuelve el problema de no poder diferenciar los segmentos duplicados con retardo de los segmentos nuevos. Sin embargo, hay un inconveniente práctico en cuanto a su uso para establecer conexiones. Como por lo general no recordamos los números de secuencia de una conexión a otra en el destino, aún no tenemos forma de saber si un segmento CONNECTION REQUEST que contiene un número de secuencia inicial es un duplicado de una conexión reciente. Este inconveniente no existe durante una conexión, ya que el protocolo de la ventana deslizante sí recuerda el número de secuencia actual.

Para resolver este problema específico se desarrolló el **acuerdo de tres vías** (three-way handshake). Este protocolo de establecimiento implica que un igual verifique con el otro que la solicitud de conexión sea realmente actual. El host 1 escoge un número de secuencia, x, y envía al host 2 un segmento CONNECTION REQUEST que contiene ese número. El host 2 responde con un segmento ACK para confirmar la recepción de x y anunciar su propio número de secuencia inicial, y. Por último, el host 1 confirma la recepción del número de secuencia inicial seleccionado por el host 2 en el primer segmento de datos que envía

![[acuerdo_de_tres_vias.png]]

Ahora veamos la manera en que funciona el acuerdo de tres vías en presencia de segmentos de control duplicados con retardo. En la segunda figura, el primer segmento es un CONNECTION REQUEST duplicado con retardo de una conexión antigua. Este segmento llega al host 2 sin el conocimiento del host 1. El host 2 reacciona a este segmento y envía al host 1 un segmento ACK, para solicitar en efecto la comprobación de que el host 1 haya tratado realmente de establecer una nueva conexión. Cuando el host 1 rechaza el intento del host 2 por establecer una conexión, el host 2 se da cuenta de que fue engañado por un duplicado con retardo y abandona la conexión. De esta manera, un duplicado con retardo no causa daño.

### Liberación de una conexión
Es más fácil liberar una conexión que establecerla. No obstante, hay más obstáculos de los que uno podría imaginar. Como mencionamos antes, hay dos estilos para terminar una conexión: liberación asimétrica y liberación simétrica. La liberación asimétrica es la manera en que funciona el sistema telefónico: cuando una de las partes cuelga, se interrumpe la conexión. La liberación simétrica trata la conexión como dos conexiones unidireccionales distintas y requiere que cada una se libere por separado.

La liberación asimétrica es abrupta y puede provocar la pérdida de datos. Considere el escenario de la figura 6-12. Una vez que se establece la conexión, el host 1 envía un segmento que llega en forma apropiada al host 2. A continuación, el host 1 envía otro segmento. Por desgracia, el host 2 emite un DISCONNECT antes de que llegue el segundo segmento. El resultado es que se libera la conexión y se pierden los datos.

![[desconexion_asimetrica.png]]

Es obvio que se requiere un protocolo de liberación más sofisticado para evitar la pérdida de los datos. Una posibilidad es usar la liberación simétrica, en la que cada dirección se libera en forma independiente de la otra. Aquí, un host puede continuar recibiendo datos, aun después de haber enviado un segmento DISCONNECT.

La liberación simétrica es ideal cuando cada proceso tiene una cantidad fija de datos por enviar y sabe con certeza cuándo los ha enviado. En otras situaciones, el proceso de determinar si se ha efectuado o no todo el trabajo y si debe terminar o no la conexión no es tan obvio. Podríamos pensar en un protocolo en el que el host 1 diga: “Ya terminé. ¿Terminaste también?” Si el host 2 responde: “Ya terminé también. Adiós”, la conexión se puede liberar sin problemas.

Por desgracia, este protocolo no siempre funciona. Hay un problema famoso que tiene que ver con ese asunto. Se conoce como el **problema de los dos ejércitos**. Imagine que un ejército blanco está acampado en un valle. En los dos cerros que rodean al valle hay ejércitos azules. El ejército blanco es más grande que cualquiera de los dos ejércitos azules por separado, pero juntos éstos son más grandes que el ejército blanco. Si cualquiera de los dos ejércitos azules ataca por su cuenta, será derrotado, pero si los dos atacan a la vez obtendrán la victoria.

Los ejércitos azules quieren sincronizar sus ataques. Sin embargo, su único medio de comunicación es el envío de mensajeros a pie a través del valle, donde podrían ser capturados y se perdería el mensaje (es decir, tienen que usar un canal de comunicación no confiable). La pregunta es: ¿existe un protocolo que permita que los ejércitos azules ganen?

![[problema_de_los_dos_ejercitos.png]]

Se puede discutir mucho, pero podemos demostrar que no existe un protocolo que funcione. Supongamos que existiera algún protocolo. O el último mensaje del protocolo es esencial, o no lo es. Si no lo es, podemos eliminarlo (así como los demás mensajes no esenciales) hasta que quede un protocolo en el que todos los mensajes sean esenciales. ¿Qué ocurre si el mensaje final no pasa? Acabamos de decir que es esencial, por lo que, si se pierde, el ataque no ocurrirá. Dado que el emisor del mensaje final nunca puede estar seguro de su llegada, no se arriesgará a atacar. Peor aún, el otro ejército azul sabe esto, por lo que tampoco atacará.

Para ver la relevancia del problema de los dos ejércitos en relación con la liberación de conexiones, simplemente sustituya “atacar” por “desconectar”. Si ninguna de las partes está preparada para desconectarse hasta estar convencida de que la otra está preparada para desconectarse también, nunca ocurrirá la desconexión.

En la práctica podemos evitar este dilema al eludir la necesidad de un acuerdo y pasar el problema al usuario de transporte, de modo que cada lado pueda decidir por su cuenta si se completó o no la comunicación. Éste es un problema más fácil de resolver y puede hacerse con un simple acuerdo de 3 vias como se ilustra a continuación.

![[liberar_una_conexion.png]]