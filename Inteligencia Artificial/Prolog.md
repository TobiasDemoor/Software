El Prolog (del francés **Pro**grammation en **log**ique) es un [[Lenguajes|lenguaje de programación]] del paradigma lógico y declarativo basado en la [[Lógica de predicados|lógica de predicados]]. Es un lenguaje históricamente ligado con la [[Inteligencia Artificial]].

En Prolog no existen estructuras de control. su ejecución se basa en los conceptos de **unificación** y **backtracking**. Y la representación de la información/conocimiento es mediante predicados. Un programa escrito en Prolog se constituye de hachos y reglas del tipo "modus ponens" (si es verdad el antecedente, entonces es verdad el consecuente) que se transforman a la forma casual y luego a cláusulas de Horn (muchos antecedentes un solo consecuente).

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
El predicado ' =:= ' y los predicados ' < ', ' =< ', ' > ', ' >= ', comparan dos valores. Si alguno de los términos representa una operación matemática, previamente realiza la operación.

El predicado ' = = ' representa la **identidad** (ambos valores deben ser idénticos), **no realiza cálculos matemáticos**. ‘\\== ‘ no idéntico

### Backtracking
Proceso por el cual cuando un predicado no se puede satisfacer permite buscar otra opción o retroceder a un predicado anterior.