## Contexto - Problema
Existen recursos compartidos entre una gran cantidad de clientes distribuidos ([[Distributed Systems|sistema distribuido]]) en el espacio físico conectados por una [[Redes de computadoras|red]] que desean acceder a los mismos. Se debe controlar el acceso y la calidad de los servicios.

## Solución
Los clientes interactúan mediante peticiones de servicios al servidor.

## Debilidades
- El servidor puede ser un potencial cuello de botella para la [[FURPS+#Performance|performance]] del sistema y a su vez puede ser un único punto de falla.
- A veces no es tan sencillo distribuir funcionalidades entre el cliente y el servidor