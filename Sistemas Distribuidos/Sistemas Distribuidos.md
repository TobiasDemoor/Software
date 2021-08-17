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

# ¿Qué queremos obtener?
## Soportar compartir recursos
Ejemplos canonicos
- Almacenamiento basado “en la nube” 
- Streaming multimedia asistido por redes P2P 
- Servicios de email compartido 
- Web hosting compartido (content distribution networks)

## Transparencia de distribución

## Apertura 
Ser capaces de interactuar con servicios de otros sistemas abiertos, independientemente del sistema subyacente
- Los sistemas deben utilizar interfaces bien definidas 
- Deberían interoperar fácilmente 
- Portabilidad de aplicaciones 
- Fácilmente extensibles

## Escalabilidad
“capacidad de crecer a un costo razonable” 
- ¿Que es ser escalable? 
- ¿Cuanto? ¿Cómo?
Características de los algoritmos descentralizados
- Ninguna máquina tiene información completa del estado del sistema
- Las distintas máquinas toman decisiones basadas solo en información local 
- La falla de un equipo no arruina todo el algoritmo 
- No se asume que existe un reloj global

Tipos de escalabilidad
**Escalabilidad respecto del tamaño**
	¿Cúantos usuarios pueden usar mi sistema?
	Se puede solucionar en un principio con mejoras en el hardware.
**Escalabilidad geográfica**
	¿Dónde pueden estar los usuarios que utilizan mi sistema?
	La escalabilidad geográfica tiene que ver con los inconvenientes que surgen al distribuirse el sistema en distancias grandes, empieza a haber latencia considerable. Una solución a esto es al comunicación asíncrona.
**Escalabilidad administrativa**
	¿Cómo se administra mi sistema a medida que crece? (Ejemplo, República Popular China, personal)

# Políticas vs Mecanismos
## Políticas
- ¿Qué tipo de consistencia requerimos para los datos en el cache de cliente? 
- ¿Que operaciones permitimos realizar a código descargado? 
- ¿Como podemos acomdar el tipo de requerimientos cuando el ancho de banda varía? 
- ¿Qué grado de secreto necesitamos para la comunicación?

## Mecanismos 
- Permitir la modificación dinamica de las politicas de caching 
- Soportar diferentes niveles de confianza para código movil 
- Proveer parámetros ajustables de calidad de servicio por stream de datos 
- Ofrecer la posibilidad de distintos algoritmos de cifrado

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
