La solución típica de **IoT** se caracteriza por muchos dispositivos (es decir, cosas) que puede usar alguna forma de gateway para comunicarse a través de una red a un servidor de backend empresarial que ejecuta un a plataforma IoT que ayuda a integrar la información de IoT con la existente en la empresa. Las funciones de los dispositivos, las pasarelas y la plataforma en la nube están bien definidos, y cada uno de ellos proporciona características y funcionalidad requerida por cualquier solución IoT robusta

Una arquitectura IoT está compuesta por 4 capas principales. Los sensores y actuadores (las cosas), en el caso de los sensores estos pueden medir una magnitud del ambiente en donde se encuentran y los actuadores llevan a cabo alguna acción (por ej. cerrar una válvula). Luego se encuentran los gateways los cuales se encargan de recolectar los datos crudos de los sensores y procesarlos para convertirlos en algo usable. Luego los servicios de red permiten conectar estos gateways entre sí. Y finalmente se agrega toda la información en los servidores centrales.

![[SSDD_IoT_architectures.png]]

Las "Cosas" en el IoT son el punto de partida para una solución de IoT. Típicamente son los creadores de los datos, e interactúan con el mundo físico Las “cosas” a menudo son muy limitadas en términos de tamaño, fuente de alimentación, procesamiento y red; por lo tanto, a menudo se programan usando microcontroladores ([[MCU]]) que tienen capacidades muy limitadas.

El **gateway IoT** actúa como el punto de agregación para un grupo de sensores y actuadores para coordinar la conectividad de estos dispositivos entre sí y a una red externa. Una puerta de enlace IoT puede ser una pieza física de hardware o funcionalidad incorporada en una "cosa" más grande que está conectada a la red. Por ejemplo, una máquina industrial podría actuar como una puerta de enlace, y también podría ser un automóvil conectado o un electrodoméstico. Una puerta de enlace IoT a menudo ofrecerá el procesamiento de los datos "en el borde" y capacidades de almacenamiento para hacer frente a la [[latencia]] de la red y fiabilidad Para la conectividad entre dispositivos. Un gateway IoT debería tratar con los problemas de interoperabilidad entre dispositivos incompatibles.

Para dispositivos de Internet de las Cosas es necesaria la conexión a [[Internet]]. La conexión a Internet permite que los dispositivos trabajen entre ellos y con servicios backend, para esto usualmente utilizan [[MQTT]]. 

Se usa MQTT por ser un protocolo de red liviano y flexible que logra el equilibrio adecuado para los desarrolladores de IoT:
* Al ser liviano le permite implementarse en hardware de dispositivos altamente limitados y en redes con alta latencia/bajo ancho de banda.
* Su flexibilidad hace que pueda soportar varios escenarios de aplicaciones para dispositivos y servicios de IoT

No se utiliza HTTP ya que es un protocolo sincrónico. El cliente espera a que el servidor responda. Un protocolo de mensajería asíncrona es mucho más adecuado para las aplicaciones de IoT. Los sensores pueden enviar lecturas y dejar que la red descubra la ruta y el momento óptimo para la entrega a dispositivos y servicios de destino.

## MQTT
![[MQTT]]

## MCU
![[MCU]]