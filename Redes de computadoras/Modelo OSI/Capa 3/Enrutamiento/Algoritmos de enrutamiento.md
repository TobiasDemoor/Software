La principal función de la [[capa de red]] es enrutar paquetes de la máquina de origen a la de destino. Los algoritmos que eligen las rutas y las estructuras de datos que usan constituyen un aspecto principal del diseño de la capa de red. El **algoritmo de enrutamiento** es aquella parte del software de la capa de red responsable de decidir por cuál línea de salida se transmitirá un paquete entrante. Si la red usa datagramas de manera interna, esta decisión debe tomarse cada vez que llega un paquete de datos, dado que la mejor ruta podría haber cambiado desde la última vez. Si la red usa circuitos virtuales internamente, las decisiones de enrutamiento se toman sólo al establecer un circuito virtual nuevo. En lo sucesivo, los paquetes de datos simplemente siguen la ruta ya establecida. Este último caso a veces se llama **enrutamiento de sesión**, dado que una ruta permanece vigente durante toda una sesión.

Podemos agrupar los algoritmos de enrutamiento en dos clases principales: no adaptativos y adaptativos. Los **algoritmos no adaptativos** no basan sus decisiones de enrutamiento en mediciones o estimaciones del tráfico y la topología actuales. En cambio, la decisión de qué ruta se usará para llegar de I a J (para todas las I y J ) se calcula por adelantado, fuera de línea, y se descarga en los enrutadores al arrancar la red. En ocasiones este procedimiento se denomina **enrutamiento estático**. Como no responde a las fallas, el enrutamiento estático es más útil para las situaciones en las que la elección de enrutamiento es clara.

En contraste, los **algoritmos adaptativos** cambian sus decisiones de enrutamiento para reflejar los cambios de topología y algunas veces también los cambios en el tráfico. Estos algoritmos de **enrutamiento dinámico** difieren en cuanto al lugar de donde obtienen su información (por ejemplo, localmente, de los enrutadores adyacentes o de todos los enrutadores), el momento en que cambian sus rutas (por ejemplo, cuando cambia la topología o cada ΔT segundos, a medida que cambia la carga) y la métrica que se usa para la optimización (por ejemplo, distancia, número de saltos o tiempo estimado de tránsito).

### La ruta más corta
La idea es construir un grafo de la red, en donde cada nodo del grafo representa un enrutador y cada arco del grafo representa una línea o enlace de comunicaciones. Para elegir una ruta entre un par específico de enrutadores, el algoritmo simplemente encuentra la ruta más corta entre ellos en el grafo.

El concepto de la **ruta más corta** merece una explicación. Una manera de medir la longitud de una ruta es mediante el número de saltos. Otra métrica es la distancia geográfica en kilómetros y también son posibles muchas otras métricas además de los saltos y la distancia física. Por ejemplo, cada arco se podría etiquetar con el retardo promedio de un paquete de prueba estándar, determinado por una serie de pruebas cada hora. Con estas etiquetas en el grafo, la ruta más corta es la ruta más rápida, en lugar de la ruta con menos arcos o kilómetros.

Para determinar las distancias mínimas se pueden usar algoritmos bien conocidos como el algoritmo de Dijkstra.

### Inundación
Cuando se implementa un algoritmo de enrutamiento, cada enrutador debe tomar decisiones con base en el conocimiento local, no en la imagen completa de la red. Una técnica local simple es la **inundación**, en la que cada paquete entrante se envía en todas las líneas de salida, excepto en la línea por la que llegó.

Sin duda la inundación genera grandes cantidades de paquetes duplicados; de hecho, puede ser una cantidad infinita a menos que se tomen algunas medidas para limitar el proceso. Una de estas medidas es integrar un contador de saltos al encabezado de cada paquete, que disminuya con cada salto, y que el paquete se descarte cuando el contador llegue a cero (TtL). Lo ideal es inicializar el contador de saltos con la longitud de la ruta entre el origen y el destino. Si el emisor desconoce el tamaño de la ruta, puede inicializar el contador para el peor caso; a saber, el diámetro total de la red.

