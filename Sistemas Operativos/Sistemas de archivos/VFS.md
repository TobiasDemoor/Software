Es una capa virtual que sirve de capa de [[abstracción]] del [[Sistemas de archivos|sistema de archivo]] real. Esta capa es la que utiliza el usuario para acceder al sistema de archivo real. Esta capa permite controlar y/o manejar de la misma manera un sistema de archivo local como un sistema de archivo de red. El primer mecanismo de sistema de archivo virtual en un sistema [[UNIX]] fue introducido en el SunOS de 1985. Esto permitía acceder a su sistema de archivo local llamado UFS como acceder a sistemas remotos [[NFS]] de forma transparente.

Podría decirse que el servicio más importante que la capa VFS ofrece es una caché de datos I/O uniforme. Linux mantiene cuatro cachés de datos de I/O: page cache, inode cache, buffer cache y directory cache. El page cache combina datos de la memoria y archivos virtuales. El buffer cache es una interfaz con el dispositivo de bloques y cachea los meta-datos de discos de bloques. El inode cache mantiene el acceso reciente a los inodos de archivo. El directory cache (d-cache) mantiene en la memoria de un árbol que representa una parte de la estructura de directorios del sistema de archivos. 

La estructura de VFS de Linux se parece a la estructura de ext2.

### VFS Superblock
Todo sistema de archivo montado está representado por el VFS superblock. El VFS contiene:

- Device: este es el identificador de dispositivo. Por ejemplo, ‘/dev/sda1’.
- Inode pointers: apunta al primer inode del sistema de archivo. El puntero de inode cubierto representa al inode del directorio donde está montado dentro del sistema. Si es el root file system no tiene puntero cubierto (covered pointer).
- Blocksize: es el tamaño de bloque en el sistema de archivo.
- Superblock operations: apunta a el grupo de rutinas del superbloque. Entre otras cosas estas rutinas son las que permite la lectura y escritura de inodos y superbloques.
- File system type: es el puntero a los datos de estructura del tipo de sistema de archivo.
- File system specific: es el puntero a la información necesaria para este sistema de archivos.

### VFS Inode
Como el sistema de archivos ext2, todo archivo, directorio y otro es representado por algún VFS inode. La información de cada inode VFS es construida desde la información extraída del sistema de archivo mediante rutinas específicas. Cada VFS inode existe solo en memoria del sistema y es mantenida dentro del inode cache. VFS inode contiene los siguientes datos:

- Device: es el identificador de dispositivo donde se encuentra el inode real.
- Inode number: Es un número único de inode dentro del sistema de archivo. Es una combinación entre el dispositivo y el número de inode.
- Mode: como el ext2 este campo describe los permisos al inode.
- Times: de creación, modificación y de escritura.
- Blocksize: tamaño de bloques.
- Inode operations: es un puntero a las direcciones de los procedimientos de inode.
- Count: es el número de componentes de sistema que están usando este inode. Cuando la suma llega a cero puede ser descartado o reusado.
- Lock: este campo es usado cuando el inode es lockeado cuando es usado por el sistema.
- Dirty: indica si el inode VFS ha sido escrito y el sistema de archivo por debajo necesita modificado.

### Registro de sistema de archivos
En Linux todo nuevo sistema de archivo debe ser registrado. Los sistemas de archivos pueden ser creados como módulos y cargados bajo demanda. Cuando son cargados el kernel registra el sistema de archivo. Uno puede ver si el archivo está registrado haciendo un cat al archivo /proc/filesystems.