%%[[Inteligencia Artificial]]%%
Lisp es el primer [[Lenguajes|lenguaje de programación funcional]] creado por John McCarthy. Lisp es una familia de lenguajes de programación de propósito general de [[Sintaxis|sintaxis]] simple y extraordinaria potencia.

* Todo programa consiste en una función.
* No posee asignaciones.
* La principar estructura de control es la recursión.
* Los [[Programa|programas]] y los [[Dato, información y conocimiento|datos]] son equivalentes.
* La principal estructura de datos es la lista.
* El código es estructurado en listas.
* La memoria es asignada por demanda.

## Expresiones en LISP
Un programa es un conjunto de **s-expresiones** (expresiones simbólicas). Una s-expresión es una notación en forma de texto para representar una estructura de datos de árbol, basada en lista anidadas, en donde cada sublista es un subárbol.

* Las s-expresiones pueden ser átomos o listas.
* Un átomo puede ser numérico o simbólico (1,2,3 son átomo numéricos y +, * son átomos simbólicos).
* Las expresiones aritméticas se denotan en forma prefija (notación polaca).

Para evaluar una s-expresión **S** se siguen las siguientes reglas:
* Si **S** es un átomo numérico *a* entonces el resultado es simplemente *a*.
* Si **S** es de la forma $(f\ a_1\  a_2\  ... \  a_n)$ entonces el intérprete evalúa recursivamente cada argumento $a_i$, obteniendo valores $v_1, v_2, ..., v_n$ y luego calcula el resultado de aplicar **f** a dichos valores.

## Celdas CONS
Una celda **cons** se compone de dos punteros (car.cdr). **car** y **cdr** son operaciones primitivas sobre las celdas **cons** (o "s-expresiones no atómicas") car extrae el primer puntero, y cdr extrae el segundo.

>**(car (cons x y))** se evalúa como x
>**(cdr (cons x y))** se evalúa como y