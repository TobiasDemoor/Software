# Modelo de referencia OSI
El modelo de interconexión de sistemas abiertos (ISO/IEC 7498-1), conocido como "modelo OSI" (Open Systems Interconnection), es el modelo de la ISO que se ocupa de la conexión de sistemas abiertos ([[Redes de computadoras]]). El modelo OSI tiene siete capas. Los principios que se aplicaron para llegar a las siete capas se pueden resumir de la siguiente manera:
1. Se debe crear una capa en donde se requiere un nivel diferente de [[Abstracción|abstracción]].
2. Cada capa debe realizar una función bien definida.
3. La función de cada capa se debe elegir teniendo en cuenta la definición de [[Protocolo|protocolos]] estandarizados internacionalmente.
4. Es necesario elegir los límites de las capas de modo que se minimice el flujo de informacion a través de las [[Interfaz|interfaces]].
5. La cantidad de capas debe ser suficiente como para no tener que agrupar funciones distintas en la misma capa; además, debe ser lo basstante pequeña como para que la arquitectura no se vuelva inmanejable.

![[modelo_osi_1.png]]

Se debe tener en cuenta que el modelo OSI en sí no es una arquitectura de red, ya que no especifica los servicios y protocolos exactos que se van a utilizar en cada capa. Sólo indica lo que una debe hacer. Sin embargo, la ISO también ha elaborado estándares para todas las capas, aunque no son parte del modelo de referencia en sí. Cada uno se publicó como un estándar internacional separado. Aunque el modelo (en parte) es muy usado, los protocolos asociados han estado en el olvido desde hace tiempo.

## Capas
### La capa física
La **capa física** se relaciona con la transmisión de bits puros a través de un canal de transmisión. Los aspectos de diseño tienen que ver con la acción de asegurarse que cuando uno de los lados envíe un bit 1 el otro lado lo reciba como un bit 1, no como un bit 0.

### La capa de enlace de datos
La principal tarea de la **capa de enlace de datos** es transformar un medio de transmisión puro en una línea que esté libre de errores de transmisión. Enmascara los errores reales, de manera que la capa de red no los vea. Para lograr esta tarea, el emisor divide los datos de entrada en **tramas de datos** (por lo general, de algunos cientos o miles de bytes) y transmite las tramas en forma secuencial. Si el servicio es confiable, para confirmar la recepción correcta de cada trama, el receptor devuelve una **trama de confirmación de recepción**.
Otra cuestión que surge en la capa de enlace de datos (y en la mayoría de las capas superiores) es cómo evitar que un transmisor rápido inunde de datos a un receptor lento. Tal vez sea necesario algún mecanismo de regulación de tráfico para notificar al transmisor cuando el receptor puede aceptar más datos.
Las redes de difusión tienen una consideración adicional en la capa de enlace de datos: cómo controlar el acceso al canal compartido. Una subcapa especial de la capa de enlace de datos, conocida como subcapa de **control de acceso al medio**, es la que se encarga de este problema

### La capa de red
La **capa de red** controla la operación de la [[Subred|subred]]. Una cuestión clave de diseño es determinar cómo se encaminan los paquetes desde el origen hasta el destino. Las rutas se pueden basar en tablas estáticas que se “codifican” en la red y rara vez cambian, aunque es más común que se actualicen de manera automática para evitar las fallas en los componentes. También se pueden determinar el inicio de cada conversación; por ejemplo, en una sesión de terminal al iniciar sesión en una máquina remota. Por último, pueden ser muy dinámicas y determinarse de nuevo para cada paquete, de manera que se pueda reflejar la carga actual en la red
Si hay demasiados paquetes en la subred al mismo tiempo, se interpondrán en el camino unos con otros y formarán cuellos de botella. El manejo de la [[Congestión|congestión]] también es responsabilidad de la capa de red, en conjunto con las capas superiores que adaptan la carga que colocan en la red. Otra cuestión más general de la capa de red es la calidad del servicio proporcionado (retardo, tiempo de tránsito, variaciones, etcétera)
Cuando un paquete tiene que viajar de una red a otra para llegar a su destino, pueden surgir muchos problemas. El direccionamiento utilizado por la segunda red puede ser distinto del que utiliza la primera. La segunda red tal vez no acepte el paquete debido a que es demasiado grande. Los protocolos pueden ser diferentes, etc. Es responsabilidad de la capa de red solucionar todos estos problemas para permitir la interconexión de redes heterogéneas.

