La **capa de red** controla la operación de la [[Subred|subred]]. Una cuestión clave de diseño es determinar cómo se encaminan los paquetes desde el origen hasta el destino. Las rutas se pueden basar en tablas estáticas que se “codifican” en la red y rara vez cambian, aunque es más común que se actualicen de manera automática para evitar las fallas en los componentes. También se pueden determinar el inicio de cada conversación; por ejemplo, en una sesión de terminal al iniciar sesión en una máquina remota. Por último, pueden ser muy dinámicas y determinarse de nuevo para cada paquete, de manera que se pueda reflejar la carga actual en la red. ^extracto

Si hay demasiados paquetes en la subred al mismo tiempo, se interpondrán en el camino unos con otros y formarán cuellos de botella. El manejo de la [[Congestión|congestión]] también es responsabilidad de la capa de red, en conjunto con las capas superiores que adaptan la carga que colocan en la red. Otra cuestión más general de la capa de red es la calidad del servicio proporcionado (retardo, tiempo de tránsito, variaciones, etcétera)
Cuando un paquete tiene que viajar de una red a otra para llegar a su destino, pueden surgir muchos problemas. El direccionamiento utilizado por la segunda red puede ser distinto del que utiliza la primera. La segunda red tal vez no acepte el paquete debido a que es demasiado grande. Los protocolos pueden ser diferentes, etc. Es responsabilidad de la capa de red solucionar todos estos problemas para permitir la interconexión de redes heterogéneas.

> La capa de red es la capa más baja que maneja la transmisión de extremo a extremo.

## Servicios proporcionados a la capa de transporte
La capa de red proporciona servicios a la [[Capa de transporte]] en la interfaz entre estas. Una pregunta importante es qué tipo de servicios proporciona precisamente la capa de red a la capa de transporte. La discución se centra en determinar si la capa de red debe proporcionar un [[Servicio orientado y no a la conexión|servicio orientado a la conexión o un servicio sin conexión]].

Un bando (representado por la comunidad de [[Internet]]) declara que la tarea de los enrutadores es mover paquetes de un lado a otro, y nada más. Desde su punto de vista, la red es de naturaleza no confiable, sin importar su diseño. Por lo tanto, los hosts deben aceptar este hecho y efectuar ellos mismos el control de errores y control de flujo.

Este punto de vista conduce a la conclusión de que el servicio de red debe ser sin conexión y debe contar tan sólo con las primitivas SEND PACKET y RECEIVE PACKET. En particular, no debe efectuarse ningún ordenamiento de paquetes ni control de flujo, pues de todos modos los hosts lo van a efectuar y por lo general se obtiene poca ganancia al hacerlo dos veces. Este razonamiento es un ejemplo del **argumento extremo a extremo** (*end-to-end argument*), un principio de diseño que ha sido muy influyente para dar forma a Internet. Además, cada paquete debe llevar la dirección de destino completa, porque cada paquete enviado se transporta de manera independiente a sus antecesores, si los hay.

El otro bando (representado por las compañías telefónicas) argumenta que la red debe proporcionar un servicio confiable, orientado a conexión. Desde este punto de vista, la calidad del servicio es el factor dominante y, sin conexiones en la red, tal calidad es muy difícil de alcanzar, en especial para el tráfico de tiempo real como la voz y el video.

Si se ofrece el servicio sin conexión, los paquetes se transmiten por separado en la red y se enrutan de manera independiente. No se necesita una configuración por adelantado. En este contexto, por lo general los paquetes se conocen como **datagramas** y la red se conoce como **red de datagramas**. Si se utiliza el servicio orientado a conexión, hay que establecer una ruta del enrutador de origen al enrutador de destino antes de poder enviar cualquier paquete de datos. Esta conexión se conoce como **VC (circuito virtual)**, en analogía con los circuitos físicos establecidos por el sistema telefónico, y la red se denomina **red de circuitos virtuales**.

![[capa_de_red_comparacion_1.png]]

### Implementación red de datagramas
Cuando un host envía un paquete a través de una red de datagramas, este paquete es recibido por el primer enrutador, el cual analiza el destino deseado y determina la ruta más adecuada en ese instante. Al recibir el siguiente paquete vuelve a realizar el mismo proceso, el cual puede dar una ruta distinta a la primera por haber cambiado algo en la red. El algorítmo que maneja las tablas y realiza las decisiones de enrutamiento se conoce como **algoritmo de enrutamiento**.

El [[IP]], que constituye la base de [[Internet]], es el ejemplo dominante de un servicio de red sin conexión. Cada paquete transporta una dirección IP de destino que los enrutadores usan para reenviar cada paquete por separado. Las direcciones son de 32 bits en los paquetes IPv4 y de 128 bits en los paquetes IPv6.

### Implementación red de circuitos virtuales
La idea detrás de los circuitos virtuales es evitar la necesidad de elegir una nueva ruta para cada paquete enviado. En cambio, cuando se establece una conexión, se elige una ruta de la máquina de origen a la máquina de destino como parte de la configuración de conexión y se almacena en tablas dentro de los enrutadores. Esa ruta se utiliza para todo el tráfico que fluye a través de la conexión, de la misma forma en que funciona el sistema telefónico. Cuando se libera la conexión, también se termina el circuito virtual. Con el servicio orientado a conexión, cada paquete lleva un identificador que indica a cuál circuito virtual pertenece

En algunos contextos, a este proceso se le conoce como **conmutación mediante etiquetas**. **MPLS (MultiProtocol Label Swithching)** es un ejemplo de servicio de red orientado a conexión. Se utiliza dentro de las redes de ISP en Internet, en donde los paquetes IP se envuelven en un encabezado MPLS que tiene un identificador de conexión o etiqueta de 20 bits.

## Algoritmos de enrutamiento
![[Algoritmos de enrutamiento]]

## Interconexión de redes
![[Interconexión de redes]]