La inundación no es práctica para enviar la mayoría de los paquetes, pero tiene algunos usos importantes. En primer lugar, asegura que un paquete se entregue en todos los nodos de la red. Esto podría ser un desperdicio si sólo hay un destino que necesite el paquete, pero es efectivo para difundir información. En las redes inalámbricas, todos los mensajes transmitidos por una estación los pueden recibir todas las demás estaciones dentro de su alcance de radio, lo cual de hecho se puede considerar como inundación; algunos algoritmos usan esta propiedad.

En segundo lugar, la inundación es en extremo robusta. Incluso si grandes cantidades de enrutadores vuelan en pedazos (por ejemplo, en una red militar ubicada en una zona de guerra), la inundación encontrará una ruta, si es que existe, para transmitir un paquete a su destino. Además, la inundación requiere muy poca configuración. Los enrutadores sólo necesitan conocer a sus vecinos. Esto significa que la inundación se puede usar como bloque de construcción para otros algoritmos de enrutamiento que son más eficientes pero requieren una configuración un poco más complicada. La inundación también se puede usar como métrica con la que se pueden comparar otros algoritmos de enrutamiento. La inundación siempre selecciona la ruta más corta debido a que selecciona todas las rutas posibles en paralelo. En consecuencia, ningún otro algoritmo puede producir un retardo más corto (si ignoramos la sobrecarga generada por el proceso de inundación mismo).

Por lo general, las redes de computadoras utilizan algoritmos de enrutamiento dinámico más complejos que la inundación, pero más eficientes debido a que encuentran las rutas más cortas para la topología actual. En particular hay dos algoritmos dinámicos que son los más populares: el enrutamiento por vector de distancia y el enrutamiento por estado del enlace.

### Enrutamiento por vector distancia
El algoritmo de **enrutamiento por vector de distancia** opera haciendo que cada enrutador mantenga una tabla (es decir, un vector) que proporcione la mejor distancia conocida a cada destino y el enlace que se puede usar para llegar ahí. Para actualizar estas tablas se intercambia información con los vecinos. Eventualmente, todos los ruteadores conocen el mejor enlace para alcanzar cada destino.

En ocasiones, el algoritmo de enrutamiento por vector de distancia recibe otros nombres, de los cuales el más común es algoritmo de enrutamiento **Bellman-Ford** distribuido, en honor a los investigadores que lo desarrollaron. Éste fue el algoritmo original de enrutamiento de ARPANET y también se usó en [[Internet]] con el nombre de [[RIP]].

En el enrutamiento por vector de distancia, cada enrutador mantiene una tabla de enrutamiento indizada por (y que contiene una entrada de) cada enrutador de la red. Esta entrada consta de dos partes: la línea preferida de salida a usar para ese destino y una estimación del tiempo o distancia a ese destino. La distancia se podría medir como la cantidad de saltos, o se podría usar otra métrica, como vimos al calcular las rutas más cortas.

#### El problema del conteo infinito
Al proceso de establecer los enrutamientos con base en las mejores rutas a través de la red se le conoce como **convergencia**. El enrutamiento por vector de distancia es útil como una simple técnica mediante la cual los enrutadores pueden calcular las rutas más cortas en forma colectiva, pero tiene una grave desventaja en la práctica: aunque converge hacia la respuesta correcta, puede llegar a hacerlo con lentitud. Básicamente reacciona rápido a las buenas noticias, pero es lento con las malas. Considere un enrutador cuya mejor ruta al destino X es larga. Si en el siguiente intercambio el vecino A informa de manera repentina un retardo corto a X, el enrutador simplemente cambia y usa la línea A para enviar tráfico a X. En un intercambio de vectores, se procesan las buenas noticias.

![[el_problema_del_conteo_infinito.png]]

En la anterior figura debe quedar clara la razón por la que las malas noticias viajan con lentitud: no hay ningún enrutador que tenga en algún momento un valor mayor en más de una unidad que el mínimo de todos sus vecinos. Gradualmente, todos los enrutadores elevan su cuenta hacia el infinito, pero el número de intercambios requerido depende del valor numérico usado para el infinito. Por esta razón, es prudente hacer que el infinito sea igual a la ruta más larga, más 1.

