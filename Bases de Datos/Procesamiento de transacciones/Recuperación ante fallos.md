Hay muchas cosas que pueden fallar a medida que la base de datos recibe consultas y es modificada. Los siguientes items son un catálogo de los modos de fallo más importantes:
- Fallo de almacenamiento secundario: pueden verse comprometidas solo algunas secciones o todo el disco. En este caso se puede proteger mediante un esquema de RAID.
- Fallo catastrófico: dentro de esta categoría se incluyen varias situaciones donde el dispositivo almacenando la base de datos puede verse destruido. Por ejemplo, explosionese, incendios, o vandalismo. Se puede proteger de este mediante backups offsite.
- Fallo del sistema: son problemas que causan que el contenido de la memoria interna se pierda y por ende el estado de las transacciones en ejecución.
- Error de transacción o sistema: overflow, división por cero, parámetros incorrectos, el usuario cancela la transacción.
- Errores locales o condiciones de excepción: la transacción no encuentra los datos a ser leídos
- Mecanismos de control de concurrencia deciden abortar una o más transacciones: puede ser por diversos motivos.

Para la recuperación ante fallos se definen dentro de las transacciones operaciones primitivas y espacios de memoria (un elemento de dato entra en un bloque). Estas operaciones primitivas son:
1. **INPUT(X):** copia el bloque de disco conteniendo el elemento de datos X al buffer de memoria. 
2. **READ(X,t):** copia el elemento de datos X a la variable local de transacción t. Si el bloque que contiene el elemento X no se encuentra en el buffer de memoria primero se ejecuta **INPUT(X)**. Luego se asigna el valor de X a la variable local t.
3. **WRITE(X,t):** copia el valor de la variable local t al elemento de datos X en el buffer de memoria. Si el bloque que contiene el elemento de datos X no se encuentra en buffer de memoria entonces primero ejecuta **INPUT(X)**. Luego copia el valor de t a X en el buffer.
4. **OUTPUT (X):** copia el bloque que contiene al elemento X del buffer al disco.

> Se usa el término elemento de datos como equivalente a item de datos.

> Ejemplo:
> Sea una transacción **T = READ(A,t); t := t*2; WRITE(A.t); READ(B.t); t := t* 2 ; WRITE(B,t);**
> ![[BD_recuperacion_ante_fallos_ejemplo_1.png]]

### Componentes
- **Transaction Managment:** Las dos tareas principales del **transaction manager** son asegurar la recuperabilidad de la base de datos a través del logging y asegurar el correcto comportamiento concurrente de las transacciones a través del **scheduler**.
- **Database Elements:** La base de datos se encuentra dividida en elementos, los cuales son típicamente bloques de disco, pero pueden ser tuplas o relaciones, por ejemplo. Los elementos de base de datos son las unidades tanto para logging como para scheduling.
- **Logging:** En el log se almacena un registro de cada acción importante de una transación (su comienzo, cambios a un elemento de base de datos, commitear o abortar). El log se debe persistir en disco en ciertos momentos relacionados a la persistencia de los cambios correspondientes en disco, este momento depende de la estrategia de logging utilizada.
- **Recovery:** Cuando un sistema crashea el log es usado para reparar la base de datos, restaurandola a un estado consistente, el **recovery manager** es el encargado de esta tarea.

![[BD_recuperacion_ante_fallos_componentes.png]]

El **transaction manager** es el componente encargado de asegurar que las transacciones son ejecutadas correctamente. Este subsistema realiza varias funciones, entre ellas:
1. Enviar señales al **log manager** para que la información necesaria pueda ser almacenada como registros de log en el log.
2. Asegurar que las transacciones ejecutandosé concurrentemente no interfieran entre ellas de manera que se puedan introducir errores.

El transaction manager envia mensajes acerca de las acciones de transacciones al log manager acerca de cuando es posible o necesario copiar el buffer a disco al **buffer manager** y al **query processor** para ejecutar las queries y otras operaciones de base de datos que formen parte de una transacción.

El **log manager** mantiene el log. Debe trabajar con el buffer manager, ya que el espacio para el log inicialmente aparece en los buffer de memoria principal, y en cierto punto estos buffers deben ser copiados a disco. Tanto el **log** como los **datos** ocupan espacio en el disco.

Finalmente el **recovery manager** se activa cuando hay un crash. Examina el log y lo usa p ara reparar los datos, si es necesario. Como en los casos anteriores, el acceso a disco es a través del buffer manager.

### Logging
En la técnica de recuperación ante fallos mediante logging se hace uso de un archivo de logs APPEND ONLY.

#### UNDO Logging
- **U1:** si la transacción T modifica el elemento de datos X, entonces se loguea un registro de la forma < T ,X ,v > previo a que el nuevo valor de X sea escrito en disco.
- **U2:** si una transacción commitea, entonces se loguea su registro de log < COMMIT T > solo después de que los elementos de la base de datos hayan sido modificados por la transacción, pero tan pronto como sea posible.

