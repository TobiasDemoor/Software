---
aliases: ["router", "routers"]
---
Los routers son dispositivos que toman decisiones de por donde enviar los paquetes como los [[Switch|switches]] y [[Bridge|bridges]]. A diferencia de estos últimos, para hacer esto desarma las tramas y las modifica ya que trabaja en la [[Capa de red|capa de red]]. Además permite unir dos [[Subred|subredes]].

Los routers están asociados a una tecnología en particular de capa 3 (o un conjunto).

> Es el dispositivo genérico de capa 3

Al momento de definir los [[algoritmos de enrutamiento]] un router puede manejar varios de estos. El criterio que utiliza para decidir qué algoritmo utilizar se encuentra definido por la **distancia administrativa** asociads a cada algoritmo. Esta toma valores por defecto definidos a continuación para cada protocolo pero puede ser modificada individualmente por el administrador (excepto si están directamente conectados).

| Protocolo               | Distancia administrativa |
| ----------------------- | ------------------------ |
| Directamente conectados | 0                        |
| Ruta estática           | 1                        |
| Ruta EIGRP resumen      | 5                        |
| BGP externa             | 20                       |
| EIGRP interna           | 90                       |
| IGRP                    | 100                      |
| OSPF                    | 110                      |
| IS-IS                   | 115                      |
| RIP                     | 120                      |
| EGP                     | 140                      |
| ODR                     | 160                      |
| EIGRP externa           | 170                      |
| BGP interna             | 200                      |
| Desconocida             | 255                      | 
