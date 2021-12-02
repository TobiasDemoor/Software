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
- Utiliza una variación de la asignación vinculada que evita el acceso secuencial a la cadena de bloques de índices.
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