## Fibra óptica
La fibra óptica se utiliza para la transmisión de larga distancia en las redes troncales, las redes LAN de alta velocidad y el acceso a [[Internet]] de alta velocidad como **FTTH (Fiber To The Home)**. Un sistema de transmisión óptico tiene tres componentes clave: la fuente de luz, el medio de transmisión y el detector. Por convención, un pulso de luz indica un bit 1 y la ausencia de luz indica un bit 0. El medio de transmisión es una fibra de vidrio ultradelgada. El detector genera un pulso eléctrico cuando la luz incide en él. Al conectar una fuente de luz a un extremo de una fibra óptica y un detector al otro extremo, tenemos un sistema de transmisión de datos unidireccional que acepta una señal eléctrica, la convierte y la transmite mediante pulsos de luz, y después reconvierte la salida a una señal eléctrica en el extremo receptor.

Este sistema de transmisión tendría fugas de luz y sería inútil en la práctica si no fuera por la **refracción**. Cuando un rayo de luz pasa de un medio a otro (por ejemplo, de sílice fundida al aire), el rayo se refracta (dobla) en el límite la sílice y el aire, como se muestra en la figura. Aquí vemos un rayo de luz que incide en el límite a un ángulo $\alpha_1$ que emerge con un ángulo $\beta_1$. El grado de refracción depende de las propiedades de los dos medios (en especial, de sus índices de refracción). Para ángulos de incidencia por encima de cierto *valor crítico*, la luz se refracta de regreso a la sílice; nada de ella escapa al aire. Por ende, un rayo de luz incidente con un ángulo igual o mayor al crítico que queda atrapado dentro de la fibra, como se muestra en la figura, y se puede propagar por muchos kilómetros prácticamente sin pérdidas.

![[fibra_optica_1.png]]

La fibra óptica al no utilizar señales eléctricas para transmitir no sufre de [[Ruido|ruido impulsivo ni de diafonía]].

### Transmisión de luz a través de fibras
El bosquejo de la figura sólo muestra un rayo atrapado, pero como cualquier rayo de luz que incida en la frontera por encima del ángulo crítico se reflejará de manera interna, habrá muchos rayos distintos rebotando con ángulos diferentes. Se dice que cada rayo tiene un modo distinto, por lo que una fibra con esta propiedad se llama **fibra multimodal**.

Pero si el diámetro de la fibra se reduce a unas cuantas longitudes de onda de luz, la fibra actúa como una guía de ondas y la luz se puede propagar sólo en línea recta, sin rebotar, con lo que se obtiene una **fibra monomodo**. Estas fibras son más costosas pero se utilizan mucho para distancias más largas. Las fibras monomodo disponibles en la actualidad pueden transmitir datos a 100 Gbps por 100 km sin necesidad de amplificación. Incluso se han logrado tasas de datos más altas en el laboratorio, para distancias más cortas.

La **[[Atenuación|atenuación]]** de la luz que pasa por el vidrio depende de la longitud de onda de la luz (así como de algunas propiedades físicas del vidrio). Se define como la relación entre la potencia de la señal de entrada y la de salida. Para el tipo de vidrio que se utiliza en las fibras ópticas, la [[Atenuación]] se muestra en la figura en unidades de decibeles por kilómetro lineal de fibra.

En la actualidad se utilizan mucho tres bandas de longitud de onda para la comunicación óptica. Estas tres bandas se centran en 0.85, 1.30 y 1.55 micrones, respectivamente. Las tres bandas tienen de 25000 a 30000 GHz de [[Ancho de banda|amplitud]]. La banda de 0.85 micrones se utilizó primero. Tiene una mayor [[Atenuación|atenuación]] y, por lo tanto, se utiliza para distancias más cortas, pero a esa longitud de onda se pueden fabricar láseres y componentes electrónicos con el mismo material (arseniuro de galio). Las últimas dos bandas tienen buenas propiedades de [[Atenuación|atenuación]] (una pérdida de menos de 5% por cada kilómetro). Hoy en día, la banda de 1.55 micrones se utiliza mucho en los amplificadores dopados con erbio que trabajan directamente en el domino óptico.

