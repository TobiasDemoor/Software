Un **sistema de archivos** es un elemento que controla cómo se almacenan y recuperan los datos. Este comunmente es una parte central de un [[Sistemas Operativos|sistema operativo]].

## Archivo
Es la unidad de representación de la información en un sistema de computación. Es el medio para concretar la persistencia de la información (permite el guardado y recuperación de la información no volátil).

Cada archivo es tratado como una entidad única y es identificado por un nombre o File-ID unívoco.

Toda información almacenada tiene forma de archivo. Es un conjunto de bits o bien un conjunto de registros homogéneos (compuestos por campos).

## **Sistema de gestión de Archivos**
El sistema de gestión de archivos es un módulo del sistema operativo y permite que un usuario o proceso pueda acceder a los archivos y manipularlos. Brinda una interfaz que evita que el programador tenga que desarrollar software específico para interactuar con sus archivos. Garantiza la corrección de los datos y la estructura de los archivos.

Ofrece un conjunto estándar de rutinas de interfaz y operaciones de E/S. Es decir, es el sistema de archivos el que decide qué operaciones puede realizar un usuario o proceso sobre un archivo. 

Debe garantizar el rendimiento de las operaciones sobre archivos.

#### Independencia lógica del dispositivo	
El sistema de gestión de archivos ofrece soporte de E/S para los diversos dispositivos del sistema de computación, garantizando la transparencia de su arquitectura (Independencia Lógica del Dispositivo). Esto quiere decir que el file system se abstrae de la arquitectura física del dispositivo donde se almacenarán los archivos. Para ello, el driver, que dialoga con el controlador, debe conocer de qué manera es almacenada la información. Por otro lado, el usuario o proceso no tiene por qué conocer la arquitectura física del dispositivo de almacenamiento.

El sistema de gestión de archivos asume a los dispositivos como un conjunto de bloques.	

#### Funciones de un sistema de gestión de archivos
1. *Identificar y ubicar un archivo en cuestión.* Para ello, utiliza un directorio que describe la ubicación de todos los archivos y sus atributos.
1. *Aplicar el control de acceso a los usuarios (Protección).* Gestionar los privilegios de usuario sobre un archivo.
1. ` `*Asignar los archivos a los bloques disponibles.* Decide físicamente dónde se van a ubicar los archivos dentro del dispositivo de almacenamiento.
1. *Gestionar el espacio libre, de manera que se conozca qué bloques están disponibles.*


## **File System**
En **sentido amplio**, es el conjunto de convenciones de diseño que determinan el manejo de la información en un SO. Estas convenciones se establecen en tiempo de diseño del producto, luego se implementan y rigen la vida de los usuarios del SO en lo que respecta al manejo de la información.

Cuando hablamos de “*el File System de Linux…”*  nos referimos al File System de un SO en **sentido amplio.**
**

**
En **sentido estricto,** es el conjunto de información, estructurada bajo determinadas pautas, en un sistema de computación. Es decir, es una **instancia.** Es el conjunto de información de cada sistema de computación.

Cuando hablamos de “*el File System de mi PC…”* nos estamos refiriendo al file system de un SO en sentido estricto.



Dos sistemas de computación con el mismo SO tienen iguales FS en sentido amplio, pero diferentes en sentido estricto, dado que la información propiamente dicha que manejan es diferente, pero en ambos casos respetan las mismas convenciones de diseño al tener el mismo sistema operativo.


#### Convenciones de diseño
Son las reglas o pautas para la manipulación de información que el sistema de gestión de archivos implementará y el usuario respetará. Refieren a:

- Nombrado.
- Estructura de archivos.
- Estructura de directorios.
- Tipos.
- Modo de acceso.
- Métodos de asignación de archivos.
- Estructuras para la gestión del espacio libre.
- Criterios de selección del espacio libre.
- Atributos.
- Operaciones.
- Organización lógica.

