%%[[Capa de enlace de datos]] Hasta 100 m%%

Ethernet es una tecnología de [[Redes de computadoras#Clasificación según escala|LAN]] definida en el estándar IEEE 802.3. Es un bus a nivel lógico.

Tradicionalmente utiliza [[Codificación Manchester]]. Utiliza CSMA/CD ([[CSMA]] con detección de colisiones)

## Cableados
### Estándar
| Nombre   | Cable                         | Max. segmento | Nodos/segmento | Ventajas                 | 
| -------- | ----------------------------- | ------------- | -------------- | ------------------------ |
| 10Base5  | Thick [[Cable coaxial\|coax]] | 500 m         | 100            | Original, ahora obsoleta |
| 10Base2  | Thin [[Cable coaxial\|coax]]  | 185 m         | 30             | No se requiere [[Hub]]   |
| 10Base-T | [[Par trenzado]]              | 100 m         | 1024           | Muy barato               |
| 10Base-F | [[Fibra óptica]]              | 2000 m        | 1024           | Entre edificios          |

Hasta 10Base2 la topología física era un bus. A partir de 10Base-T pasa a ser una estrella. El 10 es la velocidad (10 Mbps) y el "Base" es de [[Transmisión en banda base|banda base]].

### Fast Ethernet
| Nombre     | Cable            | Max. segmento | Ventajas                                              |
| ---------- | ---------------- | ------------- | ----------------------------------------------------- |
| 100Base-T4 | [[Par trenzado]] | 100 m         | UTP cat 3                                             |
| 100Base-TX | [[Par trenzado]] | 100 m         | [[Uso del canal \|Full-duplex]] 100 Mbps              |
| 100Base-FX | [[Fibra óptica]] | 2000 m        | [[Uso del canal \|Full-duplex]] 100 Mbps; cable largo |


## Detección de colisiones
Al tener un medio con características conocidas se pueden detectar colisiones. Al colisionar dos paquetes el voltaje en la línea sube al doble y así es como se detecta la colisión. La detección de colisiones puede tardar a lo sumo $2\tau$ siendo $\tau$ el tiempo de propagación entre emisor y receptor. Podemos conocer el tiempo para el peor caso ya que todo está cronometrado y ya que la red está construida acorde a especificaciones específicas (es por esto que hay un límite a la cantidad de repetidores). El valor entonces será $2\tau \le 51.2 \mu s$.

Ethernet tiene una tamaño mínimo de trama de 64 bytes (512 bits), esta surge porque es la consecuencia de usar CSMA/CD a 10 Mbps donde $2\tau \le 51.2 \mu s$. El resultado de esto es que todo el tiempo que se está esperando se están enviando bits. La trama mínima es una consecuencia directa de CSMA/CD.

## Ethernet conmutada
Los [[Hub|hubs]] fueron una solución para sacarse de encima el bus. Hoy en día se utiliza mayormente **Ethernet conmutada** mediante el uso de [[Switch|switches]].