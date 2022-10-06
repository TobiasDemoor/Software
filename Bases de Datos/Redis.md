%%Fuente: [Introduction to Redis](https://redis.io/docs/about/)%%
Redis es un almacenamiento de estructura de datos en memoria de [[Software libre|código abierto]] (con [[Licencias|licencia BSD]]) que es utilizado como [[Bases de Datos|base de datos]], caché, [[Message Oriented Middleware|broker de mensajes]], y streaming engine. Redis provee estructuras de datos tales como strings, hashes, lists, sets, sorted sets con queries por rango, bitmaps, hyperloglogs, geospatial indexes, y streams. Redis tiene [[Replicación|replicación]] incorporada, Lua scripting, LRU eviction, [[Transacciones|transactions]], diferentes niveles de persistencia en disco, provee alta disponibilidad a través de Redis Sentinel y particionamiento automático con Redis Cluster.

Se pueden ejecutar operaciones automáticas, como concatenar a un string, incrmentar el valor en un hash, agregar un elemento a una lista, calcular la intersección, unión y diferencia de conjuntos, u obtener el miembro de mayor prioridad en un set ordenado.

Para lograr mayor performance, Redis trabaja con un dataset en memoria. Dependiendo del caso de uso, Redis puede persistir la información periódicamente bajandola a disco o añadiendo cada comando a un log en disco. También se puede deshabilitar la persistencia si solo se necesita un caché en memoria, en red y con muchas features.

Redis permite replicación asíncrona con sincronización rápida no bloqueante y auto-reconeción con resincronización parcial.

%%Fuente: [Redis: almacen de datos en memoria](https://aws.amazon.com/es/redis/)%%
## ¿Qué es Redis?
Redis, que significa Remote Dictionary Server, es un rápido almacén de datos clave-valor en memoria de [[Software libre|código abierto]]. El proyecto se inició cuando Salvatore Sanfilippo, el desarrollador original de Redis, trataba de mejorar la escalabilidad de su empresa emergente italiana. A partir de ahí, desarrolló Redis, que ahora se utiliza como [[Bases de Datos|base de datos]], caché, [[Message Oriented Middleware|agente de mensajes]] y cola.

Redis ofrece tiempos de respuesta inferiores al milisegundo, lo que permite que se realicen millones de solicitudes por segundo para aplicaciones en tiempo real de la industria, como videojuegos, tecnología publicitaria, servicios financieros, sanidad e IoT. Hoy en día, Redis es uno de los motores de código abierto más populares en la actualidad, denominado la base de datos “preferida” por Stack Overflow durante cinco años consecutivos. Por su rápido rendimiento, Redis es una opción muy habitual en aplicaciones de almacenamiento en caché, administración de sesiones, videojuegos, tablas de clasificación, análisis en tiempo real, datos geoespaciales, servicios de vehículos compartidos, chat/mensajería, streaming de contenido multimedia y publicación/suscripción.

## Beneficios de Redis
### Rendimiento
Todos los datos de Redis residen en la memoria, lo que permite un acceso a datos de baja latencia y alto rendimiento. A diferencia de las bases de datos tradicionales, los almacenes de datos en memoria no requieren un viaje al disco, lo que reduce la latencia del motor a microsegundos. Debido a esto, el almacén de datos en memoria permite soportar una cantidad mucho mayor de operaciones y ofrecer tiempos de respuesta más rápidos. El resultado es un desempeño increíblemente rápido y operaciones de lectura o escritura promedio que se ejecutan en menos de un milisegundo y una capacidad para procesar millones de operaciones por segundo.  

### Estructuras de datos flexibles
A diferencia de otros almacenes de datos de clave valor simplistas que ofrecen estructuras de datos limitadas, Redis cuenta con una amplia variedad de estructuras de datos para satisfacer los requisitos de sus aplicaciones. Los tipos de datos de Redis incluyen:  

- Cadenas: datos de texto o binarios de hasta 512 MB de tamaño
- Listas: una colección de cadenas en el orden en que se agregaron
- Conjuntos: una colección desordenada de cadenas con la capacidad para intercalarse, unirse y diferenciarse de otros tipos de conjuntos
- Conjuntos ordenados: conjuntos ordenados por un valor
- Hashes: una estructura de datos para almacenar una lista de campos y valores
- Mapas de bits: un tipo de datos que ofrece operaciones a nivel de bits  
- HyperLogLogs: una estructura de datos probabilísticos para estimar los elementos únicos en un conjunto de datos 
- Secuencias: una cola de mensajes de estructura de datos de registro
- Geoespacial: mapas de entradas basados en longitud / latitud, "cercanía"
- [[JSON]]: un objeto anidado y semiestructurado de valores con nombre que admite números, cadenas, booleanos, matrices y otros objetos  

### Simplicidad y facilidad de uso
Redis le permite escribir código tradicionalmente complejo con menos líneas y más simples. Con Redis puede escribir menos líneas de código para almacenar, obtener acceso y utilizar datos en sus aplicaciones. La diferencia es que los desarrolladores que usan Redis pueden usar una estructura de comando simple en contraposición a los lenguajes de consulta de bases de datos tradicionales. Por ejemplo, puede usar la estructura de datos hash de Redis para mover datos a un almacén de datos con solo una línea de código. Una tarea de similares características en un almacén de datos sin estructuras de datos hash necesitaría muchas líneas de código para realizar la conversión de un formato a otro. Redis incluye estructuras de datos originales y muchas opciones para trabajar e interactuar con ellos.

### Replicación y persistencia
Redis utiliza una arquitectura con un servidor principal y réplicas que admite la [[Replicación|replicación]] asíncrona en la que los datos se replican en numerosos servidores de réplicas. De este modo, se logra un mejor nivel de rendimiento de lectura (ya que las solicitudes se pueden repartir entre varios servidores) y menores tiempos de recuperación cuando el servidor principal sufre un corte. Por una cuestión de persistencia, Redis admite copias de seguridad puntuales (copia el conjunto de datos Redis en el disco).  

**Redis no se creó para ser una base de datos duradera y coherente**.

### Alto nivel de disponibilidad y escalabilidad
Redis ofrece una arquitectura con servidor principal y réplica en una topología en clústeres o principal con un único nodo. Esto permite crear soluciones con un alto nivel de disponibilidad, lo que ofrece fiabilidad y rendimiento estables. Cuando se necesita ajustar el tamaño de un clúster, se encuentran disponibles diferentes opciones de escalado. Esto permite que el tamaño del clúster se ajuste a sus necesidades.  

### Código abierto
Redis es un proyecto de código abierto que cuenta con el apoyo de una comunidad activa. No hay limitaciones de proveedores ni tecnología porque Redis está basado en estándares abiertos, admite formatos de datos abiertos y cuenta con una completa base de clientes.

## Principales casos de uso de Redis
### Almacenamiento en caché
Redis es una excelente opción para implementar una caché en memoria de alta disponibilidad a fin de reducir la latencia de acceso a los datos, incrementar la capacidad de procesamiento y aliviar la carga de la aplicación y de la base de datos relacional o NoSQL. Redis puede suministrar elementos solicitados frecuentemente con tiempos de respuesta inferiores a un milisegundo, y permite ajustar la escala con facilidad en caso de cargas mayores sin tener que ampliar el costoso backend. El almacenamiento en caché de resultados de consultas en bases de datos, de sesiones persistentes, de páginas web y de objetos de uso frecuente, como imágenes, archivos y metadatos, son ejemplos comunes de tipos de almacenamiento en caché que se pueden realizar con Redis.  

### Chat, mensajería y colas
Redis admite tareas de [[Arquitecturas publish-subscriber|publicación y suscripción]] con correspondencia de patrones y una variedad de estructuras de datos, como listas, conjuntos ordenados y hashes. Eso le permite a Redis respaldar salas de chat de alto rendimiento, streaming de comentarios en tiempo real, actividades en redes sociales e intercomunicaciones entre servidores. La estructura de datos de Listas de Redis facilita la implementación de una cola liviana. Las listas ofrecen operaciones atómicas, así como capacidades de bloqueo, por lo que resultan aptas para una variedad de aplicaciones que requieren un agente de mensajes fiable o una lista circular.  

### Tablas de clasificación de videojuegos
Redis es una de las opciones favoritas de los desarrolladores de videojuegos que necesitan crear tablas de clasificación con datos generados en tiempo real. Simplemente utilice la estructura de datos de los conjuntos clasificados de Redis, que proporciona singularidad de elementos, mientras que mantiene la lista ordenada por puntaje de usuarios. Crear una lista de clasificación en tiempo real es tan sencillo como actualizar la puntuación de un usuario cada vez que cambia. También puede utilizar los conjuntos clasificados para administrar datos de serie temporal con sellos de tiempo como puntuación.  

### Almacén de sesiones
Redis, un almacén de datos en memoria con un alto nivel de disponibilidad y persistencia, es una de las opciones favoritas de los desarrolladores de aplicaciones para almacenar y administrar datos de sesiones para aplicaciones a escala de Internet. Redis ofrece la latencia menor a un milisegundo, la escala y la resiliencia necesarias para administrar datos de sesiones, como perfiles de usuarios, credenciales, estados de sesiones y personalización específica para usuarios.  

### Streaming completo de contenido multimedia
Redis ofrece un almacén de datos en memoria y ágil para respaldar casos de uso de streaming en directo. El almacenamiento de metadatos de Redis se puede utilizar para perfiles de usuarios e historial de visualizaciones, tokens/información de autenticación para millones de usuarios y archivos de manifiestos para permitir que [[CDN]] haga streaming de videos a millones de usuarios de aplicaciones móviles y de escritorio en un determinado momento.  

### Análisis geoespacial
https://www.memurai.com/blog/geospatial-queries-in-redis
Redis ofrece estructuras de datos en memoria y operadores personalizados para administrar datos geoespaciales a escala y con velocidad. Los comandos como GEOADD, GEODIST, GEORADIUS y GEORADIUSBYMEMBER utilizados para almacenar, procesar y analizar datos geoespaciales en tiempo real facilitan y agilizan las tareas con Redis. Puede usar Redis para agregar características basadas en ubicación geográfica, como tiempo de conducción, distancia recorrida y puntos de interés, a sus aplicaciones.  

### Machine Learning
https://youtu.be/RyGxAsOOXpw
Las aplicaciones modernas basadas en datos exigen que el [[Machine Learning]] procese rápidamente grandes volúmenes de datos variados y ágiles, y que automatice la toma de decisiones. Para casos de uso como la detección de fraudes en juegos y servicios financieros, las subastas en tiempo real en el sector de la tecnología publicitaria y las coincidencias en aplicaciones de citas y viajes compartidos, la capacidad para procesar datos instantáneamente y tomar decisiones en decenas de milisegundos tiene una importancia fundamental. Redis le proporciona un almacén de datos en memoria para crear, entrenar e implementar rápidamente modelos de Machine Learning.  

### Análisis en tiempo real
Redis se puede usar con soluciones de streaming como almacén de datos en memoria para incorporar, procesar y analizar datos en tiempo real con una latencia menor a un milisegundo. Redis es la opción ideal para casos de uso de análisis en tiempo real, como análisis de datos de redes sociales, focalización de anuncios, personalización e IoT.

## Redis vs. Memcached
Tanto Redis como Memcached son almacenes de datos en memoria de código abierto. Memcached, un servicio de almacenamiento en caché de memoria distribuida de alto rendimiento, está diseñado para la simplicidad, mientras que Redis ofrece un extenso conjunto de características que lo hacen efectivo para una amplia gama de casos de uso. Si desea ver una comparación de características más detallada para que lo ayude a tomar una decisión, consulte [Redis vs Memcached](https://aws.amazon.com/es/elasticache/redis-vs-memcached/). Ambos trabajan con bases de datos relacionales o de clave-valor a fin de mejorar el rendimiento, tales como MySQL, PostgreSQL, Aurora, Oracle, SQL Server, DynamoDB, etc.

%%Fuente: [Real-Time Delivery Architecture at Twitter](https://www.infoq.com/presentations/Real-Time-Delivery-Twitter/)%%
## Caso de uso Twitter
El uso surge de una necesidad de presentar en tiempo real a los usuarios los tweets que deben ver.
Se tiene una (en realidad varias mediante replicación) instancia de Redis Cache por cada timeline de usuario activo. Entonces cuando alguien tweetea algo, este se inserta en todos los cache de los usuarios que deben verlo (módulo Fanout).
Usan una lista nativa, RPUSHX, y items con una estructura estable pero dinámica (no tiene el texto de los tweets, solo su id).
El timeline service consulta redis y obtiene los tweets que debe ver, los puebla con su contenido y se los entrega al usuario.

Originalmente usaban memcached y se movieron a redis para usar las listas nativas.

%%
Fuente:
https://redis.io/docs/getting-started/faq/
https://redis.io/docs/reference/optimization/memory-optimization/
%%
## Uso de RAM
To give you a few examples (all obtained using 64-bit instances):

-   An empty instance uses ~ 3MB of memory.
-   1 Million small Keys -> String Value pairs use ~ 85MB of memory.
-   1 Million Keys -> Hash value, representing an object with 5 fields, use ~ 160 MB of memory.

Testing your use case is trivial. Use the `redis-benchmark` utility to generate random data sets then check the space used with the `INFO memory` command.

64-bit systems will use considerably more memory than 32-bit systems to store the same keys, especially if the keys and values are small. This is because pointers take 8 bytes in 64-bit systems. But of course the advantage is that you can have a lot of memory in 64-bit systems, so in order to run large Redis servers a 64-bit system is more or less required. The alternative is sharding.

Redis has built-in protections allowing the users to set a max limit on memory usage, using the `maxmemory` option in the configuration file to put a limit to the memory Redis can use. If this limit is reached, Redis will start to reply with an error to write commands (but will continue to accept read-only commands).

You can also configure Redis to evict keys when the max memory limit is reached. See the [eviction policy docs](https://redis.io/docs/manual/eviction/) for more information on this.


https://redis.io/docs/manual/persistence/
## Persistencia
How Redis writes data to disk (append-only files, snapshots, etc.)

Persistence refers to the writing of data to durable storage, such as a solid-state disk (SSD). Redis itself provides a range of persistence options:

-   **RDB** (Redis Database): The RDB persistence performs point-in-time snapshots of your dataset at specified intervals.
-   **AOF** (Append Only File): The AOF persistence logs every write operation received by the server, that will be played again at server startup, reconstructing the original dataset. Commands are logged using the same format as the Redis protocol itself, in an append-only fashion. Redis is able to [rewrite](https://redis.io/docs/manual/persistence/#log-rewriting) the log in the background when it gets too big.
-   **No persistence**: If you wish, you can disable persistence completely, if you want your data to just exist as long as the server is running.
-   **RDB + AOF**: It is possible to combine both AOF and RDB in the same instance. Notice that, in this case, when Redis restarts the AOF file will be used to reconstruct the original dataset since it is guaranteed to be the most complete.

The most important thing to understand is the different trade-offs between the RDB and AOF persistence.

### RDB advantages

-   RDB is a very compact single-file point-in-time representation of your Redis data. RDB files are perfect for backups. For instance you may want to archive your RDB files every hour for the latest 24 hours, and to save an RDB snapshot every day for 30 days. This allows you to easily restore different versions of the data set in case of disasters.
-   RDB is very good for disaster recovery, being a single compact file that can be transferred to far data centers, or onto Amazon S3 (possibly encrypted).
-   RDB maximizes Redis performances since the only work the Redis parent process needs to do in order to persist is forking a child that will do all the rest. The parent process will never perform disk I/O or alike.
-   RDB allows faster restarts with big datasets compared to AOF.
-   On replicas, RDB supports [partial resynchronizations after restarts and failovers](https://redis.io/topics/replication#partial-resynchronizations-after-restarts-and-failovers).

### RDB disadvantages

-   RDB is NOT good if you need to minimize the chance of data loss in case Redis stops working (for example after a power outage). You can configure different _save points_ where an RDB is produced (for instance after at least five minutes and 100 writes against the data set, you can have multiple save points). However you'll usually create an RDB snapshot every five minutes or more, so in case of Redis stopping working without a correct shutdown for any reason you should be prepared to lose the latest minutes of data.
-   RDB needs to fork() often in order to persist on disk using a child process. fork() can be time consuming if the dataset is big, and may result in Redis stopping serving clients for some milliseconds or even for one second if the dataset is very big and the CPU performance is not great. AOF also needs to fork() but less frequently and you can tune how often you want to rewrite your logs without any trade-off on durability.

### AOF advantages

-   Using AOF Redis is much more durable: you can have different fsync policies: no fsync at all, fsync every second, fsync at every query. With the default policy of fsync every second, write performance is still great. fsync is performed using a background thread and the main thread will try hard to perform writes when no fsync is in progress, so you can only lose one second worth of writes.
-   The AOF log is an append-only log, so there are no seeks, nor corruption problems if there is a power outage. Even if the log ends with a half-written command for some reason (disk full or other reasons) the redis-check-aof tool is able to fix it easily.
-   Redis is able to automatically rewrite the AOF in background when it gets too big. The rewrite is completely safe as while Redis continues appending to the old file, a completely new one is produced with the minimal set of operations needed to create the current data set, and once this second file is ready Redis switches the two and starts appending to the new one.
-   AOF contains a log of all the operations one after the other in an easy to understand and parse format. You can even easily export an AOF file. For instance even if you've accidentally flushed everything using the [`FLUSHALL`](https://redis.io/commands/flushall) command, as long as no rewrite of the log was performed in the meantime, you can still save your data set just by stopping the server, removing the latest command, and restarting Redis again.

### AOF disadvantages

-   AOF files are usually bigger than the equivalent RDB files for the same dataset.
-   AOF can be slower than RDB depending on the exact fsync policy. In general with fsync set to _every second_ performance is still very high, and with fsync disabled it should be exactly as fast as RDB even under high load. Still RDB is able to provide more guarantees about the maximum latency even in the case of a huge write load.

### Ok, so what should I use?

The general indication you should use both persistence methods is if you want a degree of data safety comparable to what PostgreSQL can provide you.

If you care a lot about your data, but still can live with a few minutes of data loss in case of disasters, you can simply use RDB alone.

There are many users using AOF alone, but we discourage it since to have an RDB snapshot from time to time is a great idea for doing database backups, for faster restarts, and in the event of bugs in the AOF engine.


https://redis.io/docs/manual/programmability/eval-intro/
## Scripting with Lua
Redis lets users upload and execute Lua scripts on the server. Scripts can employ programmatic control structures and use most of the commands while executing to access the database. Because scripts execute in the server, reading and writing data from scripts is very efficient.

Redis guarantees the script's atomic execution. While executing the script, all server activities are blocked during its entire runtime. These semantics mean that all of the script's effects either have yet to happen or had already happened.

Scripting offers several properties that can be valuable in many cases. These include:

Providing locality by executing logic where data lives. Data locality reduces overall latency and saves networking resources.
Blocking semantics that ensure the script's atomic execution.
Enabling the composition of simple capabilities that are either missing from Redis or are too niche to a part of it.
Lua lets you run part of your application logic inside Redis. Such scripts can perform conditional updates across multiple keys, possibly combining several different data types atomically.

Scripts are executed in Redis by an embedded execution engine. Presently, Redis supports a single scripting engine, the Lua 5.1 interpreter. Please refer to the Redis Lua API Reference page for complete documentation.

Although the server executes them, Eval scripts are regarded as a part of the client-side application, which is why they're not named, versioned, or persisted. So all scripts may need to be reloaded by the application at any time if missing (after a server restart, fail-over to a replica, etc.). As of version 7.0, Redis Functions offer an alternative approach to programmability which allow the server itself to be extended with additional programmed logic.


https://redis.io/docs/manual/scaling/
## Escalabilidad
Redis scales horizontally with a deployment topology called Redis Cluster. Redis Cluster provides a way to run a Redis installation where data is **automatically sharded across multiple Redis nodes**.

Redis Cluster also provides **some degree of availability during partitions**, that is in practical terms the ability to continue the operations when some nodes fail or are not able to communicate. However the cluster stops to operate in the event of larger failures (for example when the majority of masters are unavailable).

So in practical terms, what do you get with Redis Cluster?

-   The ability to **automatically split your dataset among multiple nodes**.
-   The ability to **continue operations when a subset of the nodes are experiencing failures** or are unable to communicate with the rest of the cluster.

### Redis Cluster data sharding
Redis Cluster does not use consistent hashing, but a different form of sharding where every key is conceptually part of what we call a **hash slot**.

There are 16384 hash slots in Redis Cluster, and to compute the hash slot for a given key, we simply take the CRC16 of the key modulo 16384.

Every node in a Redis Cluster is responsible for a subset of the hash slots, so, for example, you may have a cluster with 3 nodes, where:

-   Node A contains hash slots from 0 to 5500.
-   Node B contains hash slots from 5501 to 11000.
-   Node C contains hash slots from 11001 to 16383.

This makes it easy to add and remove cluster nodes. For example, if I want to add a new node D, I need to move some hash slots from nodes A, B, C to D. Similarly, if I want to remove node A from the cluster, I can just move the hash slots served by A to B and C. Once node A is empty, I can remove it from the cluster completely.

Moving hash slots from a node to another does not require stopping any operations; therefore, adding and removing nodes, or changing the percentage of hash slots held by a node, requires no downtime.

Redis Cluster supports multiple key operations as long as all of the keys involved in a single command execution (or whole transaction, or Lua script execution) belong to the same hash slot. The user can force multiple keys to be part of the same hash slot by using a feature called _hash tags_.

Hash tags are documented in the Redis Cluster specification, but the gist is that if there is a substring between {} brackets in a key, only what is inside the string is hashed. For example, the keys `user:{123}:profile` and `user:{123}:account` are guaranteed to be in the same hash slot because they share the same hash tag. As a result, you can operate on these two keys in the same multi-key operation.

### Redis Cluster master-replica model
To remain available when a subset of master nodes are failing or are not able to communicate with the majority of nodes, Redis Cluster uses a master-replica model where every hash slot has from 1 (the master itself) to N replicas (N-1 additional replica nodes).

In our example cluster with nodes A, B, C, if node B fails the cluster is not able to continue, since we no longer have a way to serve hash slots in the range 5501-11000.

However, when the cluster is created (or at a later time), we add a replica node to every master, so that the final cluster is composed of A, B, C that are master nodes, and A1, B1, C1 that are replica nodes. This way, the system can continue if node B fails.

Node B1 replicates B, and B fails, the cluster will promote node B1 as the new master and will continue to operate correctly.

However, note that if nodes B and B1 fail at the same time, Redis Cluster will not be able to continue to operate.

### Redis Cluster consistency guarantees
Redis Cluster does not guarantee **strong consistency**. In practical terms this means that under certain conditions it is possible that Redis Cluster will lose writes that were acknowledged by the system to the client.

The first reason why Redis Cluster can lose writes is because it uses asynchronous replication. This means that during writes the following happens:

-   Your client writes to the master B.
-   The master B replies OK to your client.
-   The master B propagates the write to its replicas B1, B2 and B3.

As you can see, B does not wait for an acknowledgement from B1, B2, B3 before replying to the client, since this would be a prohibitive latency penalty for Redis, so if your client writes something, B acknowledges the write, but crashes before being able to send the write to its replicas, one of the replicas (that did not receive the write) can be promoted to master, losing the write forever.

This is **very similar to what happens** with most databases that are configured to flush data to disk every second, so it is a scenario you are already able to reason about because of past experiences with traditional database systems not involving distributed systems. Similarly you can improve consistency by forcing the database to flush data to disk before replying to the client, but this usually results in prohibitively low performance. That would be the equivalent of synchronous replication in the case of Redis Cluster.

Basically, there is a trade-off to be made between performance and consistency.

Redis Cluster has support for synchronous writes when absolutely needed, implemented via the [`WAIT`](https://redis.io/commands/wait) command. This makes losing writes a lot less likely. However, note that Redis Cluster does not implement strong consistency even when synchronous replication is used: it is always possible, under more complex failure scenarios, that a replica that was not able to receive the write will be elected as master.

There is another notable scenario where Redis Cluster will lose writes, that happens during a network partition where a client is isolated with a minority of instances including at least a master.

Take as an example our 6 nodes cluster composed of A, B, C, A1, B1, C1, with 3 masters and 3 replicas. There is also a client, that we will call Z1.

After a partition occurs, it is possible that in one side of the partition we have A, C, A1, B1, C1, and in the other side we have B and Z1.

Z1 is still able to write to B, which will accept its writes. If the partition heals in a very short time, the cluster will continue normally. However, if the partition lasts enough time for B1 to be promoted to master on the majority side of the partition, the writes that Z1 has sent to B in the meantime will be lost.

Note that there is a **maximum window** to the amount of writes Z1 will be able to send to B: if enough time has elapsed for the majority side of the partition to elect a replica as master, every master node in the minority side will have stopped accepting writes.

This amount of time is a very important configuration directive of Redis Cluster, and is called the **node timeout**.

After node timeout has elapsed, a master node is considered to be failing, and can be replaced by one of its replicas. Similarly, after node timeout has elapsed without a master node to be able to sense the majority of the other master nodes, it enters an error state and stops accepting writes.
