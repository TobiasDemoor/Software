El **HTTP (HyperText Transfer Protocol)** es el [[protocolo]] utilizado para transportar prácticamente toda la información entre servidores web y clientes. HTTP es un protocolo simple de solicitud-respuesta que por lo general opera sobre [[TCP]]. Especifica qué mensajes pueden enviar los clientes a los servidores, y qué respuestas reciben de estos mensajes. Los encabezados de solicitud y respuesta se proporcionan en ASCII. 

HTTP es un protocolo de la [[capa de aplicación]], debido a que opera sobre TCP y está muy asociado con la web. Ésta es la razón por la que lo vemos en este capítulo. Sin embargo, en otro sentido el HTTP se está volviendo más parecido a un protocolo de transporte que provee los medios para que los procesos se comuniquen el contenido entre un límite y otro de las distintas redes. Estos procesos no tienen que ser un navegador y un servidor web. La comunicación de máquina a máquina se realiza a través de HTTP cada vez con más frecuencia.

#### Conexiones
La forma común en que un navegador contacta a un servidor es mediante el establecimiento de una conexión TCP por el puerto 80 en la máquina del servidor, aunque este procedimiento no se requiere formalmente. El valor de utilizar TCP es que ni los navegadores ni los servidores tienen que preocuparse por cómo manejar los mensajes largos, la confiabilidad o el control de la congestión. Todos estos aspectos se manejan mediante la implementación de TCP

En los primeros días de la web con el HTTP 1.0, una vez que se establecía la conexión, se enviaba una solicitud y se obtenía una respuesta. Después se liberaba la conexión TCP. Este método era adecuado en un mundo en el que una página web típica consistía por completo de texto HTML. Sin embargo, la página web promedio creció con rapidez y contenía una gran cantidad de vínculos incrustados para contenido tal como iconos y otros elementos visuales. En consecuencia, establecer una conexión TCP para transportar cada icono por separado era una manera muy costosa de operar.

Esta observación condujo al HTTP 1.1, que soporta **conexiones persistentes** (keep-alive). Con ellas es posible establecer una conexión TCP, enviar una solicitud y obtener una respuesta, para después enviar solicitudes adicionales y obtener respuestas adicionales. A esta estrategia se le conoce también como **reutilización de la conexión**. Al amortizar los costos de establecimiento, inicio y liberación de TCP entre varias solicitudes, se reduce la sobrecarga relativa debido a TCP por cada solicitud. También es posible canalizar solicitudes; es decir, enviar la solicitud 2 antes de que haya llegado la respuesta a la solicitud 1.

![[RRCC_HTTP_conexiones.png]]

Sin embargo, las conexiones persistentes no son regaladas, puesto que surge un nuevo problema: cuándo cerrar la conexión. Una conexión a un servidor debe permanecer abierta mientras se carga la página. Entonces, ¿cuál es el problema? Hay una buena probabilidad de que el usuario haga clic en un vínculo que solicite otra página al servidor. Si la conexión permanece abierta, la siguiente solicitud se puede enviar de inmediato. Por lo tanto, no hay garantía de que el cliente vaya a hacer otra solicitud al servidor en cualquier momento. En la práctica, es común que los clientes y los servidores mantengan abiertas las conexiones persistentes hasta que hayan estado inactivos durante un intervalo corto (por ejemplo, 60 segundos), o cuando tengan una gran cantidad de conexiones abiertas y necesiten cerrar algunas.

También es posible enviar una solicitud por cada conexión TCP, y ejecutar varias conexiones TCP en paralelo. Este método de **conexión paralela** se utilizaba mucho en los navegadores antes de las conexiones persistentes. Tiene la misma desventaja que las conexiones secuenciales: una sobrecarga adicional, pero a la vez ofrece un desempeño mucho mayor. Esto se debe a que al establecer y aumentar las conexiones en paralelo se oculta parte de la latencia. En nuestro ejemplo, las conexiones para las imágenes incrustadas se pueden establecer al mismo tiempo. Sin embargo, no se recomienda ejecutar muchas conexiones TCP con el mismo servidor. La razón es que TCP controla la congestión para cada conexión de manera independiente. Como consecuencia, las conexiones compiten entre sí, lo cual provoca una pérdida de paquetes adicional, y en conjunto son usuarios más agresivos de la red que una conexión individual. Las conexiones persistentes son superiores y es preferible usarlas en vez de las conexiones paralelas, ya que evitan una sobrecarga y no sufren de los problemas de congestión

