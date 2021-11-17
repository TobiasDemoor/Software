Los **remote procedure calls (RPC)** son un tipo de [[Middleware|middleware]] para permitir a aplicaciones conectadas enviar requests a otras aplicaciones conectadas a través de un llamado a procedimiento local, el cuál resulta en una request siendo empaquetada como un mesaje y enviada.

Un problema que surge al momento de implementar esto es que el proceso que llama y el llamado se encuentran en máquinas distintas y por lo tanto en espacios de memoria distintos. Por lo tanto los parámetros y los resultados deben ser transferidos, lo cual puede ser complicado, en particular si las máquinas no son idénticas. Además cualquiera o ambas de las máquinas pueden fallar y cualquiera de los fallos produce problemas distintos.

Los RPC se utilizan en redes LAN y se implementan sobre [[UDP]].

### Operación Básica
 Cuando un procedimiento es remoto el cliente tiene una referencia a un **client stub**, el cual es invocado normalmente. Este stub se encarga de empaquetar los parámetros en un mensaje y solicita el envío de este al servidor. Luego de esto el stub llama a *recieve* de manera que se bloquea en espera de la respuesta.
 
 Cuando el mensaje llega al servidor, el sistema operativo lo pasa al **server stub**. Este es el equivalente al client stub: es código que transforma requests a través de red en llamadas a procedimientos locales. El stub desarma el mensaje y pasa los parámetros al procedimiento real, luego empaqueta la respuesta y la envia al cliente.
 
 ![[RRCC_RPC_operation_1.png]]
 
 ### Pasaje de parámetros
 Al empaquetamiento de parámetros en un mensaje se lo denomina **parameter marshaling**. Uno de los inconvenientes que surge al empaquetar los parámetros es que la máquina destino puede tener una arquitectura distinta a la de origen y por ejemplo puede utilizar una representación little-endian en vez de big-endian. Para solucionar incompatibilidades entre los formatos de representación de distintas arquitecturas se debe transformar los datos a enviar a un formato independiente.
 
 Otro problema importante es como pasar los parámetros por referencia osea los punteros. Una solución posible es pohibir su uso. Sin embargo esto es poco práctico ya que su uso es muy importante. Otra solución más adecuada es reemplazar el esquema de paso por referencia en un paso por copia con restauración, osea que el stub empaqueta una copia de la estructura de datos y al recibir la respuesta reemplaza la estructura local con la recibida.
 
 ### Asynchronous RPC
 Con RPC asíncrono el servidor responde inmediatamente luego de recibir la solicitud luego de lo cual procede a llamar al procedimiento. Esta respuesta sirve como un acknowledgement de que el servidor recibió la respuesta. El cliente entonces sigue ejecutando y una vez que recibe la respuesta se ejecuta un callback (o no). También hay variaciones en las que el cliente no espera el acknowledgement.
 
 ![[RRCC_rpc_async_rpc.png]]