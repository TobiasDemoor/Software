Kanban es un método para gestionar el trabajo que surgió en Toyota Production System (TPS). La palabra Kanban viene del japonés y traducida literalmente quiere decir "letrero" o "tarjeta". En un ambiente de manufactura esta tarjeta se utiliza para indicarle a una fase anterior del proceso que produzca más. A los trabajadores en cada paso no se les permite trabajar a menos que se les indique lo contrario con un kanban proveniente de una fase posterior.

Kanban es un sistema de **arrastre**, esto significa que la producción se basa en la demanda, las necesidades del cliente son las que determinan la producción, en vez del enfoque tradicional de fabricar productos a un ritmo dado. Los inventarios tienen un tamaño máximo determinado.

Un efecto secundario interesante de los sistemas de arrastre es que limitan el trabajo-en-progreso (WIP) a una cantidad acordada, con lo que impiden que los trabajadores se saturen. Además, sólo los trabajadores en la estación donde se tiene un cuello de botella permanecen sobrecargados, todos los demás tienen tiempo de holgura.

Los kanban permiten lograr un **ritmo sustentable de trabajo**, es decir un nivel de producción que se puede mantener en el tiempo. En este ritmo los trabajadores mantienen un buen balance entre su vida laboral y personal y no se sienten aplastados por el trabajo.

Taiichi Ohno uno de los creadores del TPS y el creador del sistema Kanban dijo: “Los dos pilares del sistema de producción Toyota son [[just-in-time]] y la automatización con un toque humano (o [[Jidoka|Autonomatización]]). La herramienta utilizada para operar el sistema es kanban.” Kanban es fundamental para el kaizen (o mejora continua) utilizado en Toyota. Es el mecanismo que lo hace funcionar.

### Sistema Kanban
Un número de kanban (tarjetas) equivalente a la capacidad (acordada) del sistema es puesto en circulación. Una tarjeta es adjuntada a una parte del trabajo. Cada tarjeta actúa como un mecanismo de señalización. Una nueva parte del trabajo puede iniciarse solamente cuando una tarjeta está disponible. Esta tarjeta libre es adjuntada a una parte el trabajo y se permanece con ese trabajo a medida que fluye a través del sistema. Cuando no hay más tarjetas libres, no se puede iniciar ningún trabajo adicional. Todo trabajo nuevo tiene que esperar en cola hasta que una tarjeta esté disponible. Cuando algún trabajo ha sido completado, su tarjeta es desprendida y reciclada. Con una tarjeta ahora libre, una parte nueva del trabajo en cola puede iniciarse.

A este mecanismo se le conoce como un sistema de arrastre porque el nuevo trabajo es introducido en el sistema solamente cuando hay capacidad para llevarlo a cabo, en vez de ser empujado en el sistema basado en la demanda. Un sistema de arrastre no se puede sobrecargar si la capacidad se ha establecido adecuadamente y está efectivamente determinada por el número de tarjetas en circulación.

### Kanban aplicado en el desarrollo de software
En el desarrollo de software, estamos usando un sistema virtual de kanban para limitar el trabajo-en-progreso. Mientras que "kanban" significa "tarjetas de señal" y hay tarjetas utilizadas en la mayoría de las implementaciones de Kanban en desarrollo de software, estas tarjetas en realidad no funcionan como señales para iniciar más trabajo. En cambio, representan ítems de trabajo. De ahí el término "virtual", porque no hay una tarjeta de señal física. La señal para iniciar un nuevo trabajo se deduce a partir de la cantidad visual de trabajo-en-progreso restado de algún indicador de límite (o capacidad).

Las paredes de tarjetas se han convertido en un mecanismo de control visual popular en el [[Agile methodologies|desarrollo ágil de software]]. El uso de un tablero de anuncios de corcho con tarjetas clavadas en él o de un pizarrón blanco con notas adhesivas para seguimiento del trabajo-en-progreso se han convertido en la práctica común. Estas tarjetas no son inherentemente sistemas Kanban, sino que son tan solo sistemas de control visual. Le permiten a los equipos observar visualmente el trabajo-en-progreso; y a los equipos mismos auto-organizarse, asignar sus propias tareas y mover el trabajo del *backlog* para completarlo sin la dirección de un director de proyecto o línea. Sin embargo, si no hay un límite explícito del trabajo-en-progreso y no hay señal para tomar un nuevo trabajo a través del sistema, entonces no es un sistema Kanban.

### ¿Por qué usar un sistema Kanban?
Utilizamos un sistema Kanban para limitar la capacidad del trabajo-en-proceso en un equipo y para equilibrar la demanda en el equipo contra el throughput de su trabajo entregado. De esa manera podemos alcanzar un **ritmo sustentable de desarrollo**, de modo tal que todas las personas pueden lograr un equilibrio entre trabajo y vida personal.

Kanban también hace rápidamente obvios los asuntos que afectan el desempeño y reta al equipo a enfocarse en resolver esos asuntos con el fin de mantener un flujo continuo de trabajo. Dando visibilidad a lo problemas de calidad y de proceso se hace obvio el impacto de los defectos, los cuellos de botella, la variabilidad y los costos económicos en el flujo y en el throughput.

Haciendo todo esto, Kanban cotribuye a la evolución cultural de las organizaciones. Exponiendo los problemas, enfocando la organización en resolverlos y eliminando sus efectos en el futuro, Kanban faciliita el surgimiento de una organización de [[Mejora continua|mejora continua]] altamente apoderada que es altamente colaborativa y tiene alta confianza.

### Reconociendo una implementación del método Kanban
Un equipo que sigue el método Kanban exhibirá 5 propiedades fundamentales:
1. Visualizar el flujo de trabajo.
2. Limitar el trabajo-en-progreso.
3. Medir y administrar el flujo.
4. Hacer las políticas del proceso explícitas.
5. Utilizar modelos para reconocer oportunidades de mejora.

Y hay 5 propiedades emergentes que deberíamos esperar de una implementación de Kanban:
1. Priorizar el trabajo por costo oportunidad de retrazo.
2. Optimizar valor por medio de clases de servicio.
3. Distribuir el riesgo con la asignación de capacidad.
4. Incentivar la innovación de procesos.
5. Administrar cuantitativamente.
