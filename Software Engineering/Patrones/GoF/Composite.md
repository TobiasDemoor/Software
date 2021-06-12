## Problema
¿Cómo tratar un grupo o estructura de composición de objetos de la misma manera ([[Software Engineering/Patrones/GRASP/Polimorfismo|polimorfica]]) como a un objeto no compuesto (atómico)?

## Solución
Definir clases para los objetos compuestos y atómicos tal que implementen la misma interfaz.

## Propósito
Componer objetos de complejidad mayor mediante otros más sencillos de forma recursiva.

## Motivación
- Cuando se necesite manejar de igual forma objetos sencillos o agrupaciones de éstos.
- Se necesite representar jerarquías de objetos (árbol).