Capa 2 del [[Modelo OSI]]

La principal tarea de la **capa de enlace de datos** es transformar un medio de transmisión puro en una línea que esté libre de errores de transmisión. Enmascara los errores reales, de manera que la capa de red no los vea. Para lograr esta tarea, el emisor divide los datos de entrada en **tramas de datos** (por lo general, de algunos cientos o miles de bytes) y transmite las tramas en forma secuencial. Si el servicio es confiable, para confirmar la recepción correcta de cada trama, el receptor devuelve una **trama de confirmación de recepción**. ^extracto

Otra cuestión que surge en la capa de enlace de datos (y en la mayoría de las capas superiores) es cómo evitar que un transmisor rápido inunde de datos a un receptor lento. Tal vez sea necesario algún mecanismo de regulación de tráfico para notificar al transmisor cuando el receptor puede aceptar más datos.

![[Subcapa MAC#^extracto]]

La capa de enlace de datos implementa algoritmos para lograr una comunicación confiable y eficiente de unidades completas de información llamadas **tramas** entre dos máquinas adyacentes. Por adyacente, se quiere decir que las dos máquinas están concectadas mediante un canal de comunicaciones que actúa de manera conceptual como un alambre. La propiedad esencial del canal que lo hace asemejarse a un alambre es que los bits se entregan en el mismo orden que es enviaron.

## Tipos
Los enlaces de red se pueden dividir en dos categorías: los que utilizan conexiones [[P2P|punto a punto]] y los que utilizan [[Canales de difusión|canales de difusión]].

## Subcapa LLC
![[Subcapa LLC]]

## Subcapa MAC
![[Subcapa MAC]]

## Switches
![[Switch]]