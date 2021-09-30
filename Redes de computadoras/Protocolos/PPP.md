El [[Protocolo|protocolo]] estándar **PPP (Point to Point Protocol**) se utiliza para enviar paquetes a través de los enlaces utilizados para formar las WAN  ([[Capa de enlace de datos]]).

PPP provee tres características principales:
1. Un método de entramado que delinea sin ambigüedades el final de una trama y el inicio de la siguiente. El formato de trama también maneja la detección de errores.
2. Un protocolo de control de enlace para activar líneas, probarlas, negociar opciones y desactivarlas en forma ordenada cuando ya no son necesarias. Este protocolo se llama **LCP (Link Control Protocol)**.
3. Un mecanismo para negociar opciones de capa de red con independencia del protocolo de red que se vaya a utilizar. El método elegido debe tener un **NCP (Network Control Protocol)** distinto para cada capa de red soportada.

![[ppp_trama.png]]

![[ppp_diagrama_estados.png]]