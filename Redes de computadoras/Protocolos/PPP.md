El [[Protocolo|protocolo]] estándar **PPP (Point to Point Protocol**) se utiliza para enviar paquetes a través de los enlaces utilizados para formar las WAN  ([[Capa de enlace de datos]]).

PPP provee tres características principales:
1. Un método de entramado que delinea sin ambigüedades el final de una trama y el inicio de la siguiente. El formato de trama también maneja la detección de errores.
2. Un protocolo de control de enlace para activar líneas, probarlas, negociar opciones y desactivarlas en forma ordenada cuando ya no son necesarias. Este protocolo se llama **LCP (Link Control Protocol)**.
3. Un mecanismo para negociar opciones de capa de red con independencia del protocolo de red que se vaya a utilizar. El método elegido debe tener un **NCP (Network Control Protocol)** distinto para cada capa de red soportada.

**Formato de trama**
![[ppp_trama.png]]

* **Dirección.** Siempre se establece en 0𝑥𝐹 para indicar que todas las estaciones deben aceptar la trama en caso de usarlo para enlace de difusión.
* **Control.** Siempre se establece en 0𝑥3 . Indica que la trama no está numerada. o LCP proporciona los mecanismos necesarios para que las dos partes negocien una opción que omita los campos dirección y control y ahorre 2 bytes por trama.
* **Protocolo.** Indica la clase de paquete que está en el campo de carga útil. Se definen códigos que empiecen con un bit 0 para la versión 4 de IP, la versión 6 de IP y otros protocolos de capa de red que se podrían usar, como IPX y AppleTalk. Los códigos que comienzan con un 1 se utilizan para los protocolos de configuración PPP (LCP y NCP). LCP permite negociar para que este campo sea un solo byte (256 protocolos es un montón).
* **Carga útil.** Tamaño máximo negociable. 1500 bytes por defecto. 
* **Checksum.** Código de detección de errores. [[CRC]] de 32 o 16 bits (negociable).

**Estados de un enlace**
![[ppp_diagrama_estados.png]]

1. **Muerto.** Estado inicial. No hay conexión de capa física. 
2. **Establecer.** Se estableció la conexión en capa física. Las estaciones negocian intercambiando paquetes LCP. 
3. **Autentificar.** Negociación exitosa, ahora las dos partes verifican sus identidades.
4. **Red.** Las partes negocian la configuración de la capa de red mediante paquetes NCP. Depende del protocolo. 
5. **Abrir.** Se transportan los paquetes de datos IP en tramas PPP a través de la línea SONET. 
6. **Terminar.** Se finalizó el transporte de datos. Se desactiva la conexión de capa física y se vuelve al estado muerto