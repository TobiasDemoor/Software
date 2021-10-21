### Modelo
Este es un modelo simplificado, en las bases de datos reales por lo general se encontrará una mayor complejidad.

#### Relaciones
Las relaciones se dividen en bloques o páginas. La longitud de estos bloques se define a nivel general (se lo denota con **LB**), por lo que todas las relaciones poseen bloques del mismo tamaño.

Dada una relación R, se conocen los siguientes datos: 
* **BR**: Cantidad de bloques que ocupa R. 
* $\bf{FB_R}$: Cantidad de tuplas por bloque de R (factor de bloqueo) 
* $\bf{L_R}$: Longitud de una tupla de R 
* $\bf{T_R}$: Cantidad total de tuplas de R 
* $\bf{I_{R,A}}$: Imagen del atributo A de R. Denota la cantidad de valores distintos de ese atributo en la relación. 
* **X**: altura del árbol de búsqueda 
* $\bf{FB_I}$: Cantidad de entradas por bloque del índice I (factor de bloqueo del índice) 
* $\bf{BH_I}$: Cantidad de bloques que ocupa el índice i para nodos hoja (el índice debe ser [[B+ Tree|árbol B+]]). Si no se tiene el dato y se desea calcularlo, se utilizará el criterio de peor caso (cada nodo hoja estará completo en su mínimo, es decir, d/2, donde d es el orden del árbol). 
* $\bf{MBxB_I}$: Cantidad máxima de bloques que ocupa un bucket del índice i (el índice debe ser basado en hashing)
* $\bf{CBu_I}$: cantidad de buckets del índice I (el índice debe ser basado en hashing).

Además, asumiremos que: 
* en cada bloque de la relación R solamente hay tuplas de R (y no de otras relaciones). 
* La longitud de cada tupla es fija para cada tabla. 
* La longitud de cada tupla es siempre “bastante” menor que la longitud de un bloque, en el sentido que un bloque puede contener más de una tupla.

#### Memoria principal
La memoria principal disponible para la base de datos también se divide en bloques. Llamaremos B a la cantidad de bloques disponibles.

#### Costos
Como unidad de medida se utilizarán los **accesos a disco** (tanto lecturas como escrituras).

Vale la pena mencionar que motores de bases de datos reales pueden tener en cuenta otros factores que también influyen, como el tiempo insumido por cada acceso a disco, el tiempo insumido por cada acceso a memoria, el tiempo de procesamiento de determinadas operaciones (como ser la evaluación de una función de hashing sobre una clave).

#### Aclaraciones
* En algunos casos podría suceder, por ejemplo, que se necesitara utilizar un bloque de una relación y que éste ya se encontrara en memoria principal. Aprovechando esto, se podría evitar el acceso a disco (con el consiguiente ahorro de costos); sin embargo, es difícil predecir cómo la base de datos hará uso de la memoria principal (puede depender de varios factores como la política de reemplazos de bloques de memoria), por lo que se asumirá que siempre se accede a disco. 
* Los costos de las búsquedas serán expresados en **peor caso**.
* Dentro de un bloque sólo se almacenarán tuplas enteras. Esto va a hacer que en algunos casos se desperdicie espacio dentro de algunos bloques.
* Todos los archivos o índices están organizados en bloques. 
* Los tamaños de los bloques de disco y de memoria son iguales


### Organización de archivos
Desde un punto de vista lógico una base de datos relacional está compuesta por múltiples relaciones, que son tablas compuestas por tuplas. En un nivel físico, esas tablas son [[Archivo|archivos]] de [[Registro|registros]], los que pueden estar agrupados en páginas o bloques. Los atributos de las relaciones aquí serán los campos de los registros.

Todo registro de una tabla tiene un identificador único llamado rid (record identifier). Este identificador es independiente del contenido del registro, y es utilizado directamente por el [[DBMS]].

Usaremos dos tipos de archivos, **heap files** (archivos desordenados) y **sorted files** (archivos ordenados por algún conjunto de atributos).

![[optimización_archivos_costos.png]]