Los switches son una evolución de los [[Bridge|bridges]]. Sin embargo no solo ofrecen el bridging, sino que también proveen segmentación de micro-LAN lo que permite que cada nodo conectado al switch tenga su ancho de banda propio. Está bien plantado en la [[Capa de enlace de datos|capa de enlace de datos]], no tocan el contenido de las tramas, solo rutean internamente.

> Los switches son un tipo particular de bridge específico para la tecnología [[Ethernet]].

Los switches sólo envían tramas a los puertos para los cuales están destinadas. Cuando el puerto de un switch recibe una trama Ethernet de una estación, el switch verifica las direcciones de Ethernet para ver cuál es el puerto de destino de la trama.

Cada puerto del switch es un dominio de colisión distinto [[CSMA|CSMA/CD]] va a trabajar en cada segmento individualmente.

Tiene dos mecanismos principales para manejar el reenvio de las tramas:
* **Store & Forward**: se recibe toda la trama y se reenvia toda. Es la forma más común.
* **Cut through**: en la medida que ven recibiendo la trama ya van calculando si la tienen que reenviar y a qué interfaz. En este no se puede validar que la trama haya sido recibida correctamente por lo tanto se puede transmitir una trama corrompida..

### Llenado de tabla interna
Utiliza el algorítmo de puente [[Transparencia|transparente]]:
1. Cuando el destino no se conoce (no  está en la tabla) entonces inundar (copia la trama en todos los puertos energizados).
2. Cuando la dirección destino se encuentra en la tabla, reenviar al puerto correspondiente.
3. Cuando la dirección destino se encuentra en la tabla en la misma interfaz asociada a la dirección origen, descartar la trama.
4. La dirección origen se asocia en la tabla a la interfaz origen.

Se dice que los switch aprenden de lo ocurrido (aprenden por dirección origen) y reenvían por dirección destino. No generan ninguna trama.

Pasado cierto tiempo el switch limpia las entradas de la tabla.
