Se le conoce como WiFi al estándar de [[Wireless LAN|LAN inalámbrica]] definida en la norma **IEEE 802.11**. Es un estandar que se utiliza en la [[Capa de enlace de datos|capa de enlace a datos]] del modelo OSI. Al momento de su diseño se tomó como modelo a [[Ethernet]].

El primer problema era hallar una banda de frecuencia adecuada que estuviera disponible, de preferencia a nivel mundial. La metodología utilizada fue contraria a la que se utilizó en las redes de telefonía móvil. En vez de un espectro costoso bajo licencia, los sistemas 802.11 operan en bandas sin licencia como las bandas **ISM (Industrial, Scientifc, and Medical)** definidas por el [[Regulación del espectro electromagnético|ITU-R]]. Todos los dispositivos pueden usar este espectro siempre y cuando limiten su potencia de transmisión para dejar que coexistan distintos dispositivos. Desde luego que esto significa que los radios 802.11 podrían entrar en competencia con los teléfonos inalámbricos, los abridores de puertas de garaje y los hornos de microondas.

Las redes 802.11 están compuestas de clientes (como laptops y teléfonos móviles) y de una infraestructura llamada **AP ([[Access Point]])** que se instala en los edificios. Algunas veces a los puntos de acceso se les llama estaciones base. Los puntos de acceso se conectan a la red alámbrica y toda la comunicación entre los clientes se lleva a cabo a través de un punto de acceso.


## Capa física
[[Capa física|Capas físicas]] por orden cronológico:
- 802.11 Infrarrojo, FHSS, DSSS (estas dos últimas son codificaciones de espectro expandido)
- [[802.11b]] HR-DSSS (< 11 Mbps) (utiliza spread-spectrum) (2.4 GHz)
- [[802.11a]] [[OFDM]] (5 GHz)
- [[802.11g]] [[OFDM]] (< 54 Mbps) (compatible con 802.11b) (2.4 GHz)
- [[802.11n]] MIMO (< 600 Mbps suele ser < 150 Mbps)
- [[802.11ac]] (< 3.6 Gbps)(5 GHz)

