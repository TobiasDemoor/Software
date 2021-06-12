## Problema
- Minimizar el efecto de los cambios en el sistema ([[Bajo acoplamiento|bajar el acoplamiento]]).
- Evitar mezclar la lógica de aplicación con la interfaz de usuario así esta puede ser reusada o distribuida.

## Solución
- Organizar la estructura a gran escala de un sistema en capas discretas con responsabilidades dintinguibles y relacionadas con una [[Separación de concerns|separación de concerns]] limpia y [[Cohesión|cohesiva]] de manera que las capas más bajas son de más bajo nivel y proveen servicios más generales, y las capas más altas son más específicas.
- La colaboración y el [[Acoplamiento|acoplamiento]] son de arriba hacia abajo, el acoplamiento de abajo hacia arriba es evitado.
Una capa es un elemento a gran escala, usualmente compuesto por una serie de paquetes o subsistemas.
El patrón Capas se relaciona con la [[Arquitectura de software#Views|logical architecture]], ya que describe la organización conceptual de los elementos de diseño en grupos, independientes de el empaquetamiento físico o deployment.
El patrón define un modelo general de N niveles para la [[Arquitectura de software#Views|logical architecture]], produce una **arquitectura de capas**.

## Descripción
Se organiza el sisteam en módulos/componentes con funcionalidad relacionada. Cada capa se organiza sobre los servicios de la inmediata inferior.

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
- [[FURPS+#Mantainability|Mantenibilidad]]
- Modularidad
- Testeabilidad

## Desventajas
- [[FURPS+#Performance|Performance]] (se puede sortear con salteo de capas)

## Cualidades
- Separación e independencia entre capas (modularidad, encapsulamiento, [[FURPS+#Mantainability|mantenibilidad]]).
- Cada capa se construye sobre los servicios y recursos de la inmediata inferior (reusabilidad).
- El cambio en una capa afecta solamente a su capa adjunta ([[Acoplamiento]]).