No es del todo sorprendente que a éste se le conozca como el problema del **conteo al infinito**. Se han dado muchos intentos por resolverlo; por ejemplo, evitar que los enrutadores anuncien sus mejores rutas de vuelta a los vecinos de quienes las escucharon mediante la regla del horizonte dividido con envenenamiento en reversa que se describe en el RFC 1058. Sin embargo, ninguna de estas heurísticas funciona bien en la práctica a pesar de los nombres tan coloridos.

> El núcleo del problema es que, cuando X dice a Y que tiene una ruta hacia alguna parte, Y no tiene forma de saber si él mismo está en esa ruta.

### Enrutamiento por estado del enlace
La idea detrás del **enrutamiento por estado del enlace** es bastante simple y se puede enunciar en cinco partes. Cada enrutador debe realizar lo siguiente para hacerlo funcionar:
1. Descubrir a sus vecinos y conocer sus direcciones de red. 
2. Establecer la métrica de distancia o de costo para cada uno de sus vecinos. 
3. Construir un paquete que indique todo lo que acaba de aprender. 
4. Enviar este paquete a todos los demás enrutadores y recibir paquetes de ellos. 
5. Calcular la ruta más corta a todos los demás enrutadores

De hecho, se distribuye la topología completa a todos los enrutadores. Después se puede ejecutar el algoritmo de Dijkstra en cada enrutador para encontrar la ruta más corta a los demás enrutadores.

#### Aprender sobre los vecinos
Cuando un enrutador se pone en funcionamiento, su primera tarea es averiguar quiénes son sus vecinos. Para lograr esto envía un paquete especial HELLO en cada línea punto a punto. Se espera que el enrutador del otro extremo regrese una respuesta en la que indique su nombre. Estos nombres deben ser globalmente únicos puesto que, cuando un enrutador distante escucha después que hay tres enrutadores conectados a F, es indispensable que pueda determinar si los tres se refieren al mismo F.

#### Establecimiento de los costos de los enlaces
El algoritmo de enrutamiento por estado del enlace requiere que cada enlace tenga una métrica de distancia o costo para encontrar las rutas más cortas. El costo para llegar a los vecinos se puede establecer de modo automático, o el operador de red lo puede configurar. Una elección común es hacer el costo inversamente proporcional al ancho de banda del enlace. Por ejemplo, una red Ethernet de 1 Gbps puede tener un costo de 1 y una red Ethernet de 100 Mbps un costo de 10. Esto hace que las rutas de mayor capacidad sean mejores opciones.

Si la red está geográficamente dispersa, el retardo de los enlaces se puede considerar en el costo, de modo que las rutas a través de enlaces más cortos sean mejores opciones. La manera más directa de determinar este retardo es enviar un paquete especial ECO a través de la línea, que el otro extremo tendrá que regresar de inmediato. Si se mide el tiempo de ida y vuelta, y se divide entre dos, el enrutador emisor puede obtener una estimación razonable del retardo.

#### Construcción de los paquetes de estado del enlace
Una vez que se ha recabado la información necesaria para el intercambio, el siguiente paso es que cada enrutador construya un paquete que contenga todos los datos. El paquete comienza con la identidad del emisor, seguida de un número de secuencia, una edad y una lista de vecinos. También se proporciona el costo para cada vecino.

![[enrutamiento_de_estado_del_enlace_paquetes.png]]

Es fácil construir los paquetes de estado del enlace. La parte difícil es determinar cuándo construirlos. Una posibilidad es construirlos de manera periódica; es decir, a intervalos regulares. Otra posibilidad es construirlos cuando ocurra un evento significativo, como la caída o la reactivación de una línea o de un vecino, o cuando sus propiedades cambien en forma considerable.

