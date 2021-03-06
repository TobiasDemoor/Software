---
aliases: ["modelo TCP/IP"]
---
El **modelo de referencia TCP/IP** toma su nombre debido a sus dos [[Protocolo|protocolos]] primarios ([[TCP]] e [[IP]]). Es posterior al [[Modelo OSI|modelo de referencia OSI]] y sus objetivos principales son permitir conectar varias [[Redes de computadoras|redes]] sin problemas y sobrevivir a la pérdida de hardware de la [[Subred|subred]] sin que se interrumpieran las conversaciones existentes.

![[RRCC_model_tcp_ip_1.png]]

![[RRCC_modelo_tcp_ip_2.png]]

## Capas
### La capa de enlace
Todos estos requerimientos condujeron a la elección de una red de [[Conmutación#Conmutacion de paquetes|conmutación de paquetes]] basada en una capa sin conexión que opera a través de distintas redes. La capa más baja en este modelo es la **capa de enlace**; ésta describe qué enlaces (como las líneas seriales y Ethernet clásica) se deben llevar a cabo para cumplir con las necesidades de esta capa de interred sin conexión. En realidad no es una capa en el sentido común del término, sino una interfaz entre los hosts y los enlaces de transmisión. El primer material sobre el modelo TCP/IP tiene poco que decir sobre ello.

### La capa de interred
Esta capa es el eje que mantiene unida a toda la arquitectura. Su trabajo es permitir que los hosts inyecten paquetes en cualquier red y que viajen de manera independiente hacia el destino (que puede estar en una red distinta). Incluso pueden llegar en un orden totalmente diferente al orden en que se enviaron, en cuyo caso es responsabilidad de las capas más altas volver a ordenarlos, si se desea una entrega en orden. Tenga en cuenta que aquí utilizamos “interred” en un sentido genérico, aunque esta capa esté presente en la [[Internet|Internet]].
La capa de interred define un formato de paquete y un protocolo oficial llamado **[[IP]] (Internet Protocol)**, además de un protocolo complementario llamado **[[ICMP]] (Internet Control Message Protocol)** que le ayuda a funcionar. La tarea de la capa de interred es entregar los paquetes [[IP]] a donde se supone que deben ir. Aquí el ruteo de los paquetes es sin duda el principal aspecto, al igual que la [[Congestión|congestión]] (aunque el [[IP]] no ha demostrado ser efectivo para evitar la congestión)

### La capa de transporte
Por lo general, a la capa que está arriba de la capa de interred en el modelo TCP/IP se le conoce como **capa de transporte**; y está diseñada para permitir que las entidades pares, en los nodos de origen y de destino, lleven a cabo una conversación, al igual que en la [[Capa de transporte|capa de transporte de OSI]]. Aquí se definieron dos protocolos de transporte de extremo a extremo. El primero, **[[TCP]] (Transmission Control Protocol)**, es un [[Servicio orientado y no a la conexión|protocolo confiable orientado a la conexión]] que permite que un flujo de bytes originado en una máquina se entregue sin errores a cualquier otra máquina en la interred. Este protocolo segmenta el flujo de bytes entrante en mensajes discretos y pasa cada uno a la capa de interred. En el destino, el proceso TCP receptor vuelve a ensamblar los mensajes recibidos para formar el flujo de salida. El TCP también maneja el control de flujo para asegurar que un emisor rápido no pueda inundar a un receptor lento con más mensajes de los que pueda manejar.

El segundo protocolo en esta capa, **[[UDP]] (User Datagram Protocol)**, es un [[Servicio orientado y no a la conexión|protocolo no orientado a la conexión]], no confiable para aplicaciones que no desean la asignación de secuencia o el control de flujo de TCP y prefieren proveerlos por su cuenta. También se utiliza mucho en las consultas de petición-respuesta de una sola ocasión del tipo [[Client-Server|cliente-servidor]], y en las aplicaciones en las que es más importante una entrega oportuna que una entrega precisa, como en la transmisión de voz o video.

### La capa de aplicación
El modelo TCP/IP no tiene capas de sesión o de presentación, ya que no se consideraron necesarias. Las aplicaciones simplemente incluyen cualquier función de sesión y de presentación que requieran. La experiencia con el [[Modelo OSI|modelo OSI]] ha demostrado que esta visión fue correcta: estas capas se utilizan muy poco en la mayoría de las aplicaciones.
Encima de la capa de transporte se encuentra la **capa de aplicación**. Ésta contiene todos los protocolos de alto nivel. Entre los primeros protocolos están el de terminal virtual (TELNET), transferencia de archivos ([[FTP]]) y correo electrónico ([[SMTP]]). A través de los años se han agregado muchos otros protocolos.

## Fortalezas
En contraste al [[Modelo OSI|modelo de referencia OSI]], la fortaleza del [[Modelo TCP IP|modelo de referencia TCP/IP]] son los *[[Protocolo|protocolos]]*, que se han utilizado mucho durante varios años.

## Análisis
Al principio, el [[Modelo TCP IP|modelo TCP/IP]] no tenía una distinción clara entre los servicios, las interfaces y los protocolos, aunque las personas han tratado de reajustarlo a fin de hacerlo más parecido al [[Modelo OSI|OSI]]. Por ejemplo, los únicos servicios que realmente ofrece la capa de interred son *SEND IP PACKET* y *RECIEVE IP PACKET*. Como consecuancia, los protocolos en el [[Modelo OSI|modelo OSI]] están ocultos de una mejor forma que en el [[Modelo TCP IP|modelo TCP/IP]], además se pueden reemplazar con relativa facilidad a medida que la tecnología cambia. La capacidad de realizar dichos cambios con [[Transparencia|transparencia]] es uno de los principales propósitos de tener protocolos en capas en primer lugar ([[Layers|patron capas]]). 

## Críticas
Primero que nada como fue mencionado antes el [[Modelo TCP IP|modelo]] no diferencia con claridad los conceptos de servicios, interfaces y protocolos. La buena práctica de la ingeniería de software requiere una distinción entre la especificación y la implementación, algo que [[Modelo OSI|OSI]] hace con mucho cuidado y que TCP/IP no. En consecuencia, el modelo TCP/IP no sirve mucho de guía para diseñar modernas redes que utilicen nuevas tecnologías.

Segundo, el modelo TCP/IP no es nada general y no es muy apropiado para describir cualquier [[Pila de protocolos|pila de protocolos]] aparte de TCP/IP. Por ejemplo, es imposible tratar de usar el modelo TCP/IP para describir Bluetooth.

Tercero, la capa de enlace en realidad no es una capa en el sentido normal del término como se utiliza en el contexto de los protocolos en capas ([[Layers|patrón capas]]. Es una [[Interfaz|interfaz]] (entre las capas de red y de enlace de datos). La diferencia entre una interfaz y una capa es crucial, y hay que tener mucho cuidado al respecto.

Cuarto, el modelo TCP/IP no distingue entre la capa física y la de enlace de datos. Éstas son completamente distintas. La capa física trata sobre las características de transmisión del cable de cobre, la fibra óptica y la comunicación inalámbrica. La tarea de la capa de enlace de datos es delimitar el inicio y el fin de las tramas, además de transmitirlas de un extremo al otro con el grado deseado de confiabilidad. Un modelo apropiado debe incluir ambas capas por separado. El modelo TCP/IP no hace esto.

Por último, aunque los protocolos [[IP]] y [[TCP]] se diseñaron e implementaron con sumo cuidado, muchos de los otros protocolos se fueron creando según las necesidades del momento, producidos generalmente por un par de estudiantes de licenciatura que los mejoraban hasta fastidiarse. Después las implementaciones de los protocolos se distribuían en forma gratuita, lo cual trajo como consecuencia que se utilizaran amplia y profundamente en muchas partes y, por ende, eran difíciles de reemplazar. Algunos de ellos son un poco vergonzosos en la actualidad. Por ejemplo, el protocolo de terminal virtual TELNET se diseñó para una terminal de Teletipo mecánica de 10 caracteres por segundo. No sabe nada sobre las interfaces gráficas de usuario y los ratones. Sin embargo, aún se sigue usando a 30 años de su creación.