## Problema
¿Cómo diseñar algoritmos que pueden cambiar pero relacionados? ¿Cómo diseñar para que un algoritmo varíe sin afectar a los que lo usan?

## Solución
Definir cada [[Algorítmo|algorítmo]]/política/estrategia en una clase separada pero con el mismo contrato ([[Interfaz]]).

## Motivación
- Variar [[Algorítmo|algorítmos]] en tiempo de ejecución ([[Variaciones protegidas]]).
- La elección del [[Algorítmo|algorítmo]] a usar es transparente al cliente.

## Notas
- Es un ejemplo del GRASP [[Fabricación pura]].