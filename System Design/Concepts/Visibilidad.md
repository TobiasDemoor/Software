# Visibilidad entre objetos
Se entiende por **visibilidad** a la capacidad de un objeto de ver o tener referencia a otro objeto. Hay 4 formas cuando se está en el mismo espacio de memoria:
- De atributo: la visibilidad de atributo desde A a B se da cuando B es un atributo de A. Es un tipo de acoplamiento muy fuerte que debe desprenderse del [[Dominio|dominio]].
- Paramétrica: la visibilidad paramétrica desde A a B se da cuando B se pasa como parámetro a un método de A. Es un tipo de acoplamiento muy fuerte.
- Local: la visibilidad local desde A a B se da cuando B se declara como un objeto local dentro de un método de A. "Una barbaridad" - (Fernando Soriano, 2021)
- Global: La bisibilidad global desde A a B se da cuando B es un objeto global para A. No es buena práctica el uso de objetos globales. Una forma de implementar esto es mediante el patrón [[Singleton]].