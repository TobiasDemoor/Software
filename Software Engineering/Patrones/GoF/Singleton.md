## Problema
¿Cómo garantizar que una clase tenga solo una instancia y proporcionar un punto de acceso global a ella ([[Visibilidad#Visibilidad entre objetos]])?

## Solución
Definir un método *static* en la clase X que retorna el Singleton de X.

## Motivación
- Se requiere que algunas clases tengan solo una instancia en memoria ([[Factory|Factories]], [[Facade]], [[Strategy]]).
- Facilitar acceso y [[Visibilidad#Global|visibilidad global a un objeto]]. En cualquier punto del código, en cualquier método de cualquier clase se puede invocar SingletonClass.getInstance().

## Implementación
Se requiere anotar el método getInstance como synchronized para soportar multithreading o inicializar el campo instance en su declaración. Ambos métodos tienen sus ventajas y desventajas.