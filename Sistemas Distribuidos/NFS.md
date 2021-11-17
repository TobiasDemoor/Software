El **Network File System** de Sun Microsystem es un [[Sistemas de archivos distribuidos|sistema de archivos distribuido]] usado ampliamente en los sistemas basados en UNIX. Este sistema de archivos se encuentra basado en la arquitectura cliente servidor.

La idea básica detrás del NFS es que cada servidor de archivos proporcione una visión estandarizada de su sistema de archivo local. En otros términos, no importa cómo se implemente el sistema de archivo local, cada servidor NFS soporta el mismo modelo. Este método también ha sido adoptado por otros sistemas de archivo. El NFS cuenta con un protocolo de comunicación que permite a los clientes acceder a archivos guardados en un servidor; por tanto, es posible que un conjunto heterogéneo de procesos, quizá ejecutándose con sistemas operativos y máquinas diferentes, compartan un sistema de archivo común.

El NFS ha sido implementado para un gran número de sistemas operativos, aunque predominan las versiones basadas en UNIX. Para virtualmente todos los sistemas UNIX modernos, el NFS generalmente se implementa siguiendo la arquitectura en capas mostrada a continuación.

![[RRCC_nfs_arquitectura_basica.png]]

Un cliente accede al sistema de archivo usando las invocaciones a sistema provistas por su sistema operativo local. Sin embargo, la interfaz del sistema de archivo UNIX es reemplazada poruna interfaz para comunicarse con el **sistema de archivo virtual (VFS)** el cual por ahora es efectivamente el estándar para comunicarse con sistemas de archivo distribuidos diferentes. Virtualmente todos los [[sistemas operativos]] modernos proporcionan un VFS, y de no ser así los desarrolladores se ven obligados a reimplementar un sistema operativo enorme cuando adoptan una nueva estructura de sistema de archivo. Con el NFS, las operaciones de interfaz se transfieren o a un sistema de archivo local o a otro componente conocido como **cliente NFS**, el cual se encarga de manejar el acceso a los archivos guardados en un servidor remoto. En el NFS, toda la comunicación entre cliente y servidor se realiza mediante [[RPC]].

Del lado del servidor, la organización es similar. El **servidor NFS** se encarga de manejar las solicitudes de clientes. El resguardo de RPC desempaqueta las solicitudes y el servidor NFS las transforma en operaciones con archivos VFS regulares que posteriormente se transfieren a la capa VFS

### RPC en NFS
En NFS toda la comunicación entre un cliente y el servidor ocurre a lo largo de un protocolo **RPC de computación de red abierta (ONC [[RPC]])**.

Cada operación NFS puede ser implementada como una llamada a un procedimiento remoto única realizada a un servidor de archivos. En realidad, hasta el NFSv4, el cliente era responsable de hacer la vida del servidor tan fácil como fuera posible manteniendo las solicitudes relativamente simples. Por ejemplo, para leer datos de un archivo por primera vez, un cliente normalmente debía buscar el manejador del archivo con una operación *lookup*, después de lo cual podía emitir una solicitud *read*.

Este método requería dos RPC sucesivas. La desventaja fue evidente cuando se consideró el uso del NFS en un sistema de área amplia. En ese caso, la latencia extra de una segunda RPC degradó el desempeño. Para evitar esos problemas, el NFSv4 soporta **procedimientos compuestos** mediante los cuales varias RPC pueden agruparse en una sola solicitud.

### Asignación de nombres
La idea fundamental que constituye la base del modelo de asignación de nombres NFS es proporcionar a los clientes un acceso completamente transparente a un sistema de archivo remoto mantenido por un servidor. Esta transparencia se logra permitiendo que el cliente sea capaz de montar un sistema de archivo remoto en su propio sistema de archivo local.

![[RRCC_nfs_montaje.png]]

En lugar de montar todo un sistema de archivo, el NFS permite que los clientes monten sólo una parte. Se dice que un servidor **exporta** un directorio cuando pone a éste y a sus entradas a disposición de sus clientes. Un directorio exportado puede montarse en el espacio de nombre local del cliente.

Este método de diseño tiene una seria implicación: en principio, los usuarios no comparten espacios de nombre. Un nombre de archivo depende, por consiguiente, de cómo organizan los clientes su propio espacio de nombre local, y en dónde se monten los directorios exportados. La desventaja de usar este método en un sistema de archivo distribuido es que compartir archivos se vuelve mucho más difícil. Por ejemplo, Alicia no puede contarle a Bob acerca de un archivo utilizando el nombre que ella le asignó a dicho archivo, ya que ese nombre puede tener un significado enteramente distinto en el espacio de nombre de los archivos de Bob.

Un servidor NFS, por sí mismo, puede montar directorios exportados por otros servidores. Sin embargo, no se permite que los exporte a sus propios clientes. En cambio, un cliente tendrá que montarlos explícitamente del servidor que los contiene. Esta restricción se deriva en parte de la simplicidad. Si un servidor pudiera exportar un directorio montado desde otro servidor, tendría que regresar manejadores de archivo especiales que incluyan un identificador para un servidor. El NFS no soporta esa clase de manejadores de archivo.

![[RRCC_nfs_montaje_anidado.png]]