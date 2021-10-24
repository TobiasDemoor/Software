Hay dos motivos principales para replicar datos. Primero, los datos son replicados para incrementar la fiabilidad de un sistema. Si un sistema de archivos ha sido replicado puede ser posible continuar trabajando si una de las réplicas se cae simplemente trabajando con la otra réplica. También, manteniendo varias copias, es posible proveer protección contra la corrupción de datos.

La otra razón para replicar datos es la [[performance]]. La replicación para performance es importante cuando un [[Sistemas Distribuidos|sistema distribuido]] necesita [[Escalabilidad|escalar]] en términos de tamaño o en términos de área geográfica que cubre.

El precio de la replicación es tener que lidiar con los problemas de consistencia originados por dichas réplicas. Cuando una copia es modificada, dicha copia ahora es diferente al resto. Consecuentemente las modificaciones deben ser llevadas a cabo en todas las copias para asegurar la consistencia. El cómo y cúando se llevan a cabo dichas modificaciones determina el **precio de la replicación**.

Un posible trade-off que se debe analizar es que el mantener las copias sincronizadas puede exigir más ancho de banda de la red. Considere un proceso P que accede una réplica local N veces por segunda, mientras que la réplica misma es actualizada M veces por segundo. Suponiendo que una actualización refresca la versión anterior de la réplica. Si N << M, osea, el ratio acceso-actualización es muy pequeño, tenemos una situación donde muchas de las versiones actualizadas de la réplica local no serán accedidas por P, haciendo que todas las comunicaciones para esas versiones sea inútil. En ese caso, puede ser preferible no instalar una réplica local cerca de P, o aplicar una estrategia distinta para actualizar la réplica.

Un problema más serio es que el hecho de mantener múltiples copias consistentes puede generar problemas de escalabilidad graves. Intuitivamente una colección de copias es consistente cuando todas las copias son siempre iguales. Consecuentemente, cuando una operación de actualización es realizada sobre una copia, la actualización debería ser propagada a todas las copias antes de que una operación subsecuente tome lugar, sin importar en qué copia la operación es iniciada o realizada.

A este tipo de consistencia donde todas las copias siempre son iguales se le suele llamar **consistencia hermética** o **replicación sincrónica**. La idea clave es que una actualización es llevada a cabo en todas las copias como una sola operación atómica, o [[Transacciones|transacción]]. Desafortunadamente implementar transacciones involucrando un número elevado de réplicas distribuidas sobre una red grande es inherentemente difícil cuando al mismo tiempo se requiere rapidez.

Para poder sincronizar las réplicas surge la necesidad de que las réplicas se pongan de acuerdo en cuándo se debe llevar a cabo una actualización localmente. Por ejemplo, estas pueden necesitar decidir un orden global de operaciones ([[Sincronización]]). La sincronización global lleva mucho tiempo de comunicación, especialmente cuando las réplicas están muy distribuidas a través de una red WAN.

> Entonces arribamos a un dilema. Los problemas de **escalabilidad** pueden ser aliviados mediante **replicación** llevando a una mejor performance. Pero esta replicación suele requerir **sincronización global** lo que lleva a problemas de escalabilidad.

En muchos casos la única solución viable es relajar los **requerimientos de consistencia**. En otras palabras, si se relajan los requerimientos que las actualizaciones deben ser ejecutadas como operaciones atómicas, podemos evitar la sincronización global instantánea y por lo tanto ganar performance. El precio es que las copias no son iguales en todos lados.

## Consistencia centrada en datos
Tradicionalmente la consistencia fue discutida en el contexto de operaciones de lectura/escritura sobre datos compartidos, disponibles por medio de memoria compartida, una base de datos distribuida o un sistema de archivos. Aquí se usará el concepto **almacen de datos** o **data store** que abarca todos los anteriores. Un almacen de datos puede estar distribuido físicamente a través de varias máquinas. En particular se supone que cada proceso que puede acceder a datos del almacen tiene una copia local (o cercana) del almacen entero.

![[replicación_data_store_1.png]]

![[Modelo de consistencia]]

A falta de un reloj global es difícil determinar precisamente que operación de escritura es la última. Como alternativa, necesitamos proveer otras definiciones, llevando a un rango de modelos de consistencia. Cada modelo efectivamente restrinje los valores que una operación de lectura en un ítem puede retornar.

### Consistencia continua
Hay diferentes maneras para que las aplicaciones puedan especificar que inconsistencias puede tolerar. Un approach distingue tres ejes independientes para definir inconsistencias: desviación de valores numéricos entre réplicas, desviación en deterioro de las réplicas, y desviación con respecto al orden de las operaciones de actualización. Estas desviaciones forman rangos de **consistencia continua**.

La inconsistencia en términos de desviación númerica puede ser usada en aplicaciones para las cuales los datos tienen significado numérico. Por ejemplo se puede establecer un límite de *desviación numérica absoluta* para un precio determinado o una *desviación numérica relativa*. En ambos casos si el precio se modifica pero se mantiene dentro del rango determinado las réplicas se seguirían considerando consistentes.

La inconsistencia de deterioro de las réplicas consiste en establecer un plazo máximo para que la réplica sea actualizada. Por lo tanto si la réplica no se actualiza desde hace más tiempo del permitido se considera inconsistente y debe actualizarse.

Finalmente respecto al orden de las operaciones de actualización, hay clases de aplicaciones en donde es permitido que el ordenamiento de las actualizaciones sea dirente en varias réplicas, siempre y cuando las diferencias permanezcan dentro de un límite. Una forma de pensar estas actualizaciones es que son aplicadas tentativamente a la copia local, esperando aceptación global de todas las réplicas. Como consecuencia algunas actualizaciones deberán ser canceladas y aplicadas en un orden distinto para pasar a ser permanentes.

#### Conits
![[Conit]]

### Ordenamiento consistente de operaciones
