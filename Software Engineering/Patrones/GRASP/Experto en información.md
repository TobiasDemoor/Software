## Problema
¿Cuál es el principio general para asignar responsabilidades a los objetos?
¿Quién debería ser el responsable de conocer la información?

## Solución
Asignar a la clase que tiene toda la información necesaria para realizar una [[Responsabilidad|responsabilidad]], el experto de información.

## Ventajas
- Favorece el [[Encapsulamiento|encapsulamiento]].
- Y la [[Alta cohesión|alta cohesión]].

## Desventajas
En ocasiones, la respuesta que nos da este patrón no es deseable ya que puede generar objetos poco reusables. Por ejemplo por experto de información una entidad sería responsable de persistir sus datos ya que tiene toda la información necesaria.