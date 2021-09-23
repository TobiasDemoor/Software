La dependencia funcional (DF) es una restricción entre dos conjuntos de atributos de un [[Modelo Lógico Relacional#Esquema de relación|esquema de relación]]. Responde a la semántica de los atributos y permite modelar aspectos del "minimundo". Se define sobre un esquema de relación R y debe cumplirse para cualquier instancia r(R) que pudiera existir. Las instancias r(R) que satisfacen todas las dependencias funcionales y restricciones definidas sobre R se denominan "instancias legales de R".

### Definición
Sea $R(A_1, A_2, \cdots, A_n)$ un esquema de relación y sean X e Y subconjuntos de {$A_1, A_2, \cdots, A_n$}. Decimos que $X \rightarrow Y$ es decir "X determina funcionalmente a Y" o "Y depende funcionalmente de X", si para cualquier instancia de relación r para R, no es posible que r tenga dos tuplas que coincidan en los valores de los componentes para todos los atributos de X y no coincidan en uno o más componentes para atributos del conjunto Y.

Dicho de otro modo, la DF $X \rightarrow Y$, se cumple en R si para dos tuplas cualesquiera $t_1$ y $t_2$ de r(R), r una instancia cualquiera de R, ocurre lo siguiente:

$$t_1[X] = t_2[X]\ \Rightarrow t_1[Y] = t_2[Y]$$

Con esto podemos redefinir a una **clave candidata** sobre R:

Sea $R(A_1, A_2, \cdots, A_n)$ un esquema de relación y sean X e Y subconjuntos de {$A_1, A_2, \cdots, A_n$}. Si X es una clave candidata de R, es decir,

$$t_1[X] \ne t_2[X]\ \forall\ i, j, i \ne j \text{ para cualquier instancia de r(R)} \Rightarrow X \rightarrow Y\ \forall\ Y, Y \subseteq R$$

### Reglas de inferencia
Sea *F* un conjunto de DFs especificadas sobre un esquema de relación R. El diseñador especifica las dependencias que son semánticamente obvias. Pero, en general, otras DFs aparte de las especificadas se cumplen en todas las instancias de relación legales que satisfacen las DFs en *F*. El conjunto de todas eses DFs se denomina **CLAUSURA DE F** y se denota $\bf{F^+}$.

Una DF $X \rightarrow Y$ es inferida a partir de un conjunto de dependencias F especificado sobre R si $X \rightarrow Y$ se cumple en cada instancia de relación legal r(R).

Para determinar estas dependencias inferidas se tiene un **conjunto de reglas de inferencia (llamadas axiomas de Armstrong)**:

* IR1 Reflexividad: $X \supseteq Y \Rightarrow X \rightarrow Y$
* IR2 Aumentación: $X \rightarrow Y \Rightarrow XZ \rightarrow YZ$
* IR3 Transitividad: $X \rightarrow Y, Y \rightarrow Z \Rightarrow X \rightarrow Z$
* IR4 Descomposición o proyección: $X \rightarrow YZ \Rightarrow X \rightarrow Y$
* IR5 Unión: $X \rightarrow Y, X \rightarrow Z \Rightarrow X \rightarrow YZ$
* IR6 Pseudotransitividad: $X \rightarrow Y, WY \rightarrow Z \Rightarrow WX \rightarrow Z$

> El conjunto formado por las reglas IR1, IR2 e IR3 es correcto y completo.