La dependencia funcional (DF) es una restricción entre dos conjuntos de atributos de un [[Modelo Lógico Relacional#Esquema de relación|esquema de relación]].

Responde a la semántica de los atributos y permite modelar aspectos del "minimundo". Se define sobre un esquema de relación R y debe cumplirse para cualquier instancia r(R) que pudiera existir. Las instancias r(R) que satisfacen todas las dependencias funcionales y restricciones definidas sobre R se denominan "instancias legales de R".

### Definición
Sea $R(A_1, A_2, \cdots, A_n)$ un esquema de relación y sean X e Y subconjuntos de $\set{A_1, A_2, \cdots, A_n}$. Decimos que $X \rightarrow Y$ es decir "X determina funcionalmente a Y" o "Y depende funcionalmente de X", si para cualquier instancia de relación r para R, no es posible que r tenga dos tuplas que coincidan en los valores de los componentes para todos los atributos de X y no coincidan en uno o más componentes para atributos del conjunto Y.

Dicho de otro modo, la DF $X \rightarrow Y$, se cumple en R si para dos tuplas cualesquiera $t_1$ y $t_2$ de r(R), r una instancia cualquiera de R, ocurre lo siguiente:

$$t_1[X] = t_2[X]\ \Rightarrow t_1[Y] = t_2[Y]$$

Con esto podemos redefinir a una **clave candidata** sobre R:

Sea $R(A_1, A_2, \cdots, A_n)$ un esquema de relación y sean X e Y subconjuntos de {$A_1, A_2, \cdots, A_n$}. Si X es una clave candidata de R, es decir,

$$t_1[X] \ne t_2[X]\ \forall\ i, j, i \ne j \text{ para cualquier instancia de r(R)} \Rightarrow X \rightarrow Y\ \forall\ X, Y \subseteq R$$

### Reglas de inferencia
Una DF $X \rightarrow Y$ es inferida a partir de un conjunto de dependencias F especificado sobre R si $X \rightarrow Y$ se cumple en cada instancia de relación legal r(R).

Para determinar estas dependencias inferidas se tiene un **conjunto de reglas de inferencia (llamadas axiomas de Armstrong)**:

* IR1 Reflexividad: $X \supseteq Y \models X \rightarrow Y$
* IR2 Aumentación: $X \rightarrow Y \models XZ \rightarrow YZ$
* IR3 Transitividad: $X \rightarrow Y, Y \rightarrow Z \models X \rightarrow Z$
* IR4 Descomposición o proyección: $X \rightarrow YZ \models X \rightarrow Y$
* IR5 Unión: $X \rightarrow Y, X \rightarrow Z \models X \rightarrow YZ$
* IR6 Pseudotransitividad: $X \rightarrow Y, WY \rightarrow Z \models WX \rightarrow Z$

> El conjunto formado por las reglas IR1, IR2 e IR3 es correcto y completo.

> Usamos $A \models B$ para notar que B se infiere de A.

### Análisis
Observando una instancia no es posible afirmar que dependencias funcionales se cumplen sobre un esquema de relación R. Pero sí se puede afirmar que algunas dependencias funcionales no se cumplen. La única forma de definir correctamente las dependencias funcionales es analizando el significado de los atributos.

### Dependencia Funcional Total o Parcial
Sea $R(A_1, A_2, \cdots, A_n)$ un esquema de relación y sean X e Y subconjuntos de $\set{A_1, A_2, \cdots, A_n}$.

Una dependencia funcional $X \rightarrow Y$ es **TOTAL** si la eliminación de algún atributo A de X implica que la dependencia resultante ya no se cumple, es decir, para algún atributo $A \in X$, $(X-\set{A}) \rightarrow Y$ ya no se cumple.

Una dependencia funcional $X \rightarrow Y$ es **PARCIAL** si algún atributo $A \in X$ puede ser eliminado de X y la dependencia resultante se sigue manteniendo, $(X-\set{A}) \rightarrow Y$ en R.

### Clausura de conjunto de DF's
Sea *F* un conjunto de DFs especificadas sobre un esquema de relación R. El diseñador especifica las dependencias que son semánticamente obvias. Pero, en general, otras DFs aparte de las especificadas se cumplen en todas las instancias de relación legales que satisfacen las DFs en *F*. El conjunto de todas esas DFs se denomina **CLAUSURA DE F** y se denota $\bf{F^+}$.
$$F^+ = \set{X \rightarrow Y / F \models X \rightarrow Y}$$

### Clausura de conjunto de atributos
Se define a la clausura de un conjunto de atributos X de un esquema de relación R con respecto de un conjunto F de DFs como $X_F^+$.
$$X_F^+ = \set{A \in R / F \models X \rightarrow A}$$
$$F \models X \rightarrow Y\ sii\ Y \subseteq X^+$$

### Equivalencia de conjuntos de DF's
<u>Definición 1:</u> Un conjunto de DF's F se dice que **cubre** a otro conjunto de DF's E ($F \models E$) si cada DF en E está también en $F^+$, es decir, si cada DF en E puede ser inferida desde F; alternativamente se dice que "E es cubierto por F".

> Podemos determinar si F cubre a E calculando $X_F^+$ para cada DF A $X \rightarrow Y$ en E y luego chequeando que en $X_F^+$ esté Y. Si esto se cumple $\forall A, A \in E$ entonces F cubre a E.

<u>Definición 2:</u> Dos conjuntos de DF's Ey F son equivalentes ($E \equiv F$) si $E^+ = F^+$. La "equivalencia" implica que cada DF en E puede ser inferida de F y cada DF en F puede ser inferida de E. Es decir, E es equivalente a F si ambas condiciones (E cubre a F y F cubre a E) se cumplen.

> Utilizando esta última afirmación y la forma de verificar si un conjunto de DF's cubre a otro se puede verificar que dos conjuntos sean equivalentes.

### Conjunto minimal de DF's
Sea $F_{min}$ la cobertura minimal de F, entonces cada DF en F está en $F_{min}^+$. Si alguna DF cualquiera de $F_{min}$ es eliminada, entonces ya no se cumple que cada DF en F esté en $F_{min}^+$. $F_{min}$ no es único, puede haber varios.

#### Pasos
1. Cada DF tiene del lado derecho un único atributo (Regla de la descomposición).
2. Cada DF no tiene del lado izquierdo atributos redundantes ($B\subset X$ es redundante para $X \rightarrow A$ si $A \in (X-B)^+$).
3. No contiene DF's redundantes (en general las que se obtienen por transitividad). $X \rightarrow A$ es redundante si $(F-\set{X \rightarrow A}) \equiv F$ (para determinar esto basta con ir removiendo uno a uno y verificando si el resultado cubre al conjunto original).