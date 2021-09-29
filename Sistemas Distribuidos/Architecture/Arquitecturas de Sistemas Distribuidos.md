Los [[Sistemas Distribuidos|sistemas distribuidos]] (DS) suelen ser piezas complejas de software en las cuales por definición sus [[Componente|componentes]] están distribuidos a través de multiples equipos. Para dominar esta complejidad es necesario que estos sistemas estén correctamente organizados. Se puede realizar una división entre la organización lógica de la colección de componentes de software, y la organización física.

La organización de DS es principalmente acerca de los componentes de software que componen el sistema. Estas [[Software Architecture|arquitecturas de software]] nos dicen cómo los varios componentes van a estar organizados y como deberían interactuar.

Un objetivo importante de los DS es separar las aplicaciones de las plataformas subyacentes mediante la capa de [[Middleware|middleware]]. El adoptar esta capa es una desición arquitectónica importante, y su propósito principal es el proveer [[Transparencia de distribución|transparencia de distribución]]. Se debe notar que hay trade-offs necesarios para lograr la transparencia, eso ha llevado a varias técnicas para ajustar el middleware a las necesidades de las aplicaciones que lo utilizan.

La realización contreta del DS requiere que instanciemos y coloquemos software en hardware real. Hay varias decisiones que se deben tomar para hacer esto. La instanciación final de la arquitectura de software suele ser nombrada como la arquitectura de sistema o system architecture.

El tomar decisiones acerca de los [[Componente|componentes]] de software, su interacción, y su localización lleva a una [[Software Architecture|arquitectura de software]], también conocida como arquitectura de sistema o **system architecture**.

## Centralized organizations
![[Centralized organizations]]

## Decentralized organizations
![[Decentralized organizations]]

## Hybrid Architectures
### Edge-server systems
Los sistemas de servidores de borde (Edge-servers systems) llevan los servidores al “borde” de la [[Internet]], es decir cerca de los clientes (al extremo logico). Su objetivo es acercar los recursos a los consumidores ([[Locality]]).

### Collaborative distributed systems
Un uso notable de las arquitecturas híbridas es en los sistemas colaborativos distribuidos. El problema principal en estos sistemas es iniciar una operación, para lo que usualmente se deploya un esquema [[Client-Server|cliente-servidor tradicional]]. Una vez que un nodo se ha unido al sistema, puede usar un esquema totalmente descentralizado para la colaboración.

Un ejemplo concreto de esto es BitTorrent, que es un [[P2P systems|sistema punto a punto]] de descarga de archivos. La concepto básico de su funcionamiento es que un usuario busca un archivo, descarga fragmentos del archivo de otros usuarios hasta que está que estos pueden ser ensamblados generando el archivo completo. Un objetivo importante es el asegurar la colaboración, y en estos sistemas hay una fracción importante de participantes que solamente descargan archivos, pero sin contribuir nada, a este fenomeno se lo llama **free riding**.

![[collaborative_distributed_systems_bit_torrent_1.png]]

Para descargar un archivo, el usuario accede a un directorio global. Ese directorio contiene referencias a lo que se llama archivos torrent. Un archivo torrent o **torrent file** contiene información que es necesaria para descargar un archivo específico. En particular contiene un link a lo que es conocido como un **tracker**, el cual es un servidor que mantiene un recuento preciso de los nodos activos que tienen (segmentos) del archivo solicitado. Un nodo activo es uno que está actualmente descargando un archivo. 

Una vez que se identifican los nodos de donde van a ser descargados los segmentos, el nodo descargante se convierte en activo. En ese punto, va a ser forzado a ayudar a otros, por ejemplo proveyendo segmentos del archivo que está descargando que otros no tienen aún. Esto se asegura mediante una regla simple: si un nodo P nota que un nodo Q está descargando más de lo que está subiendo P puede decidir disminuir la velocidad con la que envía datos a Q. Este esquema funciona bien si P tiene algo para descargar de Q. Por esta razon, los nodos suelen tener referencias a muchos nodos, poniendo a todos en mejores condiciones para intercambiar datos.