#### Métodos
Aunque HTTP se diseñó para utilizarlo en la web, se ha hecho intencionalmente más general de lo necesario con miras a futuros usos orientados a objetos. Por esta razón, se soportan otras operaciones, llamadas **métodos**, diferentes a las de solicitar una página web.

| Método  | Descripción                            | Idempotente | Seguro |
| ------- | -------------------------------------- | ----------- | ------ |
| GET     | Leer una página web.                   | SI          | SI     |
| HEAD    | Leer el encabezado de una página web.  | SI          | SI     |
| POST    | Adjuntar a una página web.             | NO          | NO     |
| PUT     | Almacenar una página web.              | SI          | NO     |
| DELETE  | Eliminar la página web.                | SI          | NO     |
| TRACE   | Repetir la solicitud entrante          | SI          | SI     |
| CONNECT | Conectarse a través de un [[Proxys|proxy]]        | SI          | SI     |
| OPTIONS | Consultar las opciones para una página | SI          | SI     |

> Un método no seguro es aquel que modifica el estado interno del servidor.

El método GET solicita al servidor que envíe la página (objeto en el caso genérico). La cual está codificada de forma adecuada en MIME.

El método HEAD sólo pide el encabezado del mensaje, sin la página real. Este método se puede utilizar para recolectar información para fines de indización, o sólo para evaluar la validez de un URL.

El método POST se utiliza para enviar formularios. Al igual que GET, porta también un URL, pero en lugar de sólo recuperar una página, envía datos al servidor (es decir, el contenido del formulario o los parámetros de RPC). Después el servidor hace algo con los datos que dependen del URL; conceptualmente adjunta los datos al objeto. Finalmente, el método devuelve una página que indica el resultado. 

El método PUT es lo inverso a GET: en lugar de leer la página, la escribe. Este método hace posible la construcción de una colección de páginas web en un servidor remoto. El cuerpo de la solicitud contiene la página. Se puede codificar mediante el uso de MIME, en cuyo caso las líneas que siguen al método PUT podrían incluir encabezados de autentificación, para demostrar que el invocador realmente tiene permiso de realizar la operación solicitada.

DELETE hace lo que usted podría esperar: elimina la página, o al menos indica que el servidor web está de acuerdo con eliminar la página. Al igual que con PUT, la autentificación y el permiso juegan un papel importante aquí.

El método TRACE es para la depuración. Indica al servidor que regrese la solicitud. Este método es útil cuando las solicitudes no se están procesando de manera correcta y el cliente desea saber cuál solicitud ha obtenido realmente el servidor.

El método CONNECT permite a un usuario realizar una conexión con un servidor web por medio de un dispositivo intermedio, como una caché web

El método OPTIONS proporciona una forma para que el cliente consulte al servidor sobre una página y obtenga los métodos y encabezados que se pueden usar con esa página.

Cada solicitud obtiene una respuesta que consiste en una línea de estado, y posiblemente de información adicional (por ejemplo, toda o parte de una página web). La línea de estado contiene un código de estado de tres dígitos que indica si se atendió la solicitud, y si no, por qué. El primer dígito se utiliza para dividir las respuestas en cinco grupos principales. En la práctica, los códigos 1xx no se utilizan con frecuencia. Los códigos 2xx indican que la solicitud se manejó de manera exitosa y que se regresa el contenido (si hay alguno). Los códigos 3xx indican al cliente que busque en otro lado, ya sea mediante el uso de un URL diferente o en su propia caché. Los códigos 4xx significan que la solicitud falló debido a un error del cliente, por ejemplo: una solicitud inválida o una página inexistente. Por último, los errores 5xx indican que el servidor tiene un problema interno, debido a un error en su código o a una sobrecarga temporal.

