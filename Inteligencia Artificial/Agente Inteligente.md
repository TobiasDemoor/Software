Un agente inteligente es una entidad de software que, basándose en su propio conocimiento, realiza un conjunto de operaciones destinadas a satisfacer las necesidades de un usuario o de otro programa, bien por iniciativa propia o porque alguno de éstos se lo requiere.

Todos los agentes inteligentes son [[Programa|programas]], pero no todos los programas que realizan búsquedas son agentes inteligentes. Los agentes en sí mismos pueden ser considerados como entidades individuales (partes de programa que tienen control sobre sus propias vidas y movimientos).

Continuamente están realizando procesos que les indican qué hacer y cómo. Se comunican con otros agentes para resolver de forma adecuada su trabajo.

> Un agente es cualquier cosa que pueda ver en su **entorno** a través de **sensores** y actuar en él través de **efectores**. - (Rusell & Norving)

> Un agente es un **sistema computacional** que está situado en algún **ambiente**, y que es capaz de actuar **autónomamente y flexiblemente** en dicho ambiente con el fin de cumplir sus **objetivos**. - (Wooldridge & Jennings)

## Características de los Agentes Inteligentes
La principal característica de los Agentes Inteligentes es el conocimiento que estos poseen ([[Base de Conocimiento]]), aunado a la forma como lo utilizan para alcanzar las metas para la cual fueron diseñados. Por supuesto que al mencionar conocimiento este se refiere al conocimiento del ambiente en el cual se desempeñan y de las acciones que debe emprender basándose en las percepciones capturadas, sin olvidar las intervenciones del usuario.

## Agencia
La agencia es el grado en el cual el agente puede percibir su entorno y actuar en él. Para que un programa sea un agente debe poseer autonomía, habilidad social, pre actividad y pro actividad.

Otras características de mucha importancia son las siguientes:

### Inteligencia
Distintos grados en el cual la aplicación utiliza [[Razonamiento|razonamiento]], aprendizaje y otras técnicas para interpretar la [[Dato, información y conocimiento|información o conocimiento]] al cual tiene acceso, tales como:
- Permitir al usuario expresar sus preferencias.
- Formalizar un conjunto de reglas de razonamiento que combinadas con conocimiento y, siguiendo un proceso de inferencia puede conducir a la toma de alguna acción.
- Modificar su propia capacidad de razonamiento en la base nuevo conocimiento derivado de muchas fuentes, es decir, aprender.

### Autonomía
Capacidad de operar sin intervención directa de los humanos o de otros agentes, con un cierto tipo de control sobre sus acciones. Después del conocimiento integrado, definitivamente que la autonomía es la característica más importante de los AI dado que, esta le permitirá definir su conducta basado en su propia experiencia.

La autonomía es la capacidad de actuar basándose en su experiencia. El agente es capaz de adaptarse aunque el entorno cambie severamente.

### Flexibilidad
La flexibilidad es una o varias de las siguientes capacidades:
- **Reactividad**: capacidad de percibir su ambiente, y responder sin demoras a cambios que ocurren en él.
- **Pro-actividad**: capacidad de exhibir un comportamiento dirigido a objetivos, tomando la iniciativa.
- **Habilidad social**: capacidad de interactuar con otros agentes (y posiblemente humanos) a través de un lenguaje de comunicación.

## Cómo deben actuar los Agentes Inteligentes
Un **agente racional** es aquél que hace lo correcto u obtiene el mejor desempeño, dependiendo de la medida con que se evalúa el grado de éxito logrado. Lo correcto es aquello que permite al agente obtener el mejor desempeño.

El término **medición del desempeño** se aplica al cómo: es el criterio que sirve para definir qué tan exitoso ha sido un agente. Desde luego que no existe una medida fija que se pueda aplicar por igual a todos los agentes.

El carácter de |racionalidad de lo que se hace en un momento dado dependerá de cuatro factores:
- De la medida con la que se evalúa el grado de éxito logrado.
- De todo lo que hasta ese momento haya percibido el agente. A esta historia perceptual completa se le denomina la secuencia de percepciones.
- Del conocimiento que posea el agente acerca del medio.
- De las acciones que el agente puede comprender.

Un **agente racional ideal** es aquél que, para cada secuencia de percepciones posible, actúa de manera que se maximice su medida de desempeño.

## Estructura de los Agentes Inteligentes
El cometido de la Inteligencia Artificial es el desempeño de un **programa de agentes**: una función que permite implantar el mapeo del agente para pasar de percepciones a acciones. Se da por sentado que este programa se ejecutara en algún tipo de dispositivo de cómputo, al que se dominara **arquitectura**. El agente es la suma de la arquitectura y el programa agente.

La [[Inteligencia Artificial]] se ocupa del diseño del **programa agente**.

Antes de diseñar un programa agente tenemos que conocer los distintos elementos que caracterizan al agente (estos cuatro elementos forman el **PAMA**):
- **Percepciones.** Percepciones posibles
- **Acciones.** Acciones posibles
- **Metas.** Medida de desempeño u objetivos que debe lograr
- **Ambiente.** Tipo de entorno en el que va a operar

