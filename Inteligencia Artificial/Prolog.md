El Prolog (del francés **Pro**grammation en **log**ique) es un [[Lenguajes|lenguaje de programación]] del paradigma lógico y declarativo basado en la [[Lógica de predicados|lógica de predicados]]. Es un lenguaje históricamente ligado con la [[Inteligencia Artificial]].

En Prolog no existen estructuras de control. su ejecución se basa en los conceptos de **unificación** y **backtracking**. Y la representación de la información/conocimiento es mediante predicados. Un programa escrito en Prolog se constituye de hachos y reglas del tipo "modus ponens" (si es verdad el antecedente, entonces es verdad el consecuente) que se transforman a la forma casual y luego a cláusulas de Horn (muchos antecedentes un solo consecuente).

El Prolog funciona como una gran [[Bases de Datos/Bases de Datos|base de datos]] que maneja datos y reglas.

## Programa Prolog
Cada línea de programa es una **cláusula**. Un **hecho** representa una unidad de información que se asume como verdadera. Una **regla** representa un aserto condicional.

Un **programa Prolog** es un conjunto finito de cláusulas de la forma $A:-\ B_1,B_2,\cdots,B_m.$ Siendo $A,B_1,B_2,\cdots,B_m.$ fórmulas atómicas.
La fórmula atómica $A$ se llama **cabeza** de la cláusula y $(B_1,B_2,\cdots,B_m)$ se llama **cuerpo** de la cláusula. Si m = 0, entonces la cláusula, con el símbolo ":-" omitido, se llama la **cláusula unitaria (hecho)**.

### Expresión
En una expresión $f(T_1,T_2,\cdots,T_n)$, **f** es llamado **functor** o **símbolo funcional**, **n** es la **ariedad** y $T_1,T_2,\cdots,T_n$ son los **términos**. Un término es una variable, una constante o una expresión de la forma antes mencionada.

### Fórmula atómica
Una **fórmula atómica** es una expresión de la forma $p(T_1,T_2,\cdots,T_n)$ donde **p** es un **símbolo predicativo** y  $T_1,T_2,\cdots,T_n$ son términos. 

La distinción entre símbolo predicativo y símbolo funcional yace que en una expresión el símbolo predicativo es el más externo.

### Unificación
En el paradigma lógico no está incluido el concepto de **asignación**, una asignación permite “destruir” el valor que tiene una variable en un momento dado y reemplazarlo por otro. Las variables en el paradigma lógico se asemejan a la idea de variable matemática, y el mecanismo por el cual se le dan valores a las variables se llama **unificación**. Cuando una variable que no tiene ningún valor pasa a tenerlo se dice que dicha variable a sido **instanciada**, en caso contrario la variable se encuentra **no instanciada**. La unificación puede ser implícita o se puede realizar utilizando el símbolo ' = ‘ (que NO representa asignación).

>La **unificación** es el proceso por el cual dos términos pueden ser considerados equivalentes.

>La **instanciación**  es el proceso por el cual una variable (local a una cláusula) toma un valor. Es un caso de unificación en la que a una variable no instanciada se le asigna un valor.

Reglas de unificación:
* Una variable no instanciada unifica con cualquier término.
* Dos constantes unifican solo si son idénticas.
* Dos estructuras unifican si tienen igual functor e igual aridad y cada uno de los términos de sus argumentos unifican.
* Dos términos son unificables si ellos pueden hacerse idénticos.

### Asignación
Las expresiones aritméticas se realizan y unifican mediante el predicado **'is'**. No es un predicado lógico, con lo cual tendrá ciertas restricciones. El predicado 'is' unifica el primer argumento, con el valor calculado del segundo argumento.

### Comparación
El predicado ' =:= ' y los predicados ' < ', ' =< ', ' > ', ' >= ', '=\\=' comparan dos valores. Si alguno de los términos representa una operación matemática, previamente realiza la operación.

El predicado ' == ' representa la **identidad** (ambos valores deben ser idénticos), **no realiza cálculos matemáticos**. ‘\\== ‘ no idéntico

### Backtracking
Proceso por el cual cuando un predicado no se puede satisfacer permite buscar otra opción o retroceder a un predicado anterior.

### Lectura procedural
La lectura procedural de un programa Prolog, hace significante el orden de las cláusulas, y el orden de las submetas en cada cláusula. Cuando un programa Prolog es leído proceduralmente, las roles de la entrada-salida de variables son explícitamente indicados. De esta manera el programa Prolog pierde alguna flexibilidad en beneficio de la eficiencia.

Dada una cláusula Prolog: A:-B1,B2,...,Bn.
Declarativamente la cáusula se lee: "A si B1 y B2 y ... y Bn"
Si consideramos que represanta un **proceso**, se leerá: "Para hacer A, hacer B1, entonces B2, ... , entonces Bn"

El programa no contiene construcciones explícitas para ciclos y bifurcaciones. Las bifurcaciones se realizan mediante cláusulas alternativas, y los ciclos por recursión. En el programa Prolog, no hay declaración de datos, ni asignaciones. La construcción de datos, la asignación de variables, y el pasaje de parámetros son realizados por procesos de unificación.

Cuando hay necesidades de generar ciclos, se puede forzar el backtracking mediante el predicado incorporado *fail*.

La ejecución de un programa Prolog comienza con una pregunta considerada como meta principal. Para evaluar esa meta busca una cláusula tal que pueda unificar todas las variables. La meta es reemplazada por la cabeza de la cláusula, y todas las variables son instanciadas por la substitución obtenida, generando nuevas metas (o submetas).

El proceso de unificación continúa, hasta que una de las siguientes situaciones ocurre:
* La nueva meta es la **meta vacía**, como resultado de unificar con un **hecho**.
	* La meta inicial **sucede**.
	* El sistema compone todos los unificadores obtenidos para retornar una respuesta.
* La nueva meta no es unificable con la cabeza de ninguna cláusula en el programa.
	* El sistema retrocede a la meta precedente, y busca otra forma alternativa de ejecución.
	* El proceso se repite hasta que sucede o una falla total ocurre (es decir, no encuentra más cláusulas para unificar, y no hay metas anteriores sobre las que pueda retroceder).

El proceso utilizado en cada paso (cláusula) se llama **resolución**, y el proceso en conjunto se llama **deducción por resolución**.

#### Orden de metas y cláusulas
* Si una variable ya está instanciada, no puede instanciar con otro valor. Esta es la llamada **propiedad de unicidad referencial**. 
* El orden de las metas indica el orden en que los procesos serán ejecutados.
* El orden de las cláusulas controla el orden en se producen las ramificaciones.
* No es importante el orden de los procedimientos, si de las cláusulas dentro de cada procedimiento.

### Control de ejecución