| Código | Significado        | Ejemplos                                                          |
| ------ | ------------------ | ----------------------------------------------------------------- |
| 1xx    | Información        | 100 = el servidor acepta manejar la solicitud del cliente.        |
| 2xx    | Éxito              | 200 = la solicitud es exitosa; 204 = no hay contenido.            |
| 3xx    | Redirección        | 301 = se movió la página; 304 = la página en caché aún es válida. |
| 4xx    | Error del cliente  | 403 = página prohibida; 404 = no se encontró la página.           |
| 5xx    | Error del servidor | 500 = error interno del servidor; 503 = intentar más tarde        |

#### Encabezados de mensajes
A la línea de solicitud (por ejemplo, la línea con el método GET ) le pueden seguir líneas adicionales que contienen más información. Éstas se llaman **encabezados de solicitud**. Podemos comparar esta información con los parámetros de la llamada a un procedimiento. Las respuestas también pueden tener **encabezados de respuesta**.

#### Almacenamiento en caché
A menudo las personas regresan a las páginas web que han visto antes, y es común que las páginas web relacionadas tengan los mismos recursos incrustados. Algunos ejemplos son las imágenes que se utilizan para navegar a través del sitio, así como las hojas de estilo y las secuencias de comandos comunes. Sería un desperdicio obtener todos estos recursos para esas páginas cada vez que se desplieguen en pantalla, puesto que el navegador ya tiene una copia. HTTP tiene soporte integrado para ayudar a los clientes a identificar cuándo pueden reutilizar páginas. Este soporte mejora el desempeño al reducir tanto el tráfico como la latencia en la red. La desventaja es que el navegador ahora debe guardar páginas, pero esto casi siempre vale la pena, ya que el almacenamiento local no es muy costoso. Por lo general las páginas se mantienen en el disco, de modo que se puedan usar al ejecutar el navegador en una fecha posterior.

El verdadero problema con el almacenamiento en caché en HTTP es cómo determinar que una copia de una página previamente colocada en caché es la misma que se obtendría del servidor otra vez. No podemos hacer esta determinación únicamente con base en el URL. Por ejemplo, tal vez el URL puede proporcionar una página que muestra la noticia más reciente. El contenido de esta página se actualizará con frecuencia, incluso cuando el URL permanezca igual. O por el contrario, el contenido de la página puede ser una lista de los dioses de la mitología griega y romana. Lo más seguro es que esta página cambie con menos rapidez.

HTTP utiliza dos estrategias para lidiar con este problema, las cuales se muestran en la figura 7-40 como formas de procesamiento entre la solicitud (paso 1) y la respuesta (paso 5). La primera estrategia es la validación de páginas (paso 2). Se consulta la caché y, si tiene una copia de una página para el URL solicitado que se sabe está actualizada (es decir, aún es válida), no hay necesidad de obtenerla de nuevo del servidor. En cambio, se puede regresar la página en caché directamente. Para realizar esta determinación podemos utilizar el encabezado *Expires* que se devolvió cuando se obtuvo por primera vez la página en caché, junto con la fecha y hora actuales

![[RRCC_HTTP_almacenamiento_en_cache.png]]

En el caso que no se utilize el encabezado *Expires* se utiliza la segunda estrategia: preguntar al servidor si la copia en caché sigue siendo válida. Esta solicitud es un GET condicional y se muestra como el paso 3. Si el servidor sabe que la copia en caché aún es válida, puede enviar una respuesta corta para decirlo (paso 4a). En caso contrario, debe enviar la respuesta completa (paso 4b).

#### Versiones
| Version  | Novedad                                                      | [[RFC]] |
| -------- | ------------------------------------------------------------ | ------- |
| HTTP/1.0 | Versión pública inicial, solo tiene GET                      | 1945    |
| HTTP/1.1 | Conexiones persistentes                                      | 2616    |
| HTTP/2   | Protocolo binario en vez de texto; multiplexado; server push | 7540    |
| HTTP/3   | Adios TCP, hola [[QUIC]]                                     | 9000    |


En HTTP/3 se pasa de TCP a QUIC por las ineficiencias de TCP frente a las pérdidas de paquetes y al inicio de la conexión.

> TCP slow start se usa porque la ventana TCP arranca chica y se va agrandando. Empieza chica para evitar las retransmisiones. La pérdida de paquetes en TCP genera que se reduzca abruptamente la ventana.

#### HTTPS
![[HTTPS]]
