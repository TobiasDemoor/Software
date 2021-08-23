# Redes de computadoras
## Definición
Se llama **red de computadoras** a un conjunto de computadoras autónomas interconectadas mediante una sola tecnología. Se dice que dos computadoras están interconectadas si pueden intercambiar información. La conexión no necesita ser a través de un cable de cobre; también se puede utilizar fibra óptica, microondas, infrarrojos y satélites de comunicaciones. Las redes pueden ser de muchos tamaños, figuras y formas. Por lo general se conectan entre sí para formar rede más grandes, en donde **Internet** es el ejemplo más popular de una red de redes.

Es importante diferenciar una red de computadoras de un [[Distributed Systems|sistema distribuido]]. La diferencia clave está en que en un sistema distribuido, un conjunto de computadoras independientes aparece frente a sus usuarios como un solo sistema coherente. Por lo general, tiene un modelo o paradigma único que se presenta a los usuarios. En una red de computadoras no existe esta coherencia, modelo ni software. Los usuarios quedan expuestos a las máquinas reales, sin que el sistema haga algún intento por hacer que éstas se vean y actúen de una manera coherente.

## Hardware de red
Hablando en sentido general existen dos tipos de tecnología de transmisión que se emplean mucho en la actualidad: los enlases de **difusión** (*broadcast*) y los enlaces de [[P2P|punto a punto]].

Los enlaces de punto a punto conectan pares individuales de máquinas. Para ir del origen al destino en una red formada por enlaces de punto a punto, los mensajes cortos (conocidos como **paquetes** en ciertos contextos) tal vez tengan primero que visitar una o más máquinas intermedias. A menudo es posible usar varias rutas de distintas longitudes, por lo que es importante encontrar las más adecuadas en las redes de punto a punto. A la transmisión punto a punto en donde sólo hay un emisor y un receptor se le conoce como **unidifusión** (*unicasting*).

Por el contrario, en una red de difusión todas las máquinas en la red comparten el canal de comunicación; los paquetes que envía una máquina son recibidos por todas las demás. Un campo de dirección dentro de cada paquete especifica a quién se dirige. Cuando una máquina recibe un paquete, verifica el campo de dirección. Si el paquete está destinado a la máquina receptora, ésta procesa el paquete; si el paquete está destinado para otra máquina, sólo lo ignora. Una red inalámbrica es un ejemplo común de un enlace de difusión, en donde la comunicación se comparte a través de una región de cobertura que depende del canal inalámbrico y de la máquina que va a transmitir.

## Clasificación según escala
![[clasificacion_segun_escala.png]]