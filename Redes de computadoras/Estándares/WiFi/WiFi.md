Se le conoce como WiFi al estándar de [[Wireless LAN|LAN inalámbrica]] definida en la norma **IEEE 802.11**. Es un estandar que se utiliza en la [[Capa de enlace de datos|capa de enlace a datos]] del modelo OSI. Al momento de su diseño se tomó como modelo a [[Ethernet]].

El primer problema era hallar una banda de frecuencia adecuada que estuviera disponible, de preferencia a nivel mundial. La metodología utilizada fue contraria a la que se utilizó en las redes de telefonía móvil. En vez de un espectro costoso bajo licencia, los sistemas 802.11 operan en bandas sin licencia como las bandas **ISM (Industrial, Scientifc, and Medical)** definidas por el [[Regulación del espectro electromagnético|ITU-R]]. Todos los dispositivos pueden usar este espectro siempre y cuando limiten su potencia de transmisión para dejar que coexistan distintos dispositivos. Desde luego que esto significa que los radios 802.11 podrían entrar en competencia con los teléfonos inalámbricos, los abridores de puertas de garaje y los hornos de microondas.

Las redes 802.11 están compuestas de clientes (como laptops y teléfonos móviles) y de una infraestructura llamada **AP ([[Access Point]])** que se instala en los edificios. Algunas veces a los puntos de acceso se les llama estaciones base. Los puntos de acceso se conectan a la red alámbrica y toda la comunicación entre los clientes se lleva a cabo a través de un punto de acceso.


## Capa física
[[Capa física|Capas físicas]] por orden cronológico:
* 802.11 Infrarrojo, FHSS, DSSS (estas dos últimas son codificaciones de espectro expandido)
* [[802.11b]] HR-DSSS (< 11 Mbps) (utiliza spread-spectrum) (2.4 GHz)
* [[802.11a]] [[OFDM]] (5 GHz)
* [[802.11g]] [[OFDM]] (< 54 Mbps) (compatible con 802.11b) (2.4 GHz)
* [[802.11n]] MIMO (< 600 Mbps suele ser < 150 Mbps)
* 802.11ac (< 3.6 Gbps)(5 GHz)

