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


https://redis.io/docs/manual/persistence/#snapshotting

https://aashikahamed.medium.com/a-beginner-guide-to-redis-clustering-f34df275ac61

https://redis.io/docs/manual/programmability/eval-intro/
