Uno de los principales protocolos que se utilizan para la entrega final de [[correo electrónico ]]es **IMAP (Internet Message Access Protocol)**. La versión 4 del protocolo se define en el [[RFC]] 3501. Para usar IMAP, el servidor de correo ejecuta un servidor IMAP que escucha en el puerto 143. El agente de usuario ejecuta un cliente IMAP. El cliente se conecta al servidor y empieza a emitir comandos de los que figuran en la siguiente tabla.

| Comando      | Descripción                                                     |
| ------------ | --------------------------------------------------------------- |
| CAPABILITY   | Lista las capacidades del servidor.                             |
| STARTTLS     | Inicia transporte seguro (TLS; vea el capítulo 8).              |
| LOGIN        | Inicia sesión en el servidor.                                   |
| AUTHENTICATE | Inicia sesión con otro método.                                  |
| SELECT       | Selecciona una carpeta.                                         |
| EXAMINE      | Selecciona una carpeta de sólo lectura.                         |
| CREATE       | Crea una carpeta.                                               |
| DELETE       | Elimina una carpeta.                                            |
| RENAME       | Cambia el nombre a una carpeta.                                 |
| SUBSCRIBE    | Agrega carpeta al conjunto activo.                              |
| UNSUBSCRIBE  | Elimina carpeta del conjunto activo.                            |
| LIST         | Lista las carpetas disponibles.                                 |
| LSUB         | Lista las carpetas activas.                                     | 
| STATUS       | Obtiene el estado de una carpeta.                               |
| APPEND       | Agrega un mensaje a una carpeta.                                |
| CHECK        | Obtiene un punto de verificación de una carpeta.                |
| FETCH        | Obtiene mensajes de una carpeta.                                |
| SEARCH       | Busca mensajes en una carpeta.                                  |
| STORE        | Altera las banderas de los mensajes.                            |
| COPY         | Crea una copia de un mensaje en una carpeta.                    |
| EXPUNGE      | Elimina los mensajes marcados para eliminación.                 |
| UID          | Emite comandos mediante el uso de identificadores únicos.       |
| NOOP         | No hace nada.                                                   |
| CLOSE        | Elimina los mensajes marcados con banderas y cierra la carpeta. |
| LOGOUT       | Cierra la sesión y la conexión.                                 |

Primero, el cliente iniciará un transporte seguro si se debe usar uno (para mantener los mensajes y comandos confidenciales), y después iniciará sesión o se autentificará de alguna otra forma con el servidor. Una vez conectado, hay muchos comandos para listar carpetas y mensajes, obtener mensajes o incluso partes de ellos, marcar mensajes con banderas para eliminarlos después, y organizar los mensajes en carpetas.

IMAP tiene también muchas otras características, como la habilidad de direccionar el correo no con base en el número de mensaje, sino mediante el uso de atributos (por ejemplo, dame el primer mensaje de Alice). Se pueden realizar búsquedas en el servidor para encontrar los mensajes que cumplan con ciertos criterios, de modo que el cliente recupere sólo esos mensajes.

IMAP es una mejora de uno de los primeros protocolos de entrega final, [[POP3]].

![[POP3]]