> El modo natural de transmisión del canal es half-duplex. Vea [[#Protocolo MAC]] más abajo.

## Infraestructura vs ad hoc
Las redes 802.11 se pueden utilizar en dos modos. El modo **infraestructura** donde cada cliente se asocia con un AP ([[Access Point]]) que a su vez está conectado a otra red. El cliente envía y recibe sus paquetes a través del AP que actúa como un  [[Bridge]] [[Ethernet]] que renvía las comunicaciones sobre la red apropiada, ya sea la red cableada o la inalámbrica. Se pueden conectar varios puntos de acceso juntos, por lo general mediante una red alámbrica llamada sistema de distribución, para formar una red 802.11 extendida. En este caso, los clientes pueden enviar tramas a otros clientes a través de sus APs.

El otro modo es una **red ad hoc**. Este modo es una colección de computadoras que están asociadas de manera que puedan enviarse tramas directamente unas a otras. No hay punto de acceso. Como el acceso a Internet es la aplicación esencial para las redes inalámbricas, las redes ad hoc no son muy populares. 

![[wifi_infraestructura_ad_hoc.png]]

## Pila de protocolos
Todos los protocolos 802, incluyendo 802.11 y [[Ethernet]], tienen ciertas similitudes en su estructura. La pila es la misma para los clientes y APs. La capa física corresponde muy bien con la [[Capa física|capa física]] OSI, pero la [[Capa de enlace de datos|capa de enlace de datos]] en todos los protocolos 802 se divide en dos o más subcapas. En el estándar 802.11, la [[Subcapa MAC|subcapa MAC]] determina la forma en que se asigna el canal; es decir, a quién le toca transmitir a continuación. Arriba de dicha subcapa se encuentra la [[Subcapa LLC|subcapa LLC]], cuya función es ocultar las diferencias entre las variantes 802 con el fin de que sean imperceptibles en lo que respecta a la [[Capa de red|capa de red]].

![[wifi_pila_de_protocolos_1.png]]

## Protocolo MAC
El protocolo de la subcapa MAC para el estándar 802.11 es muy diferente al de [[Ethernet]], debido a dos factores fundamentales para la comunicación inalámbrica.

Primero, **las radios casi siempre son half-dúplex**, lo cual significa que no pueden transmitir y escuchar ráfagas de ruido al mismo tiempo en una sola frecuencia. La señal recibida puede ser un millón de veces más débil que la señal transmitida, por lo que no se puede escuchar al mismo tiempo. Con Ethernet, una estación sólo espera hasta que el medio queda en silencio y después comienza a transmitir. Si no recibe una ráfaga de ruido mientras transmite los primeros 64 bytes, es muy probable que se haya entregado la trama correctamente. En los sistemas inalámbricos, este mecanismo de detección de colisiones no funciona.

En vez de ello, el 802.11 trata de evitar colisiones con un protocolo llamado **[[CSMA|CSMA/CA]] (CSMA with Collision Avoidance)**. En concepto, este protocolo es similar al CSMA/CD de Ethernet, con detección del canal antes de enviar y retroceso exponencial después de las colisiones. Sin embargo, una estación que desee enviar una trama empieza con un retroceso aleatorio, osea cuenta cierto número de ranuras antes de intentar enviar (excepto en el caso en que no haya utilizado el canal recientemente y éste se encuentre inactivo). No espera una colisión. El número de ranuras para el retroceso se elije en el rango de 0 hasta, por decir, 15 en el caso de la capa física OFDM. La estación espera hasta que el canal está inactivo, para lo cual detecta que no hay señal durante un periodo corto y realiza un conteo descendente de las ranuras inactivas, haciendo pausa cuando se envían tramas. Envía su trama cuando el contador llega a 0. Si la trama logra pasar, el destino envía de inmediato una confirmación de recepción corta. La falta de una confirmación de recepción se interpreta como si hubiera ocurrido un error, sea una colisión o cualquier otra cosa. En este caso, el emisor duplica el periodo de retroceso e intenta de nuevo, continuando con el retroceso exponencial como en Ethernet, hasta que la trama se transmita con éxito o se llegue al número máximo de retransmisiones.

![[csma_ca_1.png]]

Este modo de operación se llama **DCF (Distributed Coordination Function)**, ya que cada estación actúa en forma independiente, sin ningún tipo de control central. El estándar también incluye un modo opcional de operación llamado **PCF (Punctual Coordination Function)**, en donde el punto de acceso controla toda la actividad en su celda, justo igual que una estación base celular. Sin embargo, PCF no se utiliza en la práctica debido a que por lo general no hay forma de evitar que las estaciones en otra red cercana transmitan tráfico conflictivo.

El segundo problema es que los rangos de transmisión de las distintas estaciones pueden ser diferentes. Con un cable, el sistema se diseña de tal forma que todas las estaciones se puedan escuchar entre sí. Con las complejidades de la propagación de RF, esta situación no es válida para las estaciones inalámbricas. En consecuencia, pueden surgir situaciones como el [[Wireless LAN#Problema de terminal oculta|problema de la terminal oculta]].

Para reducir las ambigüedades con respecto a qué estación va a transmitir, el 802.11 define la detección del canal como un proceso que consiste tanto de una detección física como de una detección virtual. En la detección física sólo se verifica el medio para ver si hay una señal válida. En la detección virtual, cada estación mantiene un registro lógico del momento en que se usa el canal rastreando el **NAV (Network Allocation Vector)**. Cada trama lleva un campo NAV que indica cuánto tiempo tardará en completarse la secuencia a la que pertenece esta trama.

Hay un mecanismo RTS/CTS opcional que usa el NAV para evitar que las terminales envíen tramas al mismo tiempo como terminales ocultas, este es similar al protocolo **[[Wireless LAN#MACA|MACA]]** pero distinto, ya que todo el que escucha la trama RTS o CTS permanece en silencio para permitir que la trama ACK llegue a su destino sin que haya una colisión. Debido a esto, no es útil con las terminales expuestas como en el caso de MACA, sólo con las terminales ocultas. Lo más frecuente es que haya unas cuantas terminales ocultas y CSMA/CA les ayuda al reducir la velocidad de las estaciones que transmiten sin éxito, sin importar cuál sea la causa, para que sus transmisiones tengan más probabilidades de tener éxito. Aunque el método RTS/CTS suena bien en teoría, es uno de esos diseños que ha demostrado ser de poco valor en la práctica.

![[wifi_rts_cts.png]]

CSMA/CA con detección física y virtual es el núcleo del protocolo 802.11. Sin embargo, existen otros mecanismos que se han desarrollado para trabajar con él. Cada uno de estos mecanismos fue impulsado por las necesidades de la operación real.

### Confiabilidad
En contraste con las redes convencionales de cables, las redes inalámbricas son ruidosas y poco confiables, lo cual se debe en gran parte a la interferencia de otros tipos de dispositivos.

La principal estrategia que se utiliza en este caso para incrementar las transmisiones exitosas es reducir la tasa de transmisión. Las tasas más bajas usan modulaciones más robustas que tienen mayor probabilidad de ser recibidas correctamente para una relación señal a ruido dada. Si se pierden demasiadas tramas, una estación puede reducir la tasa. Si se entregan tramas con pocas pérdidas, la estación puede algunas veces probar una tasa más alta para ver si es conveniente usarla.

Otra estrategia para mejorar la probabilidad de que la trama llegue sin daños es enviar tramas más cortas. Ya que dada una probabilidad de error en un bit a menor longitud de trama hay mayor probabilidad de recibirla correctamente y no tener que reenviar.

Para implementar tramas más cortas es necesario reducir el tamaño máximo del mensaje que se aceptará de la capa de red. Como alternativa, el 802.11 permite dividir las tramas en piezas más pequeñas llamadas **fragmentos**, cada una con su propia suma de verificación.

### Ahorro de energía
La vida de las baterías siempre es un asunto importante para los dispositivos inalámbricos móviles. El mecanismo básico para ahorrar energía se basa en las **tramas beacon**. Las balizas son difusiones periódicas que realiza el AP (por ejemplo, cada 100 mseg). Las tramas anuncian la presencia del AP a los clientes y llevan los parámetros del sistema, como el identificador del AP, el tiempo, cuánto falta para el siguiente beacon y la configuración de seguridad

Los clientes pueden establecer un bit de administración de energía en las tramas que envían al AP para indicarle que entrarán en el modo de ahorro de energía. En este modo, el cliente puede dormitar y el AP pondrá en el búfer el tráfico destinado a este cliente. Para verificar el tráfico entrante, el cliente se despierta durante cada baliza y verifica un mapa de tráfico que se envía como parte de ella. Este mapa indica al cliente si hay tráfico en el búfer. De ser así, el cliente envía un mensaje de sondeo al AP, quien a su vez le envía el tráfico que está en el búfer. Después el cliente puede regresar al modo suspendido hasta que se envíe la siguiente baliza.

### Calidad de servicio
El estándar IEEE 802.11 tiene un mecanismo para proveer calidad de servicio (en lo que respecta a reducir [[Latencia|latencia]] para procesos sensibles a ella), el cual se introdujo como un conjunto de extensiones bajo el nombre 802.11e. Su función consiste en extender el CSMA/CA con intervalos cuidadosamente definidos entre las tramas. Después de enviar una trama, se requiere cierta cantidad de tiempo inactivo antes de que una estación pueda enviar otra para verificar si el canal ya no se está usando. El truco es definir distintos intervalos para los distintos tipos de tramas.

El intervalo entre las tramas de datos regulares se conoce como **DIFS (DCF InterFrame Spacing)**. Cualquier estación puede intentar adquirir el canal para enviar una nueva trama después de que el medio haya estado inactivo durante un tiempo DIFS. Se aplican las reglas de contención usuales y tal vez se requiera el retroceso exponencial binario si ocurre una colisión. El intervalo más corto es **SIFS (Short InterFrame Spacing)** y se utiliza para permitir que las partes en un diálogo sencillo tengan la oportunidad de tomar el primer turno.

![[wifi_csma_ca_difs.png]]

Los dos intervalos **AIFS (Arbitration InterFrame Spacing)** muestran ejemplos de dos niveles de prioridad distintos. El intervalo corto, AIFS₁, es más pequeño que el intervalo DIFS pero más largo que SIFS. El AP lo puede usar para transportar voz u otro tipo de tráfico de alta prioridad al inicio de la línea.

## Servicios de distribución
* **Asociación.** Esto es lo que debe hacer un cliente antes de poder utilizar la red.
* **Desasociación.** Esto es lo que hace un cliente para dejar de formar parte de la red.
* **Reasociación**.
* **Distribución.** Enviar tramas de un AP a otro AP que está en la misma red.
* **Integración.** Permitir integrar una red WiFi con una red Ethernet.

## Servicios Intra-celda
* **Autenticación y Desautenticación** (no se suele hacer)
* **Privacidad** (cifrado)

## Canales
Los dispositivos WiFi deben usar el mismo canal para poder comunicarse. Elllos envían y reciben en el mismo conal, por lo que sólo un dispositivo puede transmitir en un instante determinado (half-duplex).