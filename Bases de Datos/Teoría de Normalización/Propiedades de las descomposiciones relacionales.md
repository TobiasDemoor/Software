Partimos del esquema de relación universal $R(A_1, A_2,\cdots, A_n)$ que incluye todos los atributos de la BD. Usando las [[Dependencia Funcional|DFs]] y el concepto de [[Formas Normales|formas normales]], descomponemos el esquema universal R en un conjunto de subesquemas de relación $D = \set{R_1, R_2, \cdots, R_m}$ que representará a la BD. **D es una descomposición de R**.

### Preservación de atributos
Debemos asegurarnos que cada atributo de R aparezca en al menos un subesquema de D, de forma de no perder atributos.
$$\bigcup_{i=1}^m R_1 = R$$

### Junta sin pérdida de información (SPI)
También llamada lossless join. Una descomposición $D = \set{R_1, R_2, \cdots, R_m}$ de **R** tiene la propiedad de junta sin pérdida de información (es SPI), **con respecto a un conjunto de DFs F en R**, si para cada instancia de relación r(R) que satisfaga F, se cumple lo siguiente para todos los subesquemas de D:
$$\Join(\pi_{R1}(r),\cdots,\pi_{Rm}(r)) = r, \forall r(R)$$
> Cuando se pierde información aparecen tuplas espurias (que no representan la realidad).

#### Propiedad de descomposición binaria
Una descomposición $\rho$ de R, $\rho = (R_1, R_2)$ es SPI con respecto a un conjunto de DFs F sii:
1. La DF $(R_1 \cap R_2) \rightarrow (R_1 - R_2)$ está en $F^+$ o
2. La DF $(R_1 \cap R_2) \rightarrow (R_2 - R_1)$ está en $F^+$

#### Algorítmo del Tableau
1. Dados R, F y $\rho = (R_1, R_2, \cdots, R_k)$, se construye una tabla (tableau) inicial $T_0$ donde las columnas son los atributos y las filas los subesquemas de $\rho$.
2. Se completa el tableau con símbolos distinguidos $a_j$ si $A_j \in R_i$ o con no distinguidos $b_{ij}$ si $A_j \notin R_i$.
3. Se aplican las DFs al tableau:
	Para cada DF $X \rightarrow A$, si dos filas coinciden en X entonces el A se modifica para que también coincidan dando prioridad al símbolo distinguido, generando una serie $T_0, T_1, \cdots, T^*$.
4.  Condición de parada:
	- Si encuentro una fila con todos los símbolos distinguidos $a_j$ entonces, $\rho$ **es SPI**.
	- Cuando el último tableau $T^*$ ya no cambia con la aplicación de las DFs. Si no llegué a una fila con todos los símbolos distinguidos, entonces la descomposición **es con pérdida**.

### Preservación de dependencias funcionales
Además de preservar información, una descomposición debería preservar DFs (Sin Perdida de [[Dependencia Funcional|Dependencias Funcionales]], SPDF).
- Dados R y $\rho = (R_1, R_2, \cdots, R_k)$, decimos que la proyección de F sobre un conjunto de atributos Z, $\pi_Z(F)$, es el conjunto de DFs $X \rightarrow Y \in F^+$ tal que $(X \cup Y) \subseteq Z$.
- La descomposición $\rho$ preserva DFs F si la unión de todas las proyecciones $\pi_{Ri}(F)$ para $i = 1, \cdots, k$ es un conjunto equivalente a F, es decir:
$$F \equiv \bigcup_{i=1}^k \pi_{Ri}(F)$$
$$F^+ = (\bigcup_{i=1}^k \pi_{Ri}(F))^+$$

> Una descomposición puede ser SPI y SPDF (deseable), ninguna, solo SPI o solo SPDF.