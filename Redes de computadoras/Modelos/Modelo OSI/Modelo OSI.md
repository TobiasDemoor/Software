---
cssclass: clean-embeds
---
# Modelo de referencia OSI
El modelo de interconexión de sistemas abiertos (ISO/IEC 7498-1), conocido como "modelo OSI" (Open Systems Interconnection), es el modelo de la ISO que se ocupa de la conexión de sistemas abiertos ([[Redes de computadoras]]). El modelo OSI tiene siete capas. Los principios que se aplicaron para llegar a las siete capas se pueden resumir de la siguiente manera:
1. Se debe crear una capa en donde se requiere un nivel diferente de [[Abstracción|abstracción]].
2. Cada capa debe realizar una función bien definida.
3. La función de cada capa se debe elegir teniendo en cuenta la definición de [[Protocolo|protocolos]] estandarizados internacionalmente.
4. Es necesario elegir los límites de las capas de modo que se minimice el flujo de informacion a través de las [[Interfaz|interfaces]].
5. La cantidad de capas debe ser suficiente como para no tener que agrupar funciones distintas en la misma capa; además, debe ser lo basstante pequeña como para que la arquitectura no se vuelva inmanejable.

![[modelo_osi_1.png]]

Se debe tener en cuenta que el modelo OSI en sí no es una arquitectura de red, ya que no especifica los servicios y protocolos exactos que se van a utilizar en cada capa. Sólo indica lo que una debe hacer. Sin embargo, la ISO también ha elaborado estándares para todas las capas, aunque no son parte del modelo de referencia en sí. Cada uno se publicó como un estándar internacional separado. Aunque el modelo (en parte) es muy usado, los protocolos asociados han estado en el olvido desde hace tiempo.

Al trabajar con este modelo se suelen extirpar las capas 5 y 6 y esa funcionalidad se incluye en la capa 7. Y la capa 2 por tener tanta complejidad se subdivide en dos capas, la subcapa MAC y la subcapa LLC.

