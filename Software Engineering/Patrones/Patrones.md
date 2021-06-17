Un patrón es una solución a un problema recurrente en un contexto particular. Tienen un nombre con el cual referirise al patrón. Enseñan y permiten entender cómo adaptarlo a la variante particular del problema donde se quiere aplicar. Facilitan la reutilización de diseños y [[Arquitectura de software|arquitecturas]] de software que han tenido éxito.

# Motivación a usarlos
- Fomentan la reutilización de arquitecturas y código.
- Capturan la experiencia y la hacen accesible a los no expertos.
- El conjunto de sus nombres forman un vocabulario que ayuda a que los desarrolladores se comuniquen mejor.
- Ayudan a la gente a comprender un sistema más rápidamente cuando está documentado con los patrones que usa.
- Facilitan la reestructuración de un sistema tanto si fue o no concebido con patrones en mente.

# Clasificación
Las categorías definidas por el libro *Pattern-Oriented Software Architecture* (1996), ofrecen una simple y útil categorización de patrones en 3 niveles distintos:
1. [[Patrones arquitectónicos]]: relacionados al diseño grueso y de gran escala ([[Arquitectura de software]], y típicamente aplicados durante las iteraciones más tempranas ([[Unified Process#Elaboration]]) cuando las conexiones y estructuras principales son establecidas. Por ejemplo:
	- El patrón [[Layers]] que estructura un sistema en capas principales.
2. Patrones de diseño: relacionados al diseño de mediana o pequeña escala de objetos ([[Diseño de objetos]]) y [[Framework|frameworks]]. Aplicable a diseñar una solucion para conectar los elementos de gran escala definidos mediante patrones arquitectonicos y durante el diseño detallado para cualquier aspecto de diseño local. También son conocidos como patrones micro-arquitectónicos. Por ejemplo:
	- El patrón [[Facade]], que nos permite proveer una [[Interfaz|Interfaz]] de una capa a otra.
	- El patrón [[Strategy]], para permitir algorítmos intercambiables.
3. Idioms (o patrones elementales): soluciones de diseño de bajo nivel orientadas al lenguaje o a la implementación. Por ejemplo:
	- El patrón [[Singleton]], para permitir el acceso global a una sola instancia de una clase.
Hay otras categorías que podemos construir fuera de las POSA:
- Enterprise patterns. Arquitectónicos + diseño (Martin Fowler)
	- Por ejemplo [[Data mapper]].
- Patrones de análisis (S. Ambler)
- Patrones de interfaz de usuario.
- Patrones de testing.