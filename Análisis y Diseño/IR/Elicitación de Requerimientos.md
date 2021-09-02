La elicitación o extracción de requerimientos, es el proceso de recolectar la información necesario para identificar y entender las necesidades y restricciones del producto, que requiere el usuario o el cliente. Es la etapa de mayor interacción con el usuario. Es el momento en el que se recurre, por ejemplo, a la observación, entrevistas, revisión de documentos, entre otras técnicas. Es parte de la [[Ingeniería de Requerimientos]].

La profundidad de la investigación y compresión del [[Dominio|dominio]] (en la elicitación) redundará en mejores decisiones para todos los niveles (análisis y [[Software Architecture|arquitectura]]).
           
## ¿Cómo comenzar la elicitación?
Se puede estructurar la investigación en base a los siguientes objetivos:
* Comprender el proceso.
* Identificar los datos y la información generada.
* Frecuencia y el volumen del proceso.
* Identificar los controles.

## Técnicas
Técnicas de recolección de datos individuales:
* Entrevistas.
* Cuestionarios.
* Prototipos.
* Entrevistas generales.
* Escenarios y casos de uso.
* Entrevistas dirigidas.
* Historias de usuario.

Algunas técnicas de recolección de datos grupales:
* Observación.
* Muestreo.
* Brainstorming.
* JAD: Joint Applications Development.
* Focus groups.

Otros métodos: revisión de los registros (reglamento, manuales de procedimientos estándares, etc.), observación, reúso.

## Entrevista
Es una **conversación dirigida** con un **objetivo** específico en la que se usan preguntas y respuestas. Se desea conocer las **opiniones** y comprender la **cultura** de la organización. Se debe definir el **objetivo** de la entrevista. Las entrevistas son breves, por lo tanto, no se puede obtener todo de una sola entrevista. El objetivo debe ser bien definido y acotado y las preguntas deben responder a este objetivo.

Objetivos de las entrevistas:
* Registrar información fácilmente utilizable en los procesos de la IR.
* Descubrir información proveniente del entrevistado precisa y eficientemente.
*  Asegurar al entrevistado que su comprensión del tópico ha sido explorado, atendido y valorado.

Proceso:
1. Planeamiento y preparación:
	* Establecer los objetivos.
	*  Preparar las preguntas.
	*   Adquirir conocimiento sobre el tema de la entrevista.
	*    Decidir a quién entrevistar.
	*     Organizar el ambiente para tener una entrevista efectiva.
2. Conducción de la entrevista:
	* Conversar en modo profesional usando técnicas adecuadas de preguntas.
	*  Registrar sin imponer ideas subjetivas ni prejuicios.
3. Consolidar y representar la información obtenida.
	* Elaborar resumen, informes.
	*  Consolidar notas provenientes de los diferentes entrevistados.
4. Validación de la información obtenida de los entrevistados:
	* Entrevistas de seguimiento para confirmar supuestos.
5. Dar feedback a los entrevistados acerca de las entrevistas.

Preguntas:
* Abiertas: son preguntas para que el entrevistado se explaye, por ejemplo, para conocer su opinión o que explique un proceso.
*  Cerradas: una pregunta cerrada limita al entrevistado la respuesta disponible. Son preguntas que tienen respuestas acotadas sólo se puede responder con un número finito tal como “dos”, “una” o “ninguna”. Hay un tipo especial de pregunta cerrada, la pregunta bipolar. Este tipo de pregunta limita incluso más al entrevistado, ya que sólo le permite elegir uno de dos polos, sí o no, verdadero o falso.
*  Averiguaciones, sondeo: el sondeo más sólido es el más simple: la pregunta “¿Por qué?”. Otros sondeos son: “¿Me puede dar un ejemplo de un momento en el que el sistema no haya parecido confiable?” y “¿Podría explicarme eso?”.

Estructuras:
* Pirámide.
*  Embudo.
*  Rombo.
*  Entrevistas sin estructura.

## Cuestionario
Técnica de recopilación de información que permite estudiar: creencias, actitudes, comportamientos y características principales. Permiten un mejor manejo de las palabras en las preguntas, evaluar la difusión de un concepto, cuantificar lo que se encontró en una entrevista, encontrar problemas, obtener información importante antes de una entrevista.

Se pueden usar para:
* Cuantificar lo que se encontró en la entrevista.
*  Determinar qué tan amplio o limitado es un sentimiento expresado en una entrevista.
*  Investigar en una muestra de gran tamaño.
*   Encontrar problemas.
*   Obtener datos importantes antes de una entrevista.

Son convenientes cuando:
* Hay una dispersión geográfica de los entrevistados.
*  Existe una gran cantidad de involucrados y se necesita establecer un % de aprobación.
*  Se quiere hacer un estudio exploratorio antes de encarar el proyecto.
*  Se deben identificar los problemas del sistema actual.

Tener en cuenta para las preguntas de un cuestionario:
* Deben ser muy claras.
* El flujo de las preguntas debe ser coherente.
* Se deben anticipar las preguntas del interlocutor.
* Se deben plantear la administración de los cuestionarios detalladamente.
* Las respuestas a las preguntas cerradas se pueden cuantificar, las respuestas de las preguntas abiertas se analizan e interpretan de otra manera.

Diseño:
* La redacción de preguntas no es trivial y requiere atender a las técnicas de preparación de formularios. Siempre se debe evaluar el objetivo del cuestionario, si es realmente necesario y si será útil la información que se obtendrá.
* Las escalas requieren extremo cuidado.
* El lenguaje de los cuestionarios es sumamente importante para su efectividad, debe reflejar el uso del lenguaje en la organización. Tener en cuenta:
	* Usar una redacción simple y específica.
	* Hacer preguntas cortas.
	*  No menospreciar ni suponer demasiado conocimiento del interlocutor.
	*   Dirigir las preguntas a las personas adecuadas.
	*    Las preguntas técnicas deben ser precisas.
* No siempre los interlocutores están motivados a responder, por eso es importante tener un buen diseño del cuestionario para poder vencer esa resistencia. Consideraciones generales:
	*  Usar los objetivos para determinar el formato,
	*  Dejar espacio suficiente para las respuestas.
	*  Ser consistente en el estilo de presentación.
	*  Revisar el orden de las preguntas.
	*   Agrupar conceptos similares.

Métodos de administración:
* Reunión.
* E-mail.
* Personalmente.
* Formulario Web y otros.

## Problemas
¿Dónde se puede encontrar el conocimiento de un [[Dominio|dominio]] y cómo se puede elicitar ese conocimiento? El conocimiento está distribuido en **diferentes fuentes**, muchas veces esta diversidad es conflictiva, ya que una parte importante puede residir en expertos humanos.

Problemas en la transmisión del conocimiento del [[Dominio|dominio]]:
* Los usuarios pueden estar sesgados por el sistema actual.
* Es difícil elicitar el conocimiento, en especial cuando se trata de un experto humano.
* El conocimiento no está disponible en una forma utilizable para los analistas.
* El efecto Hawthorne: la presencia de un observador deforma el resultado.
* El sesgo que introduce el ingeniero en el proceso.

Dificultades para entender los requerimientos de los usuarios:
* A menudo los usuarios no conocen lo que desean obtener, se expresan con sus propios términos y con un conocimiento implícito.
* Distintos usuarios tienen distintos requerimientos y los expresan de distinta forma.
* Influencia de los factores políticos.
* Es inevitable que el ambiente de negocios cambie durante el ciclo de desarrollo.
* Comunicación entre usuario y analista.
* El usuario puede no querer el sistema.