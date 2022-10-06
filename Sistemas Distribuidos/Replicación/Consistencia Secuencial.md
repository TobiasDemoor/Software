---
aliases: ["consistencia secuencial"]
---
En los siguientes casos se usa una notación donde se representa el eje temporal como un eje horizontal que corre de izquierda a derecha. Se utiliza la notación $W_i (x)a$ para denotar que el proceso $P_i$ escribe un valor $a$ a un item de datos x. Similarmente usamos la notación $R_i (x)b$ para representar que el proceso $P_i$ lee x y el valor leido es b. También se asume que cada item tiene valor inicial NIL.

![[SSDD_consistencia_secuencial.png]]

La **consistencia secuencial** es un importante modelo de consistencia centrado en datos (definido por Lamport\[1979] en el contexto de memoria compartida para sistemas multiprocesador).  Un almacen de datos es secuencialmente consistente  si satisface la siguiente condición:

> El resultado de cualquier ejecución es el mismo que si las operaciones (de lectura y escritura) de todos los procesos efectuados sobre el almacén de datos se ejecutaran en algún orden secuencial y las operaciones de cada proceso individual aparecieran en esa secuencia en el orden especificado por su programa.

Esta definición significa que cuando los procesos corren concurrentemente, cualquier intercalación de operaciones es aceptable, pero **todos los procesos deben tener la misma intercalación de operaciones**.