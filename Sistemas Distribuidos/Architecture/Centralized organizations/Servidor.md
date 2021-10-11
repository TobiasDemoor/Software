%%[[Client-Server]]%%
Un servidor es un [[Proceso|proceso]] implementando un servicio específico para un conjunto de [[Cliente|clientes]]. En esencia, cada servidor está organizado de la misma manera: espera un pedido de un cliente y subsecuentemente se asegura que dicho pedido sea resuelto, luego de lo cual espera el siguiente pedido.

### Servidores concurrentes vs iterativos
Hay varias maneras de organizar servidores. En el caso de un **servidor iterativo** el servidor en sí resuelve el pedido y, si es necesario, envía la respuesta al cliente solicitante. Un **servidor concurrente** no se encarga personalmente de resolver el pedido, sino que lo delega a otro [[Thread|hilo de ejecución]] o a otro [[Proceso|proceso]]. Un servidor multihilo es un ejemplo de servidor concurrente. Otra alternativa es crear un nuevo proceso para cada request recibida.

#### Servidor multihilo
El servidor usualmente se espera por una solicitud, la lleva a cabo y envía la respuesta. Una organización particularmente popular es en la cual se tiene un [[Thread|hilo]] llamado **dispatcher**, el cual lee requests entrantes y luego de examinarlas elige un **worker thread** que se encuentre suspendido y le entrega la request.

