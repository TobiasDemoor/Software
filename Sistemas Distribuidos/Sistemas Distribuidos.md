# Definición
*Aquellos sistemas que tienen componentes que están en distinto hardware conectados por una red.*

>**“Colección de elementos autónomos de computación que se presentan a los usuarios como un sistema único y coherente”.** - (Tanenbaum, Van Steen)

>“Sistema en el cual tenemos componentes comunicados por una red de computadoras coordinando sus acciones mediante el intercambio de mensajes” - (Coulouris et al)

La definición de Tannenbaum y Van Steen se refiere a dos características principales de los sistemas distribuidos. La primera es que un sistema distribuido es una colección de elementos autonomos de computacion (nodos). Los cuales pueden ser dispositivos de hardware o procesos de software. La segunda es que los usuarios o aplicaciones lo perciben como un sistema único (es [[Transparencia|transparente]]). Es decir que los nodos necesitan colaborar. Cómo establecer esta colaboración yace en el centro del desarrollo de los sistemas distribuidos.

## Colección de elementos autónomos
Los sistemas distribuidos modernos usualmente están compuestos por todo tipo de nodos, desde equipos muy grandes y de altísima performance hasta computadores diminutos. Un principio fundamental es que los nodos pueden actuar independientemente de los otros. Los nodos están programados para lograr objetivos comunos, lo cual logran mediante el intercambio de **mensajes** entre ellos. Un nodo responde a los mensajes entrantes los cuales son procesados y desencadenan el envío de más mensajes perpetuando así la comunicación.
Un observación relevante es que al estar tratando con nodos independientes no hay un **reloj global**, sino que cada componente tiene su propia noción del tiempo. La falta de esta referencia común lleva a preguntas fundamentales en lo que respecta a la **sincronización y coordinación** dentro del sistema.
El hecho de trabajar con un conjunto de nodos también hace que tengamos que administrar la pertenencia a distintos **grupos** y la organización de estos. Es decir que debemos registrar que nodos pueden o no **pertenecer al sistema**. El manejo de la pertenencia a los distintos grupos es un tema complejo el cuál tiene un efecto sobre la performance del sistema y sobre la **seguridad** del mismo.
En lo que respecta a la **organización de la colección**, en la práctica se puede observar que los sistemas distribuidos usualmente están organizados como un overlay network (**red superpuesta**). En este caso un nodo es típicamente un proceso de software equipado con una lista de otros procesos con los cuales puede comunicarse directamente. Hay dos tipos generales de overlay networks:
**Structured overlay**: En este caso cada nodo tiene un conjunto bien definido de vecinos con los cuales puede comunicarse. Por ejemplo, una estructura de arbol o de anillo.
**Unstructured overlay**: En este caso cada nodo tiene un número de referencias a nodos seleccionados aleatoriamente.
En cualquier caso un overlay network debería siempre ser conexa. Una clase conocida de overlays está formada por peer-to-peer (P2P) networks.

## Sistema único y coherente
Como fue mencionado, un sistema distribuido debería aparentar ser un sistema único y coherente. Se podría afirmar que un sistema es coherente si su comportamiento se adecua a las expectativas del usuario. Más específicamente, en un sistema único y coherente la colección de nodos opera como un todo opera de la misma manera, sin importar dónde, cuándo, o cómo se lleve a cabo la interacción entre el usuario y el sistema.
Para ofrecer una visión única y coherente se requiere que el usuario no pueda deterinar exactamente en cuál dispositvo se está ejecutando un proceso. Así mismo la localización de la información no debería ser relevante y tampoco debería ser relevante que el sistema esté replicando información para mejorar la performance. A esto se le llama **transparencia de distribución**.

# Objetivos de diseño
## Soportar compartir recursos
Un objetivo importante de un sistema distribuido es facilitar a los usuarios (y aplicaciones) acceder y compartir recursos remotos. Ejemplos canonicos:
- Almacenamiento basado “en la nube” 
- Streaming multimedia asistido por redes P2P 
- Servicios de email compartido 
- Web hosting compartido (content distribution networks)

## Transparencia de distribución
Definido en [[Transparencia de distribución]].

## Apertura 
Ser capaces de interactuar con servicios de otros sistemas abiertos, independientemente del sistema subyacente.

**Los sistemas deben utilizar interfaces bien definidas.** Los componentes deberían adherir a estándares que describen la sintaxis y semántica de qué pueden ofrecer esos componentes. Una técnica general es definir servicios a través de **interfaces** usando un **Interface Definition Language** (IDL). Estas definiciones especifícan con precisión los nombres de las funciones junto con sus parámetros, valores de retorno, excepciones posibles, etc (la sintáxis). Lo más complicado de especificar es qué hacen precisamente los servicios (la semántica), usualmente estas definiciones se dan en un lenguaje informal.

La definición completa y neutral de las interfaces es de suma inportancia para la interoperabilidad y la portabilidad. La **interoperabilidad** caracteriza el punto al que dos implementaciones de sistemas o componentes de fabricantes distintos pueden coexistir y trabajar juntos solamente dependiento en los servicios del otro tal como están especificados en el estandar común. La **portabilidad** caracteriza el punto al que una aplicación desarrollada para un sistema distribuido puede ser ejecutada, sin modificación, en un sistema distinto que implementa las mismas interfaces que el primero.

Un sistema distribuido abierto debería ser también **extensible**. Es decir, debería ser relativamente simple añadir partes que corren en sistemas operativos distintos, o hasta reemplazar un sistema de archivos entero.

Para lograr flexibilidad en sistemas distribuidos abiertos, es vital que el sistema esté organizado como una colección de componentes relativamente pequeños y fácilmente reemplazables o adaptables. Esto implica que se deberían proveer definiciones no solo de las interfaces de más alto nivel (las vistas por usuarios y aplicaciones), pero también de las interfaces internas.
Lo que necesitamos es una separación entre [[Políticas vs Mecanismos|política y mecanismo]]

## Escalabilidad
“capacidad de crecer a un costo razonable” 
- ¿Que es ser escalable? 
- ¿Cuanto? ¿Cómo?
Características de los algoritmos descentralizados
- Ninguna máquina tiene información completa del estado del sistema
- Las distintas máquinas toman decisiones basadas solo en información local 
- La falla de un equipo no arruina todo el algoritmo 
- No se asume que existe un reloj global

### Dimensiones de la escalabilidad
La escalabilidad de un sistema puede medirse sobre tres dimensiones distintas:
**Escalabilidad respecto del tamaño**
	¿Cúantos usuarios pueden usar mi sistema?
	Se puede solucionar en un principio con mejoras en el hardware.
**Escalabilidad geográfica**
	¿Dónde pueden estar los usuarios que utilizan mi sistema y los recursos que lo componen?
	La escalabilidad geográfica tiene que ver con los inconvenientes que surgen al distribuirse el sistema en distancias grandes, empieza a haber latencia considerable. Una solución a esto es al comunicación asíncrona.
**Escalabilidad administrativa**
	¿Cómo se administra mi sistema a medida que crece? (Ejemplo, República Popular China, personal)

# Errores frecuentes
Cuando se viene de diseñar sistemas centralizados a diseñar sistemas distribuidos hay una serie de suposiciones que son erroneas:
- La red es confiable
- La red es segura
- La red es homogénea
- La topología no cambia
- La latencia es cero
- El ancho de banda es infinito
- El costo del transporte es cero
- Existe un administrador

# Tipos de sistemas distribuidos