##### *Reglas de naming (nombrado)*
Establecen las pautas para la identificación de los archivos (nombre). Se deben tener en cuenta las siguientes situaciones:

- Cantidad de caracteres para el nombre.
- Cantidad de caracteres para extensión.
- Cantidad de caracteres no permitidos. Uso de caracteres especiales, espacios y puntos.
- Cantidad de puntos.
- ¿Extensión obligatoria u opcional?
- ¿Case sensitive?
- Asociación de aplicaciones a extensiones.

En Linux, las extensiones de archivo son sólo convenciones y no son impuestas por el sistema operativo, es decir, forman parte del nombre en sí. Un archivo llamado archivo.txt podría ser algún tipo de archivo de texto, pero ese nombre es más un recordatorio para el propietario que un medio para transportar información a la computadora. Si puede darse que una aplicación solo pueda trabajar con archivos que tengan extensión; por ejemplo, un compilador de C podría insistir que los archivos que va a compilar terminen con .c y podría rehusarse a compilarlos si no tienen esa terminación. 

Por el contrario, Windows hace uso consciente de las extensiones y les asigna un significado. Los usuarios (o procesos) pueden registrar extensiones con el sistema operativo y puede asignar programas a esas extensiones. Cuando un usuario hace doble clic sobre un nombre de archivo, el programa asignado a su extensión de archivo se inicia con el archivo como parámetro.

##### *Estructura de archivos*
- *No estructurados*. Una secuencia de bytes sin lógica alguna.
- *Estructurados simples.*
  - *Líneas*. Cada línea es una secuencia de bytes, unidad de lectura/escritura.
  - *Registros longitud fija*. Cierta estructura dentro de cada línea o registro de longitud fija.
  - *Registros longitud variable.*
- *Estructurados complejos.* Estructura homogénea definida por el usuario/programador.

Un **campo** es el elemento básico de datos. Un campo individual contiene un valor en particular, como la edad de una persona.

Un **registro** es un conjunto de campos relacionados que pueden ser tratados como una unidad por alguna aplicación. Por ejemplo, los datos de un empleado en particular.

Un **archivo** es una colección de registros similares. Es tratado como una entidad singular por los programas y los usuarios y son referenciados por un nombre.

Un **bloque** es la unidad mínima de lectura-escritura de la información en un dispositivo de almacenamiento. Está formado por una serie de campos.



##### *Tipos de archivos*
- *Texto.* Cadenas de caracteres sin estructura alguna.
- *Datos (registros).* Tienen una estructura de registros que permite almacenar la información.
- *Ejecutables.* Archivos que permiten iniciar la ejecución de un proceso.




##### *Atributos de archivos – Metadatos*
Los atributos de los archivos son tan persistentes como los archivos a los cuales pertenecen, al contrario de los atributos de un proceso, los cuales son volátiles por su naturaleza.

*Principales atributos:* 

- *Nombre*
- *Identificador*
- *Tipo (en caso de que el SO los soporte)*
- *Puntero a ubicación*
- *Tamaño*
- *Tiempo de última modificación*
- *Timestamp de creación*
- *Tiempo de último acceso*
- *Tamaño máximo*
- *Propietario*
- *Protección.* Mecanismo para discriminar el acceso a lectura, escritura o ejecución.

##### *Operaciones sobre archivos*
El archivo, para el SO, es un tipo de dato abstracto. Todas estas operaciones son instrucciones privilegiadas, es decir, cuando en un programa se posee una instrucción que manipula un archivo, debe realizarla mediante un system call.

