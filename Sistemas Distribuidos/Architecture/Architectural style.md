%%En el contexto de los [[Sistemas Distribuidos|sistemas distribudios]] (DS) y la [[Arquitecturas de Sistemas Distribuidos|arquitectura de sistemas distribuidos]].%%
El estilo arquitectónico es formulado en terminos de componentes, la manera en que conectan entre sí, la información intercambiada componentes, y finalmente cómo estos elementos están configurados en un sistema. Usando [[Componente|componentes]] y [[Connector|conectores]], podemos lograr varias configuraciones, que pueden ser clasificadas en distintos estilos arquitectónicos.

### Arquitecturas en capas
El concepto básico es el del [[Layers|patrón arquitectónico capas]]

#### Pila de protocolos
![[Pila de protocolos]]

#### Object-based and Service-oriented architectures
Una organización mucho más laxa es la de las **arquitecturas basadas en objetos**. En esencia, cada objeto corresponde a lo que definimos como [[Componente|componente]], y estos componente están conectados a través de un mecanismo de llamada de procedimientos. En caso de un [[Sistemas Distribuidos|sistema distribuido]], una llamada a procedimiento puede tomar lugar a través de una red ([[RPC]]).

Estas arquitecturas son atractivas ya que proveen una manera natural de [[Encapsulamiento|encapsular]] información (llamada **estado** de un objeto) y las operaciones que se pueden realizar sobre dicha información (llamados **métodos**) en una sola entidad ([[OOP]]). La [[Interfaz|interfaz]] ofrecida por un objeto oculta los detalles de implementación, lo cual esencialmente significa que podemos considerar a un objeto completamente independiente de su entorno.

Esta separación nos permite colocar una interfaz en una máquina mientras que el objeto en sí reside en otra. Esta organización se suele llamar objeto distribuido o **distributed object**.

Cuando un cliente **binds** a un objeto distribuido, una implementación de la interfaz del objeto, llamada [[Patrón Proxy|proxy]], es cargada en el espacio de direcciones del cliente ([[RMI]]).

![[RRCC_object-based_architectures_1.png]]

Una continuación de esto son las **arquitecturas orientadas a servicios**. En las arquitecturas orientadas a servicios, una aplicación distribuida o [[Sistemas Distribuidos|sistema distribuido]] es esencialmente construida como una composición de diferentes servicios. Estos servicios pueden no pertenecer todos a la misma entidad administrativa.

El problema central en desarrollar arquitecturas orientadas a servicios es el de composición de servicios o *service composition*, y asegurarse que esos servicios operan en harmonía.

#### Resource-based architectures
![[REST]]

#### Arquitecturas de publicación-suscripción
![[Arquitecturas publish-subscriber]]