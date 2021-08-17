Entidad de software que, basándose en su propio conocimiento, realiza un conjunto de operaciones destinadas a satisfacer las necesidades de un usuario o de otro programa, bien por iniciativa propia o porque alguno de éstos se lo requiere.
Todos los agentes inteligentes son [[Programa|programas]], pero no todos los programas que realizan búsquedas son agentes inteligentes. Los agentes en sí mismos pueden ser considerados como entidades individuales (partes de programa que tienen control sobre sus propias vidas y movimientos).
Continuamente están realizando procesos que les indican qué hacer y cómo. Se comunican con otros agentes para resolver de forma adecuada su trabajo.

> Un agente es cualquier cosa que pueda ver en su **entorno** a través de **sensores** y actuar en su entorno a través de **efectores**. - (Rusell & Norving)

> Un agente es un **sistema computacional** que está situado en algún **ambiente**, y que es capaz de actuar **autónomamente y flexiblemente** en dicho ambiente con el fin de cumplir sus **objetivos**. - (Wooldridge & Jennings)

**Agencia**: el grado en el cual el agente puede percibir su entorno y actuar en él. Para que un programa sea un agente debe poseer autonomía, habilidad social, pre actividad y pro actividad.

**Inteligencia**:Distintos grados en el cual la aplicación utiliza razonamiento, aprendizaje y otras técnicas para interpretar la [[Dato, información y conocimiento|información o conocimiento]] al cual tiene acceso, tales como:
- Permitir al usuario expresar sus preferencias.
- Formalizar un conjunto de reglas de razonamiento que combinadas con conocimiento y, siguiendo un proceso de inferencia puede conducir a la toma de alguna acción.
- Modificar su propia capacidad de razonamiento en la base nuevo conocimiento derivado de muchas fuentes, es decir, aprender.

**Autonomía**: capacidad de actuar basándose en su experiencia. El agente es capaz de adaptarse aunque el entorno cambie severamente.

**Flexibilidad** (una o varias de las siguientes capacidades):
- **Reactividad**: capacidad de percibir su ambiente, y responder sin demoras a cambios que ocurren en él.
- **Pro-actividad**: capacidad de exhibir un comportamiento dirigido a objetivos, tomando la iniciativa.
- **Habilidad social**: capacidad de interactuar con otros agentes (y posiblemente humanos) a través de un lenguaje de comunicación.

**Agente racional**: Agente que hace lo correcto u obtiene el mejor desempeño, dependiendo de la medida con que se evalúa el grado de éxito logrado.
**Agente racional ideal**: Agente racional que obtiene la máxima medida de rendimiento.

## Funciones de los Agentes
### Percepciones
Se incorporan en algún tipo de estructura de datos, mediante un procedimiento de toma de decisión se genera la elección de una acción. **Dependen del ambiente**, este influye en las percepciones del agente y condiciona su diseño
- **Accesibles y no accesibles**. Depende de si los sensores detectan todos los aspectos relevantes a la elección de una acción.
- **Deterministas y no deterministas**. Si el estado siguiente se determina a partir del actual y las acciones escogidas por el agente.
- **Episódicos y no episódicos**. Si cada episodio depende de un agente.
- **Estáticos y dinámicos**. Si el ambiente puede sufrir modificaciones mientras el agente delibera.
- **Discretos y continuos**. Si existe una cantidad limitada de percepciones y acciones distintas.

### Elección de acciones
**Agente conducido mediante tablas:**
Se almacenan todas las posibles percepciones y sus combinaciones, se decide la acción buscando la que corresponde en tabla. 
- Tamaño de las tablas (Ajedrez aprox. 35100 entradas).
- Tiempo de elaboración de las tablas
- Carencia de autonomía. Si el ambiente se modifica se vería perdido.
- Si tuviera mecanismo de aprendizaje, tardaría mucho en aprender todos los valores de entrada de la tabla.
**Agentes que razonan de manera lógica**
Agentes capaces de:
- Elaborar representaciones del mundo
- Aplicar un proceso de inferencia para obtener nuevas representaciones del mundo
- Utilizarlas para deducir que hacer caracterizados por:
	- Nivel de conocimiento (epistemológico)
	- Nivel lógico
	- Nivel de implementación

## Base de conocimiento
Colección de [[Dato, información y conocimiento|conocimientos]], representada utilizando un lenguaje de representación del conocimiento

**Sistema basado en conocimiento**
Programa para ampliar y/o consultar una base de conocimiento.

**Representación del conocimiento**
Una buena representación hace que el mecanismo de razonamiento de un programa sea no sólo correcto sino trivial.
Los programas de IA manipulan las representaciones internas de los hechos, generando nuevas estructuras como representaciones de hechos.

## Agente que razona
### Agente de reflejo simple
Este agente percibe el ambiente a través de sensores, determina qué es lo que ocurre ahora, a partir de reglas decide que acción debe tomar y la ejecuta.

### Agente bien informado
Este agente percibe el ambiente a través de sensores, determina qué es lo que ocurre ahora, combina esta información con el conocimiento del estado actual, de cómo evoluciona el mundo y con qué acciones puede hacer, a partir de reglas decide que acción debe tomar y la ejecuta.

### Agente basado en metas
Este agente percibe el ambiente a través de sensores, determina qué es lo que ocurre ahora, combina esta información con el conocimiento del estado actual, de cómo evoluciona el mundo y con qué acciones puede hacer, considera que ocurriría si realiza cierta acción, teniendo en cuenta sus metas decide que acción debe tomar y la ejecuta.

### Agente basado en utilidad
Este agente percibe el ambiente a través de sensores, determina qué es lo que ocurre ahora, combina esta información con el conocimiento del estado actual, de cómo evoluciona el mundo y con qué acciones puede hacer, considera que ocurriría si realiza cierta acción, determina cuán bien se encontrará en ese estado con una medida de utilidad determinada, decide que acción debe tomar y la ejecuta.

## Caracterización de un agente inteligente
Se caracteriza según el mundo en el que actúa por sus:
- Percepciones
- Acciones
- Metas
- Ambiente

Y por su comportamiento autónomo y flexible:
- Reactividad
- Iniciativa
- Sociabilidad