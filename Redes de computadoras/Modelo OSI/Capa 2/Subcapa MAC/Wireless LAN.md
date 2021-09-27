[[Redes de computadoras#Clasificación según escala|LAN]]

### Problema del emisor oculto
Puede ocurrir que teniendo 3 equipos {A, B, C} el equipo B esté en el rango de A y C pero A y C no se vean mutuamente. En el caso que C esté transmitiendo datos a B (manteniendolo ocupado), si A quiere transmitir a B no puede dado que C está transmitiendo pero no hay forma que sea conciente de esto.

Una posible solución a esto es utilizar mensajes especiales RTS (Request To Send) y CTS (Clear To Send) para notificar el comienzo de la interacción. Los que no escuchen RTS escucharan CTS, conociendo así que se está llevando a cabo una comunicación. Una vez finalizada se debe enviar un ACK para notificar que termina la interacción.