- *Create*. El archivo se crea sin datos. El propósito de la llamada es anunciar la llegada del archivo y establecer algunos de sus atributos.
- *Read.* Los datos se leen del archivo. Por lo general, los bytes provienen de la posición actual. El invocador debe especificar cuántos datos se necesitan y también debe proporcionar un búfer para colocarlos.
- *Write.* Los datos se escriben en el archivo otra vez, por lo general en la posición actual. Si la posición actual es al final del archivo, aumenta su tamaño. Si la posición actual está en medio del archivo, los datos existentes se sobrescriben y se pierden para siempre.
- *Execute.*
- *Seek.* Reposiciona el apuntador del archivo en una posición específica del archivo.
- *Append.* Esta llamada es una forma restringida de write. Sólo puede agregar datos al final del archivo.
- *Delete.* Cuando el archivo ya no se necesita, se tiene que eliminar para liberar espacio en el disco.
- *Truncate.*
- *Open.* Antes de usar un archivo, un proceso debe abrirlo. El propósito de la llamada a open es permitir que el sistema lleve los atributos y la lista de direcciones de disco a memoria principal para tener un acceso rápido a estos datos en llamadas posteriores.
- *Close.* Cuando terminan todos los accesos, los atributos y las direcciones de disco ya no son necesarias, por lo que el archivo se debe cerrar para liberar espacio en la tabla interna. Muchos sistemas fomentan esto al imponer un número máximo de archivos abiertos en los procesos. Un disco se escribe en bloques y al cerrar un archivo se obliga a escribir el último bloque del archivo, incluso aunque ese bloque no esté lleno todavía.
- *Lock.*
- *Rename.*
- *Set attributes.*
- *Get attributes.*


A su vez, el sistema puede proveer de funciones al usuario que consten de una serie de operaciones de archivos, tales como el copy/paste.

###### Open-file table
`		`Cuando un archivo es abierto por un proceso o usuario, el sistema operativo mantiene en memoria una pequeña tabla de archivos abiertos, que contiene información acerca de todos los archivos que se encuentran abiertos. De esta manera, cuando una operación sobre un archivo abierto es requerida, se accede al mismo mediante esta tabla, sin necesidad de tener que buscar el archivo nuevamente. Cuando un archivo es cerrado, el sistema operativo elimina la entrada del mismo en esta tabla.

`		`En cada entrada se contiene información referida al modo en el cual fue abierto el archivo (create, read only, write, read-write, append-only). 

`		`A su vez, el sistema operativo mantiene dos de estas tablas: una a nivel proceso, que contiene todos los archivos abiertos por un proceso y un puntero a la segunda tabla que es a nivel sistema.

#### Organización lógica de los archivos
Forma en que los archivos son organizados lógicamente por el usuario. Determina la estructura organizativa con la que el usuario dispone los archivos en los dispositivos.

Considera dos tipos de entidades:

- *Directorios*. Carpetas o contenedoras de archivos. Permiten organizar la información contenida dentro de los archivos, de modo que facilite la experiencia de uso del FS.
- *Archivos.*

##### *Directorios de archivos*
El directorio es en sí mismo un archivo que contiene la información administrativa necesaria por el SO, es decir, es un archivo manejado de una manera especial. Permite el mapping entre los nombres de archivo (identificación unívoca de los mismos) y los archivos propiamente dichos.

Contiene la siguiente información de los archivos:

- Atributos.
- Ubicación.
- Propietario.

Cada directorio de usuario es una simple lista de entrada a los archivos del usuario. Puede representarse con un simple archivo secuencial, donde el nombre de cada archivo es su clave unívoca.

Existe un directorio maestro general y uno para cada usuario. El directorio maestro general contiene una entrada para cada directorio maestro de usuario, con su información de acceso (privilegios). **No conoce la organización física de los archivos.**

Existe dos path o direcciones para archivos: relativas al directorio de trabajo y absolutas (relativas al root).
###### Directorio de un solo nivel
Consiste en un único directorio que aloja todos los archivos. Su principal ventaja reside en su facilidad de implementación y la rapidez con la que pueden localizarse archivos en la misma.

