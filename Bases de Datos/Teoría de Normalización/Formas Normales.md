Las formas normales son listadas en orden creciente de restricción. Una contiene a sus siguientes, y para afirmar que un esquema se encuentra en una forma normal se debe demostrar que no se encuentra en la siguiente.

En todas las formas normales se presentan anomalías pero se van reduciendo a medida que se pasa a formas más restrictivas.

### 1ª Forma Normal (1FN)
Es parte de la definición formal de una [[Modelo Lógico Relacional|relación]]. Evita atributos multivaluados y compuestos (relaciones adentro de relaciones). Establece que en un esquema de relación los dominios de los atributos deben incluir únicamente valores atómicos, es decir, indivisibles.

### 2ª Forma Normal (2FN)
R está en 2ª Forma Normal si cada [[Atributos primos|atributo no primo]] de R [[Dependencia Funcional#Dependencia Funcional Total o Parcial|depende funcionalmente en forma total]] de cada clave de R (cada atributo no primo no es parcialmente dependiente de alguna clave de R). 

### 3ª Forma Normal (3FN)
Sea $R(A_1, A_2, \cdots, A_n)$ un esquema de relación y sean X e Y subconjuntos de $\set{A_1, A_2, \cdots, A_n}$, A atributo de R.

R está en 3FN si para cada dependencia funcional $X \rightarrow A$ definida sobre R, si cumple una de las dos o ambas:
	a. X es superclave de R.
	b. A es atributo primo de R.
	
### Forma Normal de Boyce-Codd (FNBC)
R está en FNBC si para cada dependencia funcional no trivial $X \rightarrow Y$ definida sobre R, X es superclave de R.

Una esquema de relación en FNBC básicamente no presenta anomalías (al menos significativas). Un esquema de relación se puede descomponer en subesquemas para hacer que cumplan con FNBC. Y se puede asegurar una buena calidad de diseño.
