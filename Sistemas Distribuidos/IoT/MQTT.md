El [[protocolo]] **MQTT (Message Queue Telemetry Transport)**, que está construido sobre la pila de [[TCP]]/[[IP]], se ha convertido en el estándar para las comunicaciones de [[IoT]].

Originariamente, MQTT fue inventado y desarrollado por IBM a finales de los 90. Su aplicación original era conectar sensores de los oleoductos con satélites. Es un protocolo de comunicación de [[Arquitecturas publish-subscriber|publish subscriber]] de cola de mensajes no persistente (osea, tiene acoplamiento temporal) que soporta la comunicación asíncrona entre las partes mediante un broker.

El protocolo MQTT define los tipos de entidades en la red: un intermediario (**broker**) de mensajes y las entidades que “publican” y “suscriben”. El intermediario es un servidor que recibe todos los mensajes de quienes publican y luego los redirige a los que suscriben. 
1. El suscriptor se conecta con el intermediario. Se puede suscribir a cualquier "tema" (topic) de mensajes de intermediario. Esta conexión puede ser una conexión TCP/IP simple o una conexión TLS cifrada para mensajes confidenciales. 
2. El sensor “publica” el mensaje, sobre un tema, enviando el mensaje y el tema al intermediario. 
3. Después, el intermediario redirige el mensaje a todos aquellos que estan “suscriptos” a ese tema.

Existen mensajes 
* CONNECT 
* CONNACK 
* SUBSCRIBE 
* UNSUBSCRIBE 
* PUBLISH

![[SSDD_mqtt_1.png]]

MQTT es un protocolo de [[Capa de aplicación]] que especifica cómo se organizan los bytes de datos y cómo se transmiten a través de la red TCP/IP. Pero para propósitos prácticos, los desarrolladores no necesitan entender el protocolo de cable. Todo lo que necesitan saber es que cada mensaje tiene un comando y una carga útil de datos. El comando define el tipo de mensaje.