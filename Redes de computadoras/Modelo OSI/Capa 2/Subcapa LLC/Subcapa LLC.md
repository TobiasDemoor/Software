La **subcapa LLC** ([[LLC|Logical Link Control]]) es la subcapa superior de la [[Capa de enlace de datos|capa de enlace de datos]] que se encarga fundamentalmente del [[entramado]], [[control de errores]] y evitar que un emisor rápido sature a un receptor lento.

### Cuestiones de diseño
La capa de enlace de datos utiliza los servicios de la [[Capa física|capa física]] para enviar y recibir bits a través de los canales de comunicación. Tiene varias funciones específicas, entre las que se incluyen:
1. Proporcionar a la capa de red una [[Interfaz|interfaz]] de servicio bien definida.
2. Manejar los errores de transmisión. 
3. Regular el flujo de datos para que los emisores rápidos no saturen a los receptores lentos.

Para cumplir con estas metas, la capa de enlace de datos toma los paquetes que obtiene de la [[Capa de red|capa de red]] y los encapsula en tramas para transmitirlos. Cada trama contiene un encabezado, un campo de carga útil (payload) para almacenar el paquete y un terminador, como se muestra en la figura 3-1. El manejo de las tramas es la tarea más importante de la capa de enlace de datos.

![[RRCC_capa_de_enlace_de_datos_1.png]]

#### Servicios proporcionados a la capa de red
La función de la capa de enlace de datos es proveer servicios a la [[Capa de red|capa de red]]. El servicio principal es la transferencia de datos de la capa de red en la máquina de origen, a la capa de red en la máquina de destino. En la capa de red de la máquina de origen está una entidad, llamada [[Sistemas Operativos/Conceptos/Proceso|proceso]], que entrega algunos bits a la capa de enlace de datos para que los transmita al destino. La tarea de la capa de enlace de datos es transmitir los bits a la máquina de destino, de modo que se puedan entregar a la capa de red de esa máquina.

La capa de enlace de datos puede diseñarse para ofrecer varios servicios. Los servicios reales ofrecidos varían de un protocolo a otro. Tres posibilidades razonables que normalmente se proporcionan son: 
1. **Servicio sin conexión ni confirmación de recepción**: consiste en hacer que la máquina origen envía tramas independientes a la máquina de destino sin que ésta confime la recepción. Un ejemplo de esto es [[Ethernet]]. No se establece una conexión lógica de antemano ni se libera después. Esta clase de servicio es apropiada cuando la tasa de error es muy baja. También es apropiada para el tráfico en tiempo real, como el de voz, en donde es peor tener retraso en los datos que errores en ellos.
2. **Servicio sin conexión con confirmación de recepción**: cuando se ofrece este servicio tampoco se utilizan conexiones lógicas, pero se confirma de manera individual la recepción de cada trama enviada. De esta manera, el emisor sabe si la trama llegó bien o se perdió. Si no ha llegado en un intervalo especificado, se puede enviar de nuevo. Este servicio es útil en canales no confiables, como los de los sistemas inalámbricos. 802.11 ([[WiFi|WiFi]]) es un buen ejemplo de esta clase de servicio.
3. **Servicio orientado a conexión con confirmación de recepción**: con este servicio, las máquinas de origen y de destino establecen una conexión antes de transferir datos. Cada trama enviada a través de la conexión está numerada, y la capa de enlace de datos garantiza que cada trama enviada llegará a su destino. Es más, garantiza que cada trama se recibirá exactamente una vez y que todas las tramas se recibirán en el orden correcto. Así, el servicio orientado a conexión ofrece a los procesos de la capa de red el equivalente a un flujo de bits confiable. Es apropiado usarlo en enlaces largos y no confiables, como un canal de satélite o un circuito telefónico de larga distancia. Si se utilizara el servicio no orientado a conexión con confirmación de recepción, es posible que las confirmaciones de recepción perdidas ocasionaran que una trama se enviara y recibiera varias veces, desperdiciando ancho de banda.

#### Entramado
![[Entramado]]

#### Control de errores
![[Control de errores]]

#### Protocolos elementales de enlace de datos
![[Protocolos elementales de enlace de datos]]

#### Protocolos de ventana deslizante
![[Protocolos de ventana deslizante]]

#### Otros protocolos
##### HDLC
![[HDLC]]

##### PPP
![[PPP]]