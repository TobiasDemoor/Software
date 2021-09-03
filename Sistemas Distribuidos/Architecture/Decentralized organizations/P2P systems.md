# Peer-to-Peer Systems
Desde una perspectiva de alto nivel los procesos que consituyen un sistema [[P2P|peer-to-peer]] o punto a punto son todos iguales. Eso significa que las funciones que tienen que ser llevadas a cabo son representadas por cada proceso que constituye el [[Sistemas Distribuidos|sistema distribuido]]. Como consecuencia mucha de la interacción entre procesos es simétrica, osea, cada proceso actua como un cliente y un servidor al mismo tiempo (a esto se le suele llamar actuar como **servant** o sirviente).

Dado este comportamiento simétrico, las arquitecturas punto a punto evolucionan sobre la pregunta de cómo organizar los procesos en una [[Overlay Network|**overlay network**]].

## Structured peer-to-peer systems
Como sugiere el nombre, los nodos están organizados en una estructura que adhiere a una topología específica y determinada ([[Overlay Network|structured overlay network]]). Esta topología es usada para buscar información eficientemente. Algo característico de los sistemas punto a punto estructurados es que generalmente se encuentran basados en el uso de algo llamado inice libre de semántica. Lo que significa que cada item de datos que debe ser mantenido por el sistema está asociado univocamente a una clave y que esta clave puede ser utilizada subsecuentemente como índice.

El sistema punto a punto como un todo es responsable ahora de almacenar pares clave-valor. Con este fin, cada nodo es asignado un identificador del mismo conjunto de valores posíbles, y cada nodo es responsable de almacenar los datos asociados con un subconjunto específico de claves. En escencia, el sistema implementa una **distributed hash table (DHT)**.

## Unstructured peer-to-peer systems
En contraste a los sistemas estructurados, en los sistemas no estructurados cada nodo mantiene una lista ad hoc de vecinos ([[Overlay Network|unstructured overlay network]]). La estructura resultante se conoce como un **grafo aleatorio** (un grafo donde una arista entre dos nodos i, j existe con una cierta probabilidad P(i,j)).

En un sistema punto a punto no estructurado, cuando un nodo se une usualemente contacta un nodo conocido para obtener una lista inicial de vecinos. Esta lista puede ser usada para obtener más vecinos, y tal vez ignorar otros. Contrario a lo que ocurre con los sistemas estructurados, en los no estructurados no se puede seguir una ruta predeterminada para encontrar un elemento ya que las listas de vecinos son contruidas ad hoc. En cambio se debe recurrir a realizar un búsqueda. Podemos analizar dos extremos de búsqueda en un sistema punto a punto no estructurado:

**Flooding**: En este caso, un nodo simplemente pasa el pedido de información a todos sus vecinos. Un pedido será ignorado si el nodo receptor la ha recibido previamente (similar a los algorítmos de búsqueda en grafo tradicionales). Caso contrario este nodo busca localmente la información solicitada. Si tiene la información puede responder directamente al nodo que emitió la solicitud o enviarselo al que se lo solicito directamente (posiblemente intermediario). Si no tiene la información transmite el pedido a todos sus vecinos.
El flooding puede ser muy costoso y por esto se le asocia un tiempo de expiración o **time-to-live (TTL)**, limitando la cantidad de saltos que puede hacer.

**Random walks:** En el otro extremo al flooding, un nodo elige aleatoriamente un nodo vecino para enviar el pedido. Si este nodo no tiene la información, hace lo mismo y envia el pedido a un nodo aleatorio entre sus vecinos.
Obviamente un random walk impone una carga mucho menor sobre la red, pero a su vez puede tomar un tiempo mucho mayor. Para reducir el tiempo de espera el nodo solicitante puede empezar *n* random walks simultaneas (lo cual tiene un efecto de reducción experimental lineal sobre el tiempo de búsqueda).
Un random walk también debe ser detenido. Para esto se puede usar el TTL nuevamente o cuando un nodo recibe el pedido puede consultar al nodo originario si sigue comunicando el pedido.

En el medio de estos métodos yacen los **policy-based search methods**. Que básicamente son algoritmos de búsqueda custom.

Notablemente los sistemas punto a punto no estructurados, la localización de items de datos relevantes se torna problemático a medida que la red crece. La razón para este problema de [[Escalabilidad|escalabilidad]] es simple, no hay una manera determinística de rutear una solicitud de búsqueda para un item específico.

## Hierarchically organized peer-to-peer networks
Como solución a los inconvenientes presentados en los [[#Unstructured peer-to-peer systems|sistemas punto a punto no estructurados]] se podría proponer el uso de nodos especiales que mantengan un índice de los items de datos.
Hay otras situaciones en las que también es razonable abandonar la naturaleza simétrica de los sistemas punto a punto. Por ejemplo si se tiene una **content delivery network ([[CDN]])**, los nodos pueden ofrecer almacenamiento para hostear copias de documentos Web, permitiendo a los clientes acceder a la páginas cercanas, y así acceder a ellas más rápidamente. Lo que se necesita es un mecanismo para encontrar los mejores lugares para almacenar documentos. En este caso, el uso de un **broker** el cual recolecta información acerca del uso de recursos y disponibilidad de un número de nodos que están próximos entre ellos permitiría sleccionar rápidamente un nodo con recursos suficientes.

Estos nodos que mantienen un índice o actuan como un broker suelen ser llamados **super peers**. Como el nombre sugiere, los super peers suelen estar organizados en una red peer-to-peer, llevando a una organización jerárquica. A continuación se anexa un ejemplo donde podemos ver que todos los nodos regulares ahora llamados weak peers, están conectados a un super peer correspondiente y que todo su tráfico se rutea a través de estos.

![[p2p_systems_hierarchical_organization.png]]

En muchos casos la asociación entre weak peers y super peers es estática; cuando un weak peer se conecta a la red, se asocia a un super peer y permanece asociado hasta que se va de la red. Obviamente se espera que los super peers sean procesos con alta disponibilidad y una larga esperanza de vida.


La distribución vertical no es la única manera de organizar aplicaciones cliente-servidor. En las arquitecturas modernas, es frecuentemente la distribución de clientes y servidores la que importa, a la cual nos referimos como **horizontal distribution** o distribución horizontal. En este tipo de distribución, el cliente o servidor pueden estar separados físicamente en parte lógicamente equivalentes, pero cada parte operando individualmente en su parte del data set, por lo tanto balanceando la carga (*load balancing*). Un tipo particular de sistemas con distribución horizontal son los [[P2P systems|**sistemas peer-to-peer**]] o punto a punto.