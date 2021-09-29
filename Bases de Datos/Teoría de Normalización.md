La teoría de normalización trata de brindar un criterio para elegir un diseño de [[Bases de Datos|BD]] frente a otros diseños alternativos. Cuando se transforma el [[Diagrama Entidad Relación]] al [[Modelo Lógico Relacional]] se mide la **calidad del diseño**. Se estudian las **anomalías** del diseño. Lo que buscamos son las "buenas propiedades" de los diseños de BD relacionales y evitar los problemas o características no deseables. Estos úlitmos se pueden clasificar de la siguiente manera:

* Redundancia (ej: los datos del proveedor aparecen replicados por cada item)
* Inconsistencia Potencial (ej: al estar replicados los datos del proveedor podrían quedar inconsistentes)
* Anomalías de Actualización
	* Inserción (ej: quiero dar de alta un proveedor que no provee ningún item, no puedo)
	* Modificación (ej: quiero modificar los datos de un proveedor tengo que modificar todas sus apariciones)
	* Borrado (ej: quiero borrar todos los items de un proveedor, se borran también los datos del proveedor)

Esquema de ejemplo:
PROVEEDOR(P-nro, P-nombre, P-dir, nro-Item, nombre-Item, precio)

La **redundancia** nos lleva a otra característica no deseable que es la **incosistencia potencial**

> La redundancia de las claves foráneas es una redundancia necesaria.

## Dependencia funcional (DF)
![[Dependencia Funcional]]

## Formas Normales
Las formas normales son listadas en orden creciente de restricción. Una contiene a sus siguientes, y para afirmar que un esquema se encuentra en una forma normal se debe demostrar que no se encuentra en la siguiente.

En todas las formas normales se presentan anomalías pero se van reduciendo a medida que se pasa a formas más restrictivas.

### 1ª Forma Normal (1FN)
ES parte de la definición formal de una relación. Evita atributos multivaluados y compuestos (relaciones adentro de relaciones). Establece que en un esquema de relación los dominios de los atributos deben incluir únicamente valores atómicos, es decir, indivisibles.

### 2ª Forma Normal (2FN)
Sea $R(A_1, A_2, \cdots, A_n)$ un esquema de relación y sean X e Y subconjuntos de $\set{A_1, A_2, \cdots, A_n}$.

* <u>Definición DF TOTAL:</u> Una dependencia funcional $X \rightarrow Y$ es TOTAL si la eliminación de algún atributo A de X implica que la dependencia resultante ya no se cumple, es decir, para algún atributo $A \in X$, $(X-\set{A}) \rightarrow Y$ ya no se cumple.

* <u>Definición DF PARCIAL:</u> Una dependencia funcional $X \rightarrow Y$ es PARCIAL si algún atributo $A \in X$ puede ser eliminado de X y la dependencia resultante se sigue manteniendo, $(X-\set{A}) \rightarrow Y$ en R.

R está en 2FN si cada atributo no primo de R depende funcionalmente en forma total de cada clave de R (cada atributo no primo no es parcialmente dependiente de alguna clave de R). Un atributo primo forma parte de alguna clave candidata, el atributo no primo no forma parte de ninguna clave candidata.

### 3ª Forma Normal (3FN)
Sea $R(A_1, A_2, \cdots, A_n)$ un esquema de relación y sean X e Y subconjuntos de $\set{A_1, A_2, \cdots, A_n}$, A atributo de R.

R está en 3FN si para cada dependencia funcional $X \rightarrow Y$ definida sobre R, si cumple una de las dos o ambas:
	a. X es superclave de R.
	b. A es atributo primo de R.
	
### Forma Normal de Boyce-Codd (FNBC)
R está en FNBC si para cada dependencia funcional no trivial $X \rightarrow Y$ definida sobre R, X es superclave de R.

Una esquema de relación en FNBC básicamente no presenta anomalías (al menos significativas). Un esquema de relación se puede descomponer en subesquemas para hacer que cumplan con FNBC. Y se puede asegurar una buena calidad de diseño.

## Notas
[[Normalization]] [[Denormalization]]
La desventaja principal de normalizar es que se requieren más operaciones de junta para levantar los datos deseados.

Para aplicar las definiciones de 2FN en adelante hace falta tener las claves candidatas definidas.