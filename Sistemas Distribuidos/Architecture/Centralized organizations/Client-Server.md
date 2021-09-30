En el modelo cliente-servidor básico, los procesos en un son divididos en dos grupos (con posible solapamiento). Un proceso **servidor** es un proceso implementando un servicio específico. Un proceso **cliente** es un proceso que solicita un servicio a un servidor mediante el envio de una solicitud y subsecuentemente la espera de la respuesta. La interacción cliente-servidor también es conocida como **request-reply behavior**. ^extracto

### Contexto - Problema
Existen recursos compartidos entre una gran cantidad de clientes distribuidos ([[Sistemas Distribuidos|sistema distribuido]]) en el espacio físico conectados por una [[Redes de computadoras|red]] que desean acceder a los mismos. Se debe controlar el acceso y la calidad de los servicios.

### Solución
Los [[Cliente|clientes]] interactúan mediante peticiones de servicios al [[Servidor|servidor]].

### Debilidades
- El servidor puede ser un potencial cuello de botella para la [[Performance|performance]] del sistema y a su vez puede ser un único punto de falla.
- A veces no es tan sencillo distribuir funcionalidades entre el cliente y el servidor

### ¿Dónde está la linea entre cliente y servidor?
En esta organización todo es controlado por el servidor mientras el cliente no es nada más que una terminal boba (dumb terminal), posiblemente con solo una GUI. Sin embargo hay otras posibilidades y se puede distribuir de distintas maneras la aplicación entre estas dos máquinas, desde que la máquina servidor tenga control total sobre la interfaz que corre en la máquina cliente (el extremo de un **thin client**) hasta que la máquina cliente contenga toda la lógica de aplicación y posiblemente parte de la capa de datos (el extremo de un **fat client**).

![[client_server_fat_thin_clients.png]]

## Cliente
![[Cliente]]

## Servidor
![[Servidor]]