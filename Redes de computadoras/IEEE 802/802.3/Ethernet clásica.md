## Cableado
|        Nombre        |             Cable             | Max. segmento | Nodos/segmento | Ventajas                 |
|:--------------------:|:-----------------------------:| ------------- | -------------- | ------------------------ |
|  10Base5 <br> 802.3  | Thick [[Cable coaxial\|coax]] | 500 m         | 100            | Original, ahora obsoleta |
| 10Base2 <br> 802.3a  | Thin [[Cable coaxial\|coax]]  | 185 m         | 30             | No se requiere [[Hub]]   |
| 10Base-T <br> 802.3i |       [[Par trenzado]]        | 100 m         | 1024           | Muy barato               |
| 10Base-F <br> 802.3j |       [[Fibra óptica]]        | 2000 m        | 1024           | Entre edificios          |

Hasta 10Base2 la topología física era un bus. A partir de 10Base-T pasa a ser una estrella. El 10 es la velocidad (10 Mbps) y el "Base" es de [[Transmisión en banda base|banda base]].

## Protocolo MAC
El formato utilizado por el protocolo de la [[Subcapa MAC|subcapa MAC]] de la Ethernet clásica para enviar tramas se muestra en la figura 4-14. Primero viene un Preámbulo de 8 bytes, cada uno de los cuales contiene el patrón de bits 10101010 (con la excepción del último byte, en el que los últimos 2 bits se establecen a 11). Este último byte se llama delimitador de Inicio de trama en el 802.3. La [[Codificación Manchester|codificación Manchester]] de este patrón produce una onda cuadrada de 10 MHz durante 6.4 μseg para permitir que el reloj del receptor se sincronice con el del emisor. Los últimos dos bits indican al receptor que está a punto de empezar el resto de la trama

![[RRCC_ethernet_clasica_protocolo_mac.png]]

Después vienen dos direcciones, una para el destino y una para el origen. Cada una de ellas tiene una longitud de 6 bytes. El primer bit transmitido de la dirección de destino es un 0 para direcciones ordinarias y un 1 para direcciones de grupo. Las direcciones de grupo permiten que varias estaciones escuchen en una sola dirección. Cuando una trama se envía a una dirección de grupo, todas las estaciones del grupo la reciben. El envío a un grupo de estaciones se llama [[Multicast|multicasting]]. La dirección especial que consiste únicamente en bits 1 (FF:FF:FF:FF:FF:FF) está reservada para [[Broadcast|broadcasting]]. Una trama que contiene sólo bits 1 en el campo de destino se acepta en todas las estaciones de la red.

Una característica interesante de las direcciones de origen de las estaciones es que son globalmente únicas; el IEEE las asigna de manera central para asegurar que no haya dos estaciones en el mundo con la misma dirección. La idea es que cualquier estación pueda direccionar de manera exclusiva cualquier otra estación con sólo dar el número correcto de 48 bits. Para hacer esto, se utilizan los primeros 3 bytes del campo de dirección para un **OUI (Organizationally Unique Identifier)**.

A continuación está el campo Tipo o Longitud, dependiendo de si la trama es Ethernet o IEEE 802.3. Ethernet usa un campo Tipo para indicar al receptor qué hacer con la trama. Es posible utilizar múltiples protocolos de capa de red al mismo tiempo en la misma máquina, por lo que cuando llega una trama de Ethernet, el sistema operativo tiene que saber a cuál entregarle la trama. El campo Tipo especifica a qué proceso darle la trama. Por ejemplo, un código de tipo de 0x0800 significa que los datos contienen un paquete IPv4.

