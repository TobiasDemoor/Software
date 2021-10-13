Los hubs fueron una solución para sacarse de encima el bus. Hoy en día se utiliza mayormente **Ethernet conmutada**. El corazón de este sistema es un **conmutador** ([[Switch|switch]]) que contiene un plano posterior (backplane) de alta velocidad, el cual conecta a todos los puertos. Los switches sólo envían tramas a los puertos para los cuales están destinadas. Cuando el puerto de un switch recibe una trama Ethernet de una estación, el switch verifica las direcciones de Ethernet para ver cuál es el puerto de destino de la trama.

![[ethernet_conmutada_1.png]]

En un hub, todas las estaciones están en el mismo **dominio de colisión**. Deben usar el algoritmo CSMA/CD para programar sus transmisiones. En un switch, cada puerto es su propio dominio de colisión independiente.

Un switch mejora el desempeño de la red en comparación con un hub de dos maneras. Primero, como no hay colisiones, la capacidad se utiliza con más eficiencia. Segundo y más importante, con un switch se pueden enviar varias tramas al mismo tiempo (por distintas estaciones). Estas tramas llegarán a los puertos del switch y viajarán hacia el plano posterior de éste para enviarlos por los puertos apropiados.

## Fast Ethernet (100 Mbps)
La idea básica detrás de Fast Ethernet (**802.3u**) era simple: mantener todos los formatos, interfaces y reglas de procedimientos anteriores, pero reducir el tiempo de bits de 100 nseg a 10 nseg.

Fast Ethernet permite la interconexión mediante hubs o switches. Para asegurar que el algoritmo CSMA/CD siga trabajando, es necesario mantener la relación entre el tamaño mínimo de trama y la longitud máxima del cable a medida que la velocidad de la red aumenta de 10 Mbps a 100 Mbps. Así, el tamaño mínimo de trama de 64 bytes debe aumentar o la longitud máxima de cable de 2 500 debe disminuir, en forma proporcional. La elección fácil fue reducir la distancia máxima entre dos estaciones cualesquiera por un factor de 10, puesto que un hub con cables de 100 m ya se encuentra dentro de este nuevo valor máximo. Sin embargo, los cables 100Base-FX de 2 km son demasiado largos como para permitir un hub de 100 Mbps con el algoritmo de colisiones normal de Ethernet. Estos cables se deben conectar a un switch y operar en un modo full-dúplex para que no haya colisiones

Para el [[Entramado|entramado]] se utiliza la codificación **[[4B5B|4B/5B]]**.

### Cableado
|   Nombre   |      Cable       | Max. segmento | Ventajas                                              |
|:----------:|:----------------:| ------------- | ----------------------------------------------------- |
| 100Base-T4 | [[Par trenzado]] | 100 m         | UTP cat 3                                             |
| 100Base-TX | [[Par trenzado]] | 100 m         | [[Uso del canal \|Full-duplex]] 100 Mbps              |
| 100Base-FX | [[Fibra óptica]] | 2000 m        | [[Uso del canal \|Full-duplex]] 100 Mbps; cable largo |

## Gigabit Ethernet
En caso de usar hubs en vez de switches puede haber colisiones, por lo que se requiere el protocolo CSMA/CD estándar. Debido a que ahora se puede transmitir una trama de 64 bytes (la más corta permitida) 100 veces más rápido que en la Ethernet clásica, la longitud máxima del cable debe ser 100 veces menor, o de 25 metros, para mantener la propiedad esencial de que el emisor aún transmita cuando la ráfaga de ruido regrese a él, incluso en el peor de los casos.

Esta restricción de longitud fue tan dolorosa que se agregaron dos características al estándar para incrementar la longitud máxima del cable a 200 metros, lo cual quizás es suficiente para la mayoría de las oficinas. La primera característica, llamada **extensión de portadora**, básicamente indica al hardware que agregue su propio relleno después de la trama normal para extenderla a 512 bytes. La desventaja es que usar 512 bytes de ancho de banda para transmitir 46 bytes de datos de usuario (la carga útil de una trama de 64 bytes) tiene una eficiencia de sólo un 9%.

La segunda característica, llamada **ráfagas de trama**, permite que un emisor transmita una secuencia concatenada de múltiples tramas en una sola transmisión. Si la ráfaga total es menor que 512 bytes, el hardware la rellena de nuevo. Si hay suficientes tramas esperando su transmisión, este esquema es muy eficiente y se prefiere en vez de la extensión de portadora.

Para facilitar la actualización, el estándar provee por sí solo un mecanismo llamado **autonegociación**, el cual permite que dos estaciones negocien de manera automática la velocidad óptima (10 o 100 Mbps) y la duplicidad (half-dúplex o full-dúplex).

Para el [[Entramado|entramado]] se utiliza la codificación **8B/10B**.

### Cableado
|         Nombre          |      Cable       | Max. segmento | Ventajas                                                                                    |
|:-----------------------:|:----------------:| ------------- | ------------------------------------------------------------------------------------------- |
| 1000Base-SX <br> 802.3z | [[Fibra óptica]] | 550 m         | Fibra multimodo ($\varnothing = 50 \mu m, 62.5 \mu m$)                                      |
| 1000Base-LX <br> 802.3z | [[Fibra óptica]] | 5000 m        | Monomodo ($\varnothing = 10 \mu m$) o <br> multimodo ($\varnothing = 50 \mu m, 62.5 \mu m$) |
| 1000Base-CX <br> 802.3z |  2 pares de STP  | 25 m          | [[Par trenzado]] blindado                                                                   |
| 1000Base-T <br> 802.3ab |  4 pares de UTP  | 100 m         | UTP estándar cat 5                                                                          |

## 10 Gigabit Ethernet
Todas las versiones de Ethernet de 10 gigabits soportan sólo la operación full-dúplex. CSMA/CD ya no forma parte del diseño y los estándares se concentran en los detalles de las capas físicas que pueden operar a muy alta velocidad. Pero la compatibilidad aún sigue siendo importante, por lo que las interfaces Ethernet de 10 gigabits usan la autonegociación y cambian a la velocidad más alta soportada por ambos extremos de la línea.

Para el [[Entramado|entramado]] se utiliza la codificación **64B/66B**.

### Cableado
|   Nombre    |       Cable       | Max. segmento | Ventajas                                |
|:-----------:|:-----------------:| ------------- | --------------------------------------- |
| 10GBase-SR  | [[Fibra óptica]]  | 300 m         | Fibra multimodo ($\lambda = 0.85\mu m$) |
| 10GBase-LR  | [[Fibra óptica]]  | 10 Km         | Fibra monomodo ($\lambda = 1.3\mu m$)   |
| 10GBase-ER  | [[Fibra óptica]]  | 40 Km         | Fibra monomodo ($\lambda = 1.5\mu m$)   |
| 10GBase-CX4 | 4 pares de twinax | 15 m          | Cobre twinaxial                         |
|  10GBase-T  |  4 pares de UTP   | 100 m         | UTP cat 6a                              |
