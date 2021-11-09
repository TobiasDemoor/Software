Trabajaremos con un modelo simplificado de la [[Base de Datos]] donde:
* Se considera la BD como una colección de items de dato
* Un Item de dato puede ser campo, registro, bloque, etc.
* El tamaño del item de dato está definido (este tamaño define la **granularidad** con la que se trabaja).
* Cada item de dato tiene un nombre único para el sistema.

Una **[[Transacciones|transacción]]** es la unidad lógica de procesamiento de la Bases de Datos. Es un proceso que accede para lectura o modifica los contenidos de la BD. Las operaciones de acceso a la BD que una transacción puede incluir son Read(X) y Write(X). Y la unidad lógica de transferencia entre disco y memoria principal es el BLOQUE.

La ejecución de **Read(X)** incluye:
1. Encontrar la dirección de bloque de disco que contiene al item de dato X.
2. Copiar el bloque de disco en memoria principal (si ya no estaba en el buffer).
3. Copiar el item X desde el buffer de memoria principal a la variable X del programa (asumimos que la variable de memoria se llama igual que el item de dato).

La ejecución de **Write(X)** incluye:
1. Encontrar la dirección de bloque de disco que contiene al item de dato X.
2. Copiar el bloque de disco en memoria principal (si ya no estaba en el buffer).
3. Actualizar el item X de la variable del programa al buffer de memoria principal.
4. Actualizar el bloque en disco con el contenido del buffer de memoria (Ojo! Puede ser inmediato o diferido, esto lo decide el Recovery Manager o el S.O.)

Si no hay un control de la concurrencia pueden aparecer ciertos **problemas** y llevar a la BD a un **estado inconsistente**. Estos problemas que surgen del acceso concurrente sin control son:
1. Lost update: dos transacciones acceden al mismo item de datos con operaciones entre mezcladas y se pierde una actualización correspondiente a una de estas. Por ejemplo, en el siguiente caso se pierde la actualiación de T1 sobre x.  


   | T1        | T2        |
   | --------- | --------- |
   | read(x)   |           |
   | x = x - n |           |
   |           | read(x)   |
   |           | x = x + m |
   | write(x)  |           |
   | read(y)   |           |
   |           | write(x)  |
   | y = y + n |           |
   | write(y)  |           |

2. Dirty read: una transacción actualiza un item de datos y luego esta falla pero mientras tanto otra transacción utilizó este valor. Por ejemplo, en el siguiente caso T2 usa el valor de x modificado por T1 aunque esta transacción luego aborta.

   | T1        | T2        |
   | --------- | --------- |
   | read(x)   |           |
   | x = x - n |           |
   | write(x)  |           |
   |           | read(x)   |
   |           | x = x + m |
   |           | write(x)  |
   | read(y)   |           |
   | *abort*   |           |

3. Unrepeatable read: una transacción lee dos veces el mismo item y en el medio otra transacción lo modificó. Un ejemplo de esta es el caso de una reserva donde se pierde la disponibilidad de un instante a otro.


## Hisotria
Se define un **schedule** o **historia** como el orden en el que se entremezclan las operaciones de varias transacciones durante una ejecución concurrente. Una historia H de n transacciones $T_1, T_2, \cdots, T_n$ es un ordenamiento de las operaciones de las transacciones sujeto a que por cada $T_i$ que participa en H, las operaciones de $T_i$ en H deben aparecer en el mismo orden que en $T_i$.

Se dice que dos operaciones en una historia **conflictuan** si:
- Pertenecen a distintas transacciones, y
- Acceden al mismo item de dato, y
- Una de las operaciones es un write.

Se dice que dos historias H y H' son **equivalentes** ($H \equiv H'$) si:
1. Están definidas sobre el mismo conjunto de transacciones, y
2. Las operaciones conflictivas tienen el mismo orden.

Se dice que una historia H es **serial** ($H_S$) si para todo par de transacciones $T_i$ y $T_j$ en H, todas las operaciones de $T_i$ preceden a las de $T_j$ o viceversa.

Las historias seriales y sus equivalentes son las que consideramos como CORRECTAS.

### Teoría de serializabilidad
La **teoría de serializabilidad** se compone del desarrollo de técnicas que permitan determinar qué historias son correctas y trabajar sólo con ésas.

>**Historias serializables:** H es serializable (SR) si es equivalente a una historia serial ($H_S$).

Se utilizan **grafos de precedencia (SG)** para chequear si una historia es serializable. Dado H sobre $T = \{T_1, T_2, \cdots, T_n\}$, un SG(H) es cuyos nodos son los $T_i, T_j \in T$ y los arcos $T_i \leftarrow T_j (i \ne j)$  tal que alguna operación de $T_i$ precede y conflictúa con alguna operación de $T_j$ en H. Para su construcción se hay dos pasos principales:
1. Hacer un nodo por cada $T_i$ .
2. Si alguna operación de $T_i$ precede y conflictúa con alguna operación de $T_j (i \ne j)$ en H, hacer un arco $T_i \leftarrow T_j$.

> **Teorema 1 de la Serializabilidad:**
> - H es SR sii SG(H) es acíclico.
> - H es equivalente a cualquier $H_S$ serial que sea un ordenamiento topológico de SG(H).

## Control de concurrencia
Los **locks** o **candados** son variables asociadas a un item de datos de la BD que describen el estado del item con respecto a posibles operacioens aplicables sobre el mismo. Hay un lock por cada item de dato.

El mecanismo de locking por sí solo no garantiza serializabilidad. Es necesario un protocolo para posicionar locks y unlocks.

> **Protocolo 2PL (Two Phase Locking):** Una transacción T es 2PL si todos los locks preceden al primer unlock.

> **Teorema 2 de la serializabilidad:** Dado $T = \{T_1, T_2, \cdots, T_n\}$, si toda $T_i$ en T es 2PL, entonces todo H legal sobre T es SR.

### Locking binario
El **locking binario** permite dos estados, bloqueado o no y consta de dos operaciones, LOCK(X) y UNLOCK(X). 
- Las transacciones deben incluir las operaciones LOCK(X) y UNLOCK(X), ambas indivisibles, para acceder a un item X para lectura y/o escritura. 
- Si una transacción quiere acceder a X, y X está lockeado, debe esperar a que se libere (EL LOCKING BINARIO FUERZA [[EXCLUSIÓN MUTUA]] SOBRE EL ITEM DE DATO). 
- Una transacción debe hacer UNLOCK(X) después que todos los read(X) y write(X) se hayan completado en esta. 
- Una transacción no puede hacer un LOCK(X) si ya tiene un lock sobre X. 
- Una transacción puede hacer UNLOCK(X) sólo si tiene un lock sobre X.

> **Modelo simplificado basado en locking:** Una $T_i$ es vista como una secuencia de locks y unlocks.

### Locking ternario
El **locking ternario** permite dos tipos de bloqueo, para lectura (llamado también lock compartido) y para escritura (llamado lock exclusivo). Cuando una transacción tiene un lock de escritura nadie más puede acceder al item de datos, pero cuando se tiene un lock de lectura se pueden tener varias transacciones con un lock de este mismo tipo sobre un mismo item. Tiene tres operaciones, Read-Lock(X), Write-Lock(X) y UnLock(X).

**Lock conversion:**
1. **Upgrade:** Read-Lock (X) → Write-Lock (X), (para 2PL sólo en la fase de crecimiento ya que es una especie de lock).
2. **Downgrade:** Write-Lock(X) → Read-Lock (X), (para 2PL sólo en la fase de decrecimiento ya que es una especie de unlock).