Las redes conocidas como **VPN (Virtual Private Network)** se pueden usar para unir las redes individuales ubicadas en distintos sitios, en una sola [[Redes de computadoras|red]] extendida. En otras palabras el simple hecho de que un usuario esté a 15.000 km de distancia de sus datos no debe ser impedimento para que los utilice como si fueran locales.

Permiten la extensión de la [[LAN|red local]] sobre una red pública o no controlada, como por ejemplo [[Internet]]. Así se evita tener que pagar una conexión punto a punto.

Tipos de VPN:
- Acceso remoto: los usuarios se conectan con la red desde sitios remotos.
- Punto a punto: unir distintas áreas geográficas como una sola LAN (tunnelling)
- Over LAN: son como las punto a punto pero, en vez de un enlace punto a punto utilizan la misma red WAN.

Implementaciones:
- Por hardware: tienen mejor rendimiento y fácil configuración (SonicWALL, WatchGuard, Nortel, Cisco, Linksys, etc).
- Por software: son más configurables, pero tienen menor rendimiento y delicada configuración (Windows, GNU/Linux y los UNIX).
- Protocolos: [[IPSec]], PPTP, L2F, L2TP, [[SSL]]/[[TLS]], [[SSH]], etc.

Ventajas de las VPN:
- Brindan **integridad**, **confidencialidad** y **seguridad de datos** ([[Seguridad de la Información]]).
- Reducen los costos con fácil uso.
- Facilitan las comunicaciones entre dos usuarios en lugares distantes al extender una [[LAN]] a través de grandes distancias.
