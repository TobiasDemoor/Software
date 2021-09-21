El estándar TIA/EIA-568-B divide el cableado estructurado en siete areas. Estas son cableado horizontal (o cableado de distribución), cableado backbone (o cableado vertical), área de trabajo (WA), sala de telecomunicaciones (TR), sala de equipamiento (ER), instalación de entrada (EF), y administración.

### Cableado horizontal
El cableado horizontal es el cableado que se extiende de la sala de telecomunicaciones al área de trabajo y termina en outlets de comunicación. El cableado horizontal incluye:
* El cable del patch panel al área de trabajo (patch cord).
* Los outlets de telecomunicación.
* Las terminaciones de cables.
* Cross-connections.
* Un máximo de un punto de transición.

![[cableado_estructurado_cableado_horizontal.png]]

Los componentes específicos de aplicación no deben ser instalados como parte del cableado horizontal. Sino que deben instalarse en las salas de telecomunicaciones o áreas de trabajo.

#### Outlets de telecomunicación
Según estandar cada área de trabajo debe tener un mínimo de dos outlets. Las convenciones para cablear los outlets son T568A o T568B. Ninguna de las dos es **la correcta** sino que cualquiera es adecuada siempre que sea el mismo criterio en los dos extremos. T568A es la configuración recomendada y es la requerida actualmente en instalaciones residenciales según (ANSI/TIA/EIA-570-A)

### Cableado Backbone
El cableado vertical es necesario para conectar las EF, ER y TR. Este no consiste solamente de los cables que conectan lo anteriormente mencionado, sino también los cross-connect cables, terminaciones mecánicas, o patch cords utilizado para concexión backbone-to-backbone.

El estandar especifica requerimientos adicionales de diseño para el cableado backbone:
* Se debe tener cuidado que el tendido no genere interferencia electromagnética o interferencia en radio-frecuencia.
* No se puede tener más de dos niveles gerárcicos de cross-connectores, **la topología del backbone debe ser estrella**.
* El cableado debe ser continuo, no se permiten empalmes. 

![[cableado_estructurado_cableado_backbone.png]]

### Área de trabajo (WA)
El área de trabajo es donde termina el cableado horizontal en un outlet. En el área de trabajo, los usuarios y los equipos de telecomunicaciones se conectan a la infraestructura de cableado estructurado.

El cableado en esta área debe ser simple y fácil de manipular.

### Sala de Telecomunicaciones (TR)
La sala de telecomunicaciones es el lugar dentro del edificio donde los componentes de cableado como los cross-connects y los patch panels se encuentran. Estas salas son donde se origina el cableado horizontal. El cableado backbone termina en las salas de telecomunicaciones.

### Instalación de entrada (EF)
La instalación de entrada (según el estándar) especifíca el punto en el edificio donde el cableado interacciona con el mundo exterior. Todo el cableado externo debe entrar al edificio y terminar en un punto común. También se lo suele llamar demarc. La EF puede compartir espacio con la ER si es necesario o posible.

> El punto de demarcación o **demarc** es el punto donde el circuito brindado por un proveedor externo (como la compañía telefónica) termina. Luego de este punto, el cliente provee el equipamiento y cableado. El mantenimiento y operación pasado el demarc es responsabilidad del cliente.

### Sala de equipamiento (ER)
La sala de equipamiento es un espacio centralizado determinado para almacenar equipamiento más complejo que el de la EF o TR. Usualmente los equipos telefónicos o equipos de networking como son los [[Router|routers]], [[Switch|switches]], y [[Hub|hubs]] son localizados en esta sala.