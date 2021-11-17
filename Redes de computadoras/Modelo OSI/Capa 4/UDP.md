El **UDP (User Datagram Protocol)** es un [[protocolo]] de la [[capa de transporte]] que es parte del [[Modelo TCP IP|modelo TCP/IP]]. El protocolo UDP es sin conexión, prácticamente no hace nada más que enviar paquetes entre aplicaciones.

UDP proporciona una forma para que las aplicaciones envíen datagramas IP encapsulados sin tener que establecer una conexión. El protocolo UDP se describe en el [[RFC]] 768.

UDP transmite **segmentos** que consisten en un encabezado de 8 bytes seguido de la carga útil. En el encabezado los dos **puertos** sirven para identificar los puntos terminales dentro de las máquinas de origen y destino. Cuando llega un paquete UDP, su carga útil se entrega al proceso que está conectado al puerto de destino. El valor principal de contar con UDP en lugar de simplemente utilizar IP puro es la adición de los puertos de origen y destino. Sin los campos de puerto, la capa de transporte no sabría qué hacer con cada paquete entrante. Con ellos, entrega el segmento incrustado a la aplicación correcta.

![[RRCC_UDP_encabezado.png]]

El puerto de origen se necesita principalmente cuando hay que enviar una respuesta al origen. Al copiar el campo *Puerto de origen* del segmento entrante en el campo *Puerto de destino* del segmento que sale, el proceso que envía la respuesta puede especificar cuál proceso de la máquina emisora va a recibirlo.

El campo *Longitud UDP* incluye el encabezado de 8 bytes y los datos. La longitud mínima es de 8 bytes, para cubrir el encabezado. La longitud máxima es de 65515 bytes, lo cual es menor al número que cabe en 16 bits debido al límite de tamaño en los paquetes IP.

También se proporciona un campo *Suma de verificación* opcional para una confiabilidad adicional. Se realiza una suma de verificación para el encabezado, los datos y un pseudoencabezado IP conceptual. Al hacer este cálculo, el campo *Suma de verificación* se establece en cero y el campo de datos se rellena con un byte cero adicional si su longitud es un número impar. El algoritmo de suma de verificación consiste simplemente en sumar todas las palabras de 16 bits en complemento a uno y sacar el complemento a uno de la suma. Como consecuencia, cuando el receptor realiza el cálculo en todo el segmento (incluyendo el campo *Suma de verificación*), el resultado debe ser 0. Si no se calcula la suma de verificación, se almacena como 0, ya que por una feliz coincidencia de la aritmética de complemento a uno, un 0 calculado se almacena como 1. Sin embargo, no tiene sentido desactivarlo a menos que no importe la calidad de los datos (por ejemplo, en la voz digitalizada).

El pseudoencabezado IP contiene las direcciones IPv4 de 32 bits de las máquinas de origen y de destino, el número de protocolo para UDP (17) y la cuenta de bytes para el segmento UDP (incluyendo el encabezado). Es distinto pero análogo a IPv6. Es útil incluir el pseudoencabezado en el cálculo de la suma de verificación de UDP para detectar paquetes mal entregados, pero al incluirlo también se viola la jerarquía de protocolos debido a que las direcciones IP en él pertenecen a la capa IP, no a la capa UDP. TCP usa el mismo pseudoencabezado para su suma de verificación.

![[RRCC_UDP_pseudoencabezado_IP.png]]

Vale la pena mencionar de manera explícita algunas de las cosas que UDP no realiza. No realiza control de flujo, control de congestión o retransmisión cuando se recibe un segmento erróneo. Todo lo anterior le corresponde a los procesos de usuario. Lo que sí realiza es proporcionar una interfaz para el protocolo IP con la característica agregada de demultiplexar varios procesos mediante el uso de los puertos y la detección de errores extremo a extremo opcional. Esto es todo lo que hace.

#### Protocolos de transporte en tiempo real
![[RTP]]