## Capas
### La capa física
![[Capa física#^extracto]]

### La capa de enlace de datos
![[Capa de enlace de datos#^extracto]]

### La capa de red
![[Capa de red#^extracto]]

### La capa de transporte
![[Capa de transporte#^extracto]]

### La capa de sesión
La **capa de sesión** permite a los usuarios en distintas máquinas establecer **sesiones** entre ellos. Las sesiones ofrecen varios servicios, incluyendo el **control del diálogo** (llevar el control de quién va a transmitir), el **manejo de tokens** (evitar que dos partes intenten la misma operación crítica al mismo tiempo) y la **sincronización** (usar puntos de referencia en las transmisiones extensas para reanudar desde el último punto de referencia en caso de una interrupción)

### La capa de presentación
A diferencia de las capas inferiores, que se enfocan principalmente en mover los bits de un lado a otro, la **capa de presentación** se enfoca en la [[Sintaxis|sintaxis]] y la [[Semántica|semántica]] de la información transmitida. Para hacer posible la comunicación entre computadoras con distintas representaciones internas de datos, podemos definir de una manera abstracta las estructuras de datos que se van a intercambiar, junto con una codificación estándar que se use “en el cable”. La capa de presentación maneja estas estructuras de datos abstractas y permite definir e intercambiar estructuras de datos de mayor nivel (por ejemplo, registros bancarios).

### La capa de aplicación
![[Capa de aplicación#^extracto]]

## Fortalezas
La fortaleza del [[Modelo OSI|modelo de referencia OSI]] es el *modelo* en sí (excepto las capas de presentación y sesión), el cual ha demostrado ser excepcionalmente útil para hablar sobre [[Redes de computadoras|redes de computadoras]].

## Análisis
Hay tres conceptos básicos para le [[Modelo OSI|modelo OSI]]:
1. Servicios
2. [[Interfaz|Interfaces]]
3. [[Protocolo|Protocolos]]

Cada capa desempeña ciertos *servicios* para la capa que está sobre ella. La definición del servicio indica lo que hace la capa, no cómo acceden a ella las entidades superiores ni cómo funciona. Define la semántica de la capa.
La *interfaz* de una capa indica a los procesos superiores cómo pueden acceder a ella. Especifica cuáles son los parámetros y qué resultados se pueden esperar. Pero no dice nada sobre su funcionamiento interno.
Por último, la capa es la que debe decidir qué *protocolos* de iguales utilizar. Puede usar los protocolos que quiera, siempre y cuando realize el trabajo. También los puede cambiar a voluntad sin afectar el software de las capas superiores.

## Críticas
### Mala sincronización
El tiempo en el cual se establece un estándar es absolutamente imprescindible para su éxito. David Clark, del MIT, tiene una teoría de estándares a la que llama el *apocalipsis de los dos elefantes*, la cual se ilustra en la siguiente figura.
![[apocalipsis_de_los_dos_elefantes.png]]
Esta figura muestra la cantidad de actividad alrededor de un nuevo tema. Cuando se descubre el tema por primera vez, hay una ráfaga de actividades de investigación en forma de discusiones, artículos y reuniones. Después de cierto tiempo esta actividad disminuye, las corporaciones descubren el tema y llega la ola de inversión de miles de millones de dólares.
Es imprescindible que los estándares se escriban en el intermedio entre los dos “elefantes”. Si se escriben demasiado pronto (antes de que los resultados de la investigación estén bien establecidos), tal vez el tema no se entienda bien todavía; el resultado es un estándar malo. Si se escriben demasiado tarde, es probable que muchas empresas hayan hecho ya importantes inversiones en distintas maneras de hacer las cosas, de modo que los estándares se ignorarán en la práctica. Si el intervalo entre los dos elefantes es muy corto (ya que todos tienen prisa por empezar), la gente que desarrolla los estándares podría quedar aplastada.

En la actualidad, parece que los protocolos estándar de [[Modelo OSI|OSI]] quedaron aplastados. Para cuando aparecieron los protocolos de OSI, los protocolos [[Modelo TCP IP|TCP/IP]] competidores ya se utilizaban mucho en universidades que hacían investigaciones. Aunque todavía no llegaba la ola de inversión de miles de millones de dólares, el mercado académico era lo bastante grande como para que muchos distribuidores empezaran a ofrecer con cautela los productos TCP/IP. Para cuando llegó el modelo OSI, los distribuidores no quisieron apoyar una segunda [[Pila de protocolos|pila de protocolos]] hasta que se vieron obligados a hacerlo, de modo que no hubo ofertas iniciales. Como cada empresa estaba esperando a que otra tomara la iniciativa, ninguna lo hizo y OSI nunca se llevó a cabo.

### Mala tecnología
La segunda razón por la que [[Modelo OSI|OSI]] nunca tuvo éxito fue que tanto el modelo como los protocolos tienen fallas. La opción de siete capas era más política que técnica, además de que dos de las capas (sesión y presentación) están casi vacías, mientras que otras dos (enlace de datos y red) están demasiado llenas.

### Malas implementaciones
Dada la enorme complejidad del [[Modelo OSI|modelo]] y los protocolos, no es sorprendente que las implementaciones iniciales fueran enormes, pesadas y lentas. Todos los que las probaron se arrepintieron. No tuvo que pasar mucho tiempo para que las personas asociaran “OSI” con la “mala calidad”. Aunque los productos mejoraron con el tiempo, la imagen perduró.
En contraste, una de las primeras implementaciones de [[Modelo TCP IP|TCP/IP]] fue parte del UNIX, de Berkeley, y era bastante buena (y además, gratuita). Las personas empezaron a utilizarla rápidamente, lo cual provocó que se formara una extensa comunidad de usuarios, lo que condujo a mejoras, lo que llevó a una comunidad todavía mayor. En este caso la espiral fue hacia arriba, en vez de ir hacia abajo.

### Malas políticas
El [[Modelo OSI|modelo OSI]] se consideraba en muchas partes como la invención de los ministerios europeos de telecomunicaciones, de la Comunidad Europea y después, del gobierno de Estados Unidos. Esta creencia no era del todo justificada, pero la simple idea de un grupo de burócratas gubernamentales que trataban de obligar a los pobres investigadores y programadores que estaban en las trincheras desarrollando verdaderas redes de computadoras a que adoptaran un estándar técnicamente inferior no fue de mucha utilidad para la causa de OSI.