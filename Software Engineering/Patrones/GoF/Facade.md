## Problema
¿Cómo minimizamos la complejidad en la relación entre subsistemas, minimizando comunicaciones y dependencias entre estos?

## Solución
Creamos una clase Facade que haga de punto de entrada para las funcionalidades que deben ser expuestas.

## Ventajas
- Para modificar las clases de los subsistemas, sólo hay que realizar cambios en la clase Facade, y los clientes pueden permanecer ajenos a ello.
- Los clientes no necesitan conocer las clases que hay tras dicha [[Interfaz|Interfaz]] ([[Bajo acoplamiento]]).

## Notas
- En determinadas ocasiones puede ser conveniente que la clase Facade sea un [[Singleton]].
- Este patrón tiene una similitud comparable con el GRASP [[Controlador]].