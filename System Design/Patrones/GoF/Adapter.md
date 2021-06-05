## Problema
¿Cómo resolver incompativilidad de interfaces o proveer una interfaz estable teniendo componentes similares, pero con interfaces diferentes?

## Solución
Convertir la interfaz original de un componente en otra, por medio de un objeto adaptador.

## Motivación
- Reducir dependencia entre clases. Mayor flexibilidad ante cambios en el tiempo o servicios.
- Reusar una clase existente sin su fuente, y su interfaz no concuerda con la que se necesita.

## Ventajas
- Permite que clases con interfaces incompatibles trabajen juntas.
- (clase) Permite al adaptador reusar y/o redefinir compoertamiento de la clase adaptada.
- (clase) No requiere un puntero adicional al objeto adaptado.
- (objeto) Permite que un adapter use múltiples adaptados.