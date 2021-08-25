# Distributed Systems Architecture
Los [[Distributed Systems|sistemas distribuidos]] (DS) suelen ser piezas complejas de software en las cuales por definición sus [[Componente|componentes]] están distribuidos a través de multiples equipos. Para dominar esta complejidad es necesario que estos sistemas estén correctamente organizados. Se puede realizar una división entre la organización lógica de la colección de componentes de software, y la organización física.

La organización de DS es principalmente acerca de los componentes de software que componen el sistema. Estas [[Software Architecture|arquitecturas de software]] nos dicen cómo los varios componentes van a estar organizados y como deberían interactuar.

Un objetivo importante de los DS es separar las aplicaciones de las plataformas subyacentes mediante la capa de [[Middleware|middleware]]. El adoptar esta capa es una desición arquitectónica importante, y su propósito principal es el proveer [[Distribution Transparency|transparencia de distribución]]. Se debe notar que hay trade-offs necesarios para lograr la transparencia, eso ha llevado a varias técnicas para ajustar el middleware a las necesidades de las aplicaciones que lo utilizan.

La realización contreta del DS requiere que instanciemos y coloquemos software en hardware real. Hay varias decisiones que se deben tomar para hacer esto. La instanciación final de la arquitectura de software suele ser nombrada como la arquitectura de sistema o system architecture.

El tomar decisiones acerca de los [[Componente|componentes]] de software, su interacción, y su localización lleva a una [[Software Architecture|arquitectura de software]], también conocida como arquitectura de sistema o **system architecture**.

## Centralized organizations
Una punto donde hay mucho concenso en el area de los [[Distributed Systems|sistemas distribuidos]] es que pensar en términos de *clientes* que solicitan servicios de *servidores* ayuda a entender y administrar la complejidad de estos sistemas ([[Client-Server|patrón cliente servidor]]).

En el modelo cliente-servidor básico, los procesos en un [[Distributed Systems|sistema distribuido]] son divididos en dos grupos (con posible solapamiento). Un proceso **servidor** es un proceso implementando un servicio específico. Un proceso **cliente** es un proceso que solicita un servicio a un servidor mediante el envio de una solicitud y subsecuentemente la espera de la respuesta. La interacción cliente-servidor también es conocida como **request-reply behavior**.

Las multitiered client-server architectures son consecuencia directa de dividir aplicaciones distribuidas en componentes de interfaz de usuario, procesamiento y manejo de datos. Estos tiers corresponden directamente a la organización lógica de las organizaciones. Este tipo de distribución se llama usualmente **vertical distribution** o distribución vertical.

La organización más básica consta de dos tipos de máquinas **(physically) two-tiered architecture**:
1. Una máquina cliente que contiene solo los programas que implementan (parte de) el nivel de intefaz de usuario.
2. Una máquina servidor que contiene el resto, osea, programas implementando el nivel de procesamiento y datos.

En esta organización todo es controlado por el servidor mientras el cliente no es nada más que una terminal boba (dumb terminal), posiblemente con solo una GUI. Sin embargo hay otras posibilidades y se puede distribuir de distintas maneras la aplicación entre estas dos máquinas, desde que la máquina servidor tenga control total sobre la interfaz que corre en la máquina cliente (el extremo de un *thin client*) hasta que la máquina cliente contenga toda la lógica de aplicación y posiblemente parte de la capa de datos (el extremo de un *fat client*).

También se pueden plantear arquitecturas de tres niveles, **(physically) three-tiered architecture**. En estas arquitecturas, tradicionalmente los programas que forman parte de la capa de procesamiento son ejecutados en un servidor separado, pero pueden además estar distribuidos entre las máquinas de cliente y servidor.
Un ejemplo muy común de esto ocurre en la organización de sitios web. En este caso el web server actúa como un punto de entrada al sitio, pasando sus requests al application server donde el procesamiento en cuestión ocurre. El application server a su vez interactúa con el database server.

## Decentralized organizations: [[P2P|peer-to-peer]] systems
La distribución vertical no es la única manera de organizar aplicaciones cliente-servidor. En las arquitecturas modernas, es frecuentemente la distribución de clientes y servidores la que importa, a la cual nos referimos como **horizontal distribution** o distribución horizontal. En este tipo de distribución, el cliente o servidor pueden estar separados físicamente en parte lógicamente equivalentes, pero cada parte operando individualmente en su parte del data set, por lo tanto balanceando la carga (*load balancing*).


