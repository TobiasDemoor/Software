El **ICMP (Internet Control Message Protocol)** se encuentra en la [[Capa de red|capa de red]] y es un [[Protocolo|protocolo]] auxiliar a [[IP]]. Se encarga del los paquetes soltados (paquetes que llegan demasiado rápido para poder procesarse), de los fallos de conectividad (cuando no se puede alcanzar el sistema destino) y de la redirección (se redirige un sistema de envío para utilizar otro enrutador). Este protocolo se encuentra documentado en el **[[RFC]] 792**.

Los [[Router|enrutadores]] supervisan muy de cerca el funcionamiento de [[Internet]]. Cuando ocurre algo inesperado durante el procesamiento de un paquete en un enrutador, ICMP informa sobre el evento al emisor. ICMP también se utiliza para probar Internet. Hay definidos alrededor de una docena de tipos de mensajes ICMP, cada uno de los cuales se transporta encapsulado en un paquete IP. Se listan los más importantes a continuación:

| Tipo de mensaje                                                     | Descripción                                           |
| ------------------------------------------------------------------- | ----------------------------------------------------- |
| Destination unreachable (Destino inaccesible).                      | No se pudo entregar el paquete.                       |
| Time exceeded (Tiempo excedido).                                    | El tiempo de vida llegó a cero.                       |
| Parameter problem (Problema de parámetros).                         | Campo de encabezado inválido.                         |
| Source quench (Fuente disminuida).                                  | Paquete regulador.                                    |
| Redirect (Redireccionar).                                           | Enseña a un enrutador la geografía.                   |
| Echo and echo reply (Eco y respuesta de eco).                       | Verifica si una máquina está viva.                    |
| Timestamp request/reply (Estampa de tiempo, Petición/respuesta).    | Igual que solicitud de eco, pero con marca de tiempo. |
| Router advertisement/solicitation (Enrutamiento anuncio/solicitud). | Busca un enrutador cercano                            |

El mensaje DESTINATION UNREACHABLE (DESTINO INACCESIBLE) se usa cuando el enrutador no puede localizar el destino o cuando un paquete con el bit DF no puede entregarse porque hay una red de “paquetes pequeños” que se interpone en el camino.

El mensaje TIME EXCEEDED (TIEMPO EXCEDIDO) se envía al descartar un paquete porque su contador Ttl (Tiempo de vida) ha llegado a cero. Este evento es un síntoma de que los paquetes se están repitiendo o que los valores establecidos en el contador son muy bajos.

Un uso inteligente de este mensaje de error es la herramienta **traceroute** (tracert en Windows) desarrollada por Van Jacobson en 1987. Traceroute encuentra los enrutadores a lo largo de la ruta desde el host hasta una dirección IP de destino. Este método simplemente envía una secuencia de paquetes al destino, primero con un TtL de 1, después con un TtL de 2, 3 y así en lo sucesivo. Los contadores en estos paquetes llegarán a cero en los enrutadores sucesivos a lo largo de la ruta. Cada uno de estos enrutadores enviará obedientemente un mensaje TIME EXCEEDED de vuelta al host. A partir de estos mensajes el host puede determinar las direcciones IP de los enrutadores a lo largo de la ruta, así como mantener estadísticas y tiempos en ciertas partes de la ruta.

El mensaje PARAMETER PROBLEM (PROBLEMAS DE PARÁMETROS) indica que se ha descubierto un valor ilegal en un campo de encabezado. Este problema indica un error en el software de IP del host emisor, o tal vez en el software de un enrutador por el que se transita.

El mensaje SOURCE QUENCH (FUENTE DISMINUIDA) se utilizaba hace tiempo para regular a los hosts que estaban enviando demasiados paquetes. Se esperaba que cuando un host recibiera este mensaje, redujera la velocidad. En la actualidad raras veces se usa pues cuando ocurre una congestión, estos paquetes tienden a agravar más la situación y no está claro cómo responderles.

El mensaje REDIRECT (REDIRECCIONAR) se usa cuando un enrutador se percata de que un paquete parece estar mal enrutado. Lo utiliza el enrutador para avisar al host emisor que se actualice con una mejor ruta.

Los mensajes ECHO (ECO) y ECHO REPLY (RESPUESTA DE ECO) se utilizan para ver si un destino dado es alcanzable y está vivo. Se espera que el destino envíe de vuelta un mensaje ECHO REPLY luego de recibir el mensaje ECHO. Estos mensajes se utilizan en la herramienta **ping** que verifica si un host está activo en Internet.

Los mensajes TIMESTAMP REQUEST (PETICIÓN DE ESTAMPA DE TIEMPO) y TIMESTAMP REPLY (RESPUESTA DE ESTAMPA DE TIEMPO) son similares, excepto que el tiempo de llegada del mensaje y el tiempo de salida de la respuesta se registran en ésta. Esta característica se puede usar para medir el desempeño de la red.

Los mensajes ROUTER ADVERTISEMENT (ANUNCIO DE ENRUTADOR) y ROUTER SOLICITATION (SOLICITUD DE ENRUTADOR) se usan para permitir que los hosts encuentren los enrutadores cercanos. Un host necesita aprender la dirección IP de por lo menos un enrutador para enviar paquetes por la red local

Además de estos mensajes, se han definido otros. La lista en línea se conserva ahora en www.iana.org/assignments/icmp-parameters.