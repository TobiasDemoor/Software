New Technology File System está diseñado para cumplir con los requisitos de gama alta para estaciones de trabajo y servidores, tales como aplicaciones de cliente/servidor, servidores de bases de datos, etc.

#### Características clave
- *Recuperabilidad.* Posee una gran capacidad para recuperarse de crasheos del sistema y fallos en el disco. Cuando suceden estos eventos, NTFS es capaz de reconstruir volúmenes de disco y devolverlos a un estado consistente. Esto lo realiza usando un modelo de proceso-transacción para cambios en el FS. Cada cambio significativo es tratado como una acción atómica que se realiza en su totalidad o no se realiza en absoluto. Cada transacción que se encontraba en un proceso a la hora del error, es posteriormente retirada o llevada a cabo. Además, mantiene una copia del sistema de archivo a modo de back up.

- *[[Seguridad]].*NTFS utiliza el modelo de objetos de Windows para reforzar la seguridad. Un archivo abierto es implementado como un objeto archivo con un descriptor de seguridad que define sus atributos de seguridad. Este descriptor es almacenado como un atributo de cada archivo en disco.
- *Tamaños máximos soportados.* NTFS soporta tamaños muy grandes de discos de almacenamiento de una manera más eficiente que otros FS tales como FAT.

- *Múltiples flujos de datos. NTFS* trata los contenidos de un archivo como flujos de bytes (No estructurados). De esta forma, es posible definir múltiples flujos de datos para un mismo archivo.

- *Información mantenida.* NTFS almacena un log de todos los datos realizados sobre un archivo en los volúmenes. Los programas pueden leer esta información para identificar cuáles archivos han sido modificados.

- *Compresión y encriptado.* Los directorios y archivos pueden ser comprimidos de una forma transparente o encriptados en su totalidad.

- *Hard and symbolic links. NTFS* soporta hard links, que permite que un archivo sea accesible desde múltiples rutas en el mismo volumen. Además, soporta links simbólicos, lo que permite además acceder a archivos o directorios que se encuentran en otro volumen. Además, Windows soporta puntos de montaje, lo cual permite que un mismo volumen fijo sea dividido en múltiples volúmenes virtuales tratados de manera independiente.

#### Volumen y estructura de archivos
NTFS utiliza los siguientes conceptos de almacenamiento en un disco:
- *Sector.* Unidad física mínima de almacenamiento en un disco. 
- *Clúster.* Uno o más sectores contiguos entre sí en un disco. Es la unidad fundamental de almacenamiento en NTFS, dado que éste no reconoce sectores para la lectura y escritura de datos. Al definir un clúster como una cantidad fija de sectores, el sistema de archivos se independiza del tamaño de sector de la unidad física de almacenamiento.
- *Volumen.* Partición lógica en un disco, que consiste en uno o más clústeres y es usada por el FS para alojar espacio. El volumen consiste en información del FS, una colección de archivos y espacio libre para almacenar archivos nuevos. Un volumen puede ser una partición de un solo disco o extenderse en múltiples discos.

#### Estructura de un volumen NTFS
Cada elemento en un volumen es un archivo, y cada archivo consiste en una colección de atributos. Incluso los datos de un archivo son tratados como un atributo del mismo.

##### *Boot sector*
Se encuentra en las regiones iniciales del volumen. Contiene información acerca del diseño del volumen y la estructura del FS y el código e información necesaria para el inicio del sistema.

##### *Master file table (MFT)*
Contiene información acerca de todos los archivos y directorios. Consiste en una lista de todos los archivos y sus atributos.

- Habrá una file o record (entrada en la tabla) por cada archivo que exista en el sistema de archivos.
- Ahora bien, el concepto de archivo es bastante amplio: toda entidad almacenada individualmente es un archivo. La propia MFT es considerada un archivo y tiene su propia entrada en la MFT.
- Las primeras 16 entradas de la MFT están reservadas para almacenar archivos del sistema, es decir, información sobre el propio sistema de archivos. El resto de entradas se corresponden con los archivos y carpetas de datos.

##### *System files*
- **MFT2.** Copia de las primeras filas de la tabla de archivos, usada para garantizar acceso al volumen en caso de que se corrompa el sector donde se almacena la MFT.
- **Log file.** Lista de pasos de transacciones usadas por NTFS para restauraciones.
- **Cluster bit map.** Representación del espacio en el volumen, que indica cuáles clústers de datos están en uso y cuáles no.
- **Tabla de definición de atributos.** Define los tipos de atributos soportados en volumen e indica si pueden ser indexados y si pueden ser recuperados en una operación de recuperación del sistema.


