Se le conoce como WiFi al estándar de [[Wireless LAN|LAN inalámbrica]] definida en la norma **IEEE 802.11**. Es un estandar que se utiliza en la [[Capa de enlace de datos|capa de enlace a datos]] del modelo OSI. Al momento de su diseño se tomó como modelo a [[Ethernet]].

El primer problema era hallar una banda de frecuencia adecuada que estuviera disponible, de preferencia a nivel mundial. La metodología utilizada fue contraria a la que se utilizó en las redes de telefonía móvil. En vez de un espectro costoso bajo licencia, los sistemas 802.11 operan en bandas sin licencia como las bandas **ISM (Industrial, Scientifc, and Medical)** definidas por el [[Regulación del espectro electromagnético|ITU-R]]. Todos los dispositivos pueden usar este espectro siempre y cuando limiten su potencia de transmisión para dejar que coexistan distintos dispositivos. Desde luego que esto significa que los radios 802.11 podrían entrar en competencia con los teléfonos inalámbricos, los abridores de puertas de garaje y los hornos de microondas.

Las redes 802.11 están compuestas de clientes (como laptops y teléfonos móviles) y de una infraestructura llamada **AP ([[Access Point]])** que se instala en los edificios. Algunas veces a los puntos de acceso se les llama estaciones base. Los puntos de acceso se conectan a la red alámbrica y toda la comunicación entre los clientes se lleva a cabo a través de un punto de acceso.


## Capa física
[[Capa física|Capas físicas]] por orden cronológico:
* 802.11 Infrarrojo, FHSS, DSSS (estas dos últimas son codificaciones de espectro expandido)
* 802.11b HR-DSSS (< 11 Mbps) (utiliza spread-spectrum) (2.4 GHz)
* 802.11a [[Multiplexión#Multiplexión por división de frecuencia ortogonal|OFDM]] (5 GHz)
* 802.11g [[Multiplexión#Multiplexión por división de frecuencia ortogonal|OFDM]] (< 54 Mbps) (compatible con 802.11b) (2.4 GHz)
* [[802.11n]] MIMO (necesita varias antenas y resuelve el multipath fading) (< 600 Mbps suele ser < 150 Mbps)
* 802.11ac (< 3.6 Gbps)(5 GHz)

El modo natural de transmisión del canal es half-duplex. 

## DCF y PCF
La norma establece que se puede operar de dos maneras:
Modo ad-hoc o **DCF (Distributed Coordination Function)**, no hace falta un [[Access Point]] intermediario. Aquí ocurre el [[Wireless LAN#Problema de terminal oculta|problema de la terminal oculta]], para solucionarlo se utiliza el protocolo MACA. Este formato es muy ineficiente.

Modo infraestructura o **PCF (Puctual Coordination Function)** en este modo los clientes se comunican con una estación central llamada [[Access Point]] que actúa como un [[Bridge]] [[Ethernet]] que renvía las comunicaciones sobre la red apropiada, ya sea la red cableada o la inalámbrica. Agregando esta estación central que regula el uso del medio la eficiencia aumenta considerablemente.

## Servicios de distribución
* **Asociación.** Esto es lo que debe hacer un cliente antes de poder utilizar la red.
* **Desasociación.** Esto es lo que hace un cliente para dejar de formar parte de la red.
* **Reasociación**.
* **Distribución.** Enviar tramas de un AP a otro AP que está en la misma red.
* **Integración.** Permitir integrar una red WiFi con una red Ethernet.

## Servicios Intra-celda
* **Autenticación y Desautenticación** (no se suele hacer)
* **Privacidad** (cifrado)

## Tramas beacon
Dan información a la red de la existencia del [[Access Point|AP]] para que puedan asociarse.

## Canales
Los dispositivos WiFi deben usar el mismo canal para poder comunicarse. Elllos envían y reciben en el mismo conal, por lo que sólo un dispositivo puede transmitir en un instante determinado (half-duplex).