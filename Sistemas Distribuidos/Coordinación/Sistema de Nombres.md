Los **nombres** juegan un rol importante en los [[Sistemas de Computación]]. Son usados para compartir recursos, para identificar unívocamente entidades, para referirse a locaciones, y más. Un problema importante con el naming es que un nombre debe poder ser resuelto a la entidad que referencia. La resolución de nombres por lo tanto permite el proceso de acceder a dicha entidad nombrada. Para resolver nombres es necesario implementar un **sistema de nombres**. La diferencia entre el naming en un [[Sistemas Distribuidos|sistema distribuido]] y en uno no distribuido yace en la forma en que está implementado el sistema de nombres.

En los sistemas distribuidos, la implementación del sistema de nombres es distribuida a lo largo de múltiples máquinas. Cómo se realiza esta distribución juega un rol clave en la eficiencia y escalabilidad del sistema de nombres.

## Definiciones básicas
* **Nombre.** Un nombre en un sistema distribuido es una cadena de bits o caracteres que es utilizado para referirse a una entidad.
* **Entidad.** Una entidad puede ser prácticamente cualquier cosa. Se puede operar sobre las entidades.
* **Dirección.** Para operar sobre estas hace falta un **access point** o **punto de acceso** que es un tipo especial de entidad en un sistema distribuido. Al nombre de un punto de acceso se le llama **dirección**. Una entidad puede ofrecer más de un access point. Las direcciones son un tipo particular de nombre que se refiere a un punto de acceso de una entidad.
* **Identificador.** Un identificador es un nombre que cumple con las siguientes propiedades:
	* Un identificador referencia  a lo sumo a una entidad.
	* Cada entidad es referenciada por a lo sumo un identificador.
	* Un identificador siempre referencia a la misma entidad, osea no es reusado.

> Nota: siendo que la dirección indica el punto de acceso a una entidad podría parecer adecuado usar estas para referirse directamente a la entidad. Pero esta organización se torna inflexible y poco amigable para humanos. Por esto los nombres suelen diseñarse para ser **independientes de la localización**.

## Espacios de direccionamiento
### Espacio de direccionamiento plano
En muchos casos los identificadores son simplemente cadenas al azar de bits, a lo que se suele referir como **nombres planos**, o no estructurados. Una propiedad importante de dicho nombre es que no contiene ninguna inforamción sobre como localizar el punto de acceso asociado a dicha entidad.

#### Soluciones simples
Ambas soluciones descritas a continuación solo son aplicables a redes LAN. Sin embargo dentro de dicho entorno se comportan satisfactoriamente. Cabe notar que de cualquier manera su uso presenta problemas de [[escalabilidad]].

##### Broadcasting
Considere un sistema distribuido construido sobre una red que ofrece capacidades de [[Broadcast|difusión]] eficientes. Localizar una entidad en dicho entorno es simple: un mensaje conteniendo el identificador de dicha entidad se envía a cada máquina y cada máquina verifica si es esa entidad.

Este principio es utilizado en el protocolo [[ARP]] para encontrar la dirección de capa 2 de una máquina sabiendo solo su IP. En esencia una máquina envia un paquete en la red local preguntando quién es el dueño de una IP particular. Cuando dicho mensaje llega a una máquina el receptor verifica si debería escuchar a la IP solicitada. Si es así entonces envía una respuesta conteniendo, por ejemplo su dirección MAC.

La difusión se torna ineficiente a medida que la red crece.

##### Punteros
Una alternativa popular para localizar entidades móviles es usar punteros. El principio es simple: cuando una entidad se mueve de A a B, deja atrás un A una referencia a su nueva localización en B. La principal ventaja de este algorítmo es su simpleza. También tiene sus desventajas, por ejemplo la cadena de una entidad que se traslada frecuentemente puede tornarse excesivamente larga, tan larga que localizar dicha entidad se vuelve prohibitivo. Otro problema es que todas las localizaciones intermedias deben mantener su parte de la cadena hasta que no sea necesario. Una última desventaja es que si se pierde un enlace se pierde la capacidad de acceder a la entidad.

#### Alternativas basadas en el hogar
