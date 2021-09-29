## Definición
*Aquellos sistemas que tienen componentes que están en distinto hardware conectados por una [[Redes de computadoras|red]].*

>**“Colección de elementos autónomos de computación que se presentan a los usuarios como un sistema único y coherente”.** - (Tanenbaum, Van Steen)

>“Sistema en el cual tenemos componentes comunicados por una red de computadoras coordinando sus acciones mediante el intercambio de mensajes” - (Coulouris et al)

La definición de Tannenbaum y Van Steen se refiere a dos características principales de los sistemas distribuidos. La primera es que un sistema distribuido es una colección de elementos autonomos de computacion (**[[Nodo|nodos]]**). La segunda es que los usuarios o aplicaciones lo perciben como un **sistema único** (es [[Transparencia|transparente]]). Es decir que los nodos **necesitan colaborar**. Cómo establecer esta colaboración yace en el centro del desarrollo de los sistemas distribuidos.

### Colección de elementos autónomos
Los sistemas distribuidos modernos usualmente están compuestos por todo tipo de nodos, desde equipos muy grandes y de altísima [[Performance|performance]] hasta computadores diminutos. Un principio fundamental es que los nodos pueden actuar independientemente de los otros. Los nodos están programados para lograr objetivos comunos, lo cual logran mediante el intercambio de **mensajes** entre ellos. Un nodo responde a los mensajes entrantes los cuales son procesados y desencadenan el envío de más mensajes perpetuando así la comunicación.
Un observación relevante es que al estar tratando con nodos independientes no hay un **[[Reloj físico|reloj global]]**, sino que cada [[Componente|componente]] tiene su propia noción del tiempo. La falta de esta referencia común lleva a preguntas fundamentales en lo que respecta a la **[[Sincronización|sincronización y coordinación]]** dentro del sistema.
El hecho de trabajar con un conjunto de nodos también hace que tengamos que administrar la pertenencia a distintos **grupos** y la organización de estos. Es decir que debemos registrar que nodos pueden o no **pertenecer al sistema**. El manejo de la pertenencia a los distintos grupos es un tema complejo el cuál tiene un efecto sobre la [[Performance|performance]] del sistema y sobre la **seguridad** del mismo.
En lo que respecta a la **organización de la colección**, en la práctica se puede observar que los sistemas distribuidos usualmente están organizados como un **[[Overlay Network|red superpuesta]]**).

### Sistema único y coherente
Como fue mencionado, un sistema distribuido debería aparentar ser un sistema único y coherente. Se podría afirmar que un sistema es coherente si su comportamiento se adecua a las expectativas del usuario. Más específicamente, en un sistema único y coherente la colección de nodos opera como un todo opera de la misma manera, sin importar dónde, cuándo, o cómo se lleve a cabo la interacción entre el usuario y el sistema.
Para ofrecer una visión única y coherente se requiere que el usuario no pueda deterinar exactamente en cuál dispositvo se está ejecutando un proceso. Así mismo la localización de la información no debería ser relevante y tampoco debería ser relevante que el sistema esté replicando información para mejorar la [[Performance|performance]]. A esto se le llama **[[Transparencia de distribución|transparencia de distribución]]**.

## Objetivos de diseño
### Soportar compartir recursos
Un objetivo importante de un sistema distribuido es facilitar a los usuarios (y aplicaciones) acceder y compartir recursos remotos. Ejemplos canonicos:
- Almacenamiento basado “en la nube” .
- Streaming multimedia asistido por redes [[P2P]] .
- Servicios de email compartido.
- Web hosting compartido ([[CDN]])

### Transparencia de distribución
![[Transparencia de distribución]]

### Apertura 
Los sistemas deben ser capaces de interactuar con servicios de otros sistemas abiertos, independientemente del sistema subyacente.

**Los sistemas deben utilizar interfaces bien definidas.** Los componentes deberían adherir a estándares que describen la [[Sintaxis|sintaxis]] y [[Semántica|semántica]] de qué pueden ofrecer esos componentes. Una técnica general es definir servicios a través de **interfaces** usando un **Interface Definition Language** (IDL). Estas definiciones especifícan con precisión los nombres de las funciones junto con sus parámetros, valores de retorno, excepciones posibles, etc (la sintáxis). Lo más complicado de especificar es qué hacen precisamente los servicios (la semántica), usualmente estas definiciones se dan en un lenguaje informal.

La definición completa y neutral de las interfaces es de suma importancia para la interoperabilidad y la portabilidad. La **interoperabilidad** caracteriza el punto al que dos implementaciones de sistemas o componentes de fabricantes distintos pueden coexistir y trabajar juntos solamente dependiento en los servicios del otro tal como están especificados en el estandar común. La **portabilidad** caracteriza el punto al que una aplicación desarrollada para un sistema distribuido puede ser ejecutada, sin modificación, en un sistema distinto que implementa las mismas interfaces que el primero.

