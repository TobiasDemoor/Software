API propuesta originalmente por UC Berkeley para comunicación [[TCP]]. Luego de una gran adopción pasó a formar parte del [[Modelo TCP IP|Modelo TCP/IP]].

| Primitivas | Significado                                               | Cliente/Servidor |
| ---------- | --------------------------------------------------------- | ---------------- |
| Socket     | Crear un nuevo endpoint de comunicación                   | Servidor         |
| Bind       | Conectar una dirección local a un SOCKET                  | Servidor         |
| Listen     | Demuestra voluntad de aceptar conexiones                  | Servidor         |
| Accept     | Bloquea al invocador hasta recibir un intento de conexión | Servidor         |
| Connect    | Intentar activamente establecer una conexión              | Cliente          |
| Send       | Enviar datos sobre una conexión                           | Cliente/Servidor |
| Recieve    | Recibir datos sobre una conexión                          | Cliente/Servidor |
| Close      | Cerrar la conexión                                        | Cliente/Servidor |