### La capa de transporte
La función básica de la **capa de transporte** es aceptar datos de la capa superior, dividirlos en unidades más pequeñas si es necesario, pasar estos datos a la capa de red y asegurar que todas las piezas lleguen correctamente al otro extremo. Además, todo esto se debe realizar con eficiencia y de una manera que aísle las capas superiores de los inevitables cambios en la tecnología de hardware que se dan con el transcurso del tiempo.
La capa de transporte también determina el tipo de servicio que debe proveer a la capa de sesión y, en última instancia, a los usuarios de la red. El tipo más popular de conexión de transporte es un canal [[P2P|punto a punto]] libre de errores que entrega los mensajes o bytes en el orden en el que se enviaron. Sin embargo existen otros posibles tipos de servicio de transporte, como el de mensajes aislados sin garantía sobre el orden de la entrega y la difusión de mensajes a múltiples destinos. El tipo de servicio se determina al establecer la conexión (cabe mencionar que es imposible lograr un canal libre de errores; lo que se quiere decir en realidad con este término es que la tasa de errores es lo bastante baja como para ignorarla en la práctica).
La capa de transporte es una verdadera capa de extremo a extremo; lleva los datos por toda la ruta desde el origen hasta el destino. En otras palabras, un programa en la máquina de origen lleva a cabo una conversación con un programa similar en la máquina de destino mediante el uso de los encabezados en los mensajes y los mensajes de control. En las capas inferiores cada uno de los protocolos está entre una máquina y sus vecinos inmediatos, no entre las verdaderas máquinas de origen y de destino, que pueden estar separadas por muchos enrutadores. En el diagrama del [[Modelo OSI|modelo OSI]] se muestra la diferencia entre las capas de la 1 a la 3, que están encadenadas, y entre las capas de la 4 a la 7, que son de extremo a extremo.

### La capa de sesión
La **capa de sesión** permite a los usuarios en distintas máquinas establecer **sesiones** entre ellos. Las sesiones ofrecen varios servicios, incluyendo el **control del diálogo** (llevar el control de quién va a transmitir), el **manejo de tokens** (evitar que dos partes intenten la misma operación crítica al mismo tiempo) y la **sincronización** (usar puntos de referencia en las transmisiones extensas para reanudar desde el último punto de referencia en caso de una interrupción)

### La capa de presentación
A diferencia de las capas inferiores, que se enfocan principalmente en mover los bits de un lado a otro, la **capa de presentación** se enfoca en la sintaxis y la semántica de la información transmitida. Para hacer posible la comunicación entre computadoras con distintas representaciones internas de datos, podemos definir de una manera abstracta las estructuras de datos que se van a intercambiar, junto con una codificación estándar que se use “en el cable”. La capa de presentación maneja estas estructuras de datos abstractas y permite definir e intercambiar estructuras de datos de mayor nivel (por ejemplo, registros bancarios).

### La capa de aplicación
La **capa de aplicación** contiene una variedad de protocolos que los usuarios necesitan con frecuencia. Un protocolo de aplicación muy utilizado es **HTTP**, el cual forma la base para la Web. Cuando un navegador desea una página web, envía el nombre de la página que quiere al servidor que la hospeda mediante el uso de HTTP. Después el servidor envía la página de vuelta. Hay otros protocolos de aplicación que se utilizan para transferir archivos, enviar y recibir correo electrónico y noticias

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

En la actualidad, parece que los protocolos estándar de [[Modelo OSI|OSI]] quedaron aplastados. Para cuando aparecieron los protocolos de OSI, los protocolos [[Modelo TCP IP|TCP/IP]] competidores ya se utilizaban mucho en universidades que hacían investigaciones. Aunque todavía no llegaba la ola de inversión de miles de millones de dólares, el mercado académico era lo bastante grande como para que muchos distribuidores empezaran a ofrecer con cautela los productos TCP/IP. Para cuando llegó el modelo OSI, los distribuidores no quisieron apoyar una segunda pila de protocolos hasta que se vieron obligados a hacerlo, de modo que no hubo ofertas iniciales. Como cada empresa estaba esperando a que otra tomara la iniciativa, ninguna lo hizo y OSI nunca se llevó a cabo.

### Mala tecnología
La segunda razón por la que [[Modelo OSI|OSI]] nunca tuvo éxito fue que tanto el modelo como los protocolos tienen fallas. La opción de siete capas era más política que técnica, además de que dos de las capas (sesión y presentación) están casi vacías, mientras que otras dos (enlace de datos y red) están demasiado llenas.

### Malas implementaciones
Dada la enorme complejidad del [[Modelo OSI|modelo]] y los protocolos, no es sorprendente que las implementaciones iniciales fueran enormes, pesadas y lentas. Todos los que las probaron se arrepintieron. No tuvo que pasar mucho tiempo para que las personas asociaran “OSI” con la “mala calidad”. Aunque los productos mejoraron con el tiempo, la imagen perduró.
En contraste, una de las primeras implementaciones de [[Modelo TCP IP|TCP/IP]] fue parte del UNIX, de Berkeley, y era bastante buena (y además, gratuita). Las personas empezaron a utilizarla rápidamente, lo cual provocó que se formara una extensa comunidad de usuarios, lo que condujo a mejoras, lo que llevó a una comunidad todavía mayor. En este caso la espiral fue hacia arriba, en vez de ir hacia abajo.

### Malas políticas
El [[Modelo OSI|modelo OSI]] se consideraba en muchas partes como la invención de los ministerios europeos de telecomunicaciones, de la Comunidad Europea y después, del gobierno de Estados Unidos. Esta creencia no era del todo justificada, pero la simple idea de un grupo de burócratas gubernamentales que trataban de obligar a los pobres investigadores y programadores que estaban en las trincheras desarrollando verdaderas redes de computadoras a que adoptaran un estándar técnicamente inferior no fue de mucha utilidad para la causa de OSI.