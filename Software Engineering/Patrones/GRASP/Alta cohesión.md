## Problema
¿Cómo mantener manejabla la complejidad de un software?

## Solución
Asignar una [[Responsabilidad|responsabilidad]] de manera que la [[Cohesión|cohesión]] permanezca alta.

Una clase cohesiva "puede" tener pocos métodos, con funcionalidad altamente relacionada, y no realiza muchos trabjaos diferentes. Pero colabora con otros objetos para compartir el esfuerzo de una tarea compleja.

Una clase con baja cohesividad es difícil de entender, de reutilizar y de mantener.

## Ventajas
- Incrementa la claridad y facilita la comprensión del diseño.
- Simplifica el manteniemiento y las mejoras. ([[Mantainability]])
- Facilita la reutilización.

## Desventaja
Tradeoff con el [[Bajo acoplamiento|bajo acoplamiento]].