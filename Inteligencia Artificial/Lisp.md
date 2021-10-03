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
* Un átomo puede ser numérico, string o simbólico.
* Las expresiones aritméticas se denotan en forma prefija (notación polaca).

Para evaluar una s-expresión **S** se siguen las siguientes reglas:
* Si **S** es un átomo numérico *a* entonces el resultado es simplemente *a*.
* Si **S** es de la forma $(f\ a_1\  a_2\  ... \  a_n)$ entonces el intérprete evalúa recursivamente cada argumento $a_i$, obteniendo valores $v_1, v_2, ..., v_n$ y luego calcula el resultado de aplicar **f** a dichos valores.

## Tipos de datos en Lisp
Se tienen: números, strings, listas, símbolos y funciones. Una variable tiene un **nombre**, que es una cadena de caracteres, y puede tener un valor asociado que puede  ser un número, un string o una lista. Pero además del valor, posee otros dos espacios: un **espacio de función**, y un espacio de **lista de propiedades** o plist. Las variables no tienen tipo.

Para dar un valor a una variable se utiliza la la primitiva setq.

### Símbolos
Los símbolos son  espacios de memoria que pueden contener valores tal como lo hacen las variables en otros lenguajes. Se puede ligar una expresión a un símbolo.

### Átomos
Conceptualmente, la memoria de datos a diferencia de casi todos los demás modelos, no contiene variables, sino valores. Los átomos de las que se compone no son "contenedores" de valores, sino como la idealización del valor en sí.

Si un programa Lisp necesita un valor numérico 0, encontrará dicho valor numérico en una zona de la memoria de datos. Si ahora dicho valor tiene que cambiar a 22 no sobreescribe el 0 sino que utiliza un átomo de valor 22 presente en otra zona de la memoria de datos. Si no se encuentra uno ya existente se crea.

Los átomos pueden ser de tipo numérico, pueden ser cadenas de caracteres (" ") o pueden ser símbolos (a, b, +, -, \*, etc.).

### Celdas CONS
Una celda **cons** se compone de dos punteros (car.cdr), **car** y **cdr** son operaciones primitivas sobre las celdas **cons** (o "s-expresiones no atómicas") car extrae el primer puntero, y cdr extrae el segundo.

```lisp
; (cons x y) == '(x . y)

(car (cons x y)) ; == (first (cons x y))
	x
(cdr (cons x y)) ; == (rest (cons x y))
	y
```

### Listas
```lisp
(setq lista '(a .(b .(c . nil))))
==
(setq lista '(a b c))
==
(setq (list a b c))
```
