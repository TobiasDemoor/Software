Los grupos de control, también llamados cgroups, se refieren a una característica que permite que los procesos dentro de un sistema [[Linux]] se puedan organizar en grupos jerárquicos. Estos grupos permiten monitorear y limitar el uso de varios recursos en el sistema.

cgroups hace posible realizar limitaciones en un grupo de operaciones a varios recursos en un solo sistema. Los grupos de control se dividen en varios subsistemas, como memoria, CPU, conjuntos de CPU, bloques de memoria de entrada / salida, etc. Los subsistemas de Linux se pueden utilizar de forma independiente pero también se pueden agrupar. Un subsistema se refiere a un componente del kernel que modifica el comportamiento original en un cgroup; también podemos llamarlos controladores o controladores de recursos.

> En /sys/fs/cgroup se pueden ver los recursos que cgroups puede controlar en el SO
