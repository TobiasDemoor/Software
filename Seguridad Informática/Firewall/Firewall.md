---
aliases: ["firewall", "cortafuegos"]
---
El **firewall** es una de las herramientas de [[Seguridad|seguridad]] más eficaces disponibles para la protección de los usuarios internos de la [[Redes de computadoras|red]] contra [[Amenaza|amenazas]] externas. Están descriptos en la [[RFC]] 2979.

El firewall reside entre dos o más redes y **controla el tráfico** entre ellas, además de evitar el acceso no autorizado. Los productos de firewall usan diferentes técnicas para determinar qué acceso permitir y qué acceso denegar en una red. Estas técnicas son las siguientes:
- **Filtrado de paquetes:** evita o permite el acceso según las direcciones [[IP]] o [[Direcciones MAC|MAC]]. 
- **Filtrado de aplicaciones:** evita o permite el acceso de tipos específicos de aplicaciones según los números de puerto. 
- **Filtrado de URL:** evita o permite el acceso a sitios Web según palabras clave o [[URL]] específicos. 
- **Inspección de paquetes con estado (SPI)**

El firewall define que hacer con un paquete de acuerdo a las reglas de entrada y salida que han sido suministradas por la organización.

Hay 3 tipos principales de firewall:
- Capa de red: filtra paquetes según direcciones IP origen y/o destino ([[Capa de red|capa 3]]) y puertos origen y/o destino ([[Capa de transporte|capa 4]]). Funciona por choque de reglas.
- Capa de aplicación: trabaja a nivel de aplicación, filtra por protocolos de [[Capa de aplicación|capa 7]] (HTTP, SMPT, etc.), por URL y por datos. El caso más común es un [[Proxys|proxy]]. Tiene un costo mayor en rendimiento al trabajar en la capa más superior.
- Personal:  los anteriores están pensados para filtrar en algún punto de mi organización para todos. Un firewall personal es desde el **punto de vista de un cliente**. Es menos efectivo porque el paquete ya se encuentra en la máquina destino. Al ser molesto es menos seguro.

Ventajas:
- Protege de intrusiones. 
- Controla accesos a segmentos de la red o [[Internet]]. 
- Protección de información privada. 
- Define distintos niveles de acceso a la información. 
- Optimización de acceso. 
- Ayuda a dar serguridad.

Limitaciones, no se puede proteger de:
- Ataques cuyo tráfico no pase por el. 
- Ataques internos o usuarios inteligentes. 
- Personas que saquen información por medios fisicos (discos,etc).
- Contra los ataques de [[Ingeniería Social|ingeniería social]] 
- Ataques posibles a la red interna por virus informáticos.

Hay dos tipos básicos de políticas en la configuración de un firewall:
- **Política restrictiva**: se deniega todo excepto lo que se permite explícitamente.
- **Política permisiva**: se permite todo excepto lo que se deniega explícitamente.

Cuando se tiene una computadora [[Linux]] ruteando se puede utilizar [[iptables]] para que trabaje como firewall.

### Demilitarized Zone
![[DMZ]]