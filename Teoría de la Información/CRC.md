El **CRC** o **Cyclic Redundancy Check** es un algoritmo de **detección de errores** que es muy eficiente de implementar por hardware. Funciona particularmente bien para errores en ráfaga.

CRC funciona como una división de polinomios, considera una trama como un polinomio donde cada bit de la trama es un exponente de un polinomio. Divide el polinomio que es la trama por un polinomio generador. El resto de esta división será el enviado y se validará al recibir la trama.

A la trama se le agrega padding a derecha por el grado del polinomio generador (o su longitud - 1). Luego se van realizando xor con el polinomio generador rellenado a derecha para tener la misma longitud que la trama más su padding y desplazando a derecha por su longitud hasta tener el resto en los últimos dígitos.
