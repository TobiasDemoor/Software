# Distribution Transparency
Otro objetivo importante es el ocultar el hecho de que los procesos y recursos del sistema están distribuidos en múltiples computadoras, posiblemente separadas por grandes distancias. En otras palabras intenta lograr que esta distribución sea [[Transparencia|transparente]], es decir invisible a los usuarios y aplicaciones.

## Tipos
Hay distintos tipos de transparencia definidos en la ISO Reference Model-Open Distributed Processing 1998.

| Transparencia | Descripción                                                                                |
|---------------|--------------------------------------------------------------------------------------------|
| Acceso        | Oculta las diferencias en representación de la información y en cómo se accede a un objeto |
| Ubicación     | Oculta dónde se encuentra un objeto                                                        |
| Reubicación   | Oculta que un objeto puede ser movido a otra localización mientras está siendo utilizado   |
| Migración     | Oculta que un objeto puede moverse a otra localización                                     |
| Replicación   | Oculta que un objeto está replicado                                                        |
| Concurrencia  | Oculta que un objeto puede estar compartido por varios usuarios independientes             |
| Fallo         | Oculta el fallo y la recuperación de un objeto                                             |

### Transparencia de acceso
Ocultar las diferencias en representación de datos y la forma en que el usuario accede a los recursos (arquitecturas, OS). En un nivel básico queremos ocultar las diferencias en las arquitecturas, pero es aún más importante el llegar a un acuerdo en cómo se representa la información. Por ejemplo, podríamos tener en un sistema distribuido computadoras con distintos sistemas operativos, que tienen diferentes convenciones para nombrar archivos.

### Transparencia de ubicación 
Ocultar las diferencias donde físicamente se ubican los recursos en un sistema. Utilización de nombres lógicos (ej. http://www.slashdot.org/index.htm).

### Transparencia de reubicación 
El transporte de un recurso de una ubicación a otra no debe ser “notado” mientras lo estamos usando (portátiles en uso de un lugar a otro). En este tipo de transparencia es el sistema distribuido el que mueve el recurso de un lugar a otro.

### Transparencia de migración 
Soportar la movilidad de procesos y recursos iniciados por los usuarios. En este tipo de transparencia el sistema distribuido permite la movilidad de los objetos. Un ejemplo claro es la comunicación entre dos dispositivos móviles, aunque ambas personas se estén moviendo el sistema les permite continuar con su conversación.

### Transparencia de replicación 
Ocultar que existen diferentes copias del mismo recurso (replicas). Por lo general para que un sistema pueda permitir transparencia de replicación debe permitir transparencia de ubicación.

### Transparencia de concurrencia 
Un usuario no debería notar que otro está haciendo uso del mismo recurso. Al finalizar, el recurso tiene que estar en un estado consistente.

### Transparencia de fallas
Un usuario o aplicación no debe notar que alguna parte del sistema falla. Muchas veces es prácticamente imposible. Un gran inconveniente es la incapacidad de distinguir un proceso penosamente lento de uno muerto o una red severamente congestionada.
Tipos de fallas:
- Falla de congelación ("no responde más")
- Falla de omision
	- De recepción ("nunca se recibió el mensaje")
	- De envío ("nunca se envió la respuesta")
- Falla de tiempo (timeout)
- Falla de respuesta ("hay una respuesta pero no es lo esperado")
	- Falla de valor
	- Falla de transición de estado 
- Falla arbitraria . “Bizantina”