Un sistema distribuido abierto debería ser también **extensible**. Es decir, debería ser relativamente simple añadir partes que corren en [[Sistemas Operativos|sistemas operativos]] distintos, o hasta reemplazar un sistema de archivos entero.

Para lograr flexibilidad en sistemas distribuidos abiertos, es vital que el sistema esté organizado como una colección de componentes relativamente pequeños y fácilmente reemplazables o adaptables. Esto implica que se deberían proveer definiciones no solo de las interfaces de más alto nivel (las vistas por usuarios y aplicaciones), pero también de las interfaces internas.

Lo que necesitamos es una separación entre [[Políticas vs Mecanismos|política y mecanismo]]

### Escalabilidad
![[Escalabilidad]]

#### Características de los algoritmos descentralizados
- Ninguna máquina tiene información completa del estado del sistema
- Las distintas máquinas toman decisiones basadas solo en información local 
- La falla de un equipo no arruina todo el algoritmo 
- No se asume que existe un [[Reloj físico|reloj global]].

## Errores frecuentes
Los sistemas distribuidos difieren de los sistemas tradicionales centralizados al tener componentes distribuidos a lo largo de una red. El hecho de no tener en cuenta esta distribución de los componentes lleva a cometer errores en el desarrollo relacionados con asumir que:
- La red es confiable
- La red es segura
- La red es homogénea
- La topología no cambia
- La [[Latencia|latencia]] es cero
- El [[Ancho de banda|ancho de banda]] es infinito
- El costo del transporte es cero
- Existe un administrador

## Tipos de sistemas distribuidos
### High performance distributed computing
#### Cluster computing
El hardware subyacente consiste de una colección de workstations similares, conectadas mediante una LAN de alta velocidad. Además cada nodo corre el mismo [[Sistemas Operativos|sistema operativo]]. Se caracteriza por la homogeneidad entre los nodos. Se suele usar para programación paralela en la cual un único programa (de uso intensivo de CPU) es ejecutado de forma paralela en múltiples computadoras.

Cada cluster consiste de un conjunto de nodos que son controlados y accedidos por un único nodo maestro. Este nodo, típicamente administra la Alocación en los nodos para un programa paralelo particular y mantiene una cola de los trabajos solicitados. Además, provee a los usuarios de una interfaz del sistema.

#### Gird Computing
Similar al tipo clúster, pero los nodos computacionales que lo conforman pueden ser distintos en cuanto hardware, sistema operativo o tecnologías de red debido a los diferentes dominios administrativos. Los nodos están configurados para tareas específicas.

Este subgrupo consiste de sistemas distribuidos usualmente construidos como una federación de sistemas de computación, donde cada sistema puede caer bajo un dominio administrativo diferente, y puede ser muy diferente en lo que se refiere al hardware, software, y la tecnología de red.

![[sistemas_distribuidos_grid_computing.png]]

* **Fabric layer.** Provee interfaces a los recursos locales en un sitio en específico. Estas interfaces están diseñadas para permitir el uso compartido de recursos en una organización virtual.
* **Connectivity layer.** Consiste en protocolos de comunicación para dar soporte a las transacciones grid que suponen el uso de múltiples recursos. También contiene protocolos de seguridad para autenticar usuarios y recursos.
* **Resource layer.** Es responsable por administrar un solo recurso en particular (operaciones tales como crear un proceso o almacenar algún dato). Usas las funciones proporcionadas por la capa de conectividad y llama directamente a las interfaces del fabric layer. Se encarga del control de acceso (protección).
* **Collective layer.** Maneja el acceso a múltiples recursos y típicamente consiste en servicios para descubrimiento de recursos, alojamiento y planificación de tareas sobre múltiples recursos, replicación de datos, etc.
* **Application layer.** Consiste en las aplicaciones que operan en la organización virtual y que hacen uso del entorno de computación grid.

Las capas de Resource, Collective y Connectivity vendrían a ser el [[Middleware|middleware]] del sistema tipo grid, dado que manejan el acceso a los recursos que se encuentran potencialmente distribuidos en múltiples sitios

#### Cloud computing
Se trata de proveer los servicios para construir dinámicamente la infraestructura y componer lo que sea necesario a partir de los servicios disponibles. Cloud computing está caracterizado por un conjunto de recursos virtualizados facilmente utilizables y accesibles. La idea principal del cloud es abstraer al usuario de todas las capas inferiores.

En la práctica cloud está organizado en cuatro capas:

**Hardware:** la capa más baja formada por los medios para manejar el hardware necesario (procesadores, routers, sistemas de cooling, etc.). Es implementada generalmente en data centers y contiene los recursos que los clientes normalmente no pueden ver directamente.

**Infrastructure:** una capa importante que forma la columna vertebral de la mayor parte de las plataformas de cloud computing. Implementa técnicas de [[Virtualización|virtualización]] para proveer a los clientes una infraestructura consistente de almacenamiento virtual y recursos de computo.
   
