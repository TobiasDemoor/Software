El llamada al sistema fork() crea un proceso hijo que es una réplica exacta del proceso padre. Este nuevo proceso se conoce como proceso "hijo".

Esta llamada al sistema se llama una vez (en el proceso principal) pero regresa dos veces (una vez en el padre y la segunda en el hijo). Tener en cuenta que después de la llamada al sistema fork(), no se sabe si padre se ejecutará primero (o el hijo). Es no es determinista. Depende puramente del mecanismo de cambio de contexto. Esta llamada devuelve cero en el hijo mientras que devuelve el PID del proceso hijo en el proceso padre.

El hijo tiene su propio ID de proceso único y este PID no coincide con el ID de ningún grupo de procesos existente. Existe una forma de identificar al proceso padre (Ppid). El hijo no hereda los bloqueos de memoria de sus padres. Los contadores de tiempo de CPU y de utilización de recursos de proceso se ponen a cero en el hijo. El conjunto de señales pendientes del hijo está inicialmente vacío. El hijo no hereda los bloqueos de su padre.