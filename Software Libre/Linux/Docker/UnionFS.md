---
aliases: ["OverlayFS"]
---
Los [[Sistemas de archivos|sistemas de archivos]] tipo “unión” son una solución creativa que permite una fusión virtual de varios directorios, mientras mantiene separados sus contenidos reales. El sistema de archivos Overlay (OverlayFS) es un ejemplo de estos, aunque es más un mecanismo de montaje que un sistema de archivos.

El caso más simple involucra dos directorios, cada uno con archivos y carpetas. Podemos pensar en ellos como "superiores" e "inferiores", con el resto de Linux y aplicaciones posicionadas por encima de eso. El directorio "inferior" es de solo lectura. El acceso a los archivos a través de OverlayFS recupera los datos del directorio "superior" primero, y luego se establece de forma predeterminada en el directorio "inferior" si no existe un archivo.

![[SL_Docker_UnionFS.png]]