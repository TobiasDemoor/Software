En la [[capa de red]], la [[Internet]] puede verse como un conjunto de [[Redes de computadoras|redes]], o **Sistemas Autónomos (AS)** interconectados. No hay una estructura real, pero existen varias redes troncales (*backbones*) principales. Éstas se construyen a partir de líneas de alto ancho de banda y enrutadores rápidos. Las más grandes de estas redes troncales, a la que se conectan todos los demás para llegar al resto de Internet, se llaman **redes de Nivel 1**. Conectadas a las redes troncales hay ISP (Internet Service Provider) que proporcionan acceso a Internet para los hogares y negocios, centros de datos e instalaciones de colocación llenas de máquinas servidores y redes regionales (de nivel medio).

El pegamento que mantiene unida a Internet es el protocolo de capa de red, [[IP]]. A diferencia de la mayoría de los protocolos de capa de red anteriores, IP se diseñó desde el principio con la interconexión de redes en mente. Una buena manera de visualizar la capa de red es la siguiente: su trabajo es proporcionar un medio de **mejor esfuerzo** (es decir, sin garantía) para transportar paquetes de la fuente al destino, sin importar si estas máquinas están en la misma red o si hay otras redes entre ellas.

La comunicación en Internet funciona de la siguiente manera. La [[Capa de transporte]] toma flujos de datos y los divide para poder enviarlos como paquetes IP. En teoría, los paquetes pueden ser de hasta 64 Kbytes cada uno, pero en la práctica por lo general no sobrepasan los 1500 bytes (ya que son colocados en una trama de [[Ethernet]]). Los enrutadores IP reenvían cada paquete a través de Internet, a lo largo de una ruta de un enrutador a otro, hasta llegar al destino. En el destino, la capa de red entrega los datos a la capa de transporte, que a su vez los entrega al proceso receptor.

### DHCP
![[DHCP]]

### NAT
![[NAT]]