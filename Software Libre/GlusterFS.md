Guster es un tipo de [[Network-attached storage|NAS]] que se puede implementar en hardware estándar. 

El [[Sistemas de archivos distribuidos|sistema de archivos distribuidos]] Gluster incluye recursos de procesamiento, almacenamiento y entrada/salida agrupados en un espacio de nombres. Cada server con su almacenamiento se considera “un nodo”. La capacidad se puede escalar agregando nodos adicionales o almacenamiento adicional a cada nodo. La performance se aumenta distribuyendo el almacenamiento entre nodos. La disponibilidad se obtiene replicando el contenido de datos entre nodos.

GlusterFS tiene un componente de cliente y servidor. Los servidores normalmente se implementan como **bricks** (ladrillos) de almacenamiento, y cada servidor ejecuta un daemon glusterfsd para exportar un sistema de archivos local como un volumen. El proceso de cliente glusterfs, que se conecta a servidores con un protocolo personalizado a través de TCP/IP, InfiniBand o Sockets Direct Protocol, crea volúmenes virtuales compuestos desde múltiples servidores remotos utilizando **translators** apilables.

El translator indica cómo se implementa el almacenamiento en los bricks de servidores. Deciden cómo se mandan los archivos a los servidores. La mayoría de la funcionalidad de gluster se implementa en ellos, esta incluye: mirroring, [[Replicación|replicación]], stripping basado en archivos, balanceo de carga basado en archivos, tolerancia a fallos, quotas, etc

![[GlusterFS.png]]

GlusterFS es un sistema de archivos [[FUSE]]. Esta opción se tomó para evitar usar módulos en el kernel de [[Linux]].

### Show me the code
```sh
# instalar un servidor gluster
$ apt install glusterfs-server
$ systemctl start glusterd
$ systemctl status glusterdroot

# iniciar el cluster
$ gluster peer probe <nodo>
$ gluster peer status
# siendo debian1, debian2 y debian3 las direcciones de los servers y habiendo creado un directorio /mnt/brick1/gv0 en cada una
$ gluster volume create gv0 replica 3 debian1:/mnt/brick1/gv0 debian2:/mnt/brick1/gv0 debian3:/mnt/brick1/gv0
# ahí creamos un volumen con 3 bricks (servers) y usamos la lógica translator de replicación (replica)

# iniciar el volumen
$ gluster volume start gv0
$ gluster volume info
```

En este ejemplo usamos el Automatic File Replication (AFR). AFR es el módulo (translator) en glusterfs que provee todas las features que uno esperaría de cualquier sistema de [[Replicación|replicación]] sincrónica:
1. Actualización simultanea de todas las copias de información en los bricks replica cuando el cliente los modifica.
2. Provee disponibilidad continua a los clientes cuando, por ejemplo, un brick de la replica se cae (siempre que haya por lo menos dos para que exista concenso).
3. Reparación automática de cualquier información que fue modificada mientras que el brick estaba caido, una vez que vuelve a correr, asegurando consistencia de información en todos los bricks de la replica.

### Bibliografía
[Documentación de Gluster](https://docs.gluster.org/en/latest)