Hay diferentes maneras para que las aplicaciones puedan especificar que inconsistencias puede tolerar. Un approach distingue tres ejes independientes para definir inconsistencias: desviación de valores numéricos entre réplicas, desviación en deterioro de las réplicas, y desviación con respecto al orden de las operaciones de actualización. Estas desviaciones forman rangos de **consistencia continua**.

La inconsistencia en términos de desviación númerica puede ser usada en aplicaciones para las cuales los datos tienen significado numérico. Por ejemplo se puede establecer un límite de *desviación numérica absoluta* para un precio determinado o una *desviación numérica relativa*. En ambos casos si el precio se modifica pero se mantiene dentro del rango determinado las réplicas se seguirían considerando consistentes.

La inconsistencia de deterioro de las réplicas consiste en establecer un plazo máximo para que la réplica sea actualizada. Por lo tanto si la réplica no se actualiza desde hace más tiempo del permitido se considera inconsistente y debe actualizarse.

Finalmente respecto al orden de las operaciones de actualización, hay clases de aplicaciones en donde es permitido que el ordenamiento de las actualizaciones sea dirente en varias réplicas, siempre y cuando las diferencias permanezcan dentro de un límite. Una forma de pensar estas actualizaciones es que son aplicadas tentativamente a la copia local, esperando aceptación global de todas las réplicas. Como consecuencia algunas actualizaciones deberán ser canceladas y aplicadas en un orden distinto para pasar a ser permanentes.

#### Conits
![[Conit]]