Después están los datos, de hasta 1500 bytes. Este límite fue elegido de manera algo arbitraria cuando se estableció el estándar Ethernet. Además de haber una longitud de trama máxima, también hay una **longitud mínima**. Si bien algunas veces un campo de datos de 0 bytes es útil, causa problemas. Cuando un transceptor detecta una colisión, trunca la trama actual, lo que significa que los bits perdidos y las piezas de las tramas aparecen todo el tiempo en el cable. Para que Ethernet pueda distinguir con facilidad las tramas válidas de lo inservible, necesita que dichas tramas tengan una longitud de por lo menos 64 bytes, de la dirección de destino a la suma de verificación, incluyendo ambas. Si la porción de datos de una trama es menor que 46 bytes, el campo de Relleno se utiliza para completar la trama al tamaño mínimo.

Otra razón (más importante) para tener una trama de longitud mínima es evitar que una estación complete la transmisión de una trama corta antes de que el primer bit llegue al extremo más alejado del cable, donde podría tener una colisión con otra trama ([[#Detección de colisiones]]).

Ethernet clásica utiliza el algorítmo [[CSMA#CSMA/CD|CSMA/CD persistente-1]].

## Detección de colisiones
Al tener un medio con características conocidas se pueden detectar colisiones. Al colisionar dos paquetes la potencia recibida es mayor a la enviada (desde la perspectiva de una estación) y así es como se detecta la colisión. La detección de colisiones puede tardar a lo sumo $2\tau$ siendo $\tau$ el tiempo de propagación entre emisor y receptor. Podemos conocer el tiempo para el peor caso ya que todo está cronometrado y ya que la red está construida acorde a especificaciones específicas (es por esto que hay un límite a la cantidad de [[Repeater|repetidores]]). El valor entonces será $2\tau = 50 \mu s$.

![[RRCC_ethernet_deteccion_de_colisiones_1.png]]

Cuando B detecta que está recibiendo más potencia de la que está enviando, sabe que ha ocurrido una colisión, por lo que aborta su transmisión y genera una ráfaga de ruido de 48 bits para avisar a las demás estaciones. En otras palabras, bloquea el cable para asegurarse de que el emisor no ignore la colisión.

Ethernet tiene una tamaño mínimo de trama de 64 bytes (512 bits), esta surge porque es la consecuencia de usar [[CSMA#CSMA CD|CSMA/CD]] a 10 Mbps donde $2\tau = 50 \mu s$ (sería necesario un mínimo de 500 bits pero se redondea a 512 para mayor seguridad). El resultado de esto es que todo el tiempo que se está esperando se están enviando bits. La trama mínima es una consecuencia directa de CSMA/CD. Si una estación intenta transmitir una trama muy corta, es concebible que ocurra una colisión, pero la transmisión se completará antes de que la ráfaga de ruido llegue de regreso a la estación en $2\tau$. El emisor entonces supondrá de forma incorrecta que la trama se envió con éxito. También relacionado a esto es que el valor de la ranura sea el tiempo de 512 bits osea $51.2 \mu s$.

### Retroceso exponencial binario
Tras una colisión, el tiempo se divide en ranuras discretas cuya longitud es igual al tiempo de propagación de ida y vuelta para el peor de los casos en el cable ($2\tau$). Tomando en cuenta la ruta más larga permitida por Ethernet, el tiempo de ranura se estableció en 512 tiempos de bit o $51.2 \mu s$.

Después de la primera colisión, cada estación espera 0 o 1 tiempos de ranura al azar antes de intentarlo de nuevo. Si dos estaciones entran en colisión y ambas escogen el mismo número aleatorio, habrá una nueva colisión. Después de la segunda colisión, cada una escoge 0, 1, 2 o 3 al azar y espera ese tiempo de ranura. Si ocurre una tercera colisión (la probabilidad de que esto suceda es de 0.25), entonces para la siguiente vez el número de ranuras a esperar se escogerá al azar del intervalo 0 a 2³ − 1.

En general, después de $i$ colisiones se elige un número aleatorio $\in [0; 2^i-1]$, y se salta ese número de ranuras. Sin embargo, al llegar a 10 colisiones el intervalo de aleatorización se congela en un máximo de 1023 ranuras. Después de 16 colisiones, el controlador tira la toalla e informa a la computadora que fracasó. La recuperación posterior es responsabilidad de las capas superiores.