###### Directorio tipo árbol
- Existe un directorio maestro (root) que contiene un número determinado de directorios de usuario.
- Cada uno de estos directorios puede tener, a su vez, subdirectorios y archivos como entradas.
- Los archivos son las “hojas” del árbol.
- Cualquier archivo puede ser localizado siguiendo un camino desde el directorio raíz o maestro, descendiendo por varias ramas:
  - *Nombre de camino del archivo (Pathname, dirección absoluta).*
  - *Se pueden tener varios archivos con el mismo nombre, siempre que posean diferente nombre de camino (distinto path).*
- El directorio actual es el directorio de trabajo.
  - Las referencias a los archivos son relativas al directorio de trabajo.

###### Directorio grafo acíclico (evolución de árbol)
- Se trata de un modelo de árbol donde un nodo del mismo archivo puede tener más de un padre.
- A estos nodos se puede llegar por más de un camino, por medio de “atajos” o links que contienen la ruta absoluta del archivo linkeado.
- Se permite que los links vayan solo a archivos, no a directorios, para garantizar que sea acíclico y evitar posibles “islas” (referencias circulares). 
- Desde una carpeta se permite acceder a un archivo que se encuentra en otro directorio.
- *Dos tipos de links:*
  - *Soft link (acceso directo).* El nodo es apuntado por un puntero dentro de la estructura de la tabla de alocación de cada padre, como si fuera un archivo propio. Cuando el archivo es eliminado por alguno de sus padres, es eliminado materialmente, y el link que lo apuntaba desde el otro padre queda apuntando “al vacío”.
  - *Hard link.* El nodo es apuntado por un puntero de la estructura de la tabla de alocación de cada padre, como si fuera un archivo propio. Cuando el archivo apuntado por el hard link es eliminado, se lo deslinkea del padre que lo eliminó, pero sigue existiendo materialmente, por lo que los demás padres seguirán teniendo acceso. Requiere un contador de padres. Cuando el contador de padres llega a cero, entonces se elimina materialmente el archivo.

###### Directorio grafo general
- Permite ciclos. Un directorio puede acceder a un directorio que se encuentra en otra parte del FS. 
- Requiere un Garbage Collector para eliminar todas las estructuras cíclicas que no son alcanzables desde ningún punto del FS.
- La actividad del GC consta de recorrer el dispositivo de almacenamiento marcando los elementos que son alcanzables. Luego, en una segunda recorrida recolecta todo lo que no fue marcado como alcanzable y lo coloca en una lista de espacio libre.
## **Archivos compartidos**
En un sistema multiusuario, existe la necesidad de permitir a los usuarios compartir archivos. Se deben tener en cuenta dos cuestiones: los derechos de acceso y la gestión de los accesos simultáneos.
#### Tipos de acceso
- *Read.*
- *Write.*
- *Execute.*
- *Append.*
- *Delete.*
- *List.* Listar el nombre y los atributos del archivo.
#### Derechos de acceso
Cada archivo tiene un propietario, el cual dispone de todos los derechos de los derechos de acceso y manipulación sobre el archivo. A su vez, puede otorgar derechos a otros utilizando las siguientes clases de usuarios:

- *Usuario específico.* Se requiere una lista que contenga los identificadores de los usuarios a los cuales se les otorga cierto acceso.
- *Grupos de usuarios.*
- *Todos los usuarios (archivos públicos).*

#### Acceso simultáneo a los archivos
El usuario puede:

- *Bloquear el archivo entero cuando lo vaya a actualizar*. Dos procesos no pueden trabajar en simultáneo sobre un mismo archivo.
- *Bloquear el archivo a nivel registros.* Permite que dos o más procesos trabajen sobre un mismo archivo, siempre que no sea sobre los mismos registros.

Al diseñar la posibilidad de accesos compartidos, deben abordarse aspectos de la exclusión mutua e interbloqueo entre procesos (deadlock).

#### Record blocking
En la mayoría de los sistemas los bloques son de longitud fija para simplificar operaciones de E/S, la organización de los mismos y demás. Por otro lado, los registros que se encuentran dentro de cada bloque pueden organizarse de distinta manera:

