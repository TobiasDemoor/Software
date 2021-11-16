El **TCP (Transmission Control Protocol)** es un [[protocolo]] orientado a la conexión  de comunicación que especifica qué mensajes deben ser intercambiados para establecer o desestablecer una conexión, qué necesita hacerse para preservar el ordenamiento de la información transmitida, y qué necesitan ambas partes para detectar y corregir información que fue perdida durante la transmisión. Se encuentra en la [[capa de transporte]]. TCP se definió formalmente en el [[RFC]] 793 en septiembre de 1981. Luego de esto tuvo muchos más RFC sumando aclaraciones, correcciones y extensiones.

TCP se diseñó específicamente para proporcionar un flujo de bytes confiable de extremo a extremo a través de una interred no confiable. TCP se diseñó para adaptarse de manera dinámica a las propiedades de la interred y sobreponerse a muchos tipos de fallas.

Cada máquina que soporta TCP tiene una entidad de transporte TCP, ya sea un procedimiento de biblioteca, un proceso de usuario o (lo más común) sea parte del kernel. En todos los casos, maneja flujos TCP e interactúa con la capa IP. Una entidad TCP acepta flujos de datos de usuario de procesos locales, los divide en fragmentos que no excedan los 64 KB (en la práctica, por lo general son 1460 bytes de datos para ajustarlos en una sola trama Ethernet con los encabezados IP y TCP), y envía cada pieza como un datagrama IP independiente. Cuando los datagramas que contienen datos TCP llegan a una máquina, se pasan a la entidad TCP, la cual reconstruye los flujos de bytes originales.

La capa IP no ofrece ninguna garantía de que los datagramas se entregarán de manera apropiada, ni tampoco una indicación sobre qué tan rápido se pueden enviar los datagramas. Corresponde a TCP enviar los datagramas con la suficiente rapidez como para hacer uso de la capacidad sin provocar una congestión; también le corresponde terminar los temporizadores y retransmitir los datagramas que no se entreguen. Los datagramas que sí lleguen podrían hacerlo en el orden incorrecto; también corresponde a TCP reensamblarlos en mensajes con la secuencia apropiada. En resumen, TCP debe proporcionar un buen desempeño con la confiabilidad que la mayoría de las aplicaciones desean y que IP no proporciona.

#### El servicio TCP
El servicio TCP se obtiene al hacer que tanto el servidor como el receptor creen puntos terminales, llamados sockets. Cada socket tiene un número (dirección) que consiste en la dirección IP del host y un número de 16 bits que es local para ese host, llamado **puerto**. Un puerto es el nombre TCP para un TSAP. Para obtener el servicio TCP, hay que establecer de manera explícita una conexión entre un socket en una máquina y un socket en otra máquina.

Los números de puerto menores que 1024 están reservados para los servicios estándar que, por lo general, sólo los usuarios privilegiados pueden iniciar (por ejemplo, el usuario root en los sistemas UNIX). Éstos se llaman puertos bien conocidos, a continuación se muestra la lista de algunos de los más conocidos, la lista completa se proporciona en www.iana.org.

| Puerto | Protocolo | Uso                                           |
| ------ | --------- | --------------------------------------------- |
| 20, 21 | FTP       | Transferencia de archivos.                    |
| 22     | SSH       | Inicio de sesión remoto, reemplazo de Telnet. |
| 25     | [[SMTP]]  | Correo electrónico.                           |
| 80     | [[HTTP]]  | [[World Wide Web]].                           |
| 110    | [[POP3]]  | Acceso remoto al correo electrónico.          |
| 143    | [[IMAP]]  | Acceso remoto al correo electrónico.          |
| 443    | [[HTTPS]] | Acceso seguro a web (HTTP sobre SSL/TLS).     |
| 543    | RTSP      | Control del reproductor de medios.            |
| 631    | IPP       | Compartición de impresoras.                   |

Todas las conexiones TCP son full dúplex y de punto a punto. Full dúplex significa que el tráfico puede ir en ambas direcciones al mismo tiempo. Punto a punto significa que cada conexión tiene exactamente dos puntos terminales. TCP no soporta la multidifusión ni la difusión.

