El **HTTP (HyperText Transfer Protocol)** es el [[protocolo]] utilizado para transportar prácticamente toda la información entre servidores web y clientes. HTTP es un protocolo simple de solicitud-respuesta que por lo general opera sobre [[TCP]]. Especifica qué mensajes pueden enviar los clientes a los servidores, y qué respuestas reciben de estos mensajes. Los encabezados de solicitud y respuesta se proporcionan en ASCII. 

HTTP es un protocolo de la [[capa de aplicación]], debido a que opera sobre TCP y está muy asociado con la web. Ésta es la razón por la que lo vemos en este capítulo. Sin embargo, en otro sentido el HTTP se está volviendo más parecido a un protocolo de transporte que provee los medios para que los procesos se comuniquen el contenido entre un límite y otro de las distintas redes. Estos procesos no tienen que ser un navegador y un servidor web. La comunicación de máquina a máquina se realiza a través de HTTP cada vez con más frecuencia.

#### Conexiones
La forma común en que un navegador contacta a un servidor es mediante el establecimiento de una conexión TCP por el puerto 80 en la máquina del servidor, aunque este procedimiento no se requiere formalmente. El valor de utilizar TCP es que ni los navegadores ni los servidores tienen que preocuparse por cómo manejar los mensajes largos, la confiabilidad o el control de la congestión. Todos estos aspectos se manejan mediante la implementación de TCP

En los primeros días de la web con el HTTP 1.0, una vez que se establecía la conexión, se enviaba una solicitud y se obtenía una respuesta. Después se liberaba la conexión TCP. Este método era adecuado en un mundo en el que una página web típica consistía por completo de texto HTML. Sin embargo, la página web promedio creció con rapidez y contenía una gran cantidad de vínculos incrustados para contenido tal como iconos y otros elementos visuales. En consecuencia, establecer una conexión TCP para transportar cada icono por separado era una manera muy costosa de operar.

Esta observación condujo al HTTP 1.1, que soporta **conexiones persistentes** (keep-alive). Con ellas es posible establecer una conexión TCP, enviar una solicitud y obtener una respuesta, para después enviar solicitudes adicionales y obtener respuestas adicionales. A esta estrategia se le conoce también como **reutilización de la conexión**. Al amortizar los costos de establecimiento, inicio y liberación de TCP entre varias solicitudes, se reduce la sobrecarga relativa debido a TCP por cada solicitud. También es posible canalizar solicitudes; es decir, enviar la solicitud 2 antes de que haya llegado la respuesta a la solicitud 1.

![[HTTP_conexiones.png]]

Sin embargo, las conexiones persistentes no son regaladas, puesto que surge un nuevo problema: cuándo cerrar la conexión. Una conexión a un servidor debe permanecer abierta mientras se carga la página. Entonces, ¿cuál es el problema? Hay una buena probabilidad de que el usuario haga clic en un vínculo que solicite otra página al servidor. Si la conexión permanece abierta, la siguiente solicitud se puede enviar de inmediato. Por lo tanto, no hay garantía de que el cliente vaya a hacer otra solicitud al servidor en cualquier momento. En la práctica, es común que los clientes y los servidores mantengan abiertas las conexiones persistentes hasta que hayan estado inactivos durante un intervalo corto (por ejemplo, 60 segundos), o cuando tengan una gran cantidad de conexiones abiertas y necesiten cerrar algunas.

También es posible enviar una solicitud por cada conexión TCP, y ejecutar varias conexiones TCP en paralelo. Este método de **conexión paralela** se utilizaba mucho en los navegadores antes de las conexiones persistentes. Tiene la misma desventaja que las conexiones secuenciales: una sobrecarga adicional, pero a la vez ofrece un desempeño mucho mayor. Esto se debe a que al establecer y aumentar las conexiones en paralelo se oculta parte de la latencia. En nuestro ejemplo, las conexiones para las imágenes incrustadas se pueden establecer al mismo tiempo. Sin embargo, no se recomienda ejecutar muchas conexiones TCP con el mismo servidor. La razón es que TCP controla la congestión para cada conexión de manera independiente. Como consecuencia, las conexiones compiten entre sí, lo cual provoca una pérdida de paquetes adicional, y en conjunto son usuarios más agresivos de la red que una conexión individual. Las conexiones persistentes son superiores y es preferible usarlas en vez de las conexiones paralelas, ya que evitan una sobrecarga y no sufren de los problemas de congestión

#### Versiones
| Version | Descripción                                                  | [[RFC]] |
| ------- | ------------------------------------------------------------ | ------- |
| 1.0     | Versión pública inicial, solo tiene GET                      | 1945    |
| 1.1     |                                                              | 2616    |
| 1.2     |                                                              | 2774    |
| 2.0     | Protocolo binario en vez de texto; multiplexado; server push | 7540    |
| 3.0     | Adios TCP, hola [[QUIC]]                                         | 9000    |

> Un método no seguro es aquel que modifica el estado interno del servidor.

En HTTP/3 se pasa de TCP a QUIC por las ineficiencias de TCP frente a las pérdidas de paquetes y al inicio de la conexión.

> TCP slow start se usa porque la ventana TCP arranca chica y se va agrandando. Empieza chica para evitar las retransmisiones. La pérdida de paquetes en TCP genera que se reduzca abruptamente la ventana.
