IPsec es una extensión al protocolo [[IP]] que proporciona [[Seguridad|seguridad]] a IP y a los protocolos de capas superiores. Se encuentra descripto en el [[RFC]] 2401, está desarrollado para IPv6 y después fue portado a IPv4. Su objetivo es asegurar la autenticación, integridad y confidencialidad de la comunicación.

IPsec puede utilizarse para cifrar directamente el tráfico entre dos equipos (conocido como modo de transporte) o para construir “túneles virtuales” entre dos subredes (modo túnel). Puede proteger al datagrama IP completo (modo túnel) o sólo los protocolos de capas superiores (modo transporte).

Puede utilizarse para comunicación segura entre dos redes corporativas (en modo túnel), esto se suele conocer como red privada virtual o [[VPN]].

En **modo túnel** el datagrama IP se encapsula completamente dentro de un nuevo datagrama IP que emplea el protocolo IPsec.

En **modo transporte** IPsec sólo maneja la carga del datagrama IP.

![[SI_IPSEC.png]]

IPSEC usa dos sub-protocolos:
- **Encapsulated Security Payload (ESP):** que protege los datos del paquete IP de interferencias de terceros. Cifrando el contenido utilizando algoritmos de criptografía simétrica (como Blowfish, [[3DES]]), protege la **confidencialidad**.
- **Authentication Header (AH):** que protege la cabecera del paquete IP de interferencias de terceros así como contra la falsificación (“spoofing”), protege la **integridad**. 
  1. Calculando una suma de comprobación criptográfica (checksum). 
  2. Aplicando a los campos de cabecera IP una función hash segura. 
  3. Agrega una cabecera adicional que contiene el hash para validar la información del paquete.

Además el se usa el protocolo **IKE** para negociar las claves de los usuarios. El protocolo describe:
- Autenticación de los participantes. 
- Intercambio de claves simétricas. 
- Crea las asociaciones de seguridad. 
- El protocolo IKE emplea el puerto 500 UDP para su comunicación.