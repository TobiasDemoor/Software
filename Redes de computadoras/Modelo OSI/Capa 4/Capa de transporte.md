---
aliases: ["capa de transporte", "capa 4"]
---
La función básica de la **capa de transporte** es aceptar datos de la capa superior, dividirlos en unidades más pequeñas (**segmentos** o **datagramas**) si es necesario, pasar estos datos a la capa de red y asegurar que todas las piezas lleguen correctamente al otro extremo. Además, todo esto se debe realizar con eficiencia y de una manera que aísle las capas superiores de los inevitables cambios en la tecnología de hardware que se dan con el transcurso del tiempo. ^extracto

La capa de transporte también determina el tipo de servicio que debe proveer a la capa de sesión y, en última instancia, a los usuarios de la red. El tipo más popular de conexión de transporte es un canal [[P2P|punto a punto]] libre de errores que entrega los mensajes o bytes en el orden en el que se enviaron. Sin embargo existen otros posibles tipos de servicio de transporte, como el de mensajes aislados sin garantía sobre el orden de la entrega y la difusión de mensajes a múltiples destinos. El tipo de servicio se determina al establecer la conexión (cabe mencionar que es imposible lograr un canal libre de errores; lo que se quiere decir en realidad con este término es que la tasa de errores es lo bastante baja como para ignorarla en la práctica).

La capa de transporte es una verdadera capa de extremo a extremo; lleva los datos por toda la ruta desde el origen hasta el destino (**conectividad de extremo a extremo**). En otras palabras, un programa en la máquina de origen lleva a cabo una conversación con un programa similar en la máquina de destino mediante el uso de los encabezados en los mensajes y los mensajes de control. En las capas inferiores cada uno de los protocolos está entre una máquina y sus vecinos inmediatos, no entre las verdaderas máquinas de origen y de destino, que pueden estar separadas por muchos enrutadores. En el diagrama del [[Modelo OSI|modelo OSI]] se muestra la diferencia entre las capas de la 1 a la 3, que están encadenadas, y entre las capas de la 4 a la 7, que son de extremo a extremo.

## Servicios proporcionados a capas superiores
La meta fundamental de la capa de transporte es proporcionar un servicio de transmisión de datos eficiente, confiable y económico a sus usuarios, procesos que normalmente son de la [[Capa de aplicación]]. Para lograr este objetivo, la capa de transporte utiliza los servicios proporcionados por la [[capa de red]]. El hardware o software de la capa de transporte que se encarga del trabajo se llama **entidad de transporte**, la cual puede localizarse en el kernel (núcleo) del [[Sistemas Operativos|sistema operativo]], en un paquete de biblioteca que forma parte de las aplicaciones de red, en un proceso de usuario separado o incluso en la tarjeta de interfaz de red. Las primeras dos opciones son las más comunes en Internet.

![[RRCC_capa_de_transporte_1.png]]

Así como hay dos tipos de servicio de red, orientado a conexión y sin conexión, también hay dos tipos de servicio de transporte. El que está orientado a conexión es parecido en muchos sentidos al servicio de red orientado a conexión. En ambos casos, las conexiones tienen tres fases: establecimiento, transferencia de datos y liberación. El direccionamiento y el control de flujo también son similares en ambas capas. Además, el servicio de transporte sin conexión es muy parecido al servicio de red sin conexión. Sin embargo, puede ser difícil proveer un servicio de transporte sin conexión encima de un servicio de red orientado a conexión, ya que es ineficiente establecer una conexión para enviar un solo paquete y deshacerla justo después.

La pregunta obvia es: si el servicio de la capa de transporte es tan parecido al de la capa de red, ¿por qué hay dos capas diferentes? ¿Por qué no es suficiente una sola capa? La respuesta es sutil, pero crucial. El código de transporte se ejecuta por completo en las máquinas de los usuarios, pero la capa de red se ejecuta en su mayor parte en los enrutadores, los cuales son operados por la empresa portadora (por lo menos en el caso de una red de área amplia). ¿Qué sucede si la capa de red ofrece un servicio inadecuado? ¿Qué tal si esa capa pierde paquetes con frecuencia? ¿Qué ocurre si los enrutadores fallan de vez en cuando?

Problemas, eso es lo que ocurre. Los usuarios no tienen un control real sobre la capa de red, por lo que no pueden resolver los problemas de un mal servicio usando mejores enrutadores o incrementando el manejo de errores en la capa de enlace de datos, puesto que no son dueños de los enrutadores. **La única posibilidad es poner encima de la capa de red otra capa que mejore la calidad del servicio.** En esencia, la existencia de la capa de transporte hace posible que el servicio de transporte sea más confiable que la red subyacente.

Por esta razón, muchas personas han establecido una distinción cualitativa entre las capas 1 a 4, por una parte, y la(s) capa(s) por encima de la 4, por la otra. Las cuatro capas inferiores se pueden ver como el **proveedor del servicio de transporte**, mientras que la(s) capa(s) superior(es) son el **usuario del servicio de transporte**. Esta distinción entre proveedor y usuario tiene un impacto considerable en el diseño de las capas, además de que posiciona a la capa de transporte en un puesto clave, ya que constituye el límite principal entre el proveedor y el usuario del servicio confiable de transmisión de datos. Es el nivel que ven las aplicaciones

### Primitivas
Para permitir que los usuarios accedan al servicio de transporte, la capa de transporte debe proporcionar algunas operaciones a los programas de aplicación; es decir, una interfaz del servicio de transporte. Cada servicio de transporte tiene su propia interfaz.

El servicio de transporte es similar al servicio de red, pero también hay algunas diferencias importantes. La principal es que el propósito del servicio de red es modelar el servicio ofrecido por las redes reales, con todos sus problemas. Las redes reales pueden perder paquetes, por lo que el servicio de red por lo general no es confiable.

En cambio, el servicio de transporte orientado a conexión sí es confiable. Claro que las redes reales no están libres de errores, pero ése es precisamente el propósito de la capa de transporte: ofrecer un servicio confiable en una red no confiable.

Una segunda diferencia entre los servicios de red y de transporte es a quién están dirigidos. El servicio de red lo usan únicamente las entidades de transporte. Pocos usuarios escriben sus propias entidades de transporte y, por lo tanto, pocos usuarios o programas llegan a ver los aspectos internos del servicio de red. En contraste, muchos programas (y, por lo tanto, programadores) ven las primitivas de transporte. En consecuencia, el servicio de transporte debe ser conveniente y fácil de usar.

| Primitiva  | Paquete enviado    | Significado                                            |
| ---------- | ------------------ | ------------------------------------------------------ |
| LISTEN     | (ninguno)          | Se bloquea hasta que algún proceso intenta conectarse. |
| CONNECT    | CONNECTION REQ.    | Intenta activamente establecer una conexión.           |
| SEND       | DATA               | Envía información.                                     |
| RECEIVE    | (ninguno)          | Se bloquea hasta que llegue un paquete DATA.           |
| DISCONNECT | DISCONNECTION REQ. | Solicita que se libere la conexión                     |

> Se utilza el término **segmento** para indicar los mensajes que se envían de una entidad de transporte a otra. TCP, UDP y otros protocolos de Internet usan este término. Algunos protocolos antíguos usaban el nombre **TPDU (Transport Protocol Data Unit)**. Este término ya no se utiliza mucho, pero todavía se puede ver en publicaciones y libros antiguos.
> ![[RRCC_capa_de_transporte_segmento.png]]

### Berkeley Sockets
![[Berkeley Sockets]]

## Protocolos de transporte
![[Protocolos de transporte]]