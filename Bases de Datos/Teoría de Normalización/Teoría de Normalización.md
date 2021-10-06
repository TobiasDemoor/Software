La teoría de normalización trata de brindar un criterio para elegir un diseño de [[Bases de Datos|BD]] frente a otros diseños alternativos. Cuando se transforma el [[Diagrama Entidad Relación]] al [[Modelo Lógico Relacional]] se mide la **calidad del diseño**.

## Anomalías
Se estudian las **anomalías** del diseño. Lo que buscamos son las "buenas propiedades" de los diseños de BD relacionales y evitar los problemas o características no deseables. Estos úlitmos se pueden clasificar de la siguiente manera:
* **Redundancia** (ej: los datos del proveedor aparecen replicados por cada item)
* **Inconsistencia Potencial** (ej: al estar replicados los datos del proveedor podrían quedar inconsistentes)
* **Anomalías de Actualización**
	* **Inserción** (ej: quiero dar de alta un proveedor que no provee ningún item, no puedo)
	* **Modificación** (ej: quiero modificar los datos de un proveedor tengo que modificar todas sus apariciones)
	* **Borrado** (ej: quiero borrar todos los items de un proveedor, se borran también los datos del proveedor)

Esquema de ejemplo: PROVEEDOR(P-nro, P-nombre, P-dir, nro-Item, nombre-Item, precio)

> La **redundancia** nos lleva a otra característica no deseable que es la **incosistencia potencial**

> La redundancia de las claves foráneas es una redundancia necesaria.

## Dependencia funcional (DF)
![[Dependencia Funcional]]

## Formas Normales
![[Formas Normales]]

## Propiedades de las descomposiciones relacionales
Partiendo del esquema de relación universal $R(A_1, A_2,\cdots, A_n)$ se parte hasta tener los distintos subesquemas  de relación en 3FN o FNBC.

### Preservación de atributos
Debemos asegurarnos que cada atributo de R aparezca en al menos un subesquema de D, de forma de no perder atributos.
$$\bigcup_{i=1}^m R_1 = R$$

### Junta sin pérdida de información (SPI)
También llamada lossless join.
$$\Join(\pi_{R1}(r),\cdots,\pi_{Rm}(r)) = r, \forall r(R)$$
> Cuando se pierde información aparecen tuplas espurias (que no representan la realidad).

#### Propiedad de descomposición binaria
Una descomposición $\rho$ de R, $\rho = (R_1, R_2)$ es lossless join con respecto a un conjunto de DFs F sii:
1. la DF $(R_1 \cap R_2) \rightarrow (R_1 - R_2)$ está en $F^+$ o
2. la DF $(R_1 \cap R_2) \rightarrow (R_2 - R_1)$ está en $F^+$

#### Algorítmo del Tableau
1. Dados R, F y $\rho = (R_1, R_2, \cdots, R_k)$, se construye una tabla (tableau) inicial $T_0$ donde las columnas son los atributos y las filas los subesquemas de $\rho$.
2. Se completa el tableau con símbolos distinguidos $a_j$ si $A_j \in R_i$ o con no distinguidos $b_{ij}$ si $A_j \notin R_i$.
...

### Preservación de dependencias funcionales
Además de preservar información, una descomposición debería preservar DFs (Sin Perdida de [[Dependencia Funcional|Dependencias Funcionales]], SPDF).

> Una descomposición puede ser SPI y SPDF (deseable), ninguna, solo SPI o solo SPDF.

## Notas
[[Normalización]] [[Denormalización]]
La desventaja principal de normalizar es que se requieren más operaciones de junta para levantar los datos deseados.

Para aplicar las definiciones de 2FN en adelante hace falta tener las claves candidatas definidas.