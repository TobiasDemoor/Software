El [[Modelo Lógico Relacional]] incluye un lenguaje formal que es el álgebra relacional (AR), las consultas realizadas en este se llaman formalmente **queries**.

El AR es considerada como parte integral del modelo relacional por diversos motivos. Ya que es la base formal para los lenguajes de consulta que son utilizados por el usuario fina y permite dar un procedimiento de resolución para estas, y también debido a que es utilizado por el [[DBMS]] para la optimización de consultas.

## Operadores especificos para RDB
Son operadores unarios.

### SELECCIÓN ($\sigma$)
$\sigma_{<condición>} (R)$: Selecciona las tuplas que cumplen con la condición de selección.

La cardinalidad de la selección siempre es menor o igual a la cardinalidad de la instancia de relación original. Y la selección mantiene el grado de R.

$<condición>$: es una expresión booleana sobre los atributos de R, conformada por cláusulas de la forma,
\<nombre_atributo> \<op_comparación> \<ctte> o
\<nombre_atributo> \<op_comparación> \<nombre_atributo>

*Es conmutativa:*
$$\sigma_{<condicion 2>} (\sigma_{<condicion 1>} (R)) = \sigma_{<condicion 1>} (\sigma_{<condicion 2>} (R))$$

*Cascada:*
$$\sigma_{<c1>} (\sigma_{<c2>} (\cdots\ (\sigma_{<cn>} (R))\cdots)) (R) = \sigma_{<c1>\ AND\ <c2>\ AND\ \cdots\ AND\ <cn>} (R)$$

*Selectividad de la condición:* fracción de tuplas selecionadas.

### PROYECCIÓN ($\pi$)
$\pi_{<lista atributos>} (R)$: Proyecta la relación sobre los atributos de la lista de atributos. El resultado tiene solo los atributos de la lista de atributos (en ese orden).

La cardinalidad de la proyección es menor o igual a la cardinalidad de la instancia de relación original, es menor en el caso que luego de aplicada la proyección se repitan tuplas (no se pueden repetir tuplas por ende se suprimen). El grado de la proyección es la cantidad de atributos en la lista de atributos.

No es conmutativa, ya que no se quiere aplicar una proyección con atributos en la lista que no están en R.

### RENOMBRAMIENTO ($\rho$)
$\rho_{S(B1,\ B2,\ \cdots,\ Bn)}$: renombra la relación y los atributos.
$\rho_{S}$: renombra solo la relación.

Ejemplo:
$$ES(nom) \leftarrow \pi_{nombre}(\sigma_{sueldo>20000}(Empleado))$$
Más formalmente:
$$\rho_{ES(nom)}(\pi_{nombre}(\sigma_{sueldo>20000}(Empleado)))$$

### JUNTA ($\Join$)
$Q \leftwarrow S \Join{<condición>} R$: Permite combinar tuplas que están en distintas relaciones, es decir, procesar vinculaciones entre relaciones. Q tendrá una tupla por cada combinación de tuplas de R y S que cumplan con la condición de Junta. Se puede expresar de la siguiente manera:
$$S \Join{<condición>} R = \sigma_{<condición>}(S\ X\ R)$$

Por defecto se toma junta interna.

Inner join: $\Join$
Right outer join: ⟖
Left outer join: ⟕
Full outer join: ⟗

#### JUNTA NATURAL
No tiene una condición explicita sino que compara por igual los atributos de mismo nombre. El resultado elimina una columna de cada par de columnas igualadas.

#### JUNTA THEETA
En una JUNTA THEETA la condición es Ai θ Bj y theta es uno de los operadores {=, <, ≤, >, ≥, ≠}. Un caso particular de esta esla EQUI JUNTA donde θ es =.

### DIVISIÓN ($\div$)
Se aplica sobre R(Z) y S(X), donde $X \subseteq Z$, $T \leftarrow R \div S$. Lista las tuplas de R con atributos de R que no esten en S, los cuales se encuentran presentes con cada valor de tupla en S.

Ejemplo 1:
Listar los nombres de los empleados que trabajaron en todas las plantas de Córdoba.

Ejemplo 2:
![[algebra_relacional_division_1.png]]

## Operadores de conjunto
Son operadores binarios.

### UNIÓN, INTERSECCIÓN y DIFERENCIA ($\cup, \cap, -$)
Deben ser compatibles para la unión, es decir tener el mismo grado y cada correpondiente par de atributos en una y otra relación, tener el mismo dominio.

$R \cup S$: tuplas que están en R o S o en ambas.
$R \cap S$: tuplas que están en R y en S.
$R - S$: tupls que están en R pero no están en S.

> <u>Convención:</u> los atributos de la relación resultante tienen el mismo nombre que los de la relación R.

### PRODUCTO CARTESIANO($\times$)
Combina cada tupla de una relación con cada tupla de la otra relación.
$$Q \leftarrow R(A_1, A_2, \cdots, A_n)\ \times S(B_1, B_2, \cdots, B_n)$$
$$Q (A_1, A_2, \cdots, A_n, B_1, B_2, \cdots, B_n)$$
 La cardinalidad del resultado es el producto de las cardinalidades de las relaciones iniciales. El grado del resultado es la suma de los grados de las relaciones iniciales.
 
 grado(Q) = n + m y cardinalidad(Q) = |Q| = |R| * |S|


## Conjunto completo de operaciones AR
El conjunto {$\sigma, \pi, \cup, \rho, -, \times$} es un **conjunto completo**, es decir que cualquiera de las otras operaciones del AR puede expresarse en función de estos operadores básicos.