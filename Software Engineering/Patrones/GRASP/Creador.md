## Problema
¿Quién debería ser el responsable de la creación de una nueva instancia de alguna clase?

## Solución
B es una Creador de A, si se asigna a la clase B la [[Responsabilidad|responsabilidad]] de crear una instancia de la clase A, y se cumple uno o más de estos casos:
- B [[Relaciones entre clases#Agregación|agrega]] objetos de A.
- B [[Relaciones entre clases#Composición|contiene]] objetos de A.
- B registra o persiste instancias de objetos de A.
- B utiliza más estrechamente objetos de A.
- B tiene los datos de inicialización necesarios al momento de crear A.

## Ventajas
- [[Bajo acoplamiento]]
- [[Mantainability|Mantainability]]
- Reutilización

## Desventajas
Las funciones de creación pueden ser complejas, en cuyo caso se recomienda [[Patrones GoF|patrones GoF]] del tipo [[Factory|Factory]].