Una alternativa a esto sería correr un servidor como una gran máquina de estados de un solo hilo. Cuando se recibe una request, el hilo la examina. Si puede ser resuelta con el cache en memoria, se hace, si no, el hilo debe acceder a disco. Pero en vez de ejecutar una instrucción bloqueante, el hilo programa una operación de disco asincrónica la cual lo interrumpirá cuando esté completa (por medio del [[Sistemas Operativos|sistema operativo]]). Para lograr esto, el hilo debe almacenar el estado de la request y continuar a ver si hay otras requests entrantes ([[Thread#Máquina de estado finito|máquina de estado finito]]).

Una vez que se complete la operación el SO notifica al hilo, el cual entonces buscará el estado de la request y continuará procesandola. Eventualmente se enviará una respuesta al cliente solicitante por medio de una llamada no bloqueante.

| Modelo                   | Características                                 |
| ------------------------ | ----------------------------------------------- |
| Multithreading           | Paralelismo, llamadas al sistema bloqueantes    |
| Proceso monohilo         | No paralelismo, llamadas al sistema bloqueantes |
| Máquina de estado finito | Paralelismo, lamadas al sistema no bloqueantes  | 

### End points
Otro tema a tratar es a través de dónde se contacta un [[Cliente|cliente]] con el [[Servidor|servidor]]. En todos loss casos, los clientes envían pedidos a un **end point**, también llamado **puerto**, en la máquina donde está corriendo el servidor. Cada servidor escucha un end point específico. Ahora resta determinar cómo conoce un cliente el end point al cual acceder. Una primera alternativa es asignar globalmente end points para servicios conocidos. Este es el caso para las requests FTP con el puerto TCP 21 o con el puerto TCP 80 para los servidores HTTP.

Hay muchos servicios que no requieren un end point preasignado. Para estos podemos tener un daemon corriendo que mantenga referencia de en qué end point está cada servidor, y el cliente simplemente consulta primero a este daemon el cual escucha en un puerto conocido por la localización de un servicio en cuestión.

Usualmente implementar cada servicio en un servidor separado suele ser un desperdicio de recursos. Una solución común es tener un solo **superserver** escuchando cada end point asociado con un servicio específico. Cuando entra un pedido, el daemon crea un proceso para manejarlo.

![[servidor_endpoint_1.png]]

### Stateless vs stateful
Una decisión de diseño importante es si el [[Servidor|servidor]] va a ser stateless o no. Un **servidor stateless** (sin estado) es aquel que trata cada petición como si fuera independiente de las anteriores (no guarda estado). Notesé que en varios diseños stateless el servidor mantiene información acerca de sus [[Cliente|clientes]], pero lo crucial es que si dicha información se pierde, esto no llevará a una disrupción del servicio.

Una forma particular de diseño stateless es donde el servidor mantiene lo que se llama **soft state**. En este caso el servidor promete mantener estado por parte del cliente, pero solo por un tiempo limitado. Luego de ese tiempo el servidor retorna al comportamiento usual, así descartando cualquier información que ha mantenido por parte del cliente asociado.

En contraste, un **servidor stateful** generalmente mantiene información persistente sobre sus clientes. Esto significa que la información necesita ser borrada explícitamente por el servidor. Esta estrategia puede mejorar la [[Performance|performance]] de operaciones de lectura/escritura como es percevida por el cliente. Sin embargo, se debe considerar también la desventaja principal de los servidores stateful, que es que si este crashea o es detenido y reiniciado debe recuperar de alguna manera el estado que mantenía o de otra manera no puede asegurar la correcta ejecución.
%%Definición: https://datatracker.ietf.org/doc/html/rfc7230 %%

### Server clusters
Un [[Sistemas Distribuidos#Cluster computing|server cluster]] no es nada más que una colección de máquinas conectadas a través de una [[Redes de computadoras|red]], donde cada máquina corre uno o más [[Servidor|servidores]].

#### LAN clusters
Trataremos los clusters en los cuales las máquinas están conectadas a través de una LAN, que ofrece un alto [[Ancho de banda|ancho de banda]] y [[Latencia|latencia]] baja.

#### Organización general
Los clusters de servidores suelen estar organizados lógicamente en tres niveles. El primer nivel consiste de un switch lógico a través del cual las solicitudes de [[Cliente|clientes]] son routeadas. Estos switches pueden variara ampliamente, desde switches de capa de transporte que acepta conexiones TCP entrantes hasta un Web server que acepta requests HTTP.

Como en cualquier [[Centralized organizations#Arquitecturas multinivel|arquitectura cliente-servidor multinivel]] los clusters de servidores pueden contener servidores dedicados al procesamiento de aplicación que conforman el segundo nivel. Estos suelen correr sobre máquinas de alta performance pero no necesariamente.

Y el tercer nivel consiste de servidores de datos, notablemente file y [[Bases de Datos/Bases de Datos|database]] servers. Dependiendo de los requerimientos estos pueden correr sobre hardware especializado configurado para acceso a disco de alta velocidad y caches locales grandes.

![[lan_server_cluster_1.png]]

##### Request dispatching
Un objetivo de diseño importante para los clusters de servidores es ocultar el hecho de que hay múltiples servidores. Esta [[Transparencia de distribución#Transparencia de acceso|transparencia de acceso]] es ofrecida a través de un solo punto de entrada. El switch forma el punto de entrada para el cluster de servidores, ofreciendo una sola dirección de red. Por motivos de [[Escalabilidad|escalabilidad]] y [[Reliability|disponibilidad]], un cluster puede tener múltiples puntos de acceso, donde cada punto de acceso es implementado en una máquina separada (no se considera esto en lo siguiente).

Una forma estándar de acceder a un cluster de servidores es estableciendo una conexión TCP sobre la cual se envian los pedidos de nivel de applicación (HTTP por ejemplo) como parte de una sesión. Una sesión termina cerrando la conexión. En el caso de **transport-layer switches**, el switch acepta el pedido de conexión TCP entrante y entrega esta conexión a uno de los servidores. Hay esencialmente dos formas de hacer esto.

En el primer caso el cliente establece la conexión TCP de manera que todas las requests pasen a través del switch. El switch entonces establece una conexión TCP con el servidor seleccionado y pasa los pedidos a este servidor, también acepta las respuestas del servidor y las reenvia al cliente. En efecto el switch se encuentra en el medio de la conexión TCP actuando como un [[Proxy|proxy]] reescribiendo la dirección origen y destino. Este método es una forma de **network adress translation (NAT)**.

Alternativamente, el switch puede entregar la conexión al servidor seleccionado, tal que todas las respuestas son directamente comunicadas al cliente sin pasar a través del switch server. Este funcionamiento se suele llamar **TCP handoff**, para que funcione el servidor seleccionado debe enviar las respuestas al cliente modificando la dirección de origen para que sea la del switch (el cliente espera una respuesta de esa dirección conocida, no de cualquier otra). Esta alternativa funciona bien cuando las respuestas son mucho mayores en tamaño que las solicitudas (como es para los servidores Web).

Como se puede ver, el switch tiene un rol muy importante en el balanceo de carga entre los servidores.

#### WAN clusters
Con el desarrollo del [[Sistemas Distribuidos#Cloud computing|cloud computing]] se facilitó la creación de clusters WAN. La razón principal por la cual se desearía distribuir los servidores a través de una WAN es para ofrecer [[Locality|localidad]].

##### Request dispatching
En el caso que la [[Locality|localidad]] sea importante, entonces se vuelve importante asignar un cliente que solicita un servicio a un [[Servidor|servidor]] cercano a él. La decisión de cuál servidor debería encargarse de la solicitud del cliente es un problema de la **redirection policy** o política de redirección. Si suponemos que el cliente contacte primero a un request dispatcher análogo al switch de un cluster LAN, entonces ese dispatcher deberá tener que estimar la [[Latencia|latencia]] entre el cliente y varios servidores.

Una vez que el servidor ha sido seleccionado el dispatcher deberá informar al cliente. Hay varios mecanísmos de redirección (**redirection mechanisms**) posibles. Uno popular es que el dispatcher sea un servidor [[DNS]]. Al enviar la solicitud para buscar el nombre el cliente también envia su dirección IP, permitiendole al dispatcher encontrar el servidor óptimo. Desafortunadamente este esquema no es perfecto por dos razones.

Primero, en vez de enviar la dirección IP del cliente, lo que ocurre es que el servidor DNS local es contactado por el cliente y este a su vez contacta a nuestro dispatcher que funciona como servidor DNS. Osea que la IP que se recibe no es la del cliente.

Segundo, dependiendo del esquema utilizado para resolver un domain name, puede ser que la dirección del servidor DNS local no sea utilizada. En cambio, puede pasar que el servidor DNS que decide la dirección IP a retornar (nuestro dispatcher) sea engañado por el hecho de que la solicitud la realiza otro servidor DNS actuando como intermediario entre el cliente y el DNS final. En estos casos se pierde completamente el conocimiento de [[Locality|localidad]].

Una técnica posible para modelar este problema es el uso de **[[Geometric Overlay Networks|geometric overlay networks]]**. Donde se tienen como nodos en la red a las réplicas y a los clientes, y se busca asignarle a un cliente la réplica a menor distancia dentro de la geometric overlay network.