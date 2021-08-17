Un framework es una aplicación reusable y "semi completa", que puede ser especializada para integrarse a otra aplicación. Es una colección de clases que en conjunto constituyen una solución genérica, a una familia de requerimientos de un [[Dominio|dominio]] específico.

## Objetivo
El objetivo de un framework es el de construir aplicaciones componiendo piezas de software reusables.

## Consecuencias
Las consecuencias de el uso adecuado de frameworks son:
- Mayor productividad: se construye más software en menos tiempo ya que tenemos más componentes reutilizables.
- Mayor calidad: los componentes reusados son más confiables ya que han sido validados mediante pruebas y son más maduros.
- Mejora el mantenimiento: siempre que se utilicen componentes de software correctamente diseñados ya que hay menos código para mantener (siempre que el framework no sea candidato de generar fallas).
En términos de atributos de calidad si es un framework maduro y provado por la industria favorece [[FURPS+#Reliability]] y la [[FURPS+#Mantainability]]. Los otros atributos se pueden ver favorecidos o perjudicados según el diseño del framework y el uso que se le esté dando.

### Ventajas
 - Reutilización de código y diseño.
 - Mejora la calidad.
 - Puede simplificar la programación de un sistema.

### Desventajas
- Depende del lenguaje.
- Se complejiza el proceso de debug.
- Hay una curva de aprendizaje.
- Integración de múltiples frameworks.

## Reglas de diseño
- Keep it simple.
- Minimizar métodos hooks.
- Identificar clases internas (final).
- Uso de convenciones: naming, get/set, is/as, reset, etc.
- Evitar overloading (minimizar la cantidad de métodos y parámetros).
- Código defensivo: validaciones, excepciones, ciclo de vida, etc.
- No conocer dependencias. Fácil de aprender.
- Documentación. Diagramas y cookbook/how to.

## Diseño
- Framework por herencia (caja blanca) el usuario se abstrae de las clases del framework y simplemente hereda de ellas ([[Template Method]]). Estos son los más usados.
- Framework por composición (caja negra).

### Principio Hollywood
"Don't call us, we'll call you" (Inversión de control)
Esto significa que las clases definidas por el usuario recibirán mensajes de las clases predefinidas por el framework.

## Usuarios
Los usuarios de un framework son developers por lo tanto el framework se debe diseñar de manera que le facilite la vida al usuario.