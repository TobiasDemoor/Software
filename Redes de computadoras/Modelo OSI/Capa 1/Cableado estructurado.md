%%[[Capa física]]%%

El cableado estructurado es un enfoque sistemático del cableado. Es un método para crear un sistema de cableado organizado que pueda ser fácilmente comprendido por los instaladores, administradores de red y cualquier otro técnico que trabaje con cables.

Hay tres reglas que ayudan a garantizar la efectividad y eficiencia en los proyectos de diseño del cableado estructurado.

La primera regla es buscar una solución completa de conectividad. Una solución óptima para lograr la conectividad de redes abarca todos los sistemas que han sido diseñados para conectar, tender, administrar e identificar los cables en los sistemas de cableado estructurado. La implementación basada en estándares está diseñada para admitir tecnologías actuales y futuras. El cumplimiento de los estándares servirá para garantizar el rendimiento y confiabilidad del proyecto a largo plazo.

La segunda regla es planificar teniendo en cuenta el crecimiento futuro. La cantidad de cables instalados debe satisfacer necesidades futuras. Se deben tener en cuenta las soluciones de Categoría 5e, Categoría 6 y de fibra óptica para garantizar que se satisfagan futuras necesidades. La instalación de la capa física debe poder funcionar durante diez años o más.

La regla final es conservar la libertad de elección de proveedores. Aunque un sistema cerrado y propietario puede resultar más económico en un principio, con el tiempo puede resultar ser mucho más costoso. Con un sistema provisto por un único proveedor y que no cumpla con los estándares, es probable que más tarde sea más difícil realizar traslados, ampliaciones o modificaciones.

> Un sistema de cableado estructurado no es diseñado alrededor de una aplicación específica, sino que es diseñado para ser genérico. Esto permite que muchos aplicaciones hagan uso del sistema.

El cableado de datos se encuentra estandarizado por el ANSI/TIA/EIA-568-B Standard también conocido como *Comercial Building Telecommunications Cabling Standard* (esto en EEUU, en europa el estándar es ISO/IEC 11801 conocido como *International Standard on Information Technology Generic Cabling for Customer Premises*).

## Subsistemas de cableado estructurado
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
La sala de equipamiento es un espacio centralizado determinado para almacenar equipamiento más complejo que el de la EF o TR. Usualmente los equipos telefónicos o equipos de networking como son los [[Router|routers]], [[Switch|switches]], y hubs son localizados en esta sala.