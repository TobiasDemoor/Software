**IPv6 ([[IP]] versión 6)** es un diseño de reemplazo a IPv4 cuyo cambio principal es el aumento del tamaño de direcciones de 32 bits a 128 bits. Es un protocolo de capa de red diferente que en realidad no congenia internamente con IPv4, a pesar de tantas similitudes. Los principales objetivos de diseño para el reemplazo a IPv4 eran:
1. Soportar miles de millones de hosts, incluso con una asignación de direcciones ineficiente. 
2. Reducir el tamaño de las tablas de enrutamiento. 
3. Simplificar el protocolo para permitir a los enrutadores procesar los paquetes con más rapidez. 
4. Proporcionar mayor seguridad (autentificación y privacidad). 
5. Poner más atención en cuanto al tipo de servicio, en especial para los datos en tiempo real. 
6. Ayudar a la multidifusión al permitir la especificación de alcances. 
7. Permitir que un host deambule libremente sin tener que cambiar su dirección. 
8. Permitir que el protocolo evolucione en el futuro. 
9. Permitir que el protocolo viejo y el nuevo coexistan durante años.

IPv6 cumple bastante bien con los objetivos. Mantiene las buenas características de IP, descarta o desenfatiza las malas y agrega nuevas en donde se requiere. En general, IPv6 no es compatible con IPv4, pero es compatible con los otros protocolos auxiliares de Internet, incluyendo TCP, UDP, ICMP, IGMP, OSPF, BGP y DNS, con pequeñas modificaciones requeridas para lidiar con las direcciones más largas. A continuación se describen las principales características de IPv6.

Primero que nada, IPv6 tiene direcciones más largas que IPv4. Son de 128 bits, lo cual resuelve el problema deseado: proporcionar un suministro efectivamente ilimitado de direcciones de [[Internet]].

La segunda mejora importante de IPv6 es la simplificación del encabezado. Sólo contiene siete campos (en comparación con los 13 de IPv4). Este cambio permite a los enrutadores procesar los paquetes con más rapidez y, por ende, mejora la velocidad de transmisión real y el retardo.

La tercera mejora importante es un soporte mejorado para las opciones. Este cambio era esencial con el nuevo encabezado, ya que los campos que antes eran requeridos ahora son opcionales (debido a que no se utilizan con tanta frecuencia). Además, la forma en que se representan las opciones es distinta y así es más fácil para los enrutadores omitir las porciones que no están destinadas para ellos. Esta característica agiliza el tiempo de procesamiento de los paquetes.

Una cuarta área en la que IPv6 representa un gran avance es la seguridad. La autentificación y la privacidad son características clave del nuevo IP. Sin embargo, después se modernizaron para el IPv4, por lo que en el área de la seguridad las diferencias ya no son tan grandes.

Por último, se puso más énfasis en la calidad del servicio. Se han hecho varios esfuerzos carentes de entusiasmo para mejorar la QoS en el pasado, pero ahora con el crecimiento de la multimedia en Internet, la sensación de urgencia es mayor.

### Encabezado principal
![[IPv6_encabezado_principal.png]]

El campo *Versión* siempre es 6 para IPv6 (y 4 para IPv4). Durante el periodo de transición de IPv4 los enrutadores podrán examinar este campo para saber qué tipo de paquete tienen.

El campo *Servicios diferenciados* se utiliza para distinguir la clase de servicio para los paquetes con distintos requerimientos de entrega en tiempo real. Su uso es muy similar al campo homónimo de IPv4.

El campo Etiqueta de flujo proporciona el medio para que un origen y un destino marquen grupos de paquetes que tengan los mismos requerimientos y que la red deba tratar de la misma forma, para formar una seudoconexión. El flujo se puede establecer por adelantado, dándole un identificador. Cuando aparece un paquete con una *Etiqueta de flujo* diferente de cero, todos los enrutadores pueden buscarla en sus tablas internas para ver el tipo de tratamiento especial que requiere. En efecto, los flujos son un intento de tener lo mejor de ambos mundos: la flexibilidad de una red de datagramas y las garantías de una red de circuitos virtuales.

El campo *Longitud de carga* útil indica cuántos bytes van después del encabezado de 40 bytes. El nombre se cambió de *Longitud total* en el [[Datagrama IPv4|IPv4]] porque el significado cambió ligeramente: los 40 bytes del encabezado ya no se cuentan como parte de la longitud.

El campo *Siguiente encabezado* revela el secreto. La razón por la que pudo simplificarse el encabezado es que puede haber encabezados adicionales (opcionales) de extensión. Este campo indica cuál de los seis encabezados de extensión (en la actualidad), siguen de éste, en caso de que los haya. Si este encabezado es el último encabezado de IP, el campo Siguiente encabezado indica el protocolo de transporte (por ejemplo, TCP, UDP) al que se entregará el paquete.

El campo *Límite de saltos* se usa para evitar que los paquetes vivan eternamente. En la práctica es igual al campo *Tiempo de vida* del IPv4.

Luego vienen los campos *Dirección de origen* y *Dirección de destino*.

Para fines instructivos, podemos comparar el encabezado de IPv4 con el de IPv6 para ver lo que se ha dejado fuera del IPv6. El campo *IHL* se fue porque el encabezado de IPv6 tiene una longitud fija. El campo *Protocolo* se retiró porque el campo *Siguiente encabezado* indica lo que sigue después del último encabezado IP (por ejemplo, un segmento UDP o TCP).

Se eliminaron todos los campos relacionados con la fragmentación, puesto que el IPv6 tiene un enfoque distinto en cuanto a la fragmentación. Para empezar, todos los hosts que cumplen con el IPv6 deben determinar en forma dinámica el tamaño de paquete a usar. Para ello utilizan el procedimiento de [[Fragmentación de paquetes|descubrimiento de MTU]].

Por último, el campo Suma de verificación desapareció porque al calcularlo se reduce en gran medida el desempeño. Con las redes confiables de hoy, además del hecho de que la capa de enlace de datos y las capas de transporte por lo general tienen sus propias sumas de verificación, la ventaja de tener otra suma de verificación no valía el costo de desempeño que generaba. Al quitar estas características, el resultado es un protocolo de capa de red compacto y sólido. Por lo tanto, con este diseño se cumplió la meta del IPv6 (un protocolo rápido y flexible con bastante espacio de direcciones).

### Direcciones IPv6
Se ha desarrollado una nueva notación para escribir las direcciones de 16 bytes, las cuales se escriben como ocho grupos de cuatro dígitos hexadecimales, separando los grupos por dos puntos, como el siguiente ejemplo:
```
8000:0000:0000:0000:0123:4567:89AB:CDEF
```

Ya que muchas direcciones tendrán muchos ceros en ellas, se han autorizado tres optimizaciones. Primero, se pueden omitir los ceros a la izquierda dentro de un grupo, por lo que es posible escribir 0123 como 123. Segundo, se pueden reemplazar uno o más grupos de 16 bits cero por un par de signos de dos puntos. Por lo tanto, la dirección anterior se vuelve ahora:
```
8000::123:4567:89AB:CDEF
```

Por último, las direcciones IPv4 se pueden escribir como un par de signos de dos puntos y un número decimal anterior separado por puntos, por ejemplo
```
::192.31.20.46
```