Una conexión TCP es un flujo de bytes, no un flujo de mensajes. Los límites de los mensajes no se preservan de un extremo a otro. Por ejemplo, si el proceso emisor realiza cuatro escrituras de 512 bytes en un flujo TCP, tal vez estos datos se entreguen al proceso receptor como cuatro fragmentos de 512 bytes, dos fragmentos de 1024 bytes, uno de 2 048 bytes, o de alguna otra forma. No hay manera de que el receptor detecte la(s) unidad(es) en la(s) que se escribieron los datos, sin importar qué tanto se esfuerce.

![[TCP_flujo_conexion.png]]

#### El protocolo TCP
Una característica clave de TCP, y una que domina el diseño del protocolo, es que cada byte de una conexión TCP tiene su propio número de secuencia de 32 bits. Cuando Internet comenzó, las líneas entre los enrutadores eran principalmente líneas rentadas de 56 kbps, por lo que un host que mandaba datos a toda velocidad tardaba una semana en recorrer los números de secuencia. A las velocidades de las redes modernas, los números de secuencia se pueden consumir con una rapidez alarmante. Los números de secuencia separados de 32 bits se transmiten en paquetes para la posición de ventana deslizante en una dirección, y para las confirmaciones de recepción en la dirección opuesta.

La entidad TCP emisora y receptora intercambian datos en forma de segmentos. Un **segmento TCP** consiste en un encabezado fijo de 20 bytes (más una parte opcional), seguido de cero o más bytes de datos. El software de TCP decide qué tan grandes deben ser los segmentos. Puede acumular datos de varias escrituras para formar un segmento, o dividir los datos de una escritura en varios segmentos. Hay dos límites que restringen el tamaño de segmento. Primero, cada segmento, incluido el encabezado TCP, debe caber en la carga útil de 65515 bytes del IP. Segundo, cada enlace tiene una **MTU (Maximum Transfer Unit)**. Cada segmento debe caber en la MTU en el emisor y el receptor, de modo que se pueda enviar y recibir en un solo paquete sin fragmentar. En la práctica, la MTU es por lo general de 1500 bytes (el tamaño de la carga útil en Ethernet) y, por tanto, define el límite superior en el tamaño de segmento.

Las implementaciones modernas de TCP realizan el descubrimiento de MTU de la ruta mediante el uso de la técnica descrita en el RFC 1191. Esta técnica usa mensajes de error de [[ICMP]] para encontrar la MTU más pequeña para cualquier enlace en la ruta. Después, TCP ajusta el tamaño del segmento en forma descendente para evitar la fragmentación.

El protocolo básico que utilizan las entidades TCP es el protocolo de ventana deslizante con un tamaño dinámico de ventana. Cuando un emisor transmite un segmento, también inicia un temporizador. Cuando llega el segmento al destino, la entidad TCP receptora devuelve un segmento (con datos si existen, de otro modo sin ellos) que contiene un número de confirmación de recepción igual al siguiente número de secuencia que espera recibir, junto con el tamaño de la ventana remanente. Si el temporizador del emisor expira antes de recibir la confirmación de recepción, el emisor transmite de nuevo el segmento.

#### El encabezado del segmento TCP
Cada segmento comienza con un encabezado de formato fijo de 20 bytes. El encabezado fijo puede ir seguido de encabezado de opciones. Después de las opciones, si las hay, pueden continuar hasta 65 535 − 20 − 20 = 65 495 bytes de datos, donde los primeros 20 se refieren al encabezado IP y los segundos al encabezado TCP. Los segmentos sin datos son legales y se usan por lo común para confirmaciones de recepción y mensajes de control.

![[TCP_encabezado.png]]

Los campos *Puerto de origen* y *Puerto de destino* identifican los puntos terminales locales de la conexión. Un puerto TCP más la dirección IP de su host forman un punto terminal único de 48 bits. Los puntos terminales de origen y de destino en conjunto identifican la conexión. Este identificador de conexión se denomina **5-tupla**, ya que consiste en cinco piezas de información: el protocolo (TCP), IP de origen y puerto de origen, IP de destino y puerto de destino.

Los campos *Número de secuencia* y *Número de confirmación de recepción* desempeñan sus funciones normales. Cabe mencionar que el segundo especifica el siguiente byte en el orden esperado, no el último byte de manera correcta recibido. Es una confirmación de recepción acumulativa debido a que sintetiza los datos recibidos con un solo número. No va más allá de los datos perdidos. Ambos tienen 32 bits de longitud porque cada byte de datos está numerado en un flujo TCP.

