La esencia del análisis arquitectónico es identificar factores que deberían influenciar la [[Software Architecture|arquitectura]], entender su variabilidad y prioridad y resolverlos. La parte dificil es conocer cuáles son las preguntas a realizar, pesar los tradeoffs y conocer las múltiples maneras de resolver arquitectonicamente factores significativos, desde un abandono benévolo (benign neglect), un diseño elaborado o un producto de un tercero.
En el [[Unified Process|Proceso Unificado]], los factores arquitectónicos son anotados en la Supplementary Specification y las decisiones arquitectónicas que los resuelven son anotados en el SAD ([[Software Architecture Document]])
El análisis arquitectónico empieza temprano en el desarrollo, durante la fase de [[Unified Process#Inception|inception]] y es un punto focal de la fase de [[Unified Process#Elaboration|elaboration]]. Es una actividad de alta prioridad y muy influyente en el desarrollo de software. Es una actividad útil para:
- Reducir el reisgo de perder algo de importancia central en el [[Diseño de sistemas|diseño del sistema]].
- Evitar aplicar efuerzo por demás en problemas de baja prioridad.
- Alinear el producto con los objetivos de negocio.

El análsisi arquitectonico está enfocado en la identificación y resolución de los [[Requerimientos#Requerimientos no funcionales|requerimientos no funcionales]] del sistema en el contexto de sus [[Requerimientos#Requerimientos funcionales|requerimientos funcionales]]. En el [[Unified Process|UP]], el término incluye tanto **architectural investigation** (identificación) como **architectural design** (resolution). 

# Pasos comunes
1. Identificar y analizar los [[Requerimientos#Requerimientos no funcionales|requerimientos no funcionales]] que tienen un impacto en la [[Software Architecture|arquitectura]]. Los [[Requerimientos#Requerimientos funcionales|requerimientos funcionales]] también son relevantes (especialmente cuando se analiza la variabilidad o cambio), pero los no funcionales tienen el foco principal. En general estos pueden ser llamados **[[Architectural factors|factores de arquitectura]]** (o también **drivers de arquitectura**).
	- Este paso se puede caracterizar como [[Ingeniería de Requerimientos#Fases del proceso de IR|análisis de requerimientos]] común, pero como está hecho en el contexto de identificar el impacto en la arquitectura y decidir las soluciones arquitectónicas de alto nivel, es considerado una parte del análisis arquitectónico en [[Unified Process|UP]]
	- En términos de [[Unified Process|UP]], aguno de estos [[Requerimientos|requerimientos]] serán identificados y anotados en la Supplementary Specification o como [[Use Case|casos de uso]] durante la fase de [[Unified Process#Inception|inception]]. Durante el análisis arquitectónico, que ocurre en la [[Unified Process#Elaboration|elaboration]] temprana, el equipo investica esos [[Requerimientos|requerimientos]] más profundamente.
2. Para esos requerimientos con impacto arquitectónico significativo, analizar alternativas y crear soluciones para resolver ese impacto. Estas son **decisiones de arquitectura**.
	- Las decisiones pueden variar desde "remover el requerimiento", a una solución personalizada, a "frenar el projecto" o a "contratar un experto".

# Prioridades
Hay una jerarquía de objetivos que guía las decisiones de arquitectura:
1. [[Requerimientos#Restricciones]] inflexibles incluyendo seguridad y legales.
2. Objetivos de negocios.
3. Todo el resto de los objetivos.

Otro factor distinctivo de la toma de decisiones arquitectónicas es ela priorización por probabilidad de [[Puntos de evolución|puntos de evolución]]. Para decidir si se debería evitar "future-proofing", se puede considerar realísticamente el escenario en el que ese cambio se debe realizar en el futuro, cuando es requerido. ¿Qué tan sustancial es el cambio en el diseño e implementación? ¿Cuál va a ser el esfuerzo necesario?
