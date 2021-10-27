Lo que los hace únicos a los **sistemas penetrantes** o **pervasive systems** en comparación a los otros tipos de [[sistemas distribuidos]] es que *la separación entre usuarios y componentes del sistema está mucho menos definida*. Usualmente no hay una sola interfaz dedicada, sino que un pervasive system está equipado con muchos sensores que registran varios aspectos del comportamiento del usuario. A su vez puede tener un conjunto de actuadores para proveer información y feedback, usualmente hasta intencionalmente buscando modificar el comportamiento.

#### Sistemas ubicuos
En este tipo de sistema se avanza un poco más, el sistema es pervasive y continuamente presente. Osea que el usuario va a estar continuamente interactuando con el sistema, usualmente sin estar al tento de esto. Hay 5 requerimientos principales para que un sistema sea ubicuo:

1. **Distribution** los dispositivos están conectados, distribuidos, y accesibles de una manera transparente.
2. **Interaction** la interacción entre los usuarios y dispositivos es altamente unobtrusive ("discreta").
3. **Context awareness** el sistema está al tanto del contexto del usuario para poder optimizar su interacción.
4. **Autonomy** los dispositivos operan autonomamente sin intervención humana, y por lo tanto son altamente autoadministrados.
5. **Intelligence** el sistema como un todo debe manejar un gran rango de acciones e interacciones dinámicas.

#### Mobile computing systems
En un sistema distribuido móvil se asume que la ubicación de los dispositivos es cambiante. Una ubicación cambiante trae sus inconvenientes, por ejemplo si la ubicación de un dispositivo cambia regularmente también puede ser el caso para los servicios localmente disponibles. Como consecuencia de esto podríamos tener que prestar especial atención a descubrir dinámicamente servicios, y también permitir a los servicios anunciar su presencia.

Las ubicaciones cambiantes tienen un profundo efecto en la comunicación. Consideremos un MANET (mobile ad hoc network). supongamos que dos dispositivos en un MANET se han descubierto (en el sentido que conocen su dirección), ¿cómo ruteamos mensajes entre estos dos? Las rutas estáticas generalmente no son sostenibles ya que los nodos en el camino de routing pueden moverse fuera del rango del vecino invalidando el camino. Para MANETs grandes, usar caminos establecidos a priori no es una opción viable tampoco. Estamos lideando con lo que se llama redes tolerantes a disrupción o **disruption-tolerant networs**, que son redes en las cuales la conectividad entre dos nodos no puede asegurarse.

#### Sensor networks
Una sensor network generalmente consiste de decenas hasta centenas o miles de nodos relativamente pequeños, cada uno equipado con uno o más dispositivos de medición. A su vez los nodos también pueden actuar como actuators.