- *Registros de longitud fija.*  En cada bloque existe una cantidad fija de registros enteros almacenados, lo cual puede resultar en espacio desperdiciado.
- *Registros de longitud variable con encadenamiento.* Se utilizan registros de longitud variable y se permite particionar un registro para almacenarlo en dos bloques consecutivos.
- *Registros de longitud variable sin encadenamiento.* No permite particionar registros. Fragmentación a nivel bloque.
## **Modos de acceso a los archivos**
Métodos que definen el acceso a los bloques de datos de un archivo.
#### Directo
El acceso a un bloque del archivo se hace en forma directa, sin necesidad de haber accedido a los anteriores para lograrlo (técnicas de hashing).

#### Secuencial
El acceso a un bloque del archivo se hace de forma secuencial, requiriendo indefectiblemente haber accedido a los anteriores para lograrlo (n lecturas para leer el bloque n).

#### Indexado
El acceso a un bloque del archivo se hace mediante un puntero en una tabla (archivo) de índices que nos lleva al mismo. Como mínimo, se requiere un acceso al archivo de índices y otro al archivo de datos.

## **Alocación de archivos**
El sistema de gestión de archivos debe asignar espacio a los archivos (organización física). Esto sucede en tiempo de ejecución.

El sistema de gestión de archivos debe conocer el espacio disponible en bloques para asignar a los archivos (gestión de espacios libres).

#### Prealocación
- El archivo es un conjunto de bloques en el dispositivo.
- Requiere que se declare el tamaño máximo (en cantidad de bloques) del archivo al momento de crearlo.
- Es difícil estimar el posible tamaño del archivo a priori, por lo cual se tiende a sobreestimarlo para tener un margen para que el archivo crezca. Este “colchón” es imprescindible en archivos de datos, pero no en archivos ejecutables, dado que estos últimos poseen un código inmutable en el tiempo, por lo que su tamaño no variará.

#### Alocación dinámica
Permite el crecimiento dinámico de un archivo.




#### Métodos de asignación de espacio
##### *Contigua*
- Cuando se crea un archivo, se le asigna un único conjunto contiguo de bloques.
- La tabla de asignación necesita sólo una entrada por cada archivo:
  - Bloque de comienzo y longitud del archivo en bloques.
- Se produce fragmentación interna en el último bloque, el cual SIEMPRE puede no estar completo, no importa cuál sea el método de asignación.
- Se produce FRAGMENTACIÓN EXTERNA (bloques libres entre archivos). Requiere compactación para dejar el área disponible contigua (muy costoso, proceso ininterrumpible). Sucede que el sistema posee la capacidad para almacenar un archivo, pero dicha capacidad no se encuentra de manera contigua.
- Si se daña un bloque, se pierde solo ese.
- No favorece el crecimiento dinámico de los archivos, dado que, si no se poseen bloques consecutivos para ampliar el archivo, se debe realojar el mismo. 

##### *Vinculada*
- La asignación se hace con bloques individuales no necesariamente contiguos que se encadenan.
- Cada bloque contiene un puntero al siguiente bloque de la cadena.
- En cada bloque hay información burocrática necesaria para la administración del archivo.
- La tabla de asignación necesita una sola entrada por cada archivo.
  - *Bloque de comienzo y longitud del archivo.*
- No genera fragmentación externa. No requiere compactación.
- Se ajusta mejor para alojar archivos secuenciales, que no requieren una lógica compleja de alta de registros como en un archivo de acceso directo.
- Si se pierde un bloque, se pierde el resto de archivo luego de este dado que se rompe la cadena.
- Se puede mejorar la confiabilidad con un doble enlazamiento entre los registros.
  - *En este caso, la tabla de asignación necesita una entrada adicional, la dirección del último bloque.*
  - *Si se daña un bloque, se pierde solo ese y se permite reconstruir el archivo.*

` 	`Este método de asignación posee una gran desventaja: acceso secuencial a los registros del archivo. Para leer el bloque 50, tengo que pasar por los 49 anteriores.


