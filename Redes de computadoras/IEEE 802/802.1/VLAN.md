Definidas en la **IEEE 802.1Q**, son [[LAN]] virtuales para separar en dos o más redes lógicas en caso de que la distribución organizacional de la empresa no coincida con la de la [[Redes de computadoras|red]].

Las VLAN son una herramienta que permite definir un dominio de [[broadcast]] o [[Multicast|multicast]]. Permite que un grupo de hosts se comuniquen como si estuvieran ubicados en el mismo segmento de red LAN, a pesar de poder estar en segmentos distintos. Y ofrece ventajas en aspectos de control, la administración de la red y la [[Seguridad|seguridad]].

![[RRCC_VLAN_trama_8021Q.png]]

#### ¿Por qué usar VLANS?
- Para dividir la LAN en segmentos independientes con un solo dispositivo de conmutación [[Switch]].
- Para mantener un segmento de Red mas allá de la ubicación geográfica en la LAN.
- Para mejorar el control y la seguridad aplicando políticas de acceso entre las VLANS.

#### Tipos de VLANS
Los distintos  criterios para definir a los miembros de una VLAN son los siguientes:
- **Puertos del switch:** el puerto al que está conectada la estación determina la VLAN.
- **Direcciones MAC:** la MAC del dispositivo determina a qué VLAN pertenece (no es seguro ya que las MAC son modificables).
- **Direcciones IP de subred:** las estaciones pertenecen a la VLAN según su IP (tampoco es seguro ya que la IP es modificable).
- **Por protocolos de red:** las estaciones pertenecen según el protocolo de capa 3. Esto es útil cuando se tienen dispositivos utilizando varios protodolos de capa 3 en una misma red de capa 2, como por ejemplo si se tiene televisión digital. Es útil ya que estos dispositivos no podrían interactuar entre sí sin otro dispositivo que actue de intermediario.

#### Tipos de Puertos
- **Access port:** las tramas que salen de este puerto nunca serán etiquetadas (salen tramas 802.3), todo lo que caiga debajo de este enlace se encuentra en una misma VLAN. Es el puerto al que se conectaría una estación de trabajo.
- **Trunk port:** las tramas que salen de este puerto siempre estarán etiquetadas (salan tramas 802.1Q, o equivalente), todas las VLANs pueden estar asociadas a este puerto. Es el puerto al que se conectaría otro switch que trabaje con VLANs.