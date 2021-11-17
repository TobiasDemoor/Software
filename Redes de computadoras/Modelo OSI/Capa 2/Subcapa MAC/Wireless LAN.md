El principal estándar de [[LAN]] inalámbrica es [[WiFi|802.11]].

#### Problema de terminal oculta
Puede ocurrir que teniendo 3 equipos {A, B, C} el equipo B esté en el rango de A y C pero A y C no se vean mutuamente. En el caso que C esté transmitiendo datos a B, si A quiere transmitir a B interferirá con la transmisión que C está llevando a cabo pero no hay forma que sea conciente de esto. El problema de que una estación no pueda detectar a un competidor potencial por el medio, debido a que dicho competidor está demasiado lejos, se denomina **problema de terminal oculta**.
%%[[Problema de acceso al medio]]%%

![[RRCC_wireless_lan_problema_terminal_oculta_1.png]]

Hay un problema similar al anterior que ocurre cuando una terminal percibe que el canal está siendo utilizado y asume incorrectamente que no puede utilizarlo para comunicarse con un nodo (sería el caso de la figura con C queriendo comunicarse con D). A esta situación se la denomina **problema de la terminal expuesta**.

#### MACA
Uno de los primeros protocolos que aborda estos problemas es **MACA (Multiple Access with Collision Avoidance)**. El concepto en que se basa es que el emisor estimule al receptor para que envíe una trama corta, de manera que las estaciones cercanas puedan detectar esta transmisión y eviten ellas mismas hacerlo durante la siguiente trama de datos (grande). Se utiliza esta técnica en vez de la detección de portadora.

![[RRCC_wireless_lan_problema_terminal_oculta_2.png]]

El MACA se ilustra en la figura 4-12. Consideremos ahora la manera en que A envía una trama a B. A comienza enviando una trama **RTS (Request To Send)** a B, como se muestra en la figura 4-12(a). Esta trama corta (30 bytes) contiene la longitud de la trama de datos que seguirá después. Después B contesta con una trama **CTS (Clear To Send)**, como se muestra en la figura 4-12(b). La trama CTS contiene la longitud de los datos (que copia de la trama RTS). Al recibir la trama CTS, A comienza a transmitir

Sin duda, cualquier estación que escuche el RTS está bastante cerca de A y debe permanecer en silencio durante el tiempo suficiente para que el CTS se transmita de regreso a A sin conflicto. Es evidente que cualquier estación que escuche el CTS está bastante cerca de B y debe permanecer en silencio durante la siguiente transmisión de datos, cuya longitud puede determinar examinando la trama CTS