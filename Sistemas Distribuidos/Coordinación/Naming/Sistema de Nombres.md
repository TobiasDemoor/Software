Los **nombres** juegan un rol importante en los [[Sistemas de Computación]]. Son usados para compartir recursos, para identificar unívocamente entidades, para referirse a locaciones, y más. Un problema importante con el naming es que un nombre debe poder ser resuelto a la entidad que referencia. La resolución de nombres por lo tanto permite el proceso de acceder a dicha entidad nombrada. Para resolver nombres es necesario implementar un **sistema de nombres**. La diferencia entre el naming en un [[Sistemas Distribuidos|sistema distribuido]] y en uno no distribuido yace en la forma en que está implementado el sistema de nombres.

En los sistemas distribuidos, la implementación del sistema de nombres es distribuida a lo largo de múltiples máquinas. Cómo se realiza esta distribución juega un rol clave en la eficiencia y escalabilidad del sistema de nombres.

## Definiciones básicas
- **Nombre.** Un nombre en un sistema distribuido es una cadena de bits o caracteres que es utilizado para referirse a una entidad.
- **Entidad.** Una entidad puede ser prácticamente cualquier cosa. Se puede operar sobre las entidades.
- **Dirección.** Para operar sobre estas hace falta un **access point** o **punto de acceso** que es un tipo especial de entidad en un sistema distribuido. Al nombre de un punto de acceso se le llama **dirección**. Una entidad puede ofrecer más de un access point. Las direcciones son un tipo particular de nombre que se refiere a un punto de acceso de una entidad.
- **Identificador.** Un identificador es un nombre que cumple con las siguientes propiedades:
	- Un identificador referencia  a lo sumo a una entidad.
	- Cada entidad es referenciada por a lo sumo un identificador.
	- Un identificador siempre referencia a la misma entidad, osea no es reusado.

> Nota: siendo que la dirección indica el punto de acceso a una entidad podría parecer adecuado usar estas para referirse directamente a la entidad. Pero esta organización se torna inflexible y poco amigable para humanos. Por esto los nombres suelen diseñarse para ser **independientes de la localización**.

## Nombres planos
En muchos casos los identificadores son simplemente cadenas al azar de bits, a lo que se suele referir como **nombres planos**, o no estructurados. Una propiedad importante de dicho nombre es que no contiene ninguna inforamción sobre como localizar el punto de acceso asociado a dicha entidad.

### Soluciones simples
Ambas soluciones descritas a continuación solo son aplicables a redes LAN. Sin embargo dentro de dicho entorno se comportan satisfactoriamente. Cabe notar que de cualquier manera su uso presenta problemas de [[escalabilidad]].

#### Broadcasting
Considere un sistema distribuido construido sobre una red que ofrece capacidades de [[Broadcast|difusión]] eficientes. Localizar una entidad en dicho entorno es simple: un mensaje conteniendo el identificador de dicha entidad se envía a cada máquina y cada máquina verifica si es esa entidad.

Este principio es utilizado en el protocolo [[ARP]] para encontrar la dirección de capa 2 de una máquina sabiendo solo su IP. En esencia una máquina envia un paquete en la red local preguntando quién es el dueño de una IP particular. Cuando dicho mensaje llega a una máquina el receptor verifica si debería escuchar a la IP solicitada. Si es así entonces envía una respuesta conteniendo, por ejemplo su [[Direcciones MAC|dirección MAC]].

La difusión se torna ineficiente a medida que la red crece.

#### Punteros
Una alternativa popular para localizar entidades móviles es usar punteros. El principio es simple: cuando una entidad se mueve de A a B, deja atrás un A una referencia a su nueva localización en B. La principal ventaja de este algorítmo es su simpleza. También tiene sus desventajas, por ejemplo la cadena de una entidad que se traslada frecuentemente puede tornarse excesivamente larga, tan larga que localizar dicha entidad se vuelve prohibitivo. Otro problema es que todas las localizaciones intermedias deben mantener su parte de la cadena hasta que no sea necesario. Una última desventaja es que si se pierde un enlace se pierde la capacidad de acceder a la entidad.

### Alternativas home-based
Otra alternativa popular para permitir entidades móviles en redes de gran tamaño es introducir un **home location**, la cual mantiene información acerca de la localización actual de una entidad. En la práctica esta home location suele ser el lugar donde la entidad fue creada.

Este approach es usada como un mecanismo de resguardo para la localización de servicios basada en punteros. 

Una desventaja de esta alternativa es la latencia generada por el hecho de que la entidad puede estar en una localización completamente distinta que su **home location** entonces los mensajes deben viajar distancias posiblemente largas.

### Distributed Hash Table
El sistema de nombres se puede implementar también como una [[DHT]].

### UUID
![[UUID]]

### Alternativas Jerárquicas
En un esquema jerárquico la red es dividida en una colección de **dominios**. hay un único dominio raíz que abarca toda la red. Cada dominio puede ser subdividido en múltiples subdominios menores. Un dominio del nivel más bajo, llamado **dominio hoja**, típicamente corresponde a una LAN en un red de computadoras o a una celda en el sistema telefónico. La suposición general es que dentro de un dominio pequeño el tiempo que toma transferir un mensaje de un nodo a otro es menor que en un dominio mayor.

