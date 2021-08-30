# Visibilidad entre objetos
"For a sender object to send a message to a receiver object, the sender must be visible to the reciever"
Se entiende por **visibilidad** a la capacidad de un objeto de ver o tener referencia a otro objeto. Hay 4 formas cuando se está en el mismo espacio de memoria:

## De atributo
La visibilidad de atributo desde A a B se da cuando B es un atributo de A. Es un tipo de acoplamiento muy fuerte que debe desprenderse del [[Dominio|dominio]].
Es una visibilidad relativamente permanente ya que persiste mientras A y B existan.
Es la forma más común de visibilidad en sistemas OO.

## Paramétrica
La visibilidad paramétrica desde A a B se da cuando B se pasa como parámetro a un método de A. Es un tipo de acoplamiento muy fuerte.
Es una visibilidad relativamente temporal ya que solo persiste dentro del scope de un método.
Es la segunda forma más común de visibilidad en sistemas OO.

## Local
La visibilidad local desde A a B se da cuando B se declara como un objeto local dentro de un método de A. "Una barbaridad" - (Fernando Soriano, 2021)
Dos formas comunes para lograr la visibilidad local son:
- Crear una nueva instancia local y asignarla a una variable local (**new**).
- Asignar el objeto retornado por la invocación a un método a una variable local.
Es una visibilidad relativamente temporal ya que solo persiste dentro del scope de un método.
Es la tercera forma más común de visibilidad en sistemas OO.

## Global
La visibilidad global desde A a B se da cuando B es un objeto global para A. No es buena práctica el uso de objetos globales.
Una forma de lograr visibilidad global es asignar una instancia a una variable global (lo cual es posible en algunos lenguajes pero no en otros). La manera preferida de implementar esto es mediante el patrón [[Singleton]].
Es una visibilidad relativamente permanente ya que persiste mientras A y B existan.
Es la forma menos común de visibilidad en sistemas OO.