> El modo natural de transmisión del canal es half-duplex. Vea [[#Protocolo MAC]] más abajo.

## Infraestructura vs ad hoc
Las redes 802.11 se pueden utilizar en dos modos. El modo **infraestructura** donde cada cliente se asocia con un AP ([[Access Point]]) que a su vez está conectado a otra red. El cliente envía y recibe sus paquetes a través del AP que actúa como un  [[Bridge]] [[Ethernet]] que renvía las comunicaciones sobre la red apropiada, ya sea la red cableada o la inalámbrica. Se pueden conectar varios puntos de acceso juntos, por lo general mediante una red alámbrica llamada sistema de distribución, para formar una red 802.11 extendida. En este caso, los clientes pueden enviar tramas a otros clientes a través de sus APs.

El otro modo es una **red ad hoc**. Este modo es una colección de computadoras que están asociadas de manera que puedan enviarse tramas directamente unas a otras. No hay punto de acceso. Como el acceso a Internet es la aplicación esencial para las redes inalámbricas, las redes ad hoc no son muy populares. 

![[wifi_infraestructura_ad_hoc.png]]

## Pila de protocolos
Todos los protocolos 802, incluyendo 802.11 y [[Ethernet]], tienen ciertas similitudes en su estructura. La pila es la misma para los clientes y APs. La capa física corresponde muy bien con la [[Capa física|capa física]] OSI, pero la [[Capa de enlace de datos|capa de enlace de datos]] en todos los protocolos 802 se divide en dos o más subcapas. En el estándar 802.11, la [[Subcapa MAC|subcapa MAC]] determina la forma en que se asigna el canal; es decir, a quién le toca transmitir a continuación. Arriba de dicha subcapa se encuentra la [[Subcapa LLC|subcapa LLC]], cuya función es ocultar las diferencias entre las variantes 802 con el fin de que sean imperceptibles en lo que respecta a la [[Capa de red|capa de red]].

![[wifi_pila_de_protocolos_1.png]]

## Protocolo MAC
![[CSMA CA]]

## Servicios
El estándar 802.11 define los servicios que los clientes, los puntos de acceso y la red que los conecta deben proveer para poder ser una [[Wireless LAN|LAN inalámbrica]] que se apegue a dicho estándar. Estos servicios se dividen en varios grupos.

El servicio de **asociación** lo utilizan las estaciones móviles para conectarse ellas mismas a los AP. Por lo general, se utiliza después de que una estación se mueve dentro del alcance de radio del AP. Al llegar, la estación conoce la identidad y las capacidades del AP, ya sea mediante tramas baliza o preguntando directamente al AP. Entre las capacidades se incluyen las tasas de datos soportadas, los arreglos de seguridad, las capacidades de ahorro de energía, el soporte de la calidad del servicio, etcétera. La estación envía una solicitud para asociarse con el AP. Éste puede aceptar o rechazar dicha solicitud.

La **reasociación** permite que una estación cambie su AP preferido. Esta herramienta es útil para las estaciones móviles que cambian de un AP a otro en la misma LAN 802.11 extendida, como un traspaso (handover) en la red celular. Si se utiliza en forma correcta, no se perderán datos como consecuencia del traspaso. También es posible que la estación o el AP se **desasocien**, con lo que se rompería su relación. Una estación debe usar este servicio antes de desconectarse o salir de la red. El AP lo puede usar antes de desconectarse por cuestión de mantenimiento

Las estaciones también se deben **autentificar** antes de poder enviar tramas por medio del AP, pero la autentificación se maneja en formas distintas dependiendo del esquema de seguridad elegido. Si la red 802.11 está “abierta”, cualquiera puede usarla. En caso contrario, se requieren credenciales para autentificarse. El esquema recomendado, conocido como **WPA2 (WiFi Protected Access 2)**, implementa la seguridad según lo definido en el estándar 802.11i (el WPA simple es un esquema interno que implementa un subconjunto del 802.11i). En el WPA2, el AP se puede comunicar con un servidor de autentificación que tenga una base de datos con nombres de usuario y contraseñas para determinar si la estación puede acceder a la red. Como alternativa se puede configurar una clave precompartida, lo cual es un nombre elegante para una contraseña de red. Se intercambian varias tramas entre la estación y el AP con un reto y respuesta que permite a la estación demostrar que tiene las credenciales apropiadas. Este intercambio ocurre después de la asociación.

El esquema predecesor de WPA se llama **WEP (Wired Equivalent Privacy)**. En este esquema, la autentificación con una clave precompartida ocurre antes de la asociación.

Una vez que las tramas llegan al AP, el servicio de **distribución** determina cómo encaminarlas. Si el destino es local para el AP, las tramas se pueden enviar en forma directa por el aire. En caso contrario, habrá que reenviarlas por la red alámbrica. El servicio de **integración** maneja cualquier traducción necesaria para enviar una trama fuera de la LAN 802.11, o para que llegue desde el exterior de la LAN 802.11. Aquí el caso común es conectar la LAN inalámbrica a [[Internet]].

Y como lo esencial aquí es la transmisión de datos, es lógico que la red 802.11 provea el servicio de **entrega de datos**. Como el estándar 802.11 está modelado en base a Ethernet y no se garantiza que la transmisión por Ethernet sea 100% confiable, tampoco se garantiza que la transmisión por 802.11 sea confiable. Las capas superiores deben lidiar con la detección y corrección de errores.

La señal inalámbrica es de difusión. Para mantener confidencial la información que se envía por una LAN inalámbrica, hay que cifrarla. Para lograr esto se utiliza un servicio de **privacidad** que administra los detalles del cifrado y el descifrado. El algoritmo de cifrado para WPA2 se basa en el estándar **[[AES]] (Advanced Encryption Standard)**. Las claves que se utilizan para el cifrado se determinan durante el procedimiento de autentificación.

Los servicios se pueden clasificar en dos grupos principales:
- **Servicios de distribución:**
	- **Asociación.**
	- **Reasociación**.
	- **Desasociación.**
	- **Distribución.**
	- **Integración.** 

- **Servicios Intra-celda**
	- **Autenticación**
	- **Desautenticación**
	- **Entrega de datos**
	- **Privacidad**

## Canales
Los dispositivos WiFi deben usar el mismo canal para poder comunicarse. Elllos envían y reciben en el mismo conal, por lo que sólo un dispositivo puede transmitir en un instante determinado (half-duplex).

![[wifi_canales.png]]