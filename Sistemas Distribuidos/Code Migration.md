Hay situciones en las que pasar [[Programa|programas]], hasta a veces programas en ejecución, entre nodos simplifica el diseño del [[Sistemas Distribuidos|sistema distribuido]].

## Modelos
**Segmento de código:** contiene la parte constitutiva del programa en ejecución.
**Segmento de recursos:** contiene la referencias a recursos externos tales como impresoras, dispositivos, etc.
**Segmento de ejecución:** el estado actual de ejeución de un [[Proceso|proceso]], es decir datos privados, la pila, el contador de programa, etc.

## Razones
Tradicionalmente la migración de código en los sistemas distribuidos tomaba la forma de **process migration** (migración de procesos) en donde un [[Proceso|proceso]] entero es movido de un nodo a otro. Mover un proceso en ejecución a una máquina diferente es una tarea costosa y compleja y debe haber una buena razón para hacerlo. Esta razón siempre ha sido la [[Performance|performance]]. La idea básica es que el rendimiento del sistema en su totalidad puede ser mejorado si los procesos son movidos de nodos altamente cargados a nodos menos cargados. La carga puede ser expresada en términos de la longitud de la cola de CPU o la utilización de CPU, pero otros indicadores de rendimiento pueden ser usados también.

Sin embargo, en vez de remover carga de nodos exigidos, pordemos mover código de maner que cada nodo está lo suficientemente cargado. En particular migrar máquinas virtuales completas con sus aplicaciones a nodos con poca carga para optimizar el uso de energía es una práctica común en los data centers. Es interesante el hecho de que aunque la migración de máquinas virtuales enteras requiera más recursos, la tarea en sí es mucho menos compleja que migrar un proceso.

En general los algoritmos de balanceo de carga que toman decisiones de alocación y redistribución de tareas  con repecto a un conjunto de máquinas tienen un rol importante en los sistemas de cómputo intensivo. Sin embargo, en muchos [[Sistemas Distribuidos|sistemas distribuidos]] modernos, optimizar la capacidad de cómputo es un problema menor que, por ejemplo, intentar minimizar la comunicación. Podemos reducir la comunicación migrando procesos más cerca de donde se encuentran los datos.

Más allá del rendimiento, hay otras razones para permitir la migración de código. La más importante es la de la flexibilidad. La técnica tradicional para construir sistemas distribuidos es particionar la aplicación en distintas partes y decidir de antemano dónde se debe ejecutar cada parte. Sin embargo, si el código se puede mover entre diferentes nodos, se vuelve posible configurar dinámicamente los sistemas distribuidos.