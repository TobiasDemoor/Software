---
aliases: [direcciones IP, dirección IP, IP address]
---
Una característica que define a IPv4 consiste en sus direcciones de 32 bits. Cada host y enrutador de [[Internet]] tiene una dirección IP que se puede usar en los campos Dirección de origen y Dirección de destino de los paquetes [[IP]]. Es importante tener en cuenta que una dirección IP en realidad *no se refiere a un host, sino a una interfaz de red*, por lo que si un host está en dos redes, debe tener dos direcciones IP. Sin embargo, en la práctica la mayoría de los hosts están en una red y, por ende, tienen una dirección IP. En contraste, los enrutadores tienen varias interfaces y, por lo tanto, múltiples direcciones IP.

### Prefijos
A diferencia de las direcciones Ethernet, las direcciones IP son jerárquicas. Cada dirección de 32 bits está compuesta de una **porción de red** de longitud variable en los bits superiores, y de una **porción de host** en los bits inferiores. La porción de red tiene el mismo valor para todos los hosts en una sola red, como una LAN Ethernet. Esto significa que una red corresponde a un bloque contiguo de espacio de direcciones IP. A este bloque se le llama **prefijo**.

Las direcciones IP se escriben en notación decimal con puntos. En este formato, cada uno de los 4 bytes se escribe en decimal, de 0 a 255. Para escribir los prefijos, se proporciona la dirección IP menor en el bloque y el tamaño del mismo. El tamaño se determina mediante el número de bits en la porción de red; el resto de los bits en la porción del host pueden variar. Esto significa que el tamaño debe ser una potencia de dos. Por convención, el prefijo se escribe después de la dirección IP como una barra diagonal seguida de la longitud en bits de la porción de red. La longitud del prefijo corresponde a una máscara binaria de 1s en la porción de red. Cuando se escribe de esta forma, se denomina **máscara de subred**. Se puede aplicar un AND a la máscara de subred con la dirección IP para extraer sólo la porción de la red.

![[RRCC_direccion_ip_prefijo_y_mascara.png]]

Las direcciones jerárquicas tienen ventajas y desventajas considerables. La ventaja clave de los prefijos es que los enrutadores pueden reenviar paquetes con en base en la porción de red de la dirección, siempre y cuando cada una de las redes tenga un bloque de direcciones único. La porción del host no importa a los enrutadores, ya que enviarán en la misma dirección a todos los hosts de la misma red. Sólo hasta que los paquetes llegan a la red de destino es cuando se reenvían al host correcto. Esto hace que las tablas de enrutamiento sean mucho más pequeñas de lo que podrían ser con cualquier otro método.

Aunque el uso de una jerarquía permite a Internet escalar, tiene dos desventajas. En primer lugar, la dirección IP de un host depende de su ubicación en la red. Se necesitan diseños como IP móvil para soportar hosts que se desplacen de una red a otra, pero que deseen mantener las mismas direcciones IP.

La segunda desventaja es que la jerarquía desperdicia direcciones a menos que se administre con cuidado. Si se asignan direcciones a las redes en bloques (muy) grandes, habrá (muchas) direcciones que se asignen pero no se utilicen.

#### Subredes
![[Subredes IP]]

#### Superredes
![[Superredes IP]]

#### Direccionamiento con clases
Antes de 1993, las direcciones IP se dividían en cinco categorías llamadas clases, esta asignación se denominó **direccionamiento con clases**.

![[RRCC_direcciones_ip_clases.png]]

Existen más de 2000 millones de direcciones, pero al organizar el espacio de direcciones en clases se desperdician millones de ellas. En particular, el verdadero villano es la red clase B. Para la mayoría de las organizaciones, una red clase A con 16 millones de direcciones es demasiado grande, y una red clase C con 256 direcciones es muy pequeña. Una red clase B con 65536 direcciones es justo lo necesario. En el folclor de Internet, esta situación se conoce como el **problema de los tres osos**.

