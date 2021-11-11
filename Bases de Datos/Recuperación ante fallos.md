Hay varios tipos de fallos:
- Crash del sistema: el contenido de la memoria interna se pierde (puede ser causado por falla de hardware o error de software).
- Error de transacción o sistema: overflow, división por cero, parámetros incorrectos, el usuario cancela la transacción.
- Errores locales o condiciones de excepción: la transacción no encuentra los datos a ser leídos
- Mecanismos de control de concurrencia deciden abortar una o más transacciones: puede ser por diversos motivos.
- Falla de almacenamiento secundario

Para la recuperación ante fallos se definen dentro de las transacciones operaciones primitivas y espacios de memoria (un elemento de dato entra en un bloque). Estas operaciones primitivas son:
1. **INPUT(X):** copia el bloque de disco conteniendo el elemento de datos X al buffer de memoria. 
2. **READ(X,t):** copia el elemento de datos X a la variable local de transacción t. Si el bloque que contiene el elemento X no se encuentra en el buffer de memoria primero se ejecuta **INPUT(X)**. Luego se asigna el valor de X a la variable local t.
3. **WRITE(X,t):** copia el valor de la variable local t al elemento de datos X en el buffer de memoria. Si el bloque que contiene el elemento de datos X no se encuentra en buffer de memoria entonces primero ejecuta **INPUT(X)**. Luego copia el valor de t a X en el buffer.
4. **OUTPUT (X):** copia el bloque que contiene al elemento X del buffer al disco.

> Se usa el término elemento de datos como equivalente a item de datos.

> Ejemplo:
> Sea una transacción **T = READ(A,t); t := t*2; WRITE(A.t); READ(B.t); t := t* 2 ; WRITE(B,t);**
> ![[recuperacion_ante_fallos_ejemplo_1.png]]

### Componentes
- **Transaction Management:** The two principal tasks of the **transaction manager** are assuring recoverability of database actions through logging, and assuring correct, concurrent behavior of transactions through the **scheduler**.
- **Database Elements:** The database is divided into elements, which are typically disk blocks, but could be tuples or relations, for instance. Database elements are the units for both logging and scheduling.
- **Logging:** A record of every important action of a transaction — beginning, changing a database element, committing, or aborting — is stored on a log. The log must be backed up on disk at a time that is related to when the corresponding database changes migrate to disk, but that time depends on the particular logging method used.
- **Recovery:** When a system crash occurs, the log is used to repair the database, restoring it to a consistent state (**recovery manager**).

![[recuperacion_ante_fallos_componentes.png]]

### Logging
En la técnica de recuperación ante fallos mediante logging se hace uso de un archivo de logs APPEND ONLY.

#### UNDO Logging
- **U1:** si la transacción T modifica el elemento de datos X, entonces se loguea un registro de la forma < T ,X ,v > previo a que el nuevo valor de X sea escrito en disco.
- **U2:** si una transacción commitea, entonces se loguea su registro de log < COMMIT T > solo después de que los elementos de la base de datos hayan sido modificados por la transacción, pero tan pronto como sea posible.

![[recuperacion_ante_fallos_logging_undo_ejemplo.png]]

#### REDO Logging
- **R1:** antes de modificar cualquier elemento de datos X en disco es necesario que todos los registros de log pertinantes a esta modificación de X, incluyendo tanto el registro de update < T ,X ,v > y el registro < COMMIT T >, deben estar en disco.

![[recuperacion_ante_fallos_logging_redo_ejemplo.png]]

#### UNDO/REDO Logging
- **UR1:** antes de modificar cualquier elemento de datos X en disco por los cambios realizado por una transacción T, es necesario que el registro de update < T,X,v,w > esté en disco.
- **UR2:** un registro < COMMIT T> debe ser flusheado a disco tan pronto como aparezca en el log.

![[recuperacion_ante_fallos_logging_undo_redo_ejemplo.png]]

%%Fuente: “DATABASE SYSTEMS The Complete Book”, Second Edition, Hector Garcia-Molina, Jeffrey D. Ullman, Jennifer Widom. Department of Computer Science Stanford University, Pearson-Prentice Hall, 2009. Chapter 17: Coping With System Failures.%%