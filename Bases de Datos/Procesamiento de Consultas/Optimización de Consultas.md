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

#### Índices
Los [[índice|índices]] permiten el acceso a la información de una forma no soportada (o no eficientemente soportada) por la organización básica de un archivo.

Si los datos del archivo están ordenados físicamente en el mismo orden que uno de sus índices, decimos que ese índice es **clustered**. Caso contrario es **unclustered**. Los archivos de datos pueden tener a lo sumo un índice clustered.

Los índices **densos** son los que tienen una entrada de índice por cada valor de clave de búsqueda del archivo de datos. En cambio, si no todos los valores clave están en el índice, se llaman **no densos**. Es usual si se tiene un índice clustered optimizar el uso del espacio de índices manteniendo en un índice no denso solo el primer valor de clave de cada bloque del archivo de datos.

Se llaman índices **primarios** a aquellos que contienen todos los registros completos de un archivo. En caso de tener sólo los rids (solo la referencia al registro) se los llaman índices **secundarios**.

### Evaluación de operaciones relacionales
Las diferentes implementaciones aprovechan o explotan algunas propiedades de las tablas a efectos de lograr una mejor performance, por ejemplo: 
* Existencia de índices relevantes en los archivos input
* Ordenamiento interesante de los archivos de input
* Tamaño de los archivos de input
* Tamaño del buffer 

Los diversos algoritmos se basan en algunos de los siguientes principios: 
* **Iteración:** se examinan todas las tuplas de la relación, aunque a veces se examina el índice.
* **Indexación:** si hay una condición de selección y/o join y a su vez existe un índice sobre los campos involucrados, se utilizará el índice.
**Particionamiento:** particionando la relación según una clave de búsqueda podremos descomponer la operación en operaciones menos costosas.

Los diferentes métodos para recuperar tuplas se llaman caminos de acceso: nosotros veremos el **file scan** (recorrido sobre el archivo de datos) y el **index scan** (recorrido sobre las entradas de un índice).

Llamaremos **selectividad** de un predicado p (y lo denotamos sel(p) ) a la proporción de tuplas de una relación que satisfacen ese predicado, es decir, la división entre la cantidad de tuplas que satisfacen el predicado sobre la cantidad total de tuplas de las relación.

#### Proyección
La operación de proyección $\bf{\pi(l, R, Q)}$ procesa las tuplas de una relación de entrada R y produce un resultado Q con todas las tuplas pero sólo conteniendo los atributos indicados en la lista $l$.

Como una simplificación se considera que la **cantidad de tuplas** resultado es la misma que la cantidad de tuplas de entrada.

Para el enfoque de la materia, el **costo del output** (CO) de una operación, en caso de tener que computarse, siempre es la cantidad de bloques necesarios para escribir el resultado en disco. La cantidad de bloques necesarios se puede calcular a partir de la cantidad de tuplas, la longitud de bloque y la longitud de cada tupla.
$$FB_Q = \lceil LB / L_Q \rceil$$
$$CO = B_Q = \lceil T_Q / FB_Q \rceil$$

#### Selección
La operación de selección $\bf{\sigma (p, R, Q)}$ procesa las tuplas de una relación de entrada R y genera un resultado Q con todas las tuplas que cumplen la condición p.

Para estimar la **cantidad de tuplas** que satisfacen una condición asumiremos (salvo indicación en contrario) que la distribución de valores es uniforme y que los valores de los atributos son probabilísticamente independientes.

En el caso general, estimaremos la cantidad de tuplas a partir de la selectividad, con la siguiente fórmula $T_Q = sel(p) * T_R$.

#### Junta
La operación de Join $\bf{\Join (p, R, S, Q)}$ procesa las tuplas de dos relaciones de entrada R y S, y produce un resultado Q con todas las tuplas del producto cartesiano R X S que cumplen con la condición p.

> En todo lo que sigue asumiremos que se trata siempre de equijoins, y la condición de junta está dada por R.ri = S.sj.

La **cantidad de tuplas** del resultado estará determinada por el atributo de la junta que tenga mayor imagen en la relación a la que pertenece. Por lo tanto la cantidad de tuplas del resultado será $T_Q = (T_R * T_S) / max(I_{R,ri}, I_{S,sj})$.

> Dada $R \Join S$ R es la relación externa y S la relación interna.

##### Block Nested Loops Join (BNLJ)
**Precondición**: se tienen B bloques de memoria disponibles para la operación (B-2 bloques se utilizan para el almacenamiento de la relación R, 1 bloque se utiliza para ir leyendo los bloques de S, y el bloque restante se destina para la salida de la operación, en memoria).

**Descripción**:
```
Para cada segmento de B-2 bloques de R
	Para cada bloque de S
		Para toda tupla r del segmento de R y tupla s del bloque de S
			Si ri == sj ( o más generalmente, vale p(s) )
				Agregar <r,s> al resultado
```

**Costo de input**: $B_R + B_S * \lceil B_R / (B-2) \rceil$

##### Index Nested Loops Join (INLJ)
**Precondición**: 
* el archivo tiene un índice I según una clave k 
* el predicado p del join coincide con el índice I, o p es un predicado conjuntivo de la forma p1 and p2, donde p1 y p2 son dos predicados válidos, y p1 coincide con el índice.

**Descripción**:
```
Para cada tupla r de R
	Para cada tupla s de S / ri = sj (obtenida según el índice de S)
		Si no hay condicion adicional (o hay y s la cumple )
			Agregar <r,s> al resultado
```

**Costo de input**: $B_R + T_R$
(“buscar para la tupla $t_R$ index entry/ies en índice de S” + “buscar valor/es apuntados por index entry/ies”)

##### Sort Merge Join (SMJ)
No tiene precondiciones.

**Descripción**:
```
Si R no está ordenada en el atributo i 
	ordenar R
Si S no está ordenada en el atributo j 
	ordenar S

r = primera tupla de R // itera sobre R
s = primera tupla de S // itera sobre S

Mientras r ≠ null y s ≠ null // cuando se llega al final de un archivo se obtiene null
	si ri < sj
		// No hay partición en S para ri
		r = siguiente tupla en R
	si ri == sj
		// Se encontró la partición en S para ri...
		Mientras ri == sj //Se procesa partición actual de R
			inicio_part_s = s // Marca el inicio de la partición en S para ri 
			Mientras sj == ri // Se procesa partición actual de S
				Agregar <r,s> al resultado
				s = siguiente tupla en S
			s = inicio_part_s
			r = siguiente tupla en R
		si ri > sj
			// s no apuntaba al inicio de la partición en S de ri
			// entonces sigo buscando
			s = siguiente tupla en S
```

**Costo de input**: el costo involucra el costo de ordenar cada una de las relaciones participantes por el atributo de junta (el cósto genérico es $(\lceil log_{B-1}\lceil B_R/B \rceil \rceil +1)* 2B_R$, pero podría darse el caso que alguna esté ordenada). Y a esto se le adiciona el costo del merge ($B_R + B_S$). 

