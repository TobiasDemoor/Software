API propuesta originalmente por UC Berkeley para comunicación [[TCP]]. Luego de una gran adopción pasó a formar parte del [[Modelo TCP IP|Modelo TCP/IP]].

| Primitivas | Significado                                     | Cliente/Servidor |
| ---------- | ----------------------------------------------- | ---------------- |
| SOCKET     | Crear un nuevo endpoint de comunicación         | Servidor         |
| BIND       | Asocia una dirección local a un SOCKET          | Servidor         |
| LISTEN     | Anuncia la voluntad de aceptar conexiones       | Servidor         |
| ACCEPT     | Establece en forma pasiva una conexión entrante | Servidor         |
| CONNECT    | Intenta establecer activamente una conexión     | Cliente          |
| SEND       | Envía datos sobre una conexión                  | Cliente/Servidor |
| RECIEVE    | Recibe datos sobre una conexión                 | Cliente/Servidor |
| CLOSE      | Libera la conexión                              | Cliente/Servidor |