La *Longitud del encabezado TCP* indica la cantidad de palabras de 32 bits contenidas en el encabezado TCP. Esta información es necesaria porque el campo Opciones es de longitud variable por lo que el encabezado también.

A continuación viene un campo de 4 bits que no se usa.

A continuación vienen ocho banderas de 1 bit. *CWR* y *ECE* se utilizan para indicar congestión cuando se usa ECN (Notificación Explícita de Congestión), como se especifica en el [[RFC]] 3168. *ECE* se establece para indicar una Eco de ECN (ECN-Echo) a un emisor TCP y decirle que reduzca su velocidad cuando el receptor TCP recibe una indicación de congestión de la red. *CWR* se establece para indicar una Ventana de congestión reducida del emisor TCP al receptor TCP, de modo que sepa que el emisor redujo su velocidad y puede dejar de enviar la Repetición de ECN.

*URG* se establece en 1 si está en uso el *Apuntador urgente*. El *Apuntador urgente* se usa para indicar un desplazamiento en bytes a partir del número de secuencia actual en el que se deben encontrar los datos urgentes. Este recurso sustituye los mensajes de interrupción. Este recurso es un mecanismo rudimentario para permitir que el emisor envíe una señal al receptor sin implicar a TCP en razón de la interrupción, pero se usa muy poco.

El bit *ACK* se establece en 1 para indicar que el *Número de confirmación de recepción* es válido. Éste es el caso para casi todos los paquetes. Si *ACK* es 0, el segmento no contiene una confirmación de recepción, por lo que se ignora el campo *Número de confirmación de recepción*.

El bit *PSH* indica datos que se deben transmitir de inmediato. Por este medio se solicita atentamente al receptor que entregue los datos a la aplicación a su llegada y no los almacene en búfer hasta que se haya recibido un búfer completo (lo que podría hacer en otras circunstancias por razones de eficiencia).

El bit *RST* se usa para restablecer de manera repentina una conexión que se ha confundido debido a una falla de host o alguna otra razón. También se usa para rechazar un segmento no válido o un intento de abrir una conexión. Por lo general, si usted recibe un segmento con el bit *RST* encendido, tiene un problema entre manos.

El bit *SYN* se usa para establecer conexiones. La solicitud de conexión tiene *SYN* = 1 y *ACK* = 0 para indicar que el campo de confirmación de recepción superpuesto no está en uso. Pero la respuesta de conexión sí lleva una confirmación de recepción, por lo que tiene *SYN* = 1 y *ACK* = 1. En esencia, el bit *SYN* se usa para denotar CONNECTION REQUEST y CONNECTION ACCEPTED, y el bit *ACK* sirve para distinguir entre ambas posibilidades.

El bit *FIN* se usa para liberar una conexión y especifica que el emisor no tiene más datos que transmitir. Sin embargo, después de cerrar una conexión, el proceso encargado del cierre puede continuar recibiendo datos de manera indefinida. Ambos segmentos *SYN* y *FIN* tienen números de secuencia y, por tanto, se garantiza su procesamiento en el orden correcto.

El control de flujo en TCP se maneja mediante una ventana deslizante de tamaño variable. El campo *Tamaño de ventana* indica la cantidad de bytes que se pueden enviar, comenzando por el byte cuya recepción se ha confirmado. Un campo de *Tamaño de ventana* de 0 es válido e indica que se han recibido los bytes hasta *Número de confirmación de recepción* − 1, inclusive, pero que el receptor no ha tenido oportunidad de consumir los datos y ya no desea más datos por el momento. El receptor puede otorgar permiso más tarde para enviar mediante la transmisión de un segmento con el mismo *Número de confirmación de recepción* y un campo *Tamaño de ventana* distinto de cero.

A diferencia de los [[protocolos de ventana deslizante]] de capa 2, en TCP, las confirmaciones de recepción y los permisos para enviar datos adicionales son por completo independientes. En efecto, un receptor puede decir: “He recibido bytes hasta k, pero por ahora no deseo más”. Esta independencia (de hecho, una ventana de tamaño variable) proporciona una flexibilidad adicional.

