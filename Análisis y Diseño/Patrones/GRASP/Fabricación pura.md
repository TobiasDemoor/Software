## Problema
¿Cómo asignar responsabilidades cuando no se quiere perjudicar a otros patrones o principios de diseño?

## Solución
Crear una clase artificial (no del [[Dominio|dominio]]) y asignarle responsabilidades altamente [[Cohesión|cohesivas]].

## Ventajas
- Favorece a la [[Alta cohesión|alta cohesión]] agrupando comportamiento con fines puntuales.
- En algunos casos puede facilitar la reutilización de esas clases especializadas.

## Notas
Identificar una clase como una Fabricación Pura no es crítico. Es un concepto educativo para comunicar la idea general que algunas clases de software están inspiradas por representaciones del [[Dominio|dominio]] y otras son simplemente creadas para conveniencia del diseñador. Estas clases fabricadas suelen estar diseñadas para agrupar comportamientos y por lo tanto están más inspiradas por la [[Diseño de objetos|descomposición por comportamiento]].

## Patrones asociados
- [[Bajo acoplamiento]]
- [[Alta cohesión]]