## Problema
¿Quién sería el responsable de crear objetos cuando se desea mantener cohesividad, hay consideraciones especiales o lógica compleja para realizarlo?

## Solución
Delegar la [[Responsabilidad|responsabilidad]] a un Factory.

## Motivación
- Una clase no desea conocer sobre la creación de objetos relacionados.
- Una clase desea que sus subclases definan qué objeto crear.
- Otorgar flexibilidad a la creación de objetos.

## Ventajas
- [[Separación de concerns|Separa la responsabilidad]] de creaciones complejas en objetos cohesivos.
- Oculta la complejidad de la lógica de creación.
- Permite optimización de recursos como caché de objetos en memoria.

## Notas
- Es un ejemplo del GRASP [[Fabricación pura]].
- Es una forma de aplicar el GRASP [[Creador]].
- Es una manera de lograr mayor flexibilidad del software ([[Variaciones protegidas]]).