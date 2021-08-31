---
cssclass: clean-embeds
---

## Architectural styles
%%En el contexto de los [[Distributed Systems|sistemas distribudios]] (DS) y la [[Distributed Systems Architecture|arquitectura de sistemas distribuidos]].%%
El estilo arquitectónico es formulado en terminos de componentes, la manera en que conectan entre sí, la información intercambiada componentes, y finalmente cómo estos elementos están configurados en un sistema. Usando [[Componente|componentes]] y [[Connector|conectores]], podemos lograr varias configuraciones, que pueden ser clasificadas en distintos estilos arquitectónicos.

### Arquitecturas en capas
El concepto básico es el del [[Layers|patrón arquitectónico capas]]

![[Pila de protocolos]]

#### Object-based and Service-oriented architectures
Una organización mucho más laxa es la de las **arquitecturas basadas en objetos**. En esencia, cada objeto corresponde a lo que definimos como [[Componente|componente]], y estos componente están conectados a través de un mecanismo de llamada de procedimientos. En caso de un [[Distributed Systems|sistema distribuido]], una llamada a procedimiento puede tomar lugar a través de una red ([[Remote Procedure Calls|RPC]]).

Estas arquitecturas son atractivas ya que proveen una manera natural de [[Encapsulamiento|encapsular]] información (llamada **estado** de un objeto) y las operaciones que se pueden realizar sobre dicha información (llamados **métodos**) en una sola entidad ([[OOP|OOP]]). La [[Interfaz|interfaz]] ofrecida por un objeto oculta los detalles de implementación, lo cual esencialmente significa que podemos considerar a un objeto completamente independiente de su entorno.

Esta separación nos permite colocar una interfaz en una máquina mientras que el objeto en sí reside en otra. Esta organización se suele llamar objeto distribuido o **distributed object**.

Cuando un cliente **binds** a un objeto distribuido, una implementación de la interfaz del objeto, llamada [[Proxy|proxy]], es cargada en el espacio de direcciones del cliente ([[Remote Method Invocations|RMI]]).

![[object-based_architectures_1.png]]

Una continuación de esto son las **arquitecturas orientadas a servicios**. En las arquitecturas orientadas a servicios, una aplicación distribuida o [[Distributed Systems|sistema distribuido]] es esencialmente construida como una composición de diferentes servicios. Estos servicios pueden no pertenecer todos a la misma entidad administrativa.

El problema central en desarrollar arquitecturas orientadas a servicios es el de composición de servicios o *service composition*, y asegurarse que esos servicios operan en harmonía.

#### Resource-based architectures
![[REST]]

#### Publish-subscribe architectures
A medida que los sistemas siguen creciendo y los procesos pueden unirse e irse más fácilmente, es importante tener una arquitectura donde las dependencias entre procesos sean lo más sueltas posibles. Una gran clase de [[Distributed Systems|sistemas distribuidos]] han adoptado una arquitectura en la que hay una gran separación entre *procesamiento* y *coordinación*. La idea es ver al sistema como una colección de procesos operando autónomamente. En este modelo, **coordinación** cubre la comunicacion y cooperación entre procesos. Forma el pegamento que une las actividades realizadas por procesos en un todo.

Cuando los procesos están temporal y referencialmente [[Acoplamiento|acoplados]], la coordinación toma lugar de una manera directa, llamada **direct coordination**. El acoplamiento referencial generalmente aparece en la forma de referencias explicitas en la comunicación. Por ejemplo un proceso solo se puede comunicar si sabe el nombre o el identificador del proceso con el que quiere intercambiar información. El acoplamiento temporal significa que los procesos que se están comunicando ambos tienen que estar ejecutandose. Un ejemplo concreto de este tipo de coordinación es una llamada telefónica.

Un tipo distinto de coordinación ocurre cuando los procesos están desacoplados temporalmente, pero acoplados referencialmente, a este lo llamamos **mailbox coordination**.

La combinación de acoplamiento temporal y desacoplamiento referencial forma el grupo de **event-based coordination**. En los sistemas referencialmente desacoplados, los procesos no se tienen que conocer explicitamente entre ellos. Lo único que un proceso puede hacer es publicar una notificación describiendo la ocurrencia de un evento y suscribirse a un tipo específico de notificación.

Un último caso es la combinación de desacoplamiento temporal y referencial, llegando al **shared data space**. La idea central es que los procesos se comunican integramente a través de **tuplas**, las cuales son registros estructurados consistentes de un número de campos, similares a una fila de una tabla. Los procesos pueden colocar cualquier tipo de tupla en un shared data space. En orden de recolectar una tupla, un proceso provee un patrón de búsqueda que es comparado contra las tuplas. Cualquier tupla que coincida es retornada.