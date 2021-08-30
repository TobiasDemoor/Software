## Distribución de protocolos en capas
Para reducir la complejidad de su diseño, la mayoría de las [[Redes de computadoras|redes]] se organizan como una pila de **capas** o **niveles** ([[Layers|patrón capas]]), cada una construida a partir de la que está abajo. El número de capas, su nombre, el contenido de cada una y su función difieren de una red a otra. El propósito de cada capa es ofrecer ciertos servicios a las capas superiores, mientras les oculta los detalles relacionados con la forma en que se implementan los servicios ofrecidos. Es decir, cada capa es un tipo de máquina virtual que ofrece ciertos servicios a la capa que está encima de ella.
Cuando la capa n en una máquina lleva a cabo una conversación con la capa n en otra máquina, a las reglas y convenciones utilizadas en esta conversación se les conoce como el [[Protocolo|protocolo]] de la capa n. Las entidades que conforman las correspondientes capas en diferentes máquinas se llaman **iguales** (*peers*). Los iguales pueden ser procesos de software,dispositivos de hardware o incluso seres humanos. En otras palabras, los iguales son los que se comunican a través del protocolo.

En realidad no se transfieren datos de manera directa desde la capa n de una máquina a la capa n de otra máquina, sino que cada capa pasa los datos y la información de control a la capa inmediatamente inferior, hasta que se alcanza a la capa más baja. Debajo de la capa 1 se encuentra el **medio físico** a través del cual ocurre la comunicación real.

Entre cada par de capas adyacentes hay una [[Interfaz|interfaz]]. Ésta define las operaciones y servicios primitivos que pone la capa más baja a disposición de la capa superior inmediata.

A un conjunto de capas y protocolos se le conoce como **arquitectura de red**. A la lista de los protocolos utilizados por cierto sistema se le conoce como **pila de protocolos**.

## Servicio orientado y no a la conexión
El servicio **orientado a la conexión** está modelado a partir del sistema telefónico. Para usar un servicio de [[Redes de computadoras|red]] orientado a la conexión, el usuario del servicio establece primero una conexión, la utiliza y después la libera.
En algunos casos al establecer una conexión, el emisor, el receptor y la [[Subred|subred]] llevan a cabo una **negociación** en cuanto a los parámetros que se van a usar, como el tamaño máximo del mensaje, la calidad requerida del servicio y demás cuestiones relacionadas..

En contraste al servicio orientado a la conexión, el servicio **no orientado a la conexión** está modelado a partir del sistema postal. Cada mensaje lleva la dirección de destino completa, y cada uno es [[Router|enrutado]] hacia los nodos intermedios dentro del sistema, en forma independiente a todos los mensajes subsecuentes. hay distintos nombres para los mensajes en diferentes conextos: un **paquete** es un mensaje en la [[Capa de red|capa de red]].
![[servicio_orientado_a_la_conexión_1.png]]

### Confiabilidad
Cada tipo de servicio se puede caracterizar con base en su confiabilidad. Algunos servicios son confiables en cuanto a que nunca pierden datos. Por lo general, para implementar un servicio confiable, el receptor tiene que confirmar la recepción de cada mensaje, de manera que el emisor esté seguro de que hayan llegado. El proceso de confirmación de recepción introduce sobrecarga y retardos, que a menudo valen la pena pero algunas veces no son deseables.

Al servicio sin conexión no confiable (que significa sin confirmación de recepción) se le denomina servicio de **datagramas**, en analogía al servicio de telegramas que tampoco devuelve una confirmación de recepción al emisor.

En otros casos es conveniente no tener que establecer una conexión para enviar un mensaje, pero la confiabilidad es esencial. En estas aplicaciones se puede utilizar el servicio de **datagramas con confirmación de recepción**. Es como enviar una carta certificada y solicitar una confirmación de recepción. Al regresar la confirmación de recepción el emisor tiene la absoluta certeza de que la carta se entregó al destinatario correcto y que no se perdió en el camino. La mensajería de texto en los teléfonos móviles es un ejemplo.

## Primitivas de servicios
Un servicio se puede especificar de manera formal como un conjunto de **primitivas** (operaciones) disponibles a los procesos de usuario para que accedan al servicio. Estas primitivas le indican al servicio que desarrollen alguna acción o que informen sobre la acción que haya tomado una entidad par. Si la pila de protocolos se encuentra en el sistema operativo, como se da en la mayoría de los casos, por lo general las primitivas son llamadas al sistema. Estas llamadas provocan un salto al modo de kernel, que a su vez devuelve el control de la máquina al sistema operativo para que envíe los paquetes necesarios.

## Relación Servicio-Protocolo
Un *servicio* es un conjunto de primitivas (operaciones) que una capa proporciona a la capa que está encima de ella. El servicio define que operaciones puede realizar la capa en beneficio de sus usuario, pero no dice nada sobre cómo se implementan estas operaciones. Un servicio se relaciona con una [[Interfaz|interfaz]] entre dos capas, en donde la capa inferior es el proveedor del servicio y la capa superior es el usuario.

Un *protocolo* ([[Protocolo]]) es un conjunto de reglas que rigen el formato y el significado de los paquetes o mensajes que intercambian las entidades iguales en una capa. Las entidades utilizan protocolos para implementar sus definiciones de servicios. Pueden cambiar sus protocolos a voluntad, siempre y cuando no cambien el servicio visible para sus usuarios. De esta manera, el servicio y el protocolo no dependen uno del otro. Éste es un concepto clave que cualquier diseñador de red debe comprender bien.

## Comparación de modelos
Los modelos de referencia [[Modelo OSI|OSI]] y [[Modelo TCP IP|TCP/IP]] tienen mucho en común. Ambos se basan en el concepto de una pila de [[Protocolo|protocolos]] independientes. Además, la funcionalidad de las capas es muy similar.