También se proporciona una *Suma de verificación* para agregar confiabilidad. Realiza una suma de verificación del encabezado, los datos y un pseudoencabezado conceptual exactamente de la misma forma que [[UDP]], sólo que el pseudoencabezado tiene el número de protocolo para TCP (6) y la suma de verificación es obligatoria.

El campo Opciones ofrece una forma de agregar las características adicionales que no están cubiertas por el encabezado normal. Se han definido muchas opciones, de las cuales varias se usan con frecuencia. Las opciones son de longitud variable, llenan un múltiplo de 32 bits mediante la técnica de relleno con ceros y se pueden extender hasta 40 bytes para dar cabida al encabezado TCP más largo que se pueda especificar. Algunas opciones se transmiten cuando se establece una conexión para negociar o informar al otro extremo sobre las capacidades disponibles. Otras opciones se transmiten en paquetes durante el tiempo de vida de la conexión. Cada opción tiene una codificación Tipo-LongitudValor (TLV).

Una opción muy utilizada es la que permite a cada host especificar el **MSS (Maximum Segment Size)** que está dispuesto a aceptar. Es más eficiente usar segmentos grandes que segmentos pequeños, debido a que el encabezado de 20 bytes se puede amortizar entre más datos sean, pero los hosts pequeños tal vez no puedan manejar segmentos muy grandes. Durante el establecimiento de la conexión, cada lado puede anunciar su máximo y ver el de su compañero. Si un host no usa esta opción, tiene una carga útil predeterminada de 536 bytes. Se requiere que todos los hosts de Internet acepten segmentos TCP de 536 + 20 = 556 bytes. No es necesario que el tamaño máximo de segmento en ambas direcciones sea el mismo

#### Establecimiento de una conexión TCP
En TCP las conexiones se establecen mediante el acuerdo de tres vías. Para establecer una conexión, uno de los lados (digamos que el servidor) espera en forma pasiva una conexión entrante mediante la ejecución de las primitivas LISTEN y ACCEPT en ese orden, ya sea que se especifique un origen determinado o a nadie en particular.

El otro lado (digamos que el cliente) ejecuta una primitiva CONNECT en la que especifica la dirección y el puerto con el que se desea conectar, el tamaño máximo de segmento TCP que está dispuesto a aceptar y de manera opcional algunos datos de usuario (por ejemplo, una contraseña). La primitiva CONNECT envía un segmento TCP con el bit SYN encendido y el bit ACK apagado, y espera una respuesta.

Cuando este segmento llega al destino, la entidad TCP de ahí revisa si hay un proceso que haya ejecutado una primitiva LISTEN en el puerto que se indica en el campo *Puerto de destino*. Si no lo hay, envía una respuesta con el bit RST encendido para rechazar la conexión.

Si algún proceso está escuchando en el puerto, ese proceso recibe el segmento TCP entrante y puede entonces aceptar o rechazar la conexión. Si la acepta, se devuelve un segmento de confirmación de recepción.

![[TCP_establecimiento_de_una_conexion.png]]

#### Liberación de una conexión TCP
Aunque las conexiones TCP son full dúplex, para entender la manera en que se liberan las conexiones es mejor visualizarlas como un par de conexiones simplex. Cada conexión simplex se libera de manera independiente de su igual. Para liberar una conexión, cualquiera de las partes puede enviar un segmento TCP con el bit *FIN* establecido, lo que significa que no tiene más datos por transmitir. Al confirmarse la recepción de *FIN*, se apaga ese sentido para que no se transmitan nuevos datos. Sin embargo, lo datos pueden seguir fluyendo de manera indefinida por el otro sentido. Cuando se apagan ambos sentidos, se libera la conexión. Por lo general **se requieren cuatro segmentos TCP para liberar una conexión**: un *FIN* y un *ACK* para cada sentido. Sin embargo, es posible que el primer *ACK* y el segundo *FIN* estén contenidos en el mismo segmento, con lo cual se reduce la cuenta total a tres.

