---
aliases: ["archivos compartidos"]
---
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

Al diseñar la posibilidad de accesos compartidos, deben abordarse aspectos de la [[exclusión mutua]] e interbloqueo entre procesos ([[deadlock]]).

#### Record blocking
En la mayoría de los sistemas los bloques son de longitud fija para simplificar operaciones de E/S, la organización de los mismos y demás. Por otro lado, los registros que se encuentran dentro de cada bloque pueden organizarse de distinta manera:

- *Registros de longitud fija.*  En cada bloque existe una cantidad fija de registros enteros almacenados, lo cual puede resultar en espacio desperdiciado.
- *Registros de longitud variable con encadenamiento.* Se utilizan registros de longitud variable y se permite particionar un registro para almacenarlo en dos bloques consecutivos.
- *Registros de longitud variable sin encadenamiento.* No permite particionar registros. Fragmentación a nivel bloque.