##### *Indexada*
- Dos tipos de bloques:
  - *Bloques de índices*. Solo contienen punteros, información burocrática.
  - *Bloques de datos.* Contienen la información propiamente dicha del archivo. Bloques similares a los de la asignación contigua.
- La tabla de asignación de archivos contiene un puntero al primer bloque de índices del archivo.
- Los bloques de índices contienen N punteros ordenados a bloques de datos del archivo.
- Los bloques de índices están encadenados entre sí. El último puntero de un bloque de índices apunta a otro bloque de índice (con otros N punteros a bloques de datos).
- No hay fragmentación externa.
- Fragmentación interna en los bloques de índices y en el último bloque de datos.
- El acceso es pseudo-directo: secuencial a la lista de bloques de índices y directo a los bloques de datos.

## **Gestión del espacio libre: estructuras**
Para la gestión del espacio libre, el SO requiere estructuras de soporte. Las más conocidas son listas de libres (Free List); lista de principio y cuenta; mapas de bits (BitMaps).
#### Lista de libres
- Es una lista encadenada de bloques libres. 
- Cada bloque tiene un puntero al próximo bloque libre.
- Cuando se libera un bloque, se lo engancha al final de la cadena.
- Cuando se requiere un bloque, se desengancha uno de la cadena.
- Ideal para la asignación vinculada, malo para la asignación continua.

#### Lista de Principio y Cuenta de libres
- Se trata de una lista encadenada de bloques libres, donde cada bloque guarda la cantidad de bloques contiguos libres que tiene.
- Es una lista que encadena a los primeros bloques de cada conjunto contiguo de libres (hueco) y conoce su tamaño.
- Es más corta que la Free List, dado que agrupa los contiguos y solo almacena el primero del hueco.
- Ideal para asignación contigua. Sirve para vinculada.

#### Mapas de bits
- Se trata de un arreglo unidimensional de bits, con tantos elementos como bloques en el dispositivo.
- Cada elemento contiene un valor binario que indica si ese bloque está ocupado o libre.
- Es más económica que la Free List y de rápido acceso.
- Ideal para asignación contigua. Sire también para vinculada.

#### Indexado
Se trata de manejar los bloques libres como un archivo indexado.

#### Huecos
Es el conjunto de bloques disponibles contiguos. Para la selección del espacio libre para asignar un archivo, existen 3 estrategias o criterios:

- *First Fit.* Primer hueco, más rápido. Mayor posibilidad de fragmentación externa, no se tiene en cuenta la eficiencia de uso de los huecos.
- *Best Fit.* Mejor hueco, menos fragmentación externa, ideal para archivos inmutables. Se complica para archivos que poseen grandes posibilidades de crecimiento.
- *Worst Fit.* Peor hueco, más fragmentación externa y chances de crecimiento para los archivos sin necesidad de realojarlos. Ideal para archivos de datos que poseen alta chance de crecer.

## **UNIX**
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


## **Windows File System - NTFS**
New Technology File System está diseñado para cumplir con los requisitos de gama alta para estaciones de trabajo y servidores, tales como aplicaciones de cliente/servidor, servidores de bases de datos, etc.
#### Características clave
- ##### *Recuperabilidad.* Posee una gran capacidad para recuperarse de crasheos del sistema y fallos en el disco. Cuando suceden estos eventos, NTFS es capaz de reconstruir volúmenes de disco y devolverlos a un estado consistente. Esto lo realiza usando un modelo de proceso-transacción para cambios en el FS. Cada cambio significativo es tratado como una acción atómica que se realiza en su totalidad o no se realiza en absoluto. Cada transacción que se encontraba en un proceso a la hora del error, es posteriormente retirada o llevada a cabo. Además, mantiene una copia del sistema de archivo a modo de back up.