![[BD_recuperacion_ante_fallos_logging_undo_ejemplo.png]]

#### REDO Logging
- **R1:** antes de modificar cualquier elemento de datos X en disco es necesario que todos los registros de log pertinantes a esta modificación de X, incluyendo tanto el registro de update < T ,X ,v > y el registro < COMMIT T >, deben estar en disco.

![[BD_recuperacion_ante_fallos_logging_redo_ejemplo.png]]

#### UNDO/REDO Logging
- **UR1:** antes de modificar cualquier elemento de datos X en disco por los cambios realizado por una transacción T, es necesario que el registro de update < T,X,v,w > esté en disco.
- **UR2:** un registro < COMMIT T> debe ser flusheado a disco tan pronto como aparezca en el log.

![[BD_recuperacion_ante_fallos_logging_undo_redo_ejemplo.png]]

#### Checkpointing
El objetivo del checkpointing es limitar la cantidad de registros del Log que deben ser examinados en la recuperación. Marca un punto desde donde se puede estar seguro que todas las transacciones anteriores terminaron correctamente o fueron abortadas correctamente. Hay dos tipos principales de checkpointing, **quiescent** y **non-quiescent**. 

##### Quiescent checkpointing
1. Se dejan de aceptar nuevas transacciones (el sistema queda "inactivo").
2. Se espera hasta que todas las transacciones activas hagan COMMIT o ABORT y que dichos registros sean escritos en el Log en disco.
3. Se escribe el registro < CKPT> en el Log en disco, indicando el checkpoint.
4. Se aceptan nuevas transacciones.

Para el **recovery** se lee el Log a partir del último registro y hasta el punto de **checkpint**. Sabemos que hasta ahí todas las transacciones terminaron y sus cambios fueron guardados en disto. Luego se aplica la política de recuperación correspondiente al modelo de logging.

##### Non-quiescent checkpointing
El checkpointing non-quiescent varía según la estrategia de logging utilizada:

> Si se utiliza **UNDO**
> 1. Escribir en el Log < START CKPT (lista de transacciones activas)> y flushear log a disco.
> 2. Esperar hasta que todas las transaccions activas del START CKPT hagan COMMIT o ABORT sin dejar de aceptar nuevas transacciones.
> 3. Una vez finalizadas todas las transacciones de la lista del START CKPT, se escribe el registro < END CKPT> en el log y flushear.
>
> **Recovery:** se lee el log a partir del último registro, aplicando la política UNDO.
> 1. Si encuentro un < END CKPT>, debo leer no más allá del < START CKPT ...>. Ya que todas las transacciones iniciadas previo al START CKPT terminaron correctamente o fueron abortadas correctamente.
> 2. Si encuentro un < START CKPT ...> (osea no hay un < END CKPT> debido a un crash). Debo leer el Log hasta el START más antiguo de las transacciones de la lista del START CKPT que quedaron incompletas.

> Si se utiliza **REDO**
> 1. Escribir en el Log < START CKPT (lista de transacciones activas)> y flushear log a disco.
> 2. Escribir en disco todos los items modificados por transacciones que hicieron COMMIT al momento del START CKPT, que están en buffer y aún no fueron a disco sin dejar de aceptar nuevas transacciones.
> 3. Escribir el registro < END CKPT > en el log y flushear.
>
> **Recovery:** se aplica la política REDO.
> 1. Si encuentro un < END CKPT>, indica que las transacciones que hicieron commit antes del START CKPT tienen sus cambios en disco, por lo tanto las ignoro. Rehago las transacciones que hicieron COMMIT, y que comenzaron luego del START CKPT, o que estuvieron activas en ese momento. Leo hasta el START más antiguo de estas transacciones.
> 2. Si encuentro un < START CKPT ...> (osea no hay un < END CKPT> debido a un crash). Debo leer el Log hasta el END CKPT anterior o hasta el comienzo del Log, si no hubiera checkpoints.

> Si se utiliza **UNDO/REDO**
> 1. Escribir en el Log < START CKPT (lista de transacciones activas)> y flushear log a disco.
> 2. Escribir en disco todos los items modificados por todas las transacciones al momento del START CKPT, que están en buffer y aún no fueron a disco sin dejar de aceptar nuevas transacciones.
> 3. Escribir el registro < END CKPT > en el log y flushear.
>
> **Recovery:** se aplica la política UNDO/REDO.
> 1. Si encuentro un < END CKPT>, indica que todos los cambios antes del START CKPT están en disco.
> 2. Si encuentro un < START CKPT ...> (osea no hay un < END CKPT> debido a un crash). Debo leer el Log hasta el END CKPT anterior o hasta el comienzo del Log, si no hubiera checkpoints.

%%Fuente: “DATABASE SYSTEMS The Complete Book”, Second Edition, Hector Garcia-Molina, Jeffrey D. Ullman, Jennifer Widom. Department of Computer Science Stanford University, Pearson-Prentice Hall, 2009. Chapter 17: Coping With System Failures.%%