## Problema
¿Cómo evitar validación de tipos y/o crear componentes conectables?

## Solución
Cuando los comportamientos relacionados varíen según la clase utilice [[Concepts/Polimorfismo|operaciones polimórficas]].

## Ventajas
- Es más simple añadir nuevas variantes de funcionalidad.
- El agregar funcionalidad no afecta a otras clases.

# Nota
Este patrón está fuertemente relacionado al GRASP [[Variaciones protegidas]].