En realidad, una dirección clase B es demasiado grande para la mayoría de las organizaciones. Hay estudios que demuestran que más de la mitad de todas las redes clase B tienen menos de 50 hosts. Una red clase C habría bastado, pero sin duda todas las organizaciones que solicitaron una dirección clase B pensaron que un día el campo de hosts de 8 bits les quedaría pequeño. En retrospectiva, podría haber sido mejor que las redes clase C usaran 10 bits en lugar de 8 para el número de host, permitiendo 1022 hosts por red. De haber sido éste el caso, la mayoría de las organizaciones probablemente se habría conformado con una red clase C y hubiera existido medio millón de ellas (en vez de sólo 16384 redes clase B).

Para lidiar con estos problemas se introdujeron las subredes para asignar de manera flexible bloques de direcciones dentro de una organización. Después se agregó el CIDR para reducir el tamaño de la tabla de enrutamiento global. Hoy en día, los bits que indican si una dirección IP pertenece a una red clase A, B o C ya no se utilizan, aunque las referencias a estas clases en la literatura siguen siendo comunes

También existen otras direcciones con significados especiales. La dirección IP 0.0.0.0, que es la dirección más baja, es utilizada por los hosts al momento de encenderlos. Significa “esta red” o “este host”. Las direcciones IP con 0 como número de red se refieren a la red actual. Estas direcciones permiten que las máquinas hagan referencia a su propia red sin conocer su número (pero tienen que conocer la máscara de red para saber cuántos 0s incluir). La dirección que consiste sólo en 1s, o 255.255.255.255 (la dirección más alta), se utiliza para indicar a todos los hosts en la red especificada. Permite la difusión en la red local, por lo general una LAN. Las direcciones con un número de red apropiado y 1s en el campo de host permiten a las máquinas enviar paquetes de difusión a redes LAN distantes en cualquier parte de Internet. Sin embargo, muchos administradores de red deshabilitan esta característica, ya que es sobre todo un peligro de seguridad. Por último, todas las direcciones de la forma 127.xx.yy.zz se reservan para las pruebas de loopback. Los paquetes que se envían a esa dirección no se ponen en el cable; se procesan en forma local y se tratan como si fueran paquetes entrantes. Esto permite enviar paquetes al host sin que el emisor conozca su número, lo cual es útil para realizar pruebas.

![[RRCC_direcciones_ip_especiales.png]]

#### Enrutamiento Interdominio Classless
Los enrutadores en las organizaciones en el extremo de una red, como una universidad, necesitan tener una entrada para cada una de sus subredes, de manera que el enrutador pueda saber qué línea usar para llegar a esa red. Para las rutas a destinos fuera de la organización, sólo necesitan usar la regla simple predeterminada de enviar los paquetes en la línea hacia el ISP que conecta a la organización con el resto de Internet. Las otras direcciones de destino deben estar por ahí en alguna parte.

Los enrutadores en los ISP y las redes troncales en medio de Internet no se pueden dar esos lujos. Ellos deben saber qué ruta tomar hacia cada una de las redes; aquí no funciona la regla simple predeterminada. Se dice que estos enrutadores básicos están en la **zona libre predeterminada** de Internet. Nadie sabe en realidad cuántas redes están conectadas a Internet, pero es una gran cantidad, por lo menos un millón. Esto puede generar una tabla muy grande.

Con la agregación (superredes), las direcciones IP están contenidas en prefijos de diversos tamaños. La misma dirección IP que un enrutador trata como parte de un prefijo /22 (un bloque que contiene 210 direcciones), puede ser tratada por otro enrutador como parte de un prefijo /20 más grande (que contiene 212 direcciones). Es responsabilidad de cada enrutador tener la información del prefijo correspondiente. Este diseño funciona con las subredes y se conoce como **CIDR (Classless InterDomain Routing)** o enrutamiento interdominio sin clases.

![[RRCC_direcciones_ip_cidr.png]]

En concepto, el CIDR funciona de la siguiente manera. Cuando llega un paquete, se explora la tabla de enrutamiento para determinar si el destino está dentro del prefijo. Es posible que coincidan varias entradas con distintas longitudes de prefijos, en cuyo caso se utiliza la entrada con el prefijo más largo.