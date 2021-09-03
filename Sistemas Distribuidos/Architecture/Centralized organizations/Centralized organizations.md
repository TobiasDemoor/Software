Una punto donde hay mucho concenso en el area de los [[Sistemas Distribuidos|sistemas distribuidos]] es que pensar en términos de *clientes* que solicitan servicios de *servidores* ayuda a entender y administrar la complejidad de estos sistemas ([[Client-Server|patrón cliente servidor]]).

En el modelo cliente-servidor básico, los procesos en un [[Sistemas Distribuidos|sistema distribuido]] son divididos en dos grupos (con posible solapamiento). Un proceso **servidor** es un proceso implementando un servicio específico. Un proceso **cliente** es un proceso que solicita un servicio a un servidor mediante el envio de una solicitud y subsecuentemente la espera de la respuesta. La interacción cliente-servidor también es conocida como **request-reply behavior**.

### Arquitecturas multinivel
Las multitiered [[Client-Server|client-server architectures]] son consecuencia directa de dividir aplicaciones distribuidas en componentes de interfaz de usuario, procesamiento y manejo de datos. Estos niveles corresponden directamente a la organización lógica de las organizaciones. Este tipo de distribución se llama usualmente **vertical distribution** o distribución vertical.

La organización más básica consta de dos tipos de máquinas **(physically) two-tiered architecture**:
1. Una máquina [[Cliente|cliente]] que contiene solo los programas que implementan (parte de) el nivel de intefaz de usuario.
2. Una máquina [[Servidor|servidor]] que contiene el resto, osea, programas implementando el nivel de procesamiento y datos.

### Arquitectura de tres niveles
También se pueden plantear arquitecturas de tres niveles, **(physically) three-tiered architecture**. En estas arquitecturas, tradicionalmente los programas que forman parte de la capa de procesamiento son ejecutados en un servidor separado, pero pueden además estar distribuidos entre las máquinas de cliente y servidor.
Un ejemplo muy común de esto ocurre en la organización de sitios web. En este caso el web server actúa como un punto de entrada al sitio, pasando sus requests al application server donde el procesamiento en cuestión ocurre. El application server a su vez interactúa con el [[DBMS#Arquitectura cliente-servidor de tres niveles|database server]].