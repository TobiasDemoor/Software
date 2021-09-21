La **topología** de una [[Redes de computadoras|red]] se refiere a la disposición física de los nodos y [[Hub|hubs]] que componen la red. La elección de una topología correcta es importante ya que la topología afecta el tipo de equipamiento de red, cableado, [[Escalabilidad|escalabilidad]] y administración.

> La topología también se puede referir a la organización lógica y los métodos de transmisión de datos. Por ejemplo se puede tener una red lógica de anillo sobre una red física tipo estrella ([[Overlay Network]]).

Las redes de hoy en día caen en tres categorías:
* Estrella
* Bus
* Anillo

### Topología tipo estrella
En las topologías tipo estrella todos los nodos se encuentran conectados a un punto único centralizado. Este punto central suele ser un [[Hub|hub]]. Todo el cableado utilizado corre desde el nodo al punto central. Con esta configuración el diagnóstico es muy sencillo.

### Topología de bus
La topología de bus es la más sencilla. Todas los nodos están conectados a un cable contiguo (o un cable unido para que sea contiguo). [[Ethernet]] es un ejemplo común de una topología de bus. Cada computadora determina cuando la red no está ocupada y transmite la información que requiera. Las computadoras en una topología de bus escuchan solamente transmisiones de otras computadoras (no repiten o relevan las transmisiones). La señal viaja hacia ambos extremos del cable, para evitar que esta rebote se deben colocar terminadores en cada punta.

### Topología de anillo
Una topología de anillo requiere que todas las computadoras estén conectadas en un círculo contiguo. El anillo no tiene terminadores ni hub. Cada computadora en el anillo recibe datos de su vecino, repite la señal y lo pasa al siguiente nodo en el anillo. Como las señales deben pasar por cada nodo del anillo, un fallo en un único nodo puede dar de baja todo el anillo.