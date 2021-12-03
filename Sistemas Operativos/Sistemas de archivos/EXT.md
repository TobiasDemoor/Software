El superbloque tiene información del sistema de archivos en conjunto, como su tamaño (la información precisa aquí depende del sistema de archivos). Un nodo-i tiene toda la información de un archivo, salvo su nombre. El nombre se almacena en el directorio, junto con el número de nodo-i. Una entrada de directorio consiste en un nombre de archivo y el número de nodo-i que representa el archivo.

El nodo-i contiene los números de varios bloques de datos, que se utilizan para almacenar los datos en el archivo. Sólo hay espacio para unos pocos números de **bloques de datos** en el nodo-i; en cualquier caso, si se necesitan más, se colocan más espacios para punteros a los bloques de forma dinámica. Estos bloques colocados dinámicamente son **bloques indirectos**; el nombre indica que, para encontrar el bloque de datos, primero hay que encontrar su número en un bloque indirecto.

- **Superblock:**  contiene toda la información de la configuración del sistema de archivo. Contiene información del total de nodos-i (inodos) y bloques del sistema de archivos y cuántos están libres, cuándo fue montado, etc.
- **Inode:** cada archivo está representado por una estructura llamado un inode. Cada inode contiene la descripción del fichero, tipo de archivo, los derechos de acceso, marcas de tiempo, el tamaño y los punteros a los bloques de datos. El **bloque de indirección** es un inode que se usa para apuntar a otros inodos cuando la cantidad de inodos se acaba.
- **Directorios:** los directorios se estructuran en un árbol jerárquico. Cada directorio puede contener archivos o directorios. Los directorios son un tipo especial de archivos.
- **Enlaces:** los sistemas de archivos UNIX implementan el concepto de enlace. Varios nombres se pueden asociar con un inode. El inode contiene un campo que contiene el número asociado con el archivo.
- **Archivos especiales de dispositivo:** en los sistemas operativos tipo UNIX, los dispositivos pueden acceder a través de ficheros especiales. Un archivo especial de dispositivo no utiliza ningún espacio en el sistema de ficheros. Es sólo un punto de acceso al controlador de dispositivo. (Existen dos tipos de archivos especiales: character/block special files. La primera permite operaciones I/O en modo caracteres mientras que el segundo requiere datos a escribir en modo bloque a través de las funciones de caché del buffer. Cuando una solicitud de I/O se realiza en un archivo especial, se envía a un (pseudo) controlador de dispositivo. Un archivo especial hace referencia a un número importante, que identifica el tipo de dispositivo y un número que identifica la unidad.

#### Tipos de archivos
*Regular u ordinario.* Contiene datos arbitrarios en cero o más bloques de datos. Contienen información introducida por un usuario, una aplicación de usuario o de utilidad del sistema.

*Directorio.* Contiene una lista de nombres y punteros a inodos asociados. Poseen una organización jerárquica. Cada directorio puede contener otro directorio y archivos. Los directorios son archivos tratados de una manera especial y que poseen privilegios de protección de escritura, donde solo el FS puede escribir en él, pero los accesos de lectura están permitidos para los programas de usuario. Este archivo solo contiene una lista de punteros a inodos y nombres de archivos. Esto nos indica que un mismo inodo puede contener uno o más nombres, dependiendo del directorio en el que se encuentra.

*Especiales.* No contienen datos, pero proveen un mecanismo para mapear dispositivos físicos a nombres de archivos. Estos nombres de archivo son usados para acceder a dispositivos periféricos, tales como terminales e impresoras. Cada dispositivo de E/S está asociado a un archivo especial.

*Named pipes.* Archivos que funcionan como búfer de datos de entrada para que un proceso pueda leer dichos datos desde la salida del “canal”.

*Links.* Nombre de archivo alternativo para un archivo ya existente.

*Links simbólicos.* Archivo de datos que contiene el nombre del archivo al cual está linkeado.

#### Inodos
Un inodo es una estructura de control que contienen información clave requerida por el sistema operativo para un archivo particular. Unix almacena los nombres de los archivos fuera de estos inodos, de forma que varios nombres pueden referenciar al mismo inodo, pero un archivo está asociado a un solo inodo.
##### *Principales atributos:*
- Tipo y modo de acceso del archivo.
- Dueño del archivo e identificador de grupo de acceso.
- Timestamp de creación y última modificación.
- Tamaño en bytes
- Secuencia de punteros a bloques
- Número de bloques físicos utilizados por el archivo, incluyendo bloques indirectos.
- Número de entradas de directorio que referencian al archivo.
- Flags que describen características del archivo.

#### Asignación de archivos
- Utiliza una variación de la asignación vinculada que evita el acceso secuencial a la cadena de bloques de [[índice|índices]].
  - *Bloques de índices de 1er nivel* (contienen punteros directos a bloques de datos)
  - *Bloques de índices de 2do nivel* (contienen punteros a bloques de índices que, a su vez, contienen punteros directos a bloques de datos).
  - *Bloques de índices de 3er nivel….*
  - *Bloques de datos (información propiamente dicha).*
- Los bloques de índices de 2do y 3er nivel disminuyen exponencialmente el tiempo de acceso a un bloque de datos, al no tener que recorrer secuencialmente como en la indexada pura (que puede ser una cadena muy larga en archivos grandes).
- No hay fragmentación externa.
- El acceso es pseudo-directo, pero mucho más rápido: secuencial a los bloques de índices (a lo sumo 3 accesos a bloques de índices y uno a bloques de datos).
- La tabla de asignación de archivos contiene una estructura de acceso para cada archivo denominada i-nodo que contiene 13 punteros:
  - *10 punteros a bloques de datos.* Cada puntero señala a un bloque de datos puros y garantiza que el acceso a los primeros bloques de datos del archivo sea directo. Si un archivo tuviera un solo registro, sería un desperdicio indexar ese único registro.
  - *1 puntero a bloque de índices de 1er nivel.*
  - *1 puntero a bloque de índices de 2er nivel.*
  - *1 puntero a bloque de índices de 3er nivel.*

#### Estructura del volumen
*Bloque de booteo.* Contiene código requerido para iniciar el sistema operativo.

*Super bloque.* Contiene atributos e información acerca del file system, como el tamaño de partición y el tamaño de la tabla de inodos.

*Tabla de inodos de cada archivo.*

*Bloques de datos.*