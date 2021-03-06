En el **modelo logico relacional** , una [[Bases de Datos|base de datos]] es un conjunto de **relaciones**. Intuitivamente, una relación puede pensarse como una tabla, con filas y columnas. Cada fila, a la que denominamos **tupla**, está formada por un conjunto de valores de datos relacionados que representan un hecho de la realidad. Cada columna de la tabla representa un **atributo**, asociado a un conjunto de valores posibles que puede tomar. A este conjunto lo llamamos *dominio* del atributo.

El conjunto de datos de la relación en un momento dado se denomina **instancia de relación** y la estructura de la relación, es decir su nombre y lista de atributos se denomina **esquema de relación**.

 La mayoría de bases de datos relacionales usan el lenguaje de query de alto nivel [[SQL]] y soporta una versión limitada de vistas de usuario.

### Esquema de relación
Describe la relación R como *R(A₁, A₂, ..., An)*. Los *atributos subrayados con línea continua* son identificadores y constituyen la **clave primaria (PK)** de cada esquema.

Los *atributos subrayados con línea punteada* constituyen una **clave foránea (FK)**, es decir, hacen referencia a valores existentes en atributos *clave* de otra relación. En algunas ocaciones las claves foráneas pueden tomar valor nulo.

El conjunto de esquemas de relación, junto con las restricciones adicionales asociadas, constituyen el **diseño lógico** de la base de datos. Es deseable y necesario que el diseño lógico cumpla con ciertas propiedades y no presenta anomalías. El proceso de *[[Normalización|normalización]]* es una herramienta que posibilita arribar a un buen diseño de base de datos relacional.

> **Instancia de relación de un esquema de relación R(A₁, A₂, ..., An):** r(R) es un subconjunto del producto cartesiano de los dominios que definen R, 
> $r(R) \subseteq (dom(A_1) x dom(A_1) x \cdots x dom(A_n))$
> Una relación, por ser un conjunto, nunca tiene tuplas repetidas.

### Restricciones
- Dominio:
	> Cada atributo tiene un dominio definido y debe tomar valores pertenecientes a este
- Clave (superclave - clave candidata, CK - clave primaria, PK):
	> Dado R, para cualquier r(R), t₁ y t₂ dos tuplas distintas cualesquiera, SK conjunto de atributos que constituyen una superclave en $R: t_1[SK] ≠ t_2[SK]$.
	> La superclave puede tener elementos redundantes, pero la clave debe ser minimal.
	> Una clave nunca debe tomar valor nulo.
* Integridad referencial (clave foránea, FK):
	> Sean R₁ y R₂ dos esquemas de relación y FK un subconjunto de atributos en R₂. FK es **clave foránea** en R₂ si:
	> - Los atributos en FK tienen el mismo dominio que los atributos de la clave primaria de R₁.
	> - Un valor para FK en la tupla t₂ en R₂ debe existir como valor de clave primaria para alguna tupla t₁ en R₁, o en caso que no exista debe tomar valor nulo.
- Dependencias de datos (ej: [[Dependencia Funcional|dependencias funcionales]])
%%[[Integrity constraints]]%%
	
### Esquema lógico de la base de datos
Al conjunto de esquemas relacionales que conforman una base de datos junto con las restricciones asociadas se lo denomina esquema lógico de la base de datos.

Se llama instancia de un esquema relacional a un conjunto de instancias $r_i$ tal que $r_i$ es una instancia de$R_i$ y tal que $r_i$ cumpla con las restricciones.

### Superclave
Una superclave de un esquema de relación $R = \set{A_1, A_2, ..., A_n}$ es un conjunto de atributos $S \subseteq R$, tal que para ningún par de tuplas $t-i, t_j, i \ne j$ de cualquier instancia legal r(R) ocurre $t_i[S] = t_j[S]$. Para toda superclave S $S \rightarrow R$ (se puede demostrar por el absurdo).

Utilizando la [[Dependencia Funcional#Clausura de conjunto de atributos|clausura de un conjunto de atributos]] se puede afirmar que si $S \subseteq R, S^+ = R$ entonces S es superclave de R.

### Clave
Una clave de un esquema de relación $R = \set{A_1, A_2, ..., A_n}$ es un conjunto de atributos $K \subseteq R$ tal que **K es superclave** y **K es un conjunto minimal**. Osea que la eliminación de cualquier atributo de K causará que K no sea más superclave. Para toda superclave K $K \rightarrow R$ (por ser K superclave).

#### Claves candidatas (CK)
Sea R un esquema de relación con F un conjunto de [[Dependencia Funcional|DFs]]. Un conjunto de atributos que no está determinado funcionalmente por ningún otro conjunto de atributos en R, es decir, todo conjunto de atributos que no se encuentra del lado derecho de ninguna DF, formará parte de toda CK de R.