Los servicios IaaS a menudo ofrecen recursos como imágenes de disco de [[Virtualización|máquinas virtuales]], almacenamiento orientado a bloques , almacenamiento de archivos u objetos, firewalls, balanceadores de carga, direcciones IP públicas, redes de área local virtual (VLAN)

**Platform:** se puede argumentar que la capa de plataforma provee al cliente de cloud computing lo que un [[Sistemas Operativos|sistema operativo]] provee a los developers de aplicaciones, osea los medios para desarrollar y deployar aplicaciones con facilidad. En la práctica se le ofrece al developer una [[API]] específica del proveedor que incluye las llamadas para subir y ejecutar un programa en el cloud de dicho proveedor. Al igual que los [[Sistemas Operativos|sistemas operativos]], la capa de plataforma provee abstracciones de más alto nivel para el almacenamiento y el resto de los recursos.

**Application:** aplicaciones completas corren en esta capa y son ofrecidas a los usuarios para mayor customización. Estas aplicaciones son ejecutadas en el cloud del proveedor.

El proveedor forece estas capas a sus clientes mediante varias interfaces, llevando a la definicion de diferentes tipos de servicios:
- **Infrastructure-as-a-Service (IaaS)** que incluye las capas de hardware e infraestructura.
- **Platform-as-a-Service (PaaS)** para la capa de plataforma.
- **Software-as-a-Service (SaaS)** para la capa de aplicación.

### Distributed Information Systems
Una clase importante de sistema distribuido se encuentra en las organizaciones que tienen una gran cantidad de aplicaciones interconectadas, en estos caso la interoperabilidad de estas aplicaciones se vuelve un punto importante a considerar. Si un programa cliente envia un request que incluye varios request menores (posiblemente para diferentes servers) debe ser ejecutado como una [[Distributed Transactions|transacción distribuida]].

### Pervasive systems (IoT)
Los sistemas antes descriptos se caracterizan por su estabilidad, los nodos son fijos y tienen conexiones de red más o menos permanentes y de alta calidad. Sin embargo, luego de la introducción de dispositivos móviles y embebidos ha habido un cambio que ha llevado a lo que usualmente se denominan **pervasive systems** (literalmente "sistema penetrante"). Estos sistemas se caracterizan y están diseñados para mezclarse en nuestro entorno, son naturalemente sistemas distribuidos.

Lo que los hace únicos en comparación a los anteriores es que *la separación entre usuarios y componentes del sistema está mucho menos definida*. Usualmente no hay una sola interfaz dedicada, sino que un pervasive system está equipado con muchos sensores que registran varios aspectos del comportamiento del usuario. A su vez puede tener un conjunto de actuadores para proveer información y feedback, usualmente hasta intencionalmente buscando modificar el comportamiento.

#### Sistemas ubicuos
En este tipo de sistema se avanza un poco más, el sistema es pervasive y continuamente presente. Osea que el usuario va a estar continuamente interactuando con el sistema, usualmente sin estar al tento de esto. Hay 5 requerimientos principales para que un sistema sea ubicuo:

1. **Distribution** los dispositivos están conectados, distribuidos, y accesibles de una manera transparente.
2. **Interaction** la interacción entre los usuarios y dispositivos es altamente unobtrusive ("discreta").
3. **Context awareness** el sistema está al tanto del contexto del usuario para poder optimizar su interacción.
4. **Autonomy** los dispositivos operan autonomamente sin intervención humana, y por lo tanto son altamente autoadministrados.
5. **Intelligence** el sistema como un todo debe manejar un gran rango de acciones e interacciones dinámicas.

#### Mobile computing systems
En un sistema distribuido móvil se asume que la ubicación de los dispositivos es cambiante. Una ubicación cambiante trae sus inconvenientes, por ejemplo si la ubicación de un dispositivo cambia regularmente también puede ser el caso para los servicios localmente disponibles. Como consecuencia de esto podríamos tener que prestar especial atención a descubrir dinámicamente servicios, y también permitir a los servicios anunciar su presencia.

Las ubicaciones cambiantes tienen un profundo efecto en la comunicación. Consideremos un MANET (mobile ad hoc network). supongamos que dos dispositivos en un MANET se han descubierto (en el sentido que conocen su dirección), ¿cómo ruteamos mensajes entre estos dos? Las rutas estáticas generalmente no son sostenibles ya que los nodos en el camino de routing pueden moverse fuera del rango del vecino invalidando el camino. Para MANETs grandes, usar caminos establecidos a priori no es una opción viable tampoco. Estamos lideando con lo que se llama redes tolerantes a disrupción o **disruption-tolerant networs**, que son redes en las cuales la conectividad entre dos nodos no puede asegurarse.

#### Sensor networks
Una sensor network generalmente consiste de decenas hasta centenas o miles de nodos relativamente pequeños, cada uno equipado con uno o más dispositivos de medición. A su vez los nodos también pueden actuar como actuators.

## Bibliografía
En su gran mayoría el contenido teórico relacionado a los sistemas distribuidos ha sido obtenido del libro Distributed Systems Version 3.0.1 - van Steen, Tannenbaum