- ##### *Seguridad.* NTFS utiliza el modelo de objetos de Windows para reforzar la seguridad. Un archivo abierto es implementado como un objeto archivo con un descriptor de seguridad que define sus atributos de seguridad. Este descriptor es almacenado como un atributo de cada archivo en disco.
##### 
- ##### *Tamaños máximos soportados.* NTFS soporta tamaños muy grandes de discos de almacenamiento de una manera más eficiente que otros FS tales como FAT.

- ##### *Múltiples flujos de datos. NTFS* trata los contenidos de un archivo como flujos de bytes (No estructurados). De esta forma, es posible definir múltiples flujos de datos para un mismo archivo.

- ##### *Información mantenida.* NTFS almacena un log de todos los datos realizados sobre un archivo en los volúmenes. Los programas pueden leer esta información para identificar cuáles archivos han sido modificados.

- ##### *Compresión y encriptado.* Los directorios y archivos pueden ser comprimidos de una forma transparente o encriptados en su totalidad.

- ##### *Hard and symbolic links. NTFS* soporta hard links, que permite que un archivo sea accesible desde múltiples rutas en el mismo volumen. Además, soporta links simbólicos, lo que permite además acceder a archivos o directorios que se encuentran en otro volumen. Además, Windows soporta puntos de montaje, lo cual permite que un mismo volumen fijo sea dividido en múltiples volúmenes virtuales tratados de manera independiente.

#### Volumen y estructura de archivos
NTFS utiliza los siguientes conceptos de almacenamiento en un disco:
- ##### *Sector.* Unidad física mínima de almacenamiento en un disco. 
- ##### *Clúster.* Uno o más sectores contiguos entre sí en un disco. Es la unidad fundamental de almacenamiento en NTFS, dado que éste no reconoce sectores para la lectura y escritura de datos. Al definir un clúster como una cantidad fija de sectores, el sistema de archivos se independiza del tamaño de sector de la unidad física de almacenamiento.
- ##### *Volumen.* Partición lógica en un disco, que consiste en uno o más clústeres y es usada por el FS para alojar espacio. El volumen consiste en información del FS, una colección de archivos y espacio libre para almacenar archivos nuevos. Un volumen puede ser una partición de un solo disco o extenderse en múltiples discos.

#### Estructura de un volumen NTFS
Cada elemento en un volumen es un archivo, y cada archivo consiste en una colección de atributos. Incluso los datos de un archivo son tratados como un atributo del mismo.

##### *Boot sector*
Se encuentra en las regiones iniciales del volumen. Contiene información acerca del diseño del volumen y la estructura del FS y el código e información necesaria para el inicio del sistema.

##### *Master file table (MFT)*
Contiene información acerca de todos los archivos y directorios. Consiste en una lista de todos los archivos y sus atributos.

##### *System files*
###### MFT2. Copia de las primeras filas de la tabla de archivos, usada para garantizar acceso al volumen en caso de que se corrompa el sector donde se almacena la MFT.
###### Log file. Lista de pasos de transacciones usadas por NTFS para restauraciones.
###### Cluster bit map. Representación del espacio en el volumen, que indica cuáles clústers de datos están en uso y cuáles no.
###### Tabla de definición de atributos. Define los tipos de atributos soportados en volumen e indica si pueden ser indexados y si pueden ser recuperados en una operación de recuperación del sistema.

## **MS – DOS**
Es un sistema de archivo basado en una tabla de asignación de archivos (FAT). El propósito de dicha tabla es realizar un seguimiento para saber dónde encontrar archivos en el disco.

El directorio raíz es “drive:\”. El separador de directorios es usualmente “\”, pero el sistema operativo también reconoce internamente una “/”. Las unidades físicas y virtuales son nombradas con una letra de dispositivo, en vez de ser fusionados. Esto significa que no hay un directorio raíz formal, sino que hay un directorio raíz independiente en cada unidad. Cada directorio puede contener otros directorios o archivos.

Limita el nombre de los archivos a 8 caracteres y la extensión a 3 caracteres.

