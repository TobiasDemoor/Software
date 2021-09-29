%%[[Client-Server]]%%
### Clientes concurrentes
Para estableces un alto nivel de [[Transparencia de distribución|transparencia de distribución]], los [[Sistemas Distribuidos|sistemas distribuidos]] que operan en una red WAN deben ocultar los [[Latencia|tiempo de latencia]] altos. La manera usual de ocultar latencias de comunicación es iniciar la comunicación e inmediatamente proceder con otra cosa. Por ejemplo una página se puede mostrar parcialmente permitiendo la navegación mientras se siguen cargando otras cosas. Para esto es claro que el cliente requiere ser implementado como una aplicación [[Thread|multihilo]].

### Client-side distribution transparency
El software de cliente no solo abarca la interfaz de usuario. En muchos casos parte del nivel de procesamiento y el nivel de datos de una [[Client-Server|aplicación cliente servidor]] son ejecutados en el cliente. El software de cliente también tiene [[Componente|componentes]] destinados a lograr la [[Transparencia de distribución|transparencia de distribución]].

La **transparencia de acceso** suele ser manejada a través de la generación de un **client stub** a partir de una definición de [[Interfaz|interfaz]] de qué es lo que ofrece el servidor. El stub provee la misma interfaz disponible en el servidor pero oculta las diferencias en arquitectura de máquina, así como la comunicación en sí. El client stub transforma mensajes locales en mensajes que son enviados al servidor y vice versa.

Hay distintas maneras de lograr **transparencia de ubicación**, **migración** y **reubicación** en el cliente. En muchos casos la cooperación entre el servidor y el cliente es crucial. Por ejemplo si un cliente ya está conectado con un servidor, el cliente puede ser informado directamente cuando el servidor cambia de ubicación. En este caso el [[Middleware|middleware]] del cliente puede ocultar al usuario la localización actual del servidor, y también reconectarse transparentemente si es necesario.

La **transparencia de replicación** se puede solucionar por ejempo, si tenemos un [[Sistemas Distribuidos|sistema distribuido]] con servidores replicados, enviando una request a cada réplica y el software de cliente puede recolectar las respuestas transparentemente y pasar una sola respuesta a la aplicación cliente.

En cuanto a la **transparencia de fallos**, ocultar fallos de comunicación con un servidor se suele hacer a través del [[Middleware|middleware]] del cliente. Por ejemplo, el middleware puede ser configurado para intentar conectarse al servidor repetidamente, o tal vez intentar otro servidor luego de varios intentos ([[Tácticas para disponibilidad#Recuperación de fallas]]). Hay ocasiones en las que el middleware puede retornar datos cacheados si el servidor no responde.

Finalmente para **transparencia de concurrencia** puede ser manejada a través de servidores intermediarios, notablemente monitores de transacciones, y requiere menos soporte por parte de los clientes.