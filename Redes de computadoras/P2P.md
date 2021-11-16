---
aliases: [peer-to-peer, punto a punto]
---

Los **enlaces de punto a punto** conectan pares individuales de máquinas. Para ir del origen al destino en una red formada por enlaces de punto a punto, los mensajes cortos (conocidos como **paquetes** en ciertos contextos) tal vez tengan primero que visitar una o más máquinas intermedias. A menudo es posible usar varias rutas de distintas longitudes, por lo que es importante encontrar las más adecuadas en las redes de punto a punto. A la transmisión punto a punto en donde sólo hay un emisor y un receptor se le conoce como **unidifusión** (*unicasting*). ^extracto

En este modelo los individuos que forman un grupo informal se pueden comunicar con otros miembros del grupo. En teoría, toda persona se puede comunicar con una o más personas; no hay una división fija en clientes y servidores (como en el modelo [[Client-Server|cliente servidor]]).

Muchos sistemas peer-to-peer, como BitTorrent no tienen una DB central para el contenido. En su defecto, cada usuario mantiene su propia base de datos en forma local y provee una lista de otras personas cercanas que son miembros del sistema. Así, un nuevo usuario puede ir con cualquier miembro para ver qué información tiene y obtener los nombres de otros miembros para inspeccionar si hay más contenido y más nombres. Este proceso de búsqueda se puede repetir de manera indefinida para crear una amplia base de datos local de lo que hay disponible en la [[Redes de computadoras|red]].