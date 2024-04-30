---
aliases: ["consistencia débil"]
---
Los [[Modelo de Consistencia|modelos de consistencia]] débil se caracterizan porque:
1. Todos los accesos a variables de sincronización son vistos por todos los porcesos (o nodos) en el mismo orden (secuencialmente). El acceso a las secciones críticas es visto de manera secuencial.
2. Todos los otros accesos pueden ser vistos en diferente orden por diferentes procesos.
3. El conjunto de operaciones lectura y escritura entre diferentes operaciones de sincronización es el mismo en cada proceso.

Por lo tanto, no puede haber acceso a variables de sincronización si hay operaciones de escritura pendientes.Y no se pueden iniciar nuevas operaciones de lectura/escritura si el sistema está realizando alguna operación de sincronización.

Una definición general de este concepto se suele aplicar a cualquier modelo más débil que el de [[Consistencia Secuencial]].