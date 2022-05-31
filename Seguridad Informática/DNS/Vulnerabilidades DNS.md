El servicio de [[DNS]] no fue concevido teniendo en cuenta la existencia de actores maliciosos. Se basa en un principio de buena fé entre el cliente y el servidor DNS, el primero pregunta y confía en la respuesta. Esto da a lugar a numerosas [[Vulnerabilidad|vulnerabilidades]].

### Algunos ataques
#### DNS cache poisoning
![[DNS cache poisoning]]

#### Túnel de DNS
El Atacante utiliza otros protocolos para hacer un túnel a través de consultas y respuestas de DNS

#### Secuestro de DNS
El secuestro de DNS, el atacante redirige las consultas a un servidor de nombres de dominio diferente.

#### Ataque NXDOMAIN
Este es un tipo de ataque de inundación de DNS en el que un atacante inunda un servidor DNS con solicitudes, FALSAS, en un intento de causar una [[DoS|denegación de servicio]] para tráfico legítimo.
También pueden apuntar a un RESOLVER recursivo con el objetivo de llenar el caché del RESOLVER con solicitudes basura.

#### Ataque de dominio fantasma
Logra lo mismo que NXDOMAIN en el RESOLVER DNS. Con un un grupo de servidores DNS 'FANTASMA' que responden a las solicitudes muy lentamente o no responden. El RESOLVER se ve saturado de peticiones sin resolver --> denegacon de servicio.

#### Ataque de subdominio aleatorio
En este caso, el atacante envía consultas DNS para varios subdominios aleatorios e inexistentes de un sitio legítimo. El objetivo es crear una denegación de servicio.

#### Ataque de CPE basado en botnet
Los atacantes comprometen los CPE (Costumer Premises Equipment, los routers de comunicación de los clientes) y los dispositivos se convierten en parte de una botnet , utilizada para realizar ataques aleatorios de subdominios contra un sitio o dominio.

### Mitigación y algunas soluciones
1. Ser meticuloso en la configuración (restringir el forward).
2. Dar informacion a quien este autorizado (transferencia de zonas).
3. Utilizar rndc para la administración.
4. En lo posible tratarde implementar versión segura de DNS, DNSSEC.

#### DNSSEC
![[DNSSEC]]