También se pueden caracterizar por su comportamiento autónomo y flexible:
- **Reactividad**: capacidad de precibir el medio ambiente y responder a tiempo a los cambios en él, a través de acciones.
- **Iniciativa**: capacidad de exhibir un comportamento orientado por sus metas, tomando la iniciativa para satisfacer sus objetivos de diseño (proactivo).
- **Sociabilidad**: capacidad de interaccionar con otros agentes, posiblemente tan complejos como los seres humanos, con miras a la satisfacción de sus objetivos.

### Tipos principales
**Agente basado en una tablas**
Un agente basado en una tabla almacena la **transformación de secuencias de percepciones en acciones**. Los inconvenientes que surgen de este modelo son que la tabla podría ser enorme y difícil construir, y el agente no tendría autonomía.

**Agentes que razonan de manera lógica**
Son agentes capaces de elaborar representaciones del mundo y aplicar un proceso de inferencia para obtener nuevas representaciones del mundo. Y utilizarlas para deducir que hacer caracterizados por:
- Nivel de conocimiento (epistemológico)
- Nivel lógico
- Nivel de implementación

**Agente de reflejo simple**
Este agente percibe el ambiente a través de sensores, determina qué es lo que ocurre ahora, a partir de **reglas condición-acción** decide que acción debe tomar y la ejecuta.

**Agente bien informado (o de reflejo con estado interno)**
Este agente percibe el ambiente a través de sensores, determina qué es lo que ocurre ahora, combina esta información con el **conocimiento del estado actual**, de cómo evoluciona el mundo y con qué acciones puede hacer, a partir de reglas decide que acción debe tomar y la ejecuta.

**Agente basado en metas**
Este agente percibe el ambiente a través de sensores, determina qué es lo que ocurre ahora, combina esta información con el conocimiento del estado actual, de cómo evoluciona el mundo y con qué acciones puede hacer, considera que ocurriría si realiza cierta acción, teniendo en cuenta sus metas decide que acción debe tomar y la ejecuta.

**Agente basado en utilidad**
Este agente percibe el ambiente a través de sensores, determina qué es lo que ocurre ahora, combina esta información con el conocimiento del estado actual, de cómo evoluciona el mundo y con qué acciones puede hacer, considera que ocurriría si realiza cierta acción, determina cuán bien se encontrará en ese estado con una medida de utilidad determinada, decide que acción debe tomar y la ejecuta.

## Ambiente
El ambiente influye en las percepciones del agente y condiciona su diseño. Los ambientes se pueden clasificar como:
- **Accesibles y no accesibles.** Si el aparato sensorial de un agente le permite tener **acceso al estado total** de un ambiente, se dice que este es **accesible** a tal agente. Un agente es realmente accesible si los sensores detectan todos los aspectos relevantes a la elección de una acción. Los ambientes accesibles son cómodos, puesto que no es necesario que el agente mantenga un estado interno para estar al tanto de lo que sucede en el mundo.

- **Deterministas y no deterministas.** Si el estado siguiente de un ambiente se determina completamente mediante el estado actual y las acciones escogidas por los agentes, se dice que el ambiente es determinista. En principio, un agente no tiene por que preocuparse sobre la incertidumbre en un ambiente accesible y determinista. Pero si el ambiente es inaccesible, entonces podría parecer que es no determinista. Lo anterior es especialmente valido cuando el ambiente es complejo, dificultando el estar al tanto de todos los aspectos inaccesibles. Por ello, es mas conveniente calificar el que un ambiente sea determinista o no determinista considerando el punto de vista el agente.

- **Episódicos y no episódicos.** En un ambiente episódico, la experiencia del agente se divide en “episodios” cada episodio consta de un agente que percibe y actúa. la calidad de su actuación dependerá del episodio mismo, dado que los episodios subsecuentes no dependerán de las acciones producidas en episodios anteriores. Los ambientes episódicos son más sencillos puesto que el agente no tiene que pensar por adelantado.

- **Estáticos y dinámicos.** Si existe la posibilidad de que el ambiente sufra modificaciones mientras el agente se encuentra deliberando, se dice que tal ambiente se comporta en forma dinámica en relación con el ambiente; de lo contrario, se dice que es estático. Es mas fácil trabajar con ambientes estáticos puesto que el agente no tiene que observar lo que sucede en el mundo al mismo tiempo que decide sobre el curso de una acción, ni tampoco tiene que preocuparse por el paso del tiempo. Si el ambiente no cambia con el paso del tiempo, pero si se modifica la calificación asignada al desempeño de un agente, se dice que el ambiente es semidinámico.

- **Discretos y continuos.** Si existe una cantidad limitada de percepciones y acciones distintas y claramente discernibles, se dice que el ambiente es discreto. El ajedrez es discreto: existe una cantidad fija de posibles jugadas en cada ronda. La conducción de un taxi es continua: la velocidad y la ubicación del taxi y de los demás vehículos se extiende a través de un rango de valores continuos

Las características del entorno influyen en el diseñó del agente, por ejemplo:
- Si el entorno es accesible el agente no necesita un estado interno
- Si el entorno es episódico el agente no tiene que preocuparse del impacto de sus decisiones 
- Si el entorno es dinámico el agente tiene que seguir observando mientras razona

![[agentes_inteligentes_ambiente_ejemplos.png]]

