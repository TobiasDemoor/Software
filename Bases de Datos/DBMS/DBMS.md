# Database Managment System (DMBS)
Un **sistema de gestión de base de datos** (database management system, DBMS) es un sistema computarizado que permite a los usuarios crear y mantener una [[Bases de Datos|base de datos]]. El DBMS es un software de propósito general que facilita los procesos de *definición*, *construcción*, *manipulación* y *sharing* de bases de datos entre varios usuarios y aplicaciones. La **definición** de una base de datos incluye especificar los tipos de datos, estructuras, y [[Integrity constraints|restricciones]] de la información a ser almacenada en la base de datos. La definición de base de datos o información descriptiva también es almacenada por el DBMS en la forma de un catálogo de bases de datos o diccionario (**meta-data**).  La **construcción** de una base de datos es el proceso de almacenar la información en algún medio de almacenamiento controlado por el DBMS. La **manipulación** de una base de datos incluye funciones tales como la consulta de la base para obtener información específica (*querying*), actualizar la base de datos para reflejar cambios en el minimundo (*updating*), y generar reportes a partir de la información. El **sharing** de una base de datos permite a múltiples usuario y programas acceder a la base de datos simultaneamente.

Otra función importante provista por el DBMS incluye la *protección* y *mantenimiento* de la base de datos a través de un período de tiempo prolongado. La **protección** incluye la *protección del sistema* contra errores de hardware o software y *protección de seguridad* contra uso no autorizado o malicioso. Una base de datos puede tener un ciclo de vida de muchos años y el DBMS debe ser capaz de **mantener** la base de datos, permitiendo que el sistema evolucione a medida que los [[Requerimientos|requerimientos]] cambian a través del tiempo.

![[database_management_system_1.png]]

## Lenguajes
Una vez que el diseño de la [[Bases de Datos|base de datos]] está completo y se haya escogido un [[DBMS|DBMS]], el primer paso es especificar los schemas conceptual e interno para la base de datos. En muchos DBMSs donde no hay una separación estricta entre niveles, un lenguaje, llamado **data definition language (DDL)**, es usado para definir ambos schemas.

En DMBSs con una separación clara entre los niveles, el DDL es utilizado para definir solamente el schema conceptual y el schema interno es definido usando un **storage definition language (SDL)**. Para una verdadera [[Three-Schema Architecture|arquitectura de tres schemas]], necesitaríamos un tercer lenguaje, el **view definition language (VDL)**, para especificar las vistas de usuarios, pero en la mayoría de los DBMSs el DDL es utilizado para definir los schemas conceptual y externo. En [[RDBMS|RDMBSs]], [[SQL]] es utilizado en el rol de VDL para definir vistas de usuario o vistas de aplicación.

Una vez que se tienen los schemas de base de datos, los usuarios requieren un medio para manipular la base. El DMBS provee un conjunto de operaciones o un lenguaje llamado **data manipulation language (DML)** con este fin.

En los DBMSs actuales estos lenguajes anteriores usualmente no se consideran lenguajes separados, sino un lenguaje integrado compehensivo es usado que incluye las herramientas para la definición del schema conceptual, definición de vistas, y manipulación de datos. La definición de almacenamiento suele mantenerse separado. Un ejemplo típico de un lenguaje integrado es el lenguaje de base de datos relacional [[SQL]], el cual representa una combinación de DDL, VDL, y DML.

## Arquitectura cliente-servidor de dos niveles
Estas arquitecturas consisten en distribuir los [[Componente|componentes]] en dos sistemas: cliente y servidor ([[Client-Server]]). El cliente suele contener los componentes de interfaz de usuario y programas de aplicación. Mientras tanto el servidor contiene la funcionalidad de queries y [[Transacciones|transacciones]] (lo relacionado a [[SQL]] para los [[RDBMS|RDMBS]]), este servidor se suele llamar **query server** o **transaction server** justamente porque provee estas funcionalidades (o SQL server para los [[RDBMS|RDBMS]]).

Existe un estandar llamada **Open Database Connectivity (ODBC)** que provee una [[API|API]] que permite a los programas client-side invocar al [[DBMS|DBMS]]. Existe también un estandar relacionado para Java llamado **Java Database Connectivity (JDBC)**.

La ventaja de esta arquitectura es su simplicidad y compatibilidad con los sistemas existentes. Con la aparición de la Web los roles de cliente y servidor cambiaron, llevando a la [[#Arquitectura cliente-servidor de tres niveles|arquitectura de tres niveles]].

## Arquitectura cliente-servidor de tres niveles
Muchas aplicaciones Web utilizan la arquitectura de tres niveles, la cual añade una capa intermedia entre el cliente y el servidor de base de datos (comparado a la [[#Arquitectura cliente-servidor de dos niveles|arquitectura de dos niveles]]).

![[database_three_tiered_client_sever_architecture.png]]

Esa capa intermedia es llamada servidor de aplicación o web server. Este juega un rol intermediario corriendo los programas de aplicación y almacenando reglas de negocios que son utilizadas para acceder a la información del servidor de base de datos.

## Clasificación
Los [[DBMS|DMBSs]] se pueden clasificar según varios criterios. El primero es el [[Data Model|**data model**]] sobre el cual se basan. El data model más usado actualmente es el **[[Modelo Relacional|modelo relacional]]** y los sistemas basados en este son conocidos como **sistemas SQL** ([[RDBMS]]). El **[[Modelo Orientado a Objetos|modelo orientado a objetos]]** ha sido implementado en algunos sistemas comerciales pero no tiene un uso masivo ([[ODBMS]]). Recientemente, los llamados **sistemas big data**, también conocidos como **sistemas de almacenamiento clave-valor** y **sistemas NOSQL** (leasé Not Only SQL), utilizan varios data models: **document-based**, **graph-based**, **column-based**, y **key-value** (clave-valor).

El segundo criterio para clasificarlos es la **cantidad de usuarios** permitidos por el sistema. Los **sistemas mono-usuario** soportan un solo usuario concurrente y son mayormente usados en computadoras personales. Los **sistemas multi-usuario** soportan múltiples usuarios concurrentes (aquí caen la mayoría de los [[DBMS|DBMSs]]).

El tercer criterio es la **cantidad de sitios** sobre los cuales puede estar distribuida la base de datos. Una [[DBMS|DBMS]] se dice **centralizado** si los datos son almacenados en un solo sitio (una sola máquina). Un DBMS centralizado puede soportar múltiples usuarios, pero el [[Database System|sistema de base de datos]] reside completamente en un único lugar. Un [[DBMS|DBMS]] **distribuido** ([[DDBMS]]) puede tener la base de datos en sí y el DBMS distribuido a través de muchos sitios.

Por último los [[DBMS|DBMSs]] pueden ser **general purpose** o **special purpose**. Cuando la [[Performance|performance]] es una consideración primaria, una DBMS special purpose puede ser diseñada y construida para una aplicación específica; tal sistema no puede ser utilizado para otras aplicaciones sin cambios considerables.