#### Distribución de los paquetes de estado del enlace
Esta es la parte más complicada del algoritmo es la distribución de los paquetes de estado del enlace. Todos los enrutadores deben recibir todos los paquetes de estado del enlace con rapidez y confiabilidad. Si se utilizan distintas versiones de la topología, las rutas que se calculen podrían tener inconsistencias como ciclos, máquinas inalcanzables y otros problemas.

La idea fundamental es utilizar inundación para distribuir los paquetes de estado del enlace a todos los enrutadores. Con el fin de mantener controlada la inundación, cada paquete contiene un número de secuencia que se incrementa con cada nuevo paquete enviado. Los enrutadores llevan el registro de todos los pares (enrutador de origen, secuencia) que ven. Cuando llega un nuevo paquete de estado del enlace, se verifica y compara con la lista de paquetes ya vistos. Si es nuevo, se reenvía a través de todas las líneas, excepto aquella por la que llegó. Si es un duplicado, se descarta. Si llega un paquete con número de secuencia menor que el mayor visto hasta el momento, se rechaza como obsoleto debido a que el enrutador tiene datos más recientes.

Este algoritmo tiene algunos problemas, pero son manejables. Primero, si los números de secuencia vuelven a comenzar, reinará la confusión. La solución aquí es utilizar un número de secuencia de 32 bits. Con un paquete de estado del enlace por segundo, el tiempo para volver a empezar será de 137 años, por lo que podemos ignorar esta posibilidad.

Segundo, si llega a fallar un enrutador, perderá el registro de su número de secuencia. Si comienza nuevamente en 0, se rechazará como duplicado el siguiente paquete que envíe.

Tercero, si llega a corromperse un número de secuencia y se recibe 65540 en vez de 4 (un error de 1 bit), los paquetes 5 a 65 540 se rechazarán como obsoletos, dado que se piensa que el número de secuencia actual es 65 540.

La solución a todos estos problemas es incluir la edad de cada paquete después del número de secuencia y disminuirla una vez cada segundo. Cuando la edad llega a cero, se descarta la información de ese enrutador. Por lo general, un paquete nuevo entra, por ejemplo, cada 10 segundos, por lo que la información de los enrutadores sólo expira cuando un enrutador está caído (o cuando se pierden seis paquetes consecutivos, un evento poco probable). Los enrutadores también decrementan el campo Edad durante el proceso inicial de inundación para asegurar que no pueda perderse ningún paquete y sobrevivir durante un periodo de tiempo indefinido (se descarta el paquete cuya edad sea cero)

#### Cálculo de las nuevas rutas
Ahora se puede ejecutar localmente el algoritmo de Dijkstra para construir las rutas más cortas a todos los destinos posibles. Los resultados de este algoritmo indican al enrutador qué enlace debe usar para llegar a cada destino. Esta información se instala en las tablas de enrutamiento y se puede reanudar la operación normal.

En comparación con el enrutamiento por vector de distancia, el enrutamiento por estado del enlace requiere más memoria y poder de cómputo. Para una red con n enrutadores, cada uno de los cuales tiene k vecinos, la memoria requerida para almacenar los datos de entrada es proporcional a kn, que es por lo menos tan grande como una tabla de enrutamiento que lista todos los destinos. Además, el tiempo de cómputo también crece con más rapidez que kn, incluso con las estructuras de datos más eficientes; un problema en las grandes redes. Sin embargo, en muchas situaciones prácticas, el enrutamiento por estado del enlace funciona bien debido a que no sufre de los problemas de convergencia lenta.

### Enrutamiento jerárquico
Cuando se utiliza el enrutamiento jerárquico, los enrutadores se dividen en lo que llamaremos **regiones**. Cada enrutador conoce todos los detalles para enrutar paquetes a destinos dentro de su propia región, pero no sabe nada de la estructura interna de las otras regiones. Cuando se interconectan diferentes redes, es natural considerar cada una como región independiente con el fin de liberar a los enrutadores de una red de la necesidad de conocer la estructura topológica de las demás redes.

![[enrutamiento_jerarquico.png]]

### Enrutamiento intradominio
![[Enrutamiento intradominio]]

### Enrutamiento intredominio
![[Enrutamiento intredominio]]