Para evitar el problema de los dos ejércitos, se usan temporizadores. Si no llega una respuesta a un *FIN* en un máximo de dos tiempos de vida del paquete, el emisor del *FIN* libera la conexión. Tarde o temprano el otro lado notará que, al parecer, ya nadie lo está escuchando, y también expirará su temporizador. Aunque esta solución no es perfecta, dado el hecho de que teóricamente es imposible una solución perfecta, tendremos que conformarnos con ella. En la práctica, pocas veces ocurren problema.

### Modelado de administración de conexiones TCP
Los pasos requeridos para establecer y liberar conexiones se pueden representar en una máquina de estados finitos con los 11 estados que se listan más adelante. Al ocurrir un evento legal, debe emprenderse alguna acción. Si ocurre algún otro evento, se reporta un error.

Cada conexión comienza en el estado CLOSED (cerrado) y deja ese estado cuando hace una apertura pasiva (LISTEN) o una apertura activa (CONNECT). Si el otro lado realiza la acción opuesta, se establece una conexión y el estado se vuelve ESTABLISHED (establecida). La liberación de la conexión se puede iniciar desde cualquiera de los dos lados. Al completarse, el estado regresa a CLOSED.

| Estado      | Descripción                                    |
| ----------- | ---------------------------------------------- |
| CLOSED      | No hay conexión activa o pendiente.            |
| LISTEN      | El servidor espera una llamada entrante.       |
| SYN RCVD    | Llegó una solicitud de conexión; espera ACK.   |
| SYN SENT    | La aplicación empezó a abrir una conexión.     |
| ESTABLISHED | El estado normal de transferencia de datos.    |
| FIN WAIT 1  | La aplicación notificó que ya terminó.         |
| FIN WAIT 2  | El otro lado acordó liberar.                   |
| TIME WAIT   | Espera a que todos los paquetes expiren.       |
| CLOSING     | Ambos lados intentaron cerrar al mismo tiempo. |
| CLOSE       | WAIT El otro lado inició una liberación.       |
| LAST        | ACK Espera a que todos los paquetes expiren.   |

El caso común de un cliente que se conecta activamente a un servidor pasivo se indica con líneas gruesas (continuas para el cliente, punteadas para el servidor). Las líneas delgadas son secuencias de eventos no usuales. Cada línea de la máquina se marca mediante un par *evento/acción*. El evento puede ser una llamada de sistema iniciada por el usuario (CONNECT, LISTEN, SEND o CLOSE), la llegada de un segmento (*SYN*, *FIN*, *ACK* o *RST*) o, en un caso, una expiración de temporizador del doble del tiempo de vida máximo del paquete. La acción es el envío de un segmento de control (*SYN*, *FIN* o *RST*) o nada, lo cual se indica mediante (—). Los comentarios aparecen entre paréntesis.

![[TCP_maquina_de_estados_finitos.png]]

#### Ventana deslizante de TCP
La administración de ventanas en TCP separa los aspectos de la confirmación de la recepción correcta de los segmentos y la asignación del búfer en el receptor. Por ejemplo, suponga que el receptor tiene un búfer de 4096 bytes, como se muestra en la figura 6-40. Si el emisor transmite un segmento de 2048 bytes que se recibe correctamente, el receptor enviará la confirmación de recepción del segmento. Sin embargo, dado que ahora sólo tiene 2048 bytes de espacio de búfer (hasta que la aplicación retire algunos datos de éste), anunciará una ventana de 2048 comenzando con el siguiente byte esperado.

![[TCP_ventana_deslizante.png]]

Ahora el emisor envía otros 2048 bytes, para los cuales el receptor envía la confirmación de recepción, pero la ventana anunciada tiene un tamaño de 0. El emisor debe detenerse hasta que el proceso de aplicación en el host receptor retire algunos datos del búfer, momento en el que TCP podrá anunciar una ventana más grande y se podrán enviar más datos.

Cuando la ventana es de 0, el emisor por lo general no puede enviar segmentos, salvo en dos situaciones. En primer lugar, se pueden enviar datos urgentes (por ejemplo, para permitir que el usuario elimine el proceso en ejecución en la máquina remota). En segundo lugar, el emisor puede enviar un segmento de 1 byte para hacer que el receptor vuelva a anunciar el siguiente byte esperado y el tamaño de la ventana. Este paquete se denomina **sonda de ventana**. El estándar TCP proporciona explícitamente esta opción para evitar un interbloqueo si llega a perderse una actualización de ventana