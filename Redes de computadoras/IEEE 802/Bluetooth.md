**802.15**

Los protocolos de **Bluetooth** permiten a estos dispositivos encontrarse y conectarse entre sí, a lo cual se le conoce como **emparejamiento** (*pairing*), además de que pueden transferir datos en forma segura.

## Arquitectura de Bluetooth
La unidad básica de un sistema Bluetooth es una **piconet**, la cual consta de un nodo maestro y hasta siete nodos esclavos activos a una distancia máxima de 10 metros. Puede haber varias piconets en el mismo cuarto (grande), e incluso se pueden conectar mediante un nodo puente que participa en varias piconets, como se muestra en la figura 4-34. A una colección interconectada de piconets se le conoce como **scatternet**.

![[RRCC_bluetooth_scatternet.png]]

Además de los siete nodos esclavos activos en una piconet, puede haber hasta 255 nodos estacionados en la red. Éstos son dispositivos que el nodo maestro ha cambiado a un estado de bajo consumo de energía para reducir el desgaste innecesario de sus pilas. En el estado estacionado, un dispositivo no puede hacer nada excepto responder a una señal de activación o una señal baliza por parte del dispositivo maestro. También existen dos estados intermedios, hold y sniff, pero en este caso no son de nuestra incumbencia.

La razón del diseño maestro/esclavo es que los diseñadores pretendían facilitar la implementación de chips Bluetooth completos por menos de 5 dólares. La consecuencia de esta decisión es que los esclavos son sumamente pasivos y básicamente realizan todo lo que los maestros les indican. En esencia, una piconet es un sistema [[TDM]] centralizado, en el cual el maestro controla el reloj y determina qué dispositivo se comunica en una ranura de tiempo específica. Toda la comunicación es entre el maestro y el esclavo; no es posible una comunicación directa de esclavo a esclavo.

## Aplicaciones de Bluetooth
La mayoría de los protocolos de red sólo proporcionan canales entre las entidades que se comunican y permiten a los diseñadores de aplicaciones averiguar para qué desean utilizarlos. En contraste, el SIG de Bluetooth especifica el soporte de aplicaciones específicas y provee distintas pilas de protocolos para cada una de ellas. Al momento de escribir esto hay 25 aplicaciones, las cuales se denominan **perfiles**. Por desgracia, esta metodología conduce a un alto grado de complejidad. Aquí se omitirá la complejidad, pero se analizará brevemente los perfiles para ver con más claridad lo que el SIG de Bluetooth trata de lograr.

Seis de los perfiles son para distintos usos de audio y video. Por ejemplo, el perfil *intercom* permite conectar dos teléfonos como walkie-talkies. Los perfiles *headset* y *hands-free* proveen comunicación de voz entre un auricular y su estación base, y se podrían usar para la telefonía de manos libres al conducir un automóvil. Hay otros perfiles para flujo continuo de audio y video con calidad estereofónica; por ejemplo, de un reproductor de música portátil a los auriculares o de una cámara digital a una TV.

El perfil de *HID (Human Interface Device)* es para conectar teclados y ratones a las computadoras. Otros perfiles permiten a un teléfono móvil u otra computadora recibir imágenes de una cámara o enviar imágenes a una impresora. Tal vez sea más interesante un perfil para usar un teléfono móvil como control remoto para una TV (habilitada para Bluetooth).

Existen otros perfiles que permiten la conexión en red. El perfil de red de área personal permite a dispositivos Bluetooth formar una red *ad hoc* o acceder en forma remota a otra red, como una LAN 802.11, por medio de un punto de acceso. El perfil de *red de marcación telefónica* fue de hecho la motivación original de todo el proyecto. Este perfil permite que una computadora portátil se conecte a un teléfono móvil que contenga un módem integrado sin necesidad de usar cables.

También se han definido perfiles para el intercambio de información de capas superiores. El perfil de *sincronización* está diseñado para cargar datos en un teléfono móvil al salir del hogar y recolectar datos de éste al momento de regresar.

Se omiten el resto de los perfiles, sólo mencionaremos que algunos de ellos sirven como bloques básicos sobre los cuales se basan los perfiles anteriores. El perfil de acceso genérico, en el que se basan todos los demás perfiles, provee una forma de establecer y mantener enlaces (canales) seguros entre el maestro y los esclavos. Los otros perfiles genéricos definen los fundamentos del intercambio de objetos, así como el transporte de audio y video. Los perfiles utilitarios se usan mucho para funciones como emular una línea serial, que es muy útil para muchas aplicaciones heredadas.

¿Era realmente necesario explicar en detalle todas estas aplicaciones y proporcionar diferentes pilas de protocolos para cada una? Tal vez no, pero había varios grupos de trabajo distintos que diseñaron las diferentes partes del estándar, cada uno de los cuales se enfocó en su problema específico y generó su propio perfil. Piense en esto como la [[Ley de Conway]] en acción.

## La pila de protocolos de Bluetooth
