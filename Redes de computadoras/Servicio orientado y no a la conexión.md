El servicio **orientado a la conexión** está modelado a partir del sistema telefónico. Para usar un servicio de [[Redes de computadoras|red]] orientado a la conexión, el usuario del servicio establece primero una conexión, la utiliza y después la libera.

En algunos casos al establecer una conexión, el emisor, el receptor y la [[Subred|subred]] llevan a cabo una **negociación** en cuanto a los parámetros que se van a usar, como el tamaño máximo del mensaje, la calidad requerida del servicio y demás cuestiones relacionadas..

En contraste al servicio orientado a la conexión, el servicio **no orientado a la conexión** está modelado a partir del sistema postal. Cada mensaje lleva la dirección de destino completa, y cada uno es [[Router|enrutado]] hacia los nodos intermedios dentro del sistema, en forma independiente a todos los mensajes subsecuentes. Hay distintos nombres para los mensajes en diferentes conextos: un **paquete** es un mensaje en la [[Capa de red|capa de red]].

![[servicio_orientado_a_la_conexión_1.png]]

### Confiabilidad
Cada tipo de servicio se puede caracterizar con base en su confiabilidad. Algunos servicios son confiables en cuanto a que nunca pierden datos. Por lo general, para implementar un servicio confiable, el receptor tiene que confirmar la recepción de cada mensaje, de manera que el emisor esté seguro de que hayan llegado. El proceso de confirmación de recepción introduce sobrecarga y retardos, que a menudo valen la pena pero algunas veces no son deseables.

Al servicio sin conexión no confiable (que significa sin confirmación de recepción) se le denomina servicio de **datagramas**, en analogía al servicio de telegramas que tampoco devuelve una confirmación de recepción al emisor.

En otros casos es conveniente no tener que establecer una conexión para enviar un mensaje, pero la confiabilidad es esencial. En estas aplicaciones se puede utilizar el servicio de **datagramas con confirmación de recepción**. Es como enviar una carta certificada y solicitar una confirmación de recepción. Al regresar la confirmación de recepción el emisor tiene la absoluta certeza de que la carta se entregó al destinatario correcto y que no se perdió en el camino. La mensajería de texto en los teléfonos móviles es un ejemplo.