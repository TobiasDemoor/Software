## Architectural styles
%%En el contexto de los [[Distributed Systems|sistemas distribudios]] (DS) y la [[Distributed Systems Architecture|arquitectura de sistemas distribuidos]].%%
El estilo arquitectónico es formulado en terminos de componentes, la manera en que conectan entre sí, la información intercambiada componentes, y finalmente cómo estos elementos están configurados en un sistema. Usando [[Component|componentes]] y [[Connector|conectores]], podemos lograr varias configuraciones, que pueden ser clasificadas en distintos estilos arquitectónicos.

### Layered architectures
El concepto básico es el del [[Layers|patrón arquitectónico capas]]

#### Layered communication protocols
Una arquitectura de capas bien conocida es la de los *communication-protocol stacks*. En los [[Communication protocol|communication-protocol]] stacks, cada capa implementa uno o varias servicios de comunicación (**communication services**) permitiendo el envio de información desde un origen a varios destinos. Para esto, cada capa ofrece una [[Interfaz|interfaz]] especificando las funciones que pueden ser llamadas. En principio la interfaz debería ocultar completamente la implementación del servicio.
Es importante comprender la diferencia entre un servicio ofrecido por una capa, la interfaz mediante la cual el servicio se hace disponible y el [[Protocolo|protocolo]] que esa capa implementa para establecer la comunicación.
![[layered_communication_protocols_1.png]]
Para reforzar la distincion, consideremos un servicio orientado a conexión fiable, el cual es proveido por varios sistemas de comunicación. En este caso, un miembro de la comunicación primero debe establecer una conexión con el otro miembro antes que puedan enviar y recibir mensajes. El ser fiable significa que se da una importante garantía de que los mensajes enviados llegarán a destino, hasta cuando el riesgo de pérdida de mensajes sea alto. Además estos servicios generalmente aseguraan que los mensajes sean recibidos en el mismo orden que en el que fueron enviados. Este tipo de servicio se encuentra realizado en el [[TCP|Transmission Control Protocol (TCP)]].

### Object-based and Service-oriented architectures
Una organización mucho más laxa es la de las **arquitecturas basadas en objetos**. En esencia, cada objeto corresponde a lo que definimos como [[Component|componente]], y estos componente están conectados a través de un mecanismo de llamada de procedimientos. En caso de un DS, una llamada a procedimiento puede tomar lugar a través de una red.

Estas arquitecturas son atractivas ya que proveen una manera natural de [[Encapsulamiento|encapsular]] información (llamada **estado** de un objeto) y las operaciones que se pueden realizar sobre dicha información (llamados **métodos**) en una sola entidad ([[Object oriented programming|OOP]]). La [[Interfaz|interfaz]] ofrecida por un objeto oculta los detalles de implementación, lo cual esencialmente significa que podemos considerar a un objeto completamente independiente de su entorno.

Esta separación nos permite colocar una interfaz en una máquina mientras que el objeto en sí reside en otra. Esta organización se suele llamar objeto distribuido o **distributed object**.

Cuando un cliente **binds** a un objeto distribuido, una implementación de la interfaz del objeto, llamada proxy, es cargada en el espacio de direcciones del cliente.
![[object-based_architectures_1.png]]

Una continuación de esto son las **arquitecturas orientadas a servicios**. En las arquitecturas orientadas a servicios, una aplicación distribuida o SD es esencialmente construida como una composición de diferentes servicios. Estos servicios pueden no pertenecer todos a la misma entidad administrativa.

El problema central en desarrollar arquitecturas orientadas a servicios es el de composición de servicios o *service composition*, y asegurarse que esos servicios operan en harmonía.

#### Resource-based architectures
Como una alternativa a la vista centrada en servicios, uno puede ver a un DS como una gran colección de recursos que son administrados individualmente por [[Component|componentes]]. Los recursos pueden ser añadidos o removidos por aplicaciones remotas y a su vez pueden ser consultados o modificados. Este approach fue muy adoptado para la Web y es conocido como [[Representational State Transfer|Representational State Transfer (REST)]].

#### Publish-subscribe architectures
A medida que los sistemas siguen creciendo y los procesos pueden unirse e irse más fácilmente, es importante tener una arquitectura donde las dependencias entre procesos sean lo más sueltas posibles. Una gran clase de DS han adoptado una arquitectura en la que hay una gran separación entre *procesamiento* y *coordinación*. La idea es ver al sistema como una colección de procesos operando autónomamente. En este modelo, **coordinación** cubre la comunicacion y cooperación entre procesos. Forma el pegamento que une las actividades realizadas por procesos en un todo.

Cuando los procesos están temporal y referencialmente acoplados, la coordinación toma lugar de una manera directa, llamada **direct coordination**. El acoplamiento referencial generalmente aparece en la forma de referencias explicitas en la comunicación. Por ejemplo un proceso solo se puede comunicar si sabe el nombre o el identificador del proceso con el que quiere intercambiar información. El acoplamiento temporal significa que los procesos que se están comunicando ambos tienen que estar ejecutandose. Un ejemplo concreto de este tipo de coordinación es una llamada telefónica.

Un tipo distinto de coordinación ocurre cuando los procesos están desacoplados temporalmente, pero acoplados referencialmente, a este lo llamamos **mailbox coordination**.

La combinación de acoplamiento temporal y desacoplamiento referencial forma el grupo de **event-based coordination**. En los sistemas referencialmente desacoplados, los procesos no se tienen que conocer explicitamente entre ellos. Lo único que un proceso puede hacer es publicar una notificación describiendo la ocurrencia de un evento y suscribirse a un tipo específico de notificación.

Un último caso es la combinación de desacoplamiento temporal y referencial, llegando al **shared data space**. La idea central es que los procesos se comunican integramente a través de **tuplas**, las cuales son registros estructurados consistentes de un número de campos, similares a una fila de una tabla. Los procesos pueden colocar cualquier tipo de tupla en un shared data space. En orden de recolectar una tupla, un proceso provee un patrón de búsqueda que es comparado contra las tuplas. Cualquier tupla que coincida es retornada.