Cada dominio D tiene asociado un nodo directorio *dir(D)* que lleva cuenta de las entidades en ese dominio. Esto lleva a un árbol de nodos directorio. El nodo directorio del dominio raíz, llamado **nodo (directorio) raíz**, conoce todas las entidades.

![[SSDD_sistema_de_nombres_hierarchical_approches_1.png]]

Para rastrear la localización de una entidad, cada entidad que se encuentra actualmente en un dominido D es represetnada por un **registro de localización** en el nodo directorio *dir(D)*. Un registro de localización para la entidad E en el nodo directorio N para un dominio hoja D contiene la dirección actual de la entidad en ese dominio. En contraste el nodo directorio N' para el dominio de un nivel superior D' que contiene a D, va a tener el registro de localización para E conteniendo soo un puntero a N. Así mismo, el nodo padre de N' va a mantener un registro de localización para E conteniendo solo un puntero a N'.

Una entidad puede tener múltiples direcciones, por ejemplo si está replicada. Si una entidad tiene una dirección en el dominio hoja D₁ y D₂ respectivamente, entonces el nodo directorio del dominio más pequeño que contiene a ambos D₁ y D₂ va a tener dos punteros, uno por cada subdominio que contiene la dirección.

## Nombres estructurados
Los nombres planos son buenos para las máquinas pero por lo general no son convenientes para los humanos. Como alternativa los sistemas de nombres generalmente soportan el uso de nombres estructurados que están compuestos por nombres simples y legibles por humanos.

### Espacios de nombres
![[Espacio de nombres]]

### Resolución de nombres
![[Resolución de nombres]]

### Implementación de un espacio de nombres
Un espacio de nombres forma el corazón de un **servicio de nombres**, osea, un servicio que permite a los usuarios y procesos añadir, remover y buscar nombres. Un servicio de nombres es implementado por **servidores de nombres**. Si un sistema distribuido está restringido a una LAN, es posible implementar el servicio ocn un solo servidor. Sin embargo, en los sistemas distribuidos de gran escala con muchas entidades posiblemente distribuidas a lo largo de un área grande es necesario distribuir la implementación de un espacio de nombres sobre muchos servidores.

#### Distribución de espacio de nombres
Los espacios de nombres para sistemas distribuidos de gran escala suelen estar organizados jerárquicamente. Para implementar dicho sistema efectivamente es conveniente particionarlo en capas lógicas.

La **capa global** o **global layer** está formada por los nodos de más alto nivel, es decir, la raíz y otros nodos directorio lógicamente cercanos a la raíz. Los nodos en la capa global suelen estár caracterizados por su estabilidad en el sentido que sus tablas directorio prácticamente no cambian.

La **capa de administración** o **administration layer** está formada por nodos directorio que están administrados dentro de una sola organización. Una propiedad característica de los nodos en la capa de administración es que representan grupos de entidades que pertenecen a la misma organización o unidad de administración. Estos nodos son relativamente estables aunque pueden ocurrir cambios más frecuentemente que en la capa global.

Finalmente la **capa gerencial** o **managerial layer** consiste de nodos que pueden cambiar frecuentemente. Estos nodos representan hosts en la red local, archivos compartidos y, directorios y archivos definidos por usuarios.

![[RRCC_dns_1.png]]

#### Implementación de resolución de nombres
La distribución de el espacio de nombres a lo largo de múltiples servidores de nombres afecta la implementación de la resolución de nombres. Cada cliente tiene acceso a un **name resolver** local, el cual es responsable de asegurar que se lleve a cabo el proceso de resolución de nombres. Hay dos maneras principales de implementar la resolución de nombres.

En la **resolución de nombres iterativa**, un name resolver entrega el nombre completo al servidor raíz. Es asumido que la dirección donde se puede contactar al servidor raíz es conocida. El servidor raíz resuelve la ruta hasta donde puede y retorna el resultado al cliente. En ese punto el cliente pasa la ruta restante al nuevo servidor de nombres retornado por el primero. Y así continua iterativamente hasta que un servidor tiene la información de la entidad puntual que se está buscando.

![[RRCC_naming_iterative_name_resolution.png]]

La alternativa a una resolución iterativa es una **resolución de nombres recursiva**. En esta el proceso de  encadenamiento de servidores de nombres ocurre entre los servidores. Entonces el name resolver contacta a el servidor raíz y este contacta a su vez al próximo servidor, y este al próximo, así hasta obtener un resultado, el cual vuelve sobre la pila y es retornado al name resolver.

![[RRCC_naming_recursive_name_resolution_1.png]]

La principal desventaja de la resolución recursiva es que pone una demanda mucho mayor sobre cada servidor de nombres. Básicamente, se requiere que un servidor de nombres pueda manejar la resolución completa de una ruta, aunque pueda hacerlo en cooperación con otros servidores. Esta sobrecarga es tán alta que los servidores en la capa global solo suelen soportar resolución iterativa.

Una ventaja importante de la resolución recursiva es que permite un caching más efectivo de los resultados en comparación con la resolución iterativa. Una segunda ventaja es que los costos de comunicación pueden ser reducidos, esto se puede ilustrar más fácilmente en la siguiente figura.

![[RRCC_naming_recursive_name_resolution_2.png]]