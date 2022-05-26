---
aliases: ["gramáticas regulares", "gramática regular"]
---
Los lenguajes representados por este tipo de gramáticas se denominan [[lenguajes regulares]]. **Un lenguaje se dice regular si existe una gramática regular que lo genere.**

Estas gramáticas se clasifican en los dos grupos siguientes:

### Gramáticas lineales por izquierda
Cuyas reglas de producción tendrán la forma:

A ::= a,  A ::= Ba,  A ::= λ  (donde $A,B \in V_N ; a \in V_T$) 

### Gramáticas lineales por derecha
Cuyas reglas de producción tendrán la forma:

A ::= a,  A ::= aB,  A ::= λ  (donde $A,B \in V_N ; a \in V_T$) 