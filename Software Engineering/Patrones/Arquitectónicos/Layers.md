# Layers
## Contexto
Todos los sistemas experimentan la necesidad de desarrollar porciones del mismo de manera independiente. Para ello, los developers necesitan una documentación clara de la separación de responsabilidades de los módulos, para que éstos puedan ser mantenidos y desarrollados de manera independiente.

## Problema
El software necesita ser segmentado de manera que los módulos puedan ser desarrollados de manera independiente con una pequeña interacción entre ellos, soportando portabilidad, [[Encapsulamiento|encapsulamiento]], [[FURPS+#Mantainability|reusabilidad y modificabilidad]].
- Minimizar el efecto de los cambios en el sistema ([[Bajo acoplamiento|bajar el acoplamiento]]).
- Evitar mezclar la lógica de aplicación con la interfaz de usuario así esta puede ser reusada o distribuida.

## Solución
- Organizar la estructura a gran escala de un sistema en capas discretas con responsabilidades dintinguibles y relacionadas con una [[Separación de concerns|separación de concerns]] limpia y [[Cohesión|cohesiva]] de manera que las capas más bajas son de más bajo nivel y proveen servicios más generales, y las capas más altas son más específicas.
- La colaboración y el [[Acoplamiento|acoplamiento]] son de arriba hacia abajo, el acoplamiento de abajo hacia arriba es evitado.
Una capa es un elemento a gran escala, usualmente compuesto por una serie de paquetes o subsistemas.
El patrón Capas se relaciona con la [[Software Architecture#Views|logical architecture]], ya que describe la organización conceptual de los elementos de diseño en grupos, independientes de el empaquetamiento físico o deployment.
El patrón define un modelo general de N niveles para la [[Software Architecture#Views|logical architecture]], produce una **arquitectura de capas**.

## Descripción
Se organiza el sisteam en módulos/[[Componente|componentes]] con funcionalidad relacionada. Cada capa se organiza sobre los servicios de la inmediata inferior.

### Capas típicas
- Presentation:
	- GUI windows
	- reports
	- speech interface
	- HTML, XML XSLT, JSP, JS
- Application
	- handles presentation layer requests
	- workflow
	- session state
	- window/page transitions
	- consolidation/transformation of disparate data for presentation
- Domain
	- handles application layer requests
	- implementation of domain rules
	- domain services
	- Eg.: *POS, Inventory*
- Business Infrastructure
	- very general low-level business services
	- used in many business domains
	- Eg.: *CurrencyConverter*
- Technical Services:
	- (relatively) high-level technical services and [[Framework|frameworks]].
	- Eg.: *Persistence Security*
- Foundation
	- los-level technical services, utilities and [[Framework|frameworks]].
	- data structures, threads, math, file, DB, and network I/O.

## Usos
Agregar funcionalidad sobre servicios core, distribución del desarrollo, se requiere seguridad multinivel.

## Ventajas
[[FURPS+#Mantainability|Mantenibilidad, Modularidad y Testeabilidad]]

## Desventajas
- [[FURPS+#Performance|Performance]] (se puede sortear con salteo de capas)

## Cualidades
- Separación e independencia entre capas (modularidad, encapsulamiento, [[FURPS+#Mantainability|mantenibilidad]]).
- Cada capa se construye sobre los servicios y recursos de la inmediata inferior (reusabilidad).
- El cambio en una capa afecta solamente a su capa adjunta ([[Acoplamiento]]).