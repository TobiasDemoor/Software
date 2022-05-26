---
aliases: ["expresiones regulares", "regular expresions", "expresión regular", "regular expresion", "regex"]
---
Las expresiones regulares pueden considerarse como una forma alternativa de descripción de [[lenguajes regulares]], con la ventaja de ser fáciles de entender y describir.

Un lenguaje es **regular** si existe una expresión regular que lo describa. **Todo lenguaje finito es regular.**

- $\emptyset$ es una ER (la expresión nula)
- $\lambda$ es una ER (siendo $\lambda$ el símbolo nulo)
- Si $a \in A$ y A es el alfabeto => a es una ER (cualquier símbolo es una ER) 
- Si $a$ y $b$ son ER => $ab$ es ER (concatenación)
- Si $a$ y $b$ son ER => $a|b$ es ER (se lee como $a$ o $b$)
- Si $a$ es ER => $a^{*}$ es ER (clausura, cualquiér repetición de $a$) 
- Si $a$ es ER => $a^{n}$ es ER (clausura n-esima, $a$ concatenado n veces) 

- $[a|b] \equiv (a|b|\lambda)$

#### Ejemplos en la programación
La ER $(a|b|...|z|0|1|...|9|\_|-)^n, n \in [6,18]$
``` js
"/^[a-z0-9_-]{6,18}$/"
```