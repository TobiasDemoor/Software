El servicio de transporte se implementa mediante un **protocolo de transporte** entre las dos entidades de transporte. En ciertos aspectos, los protocolos de transporte se parecen a los protocolos de enlace de datos, ambos se encargan del control de errores, la secuenciación y el control de flujo, entre otros aspectos.

Sin embargo, existen diferencias considerables entre los dos, las cuales se deben a disimilitudes importantes entre los entornos en que operan ambos protocolos. En la capa de enlace de datos, dos enrutadores se comunican de forma directa mediante un canal físico, ya sea cableado o inalámbrico, mientras que, en la capa de transporte, ese canal físico se sustituye por la red completa. Esta diferencia tiene muchas implicaciones importantes para los protocolos.

![[entorno_protocolos_de_transporte.png]]

### Direccionamiento
Cuando un proceso de aplicación (por ejemplo, un usuario) desea establecer una conexión con un proceso de aplicación remoto, debe especificar a cuál se conectará. El método que se emplea por lo general es definir direcciones de transporte en las que los procesos puedan escuchar las solicitudes de conexión. En Internet, estos puntos terminales se denominan **puertos**. Usaremos el término genérico **TSAP (Transport Service Access Point)** para indicar un endpoint específico en la capa de transporte. Así mismo, los puntos terminales análogos en la capa de red (es decir, direcciones de capa de red) se llamen **NSAP (Network Service Access Point)**. Las [[direcciones IP]] son ejemplos de NSAP.

Los procesos de aplicación, tanto clientes como servidores, se pueden enlazar por sí mismos a un TSAP para establecer una conexión a un TSAP remoto. Estas conexiones se realizan a través de puntos NSAP en cada host, como se muestra. El propósito de tener puntos TSAP es que, en algunas redes, cada computadora tiene un solo NSAP, por lo que se necesita alguna forma de diferenciar los múltiples puntos terminales de transporte que comparten ese punto NSAP.

![[direccionamiento_tsap_nsap.png]]

### Establecimiento de una conexión
El proceso de establecer una conexión suena fácil, pero en realidad es sorprendentemente complicado. A primera vista parecería suficiente con que una entidad de transporte enviara tan sólo un segmento CONNECTION REQUEST al destino y esperara una respuesta CONNECTION ACCEPTED. El problema ocurre cuando la red puede perder, retrasar, corromper y duplicar paquetes. Este comportamiento causa complicaciones serias.

Imagine una red que está tan congestionada que las confirmaciones de recepción casi nunca regresan a tiempo, y cada paquete expira y se retransmite dos o tres veces. Suponga que la red usa datagramas en su interior y que cada paquete sigue una ruta diferente. Algunos de los paquetes podrían atorarse en un congestionamiento de tráfico dentro de la red y tardar mucho tiempo en llegar. Es decir, se pueden retardar en la red y reaparecer mucho después, cuando el emisor piense que se han perdido.