![[fibra_optica_2.png]]

La longitud de los pulsos de luz que se transmiten por una fibra aumenta conforme se propagan. A este fenómeno se le conoce como **dispersión cromática**. Su magnitud depende de la longitud de onda. Una forma de evitar que se traslapen estos pulsos dispersos es aumentar la distancia entre ellos, pero esto se puede hacer sólo si se reduce la tasa de transmisión. Por fortuna se descubrió que si se da a los pulsos una forma especial relacionada con el recíproco del coseno hiperbólico, se cancelan casi todos los efectos de la dispersión y es posible enviar pulsos a miles de kilómetros sin una distorsión apreciable de la forma. Estos pulsos se llaman **solitones**.

### Cables de fibras
Los cables de fibra óptica son similares a los coaxiales, excepto por el trenzado. En la figura aparece una fibra óptica individual, vista de lado. Al centro se encuentra el núcleo de vidrio, a través del cual se propaga la luz. En las fibras multimodales, el núcleo es por lo general de 50 micrones de diámetro, aproximadamente el grosor de un cabello humano. En las fibras de monomodo, el núcleo es de 8 a 10 micrones.

El núcleo está rodeado de un revestimiento de vidrio con un índice de refracción más bajo que el del núcleo, con el fin de mantener toda la luz en el núcleo. Después viene una cubierta delgada de plástico para proteger el revestimiento. Por lo general las fibras se agrupan en haces, protegidas por una funda exterior.

![[fibra_optica_3.png]]

Las fibras se pueden conectar de tres maneras distintas. Primera, pueden terminar en conectores e insertarse en clavijas de fibra. Los conectores pierden entre un 10 y 20% de la luz, pero facilitan la reconfiguración de los sistemas.

Segunda, se pueden empalmar en forma mecánica. Los empalmes mecánicos simplemente acomodan los dos extremos cortados con cuidado, uno junto a otro en una manga especial y los sujetan en su lugar. Para mejorar la alineación se puede pasar luz a través de la unión para después realizar pequeños ajustes de modo que se maximice la señal. El personal capacitado tarda cerca de cinco minutos en crear empalmes mecánicos y se produce una pérdida de luz de 10%.

Tercera, se pueden fusionar (fundir) dos piezas de fibra para formar una conexión sólida. Un empalme por fusión es casi tan bueno como una sola fibra, pero incluso en este caso se produce una pequeña cantidad de [[Atenuación|atenuación]].

En los tres tipos de empalmes se pueden producir reflejos en el punto del empalme; además la energía reflejada puede interferir con la señal.

Por lo general se utilizan dos tipos de fuentes de luz para producir las señales: LED y láseres semiconductores. Estas fuentes de luz tienen distintas propiedades, como se muestra en la siguiente tabla.

| Característica                | LED       | Láser semiconductor  |
| ----------------------------- | --------- | -------------------- |
| Tasa de datos                 | Baja      | Alta                 |
| Tipo de fibra                 | Multimodo | Multimodo o monomodo |
| Distancia                     | Corta     | Larga                |
| Tiempo de vida                | Larga     | Corta                |
| Sensibilidad a la temperatura | Poca      | Considerable         |
| Costo                         | Bajo      | Elevado              |

El extremo receptor de una fibra óptica consiste en un fotodiodo, el cual emite un pulso eléctrico cuando lo golpea la luz. El tiempo de respuesta de los fotodiodos, que convierten la señal óptica en eléctrica, limita la tasa de datos a cerca de 100 Gbps. El [[Ruido|ruido térmico]] es otro inconveniente, por lo que un pulso de luz debe llevar suficiente potencia para detectarlo. Cuando los pulsos tienen la potencia suficiente, la tasa de error se puede reducir de manera considerable.