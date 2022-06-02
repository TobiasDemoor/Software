---
aliases: ["árboles B+", "árbol B+"]
---
Sólo las hojas contienen elementos, los nodos internos contienen claves para dirigir la búsqueda (esas claves se encuentran también en los nodos hoja). Los nodos hoja forman una lista enlazada (simple o doble).

Se utilizan en archivos secuenciales indexados, permiten una mejor recorrida por algún tipo de orden. Es un [[Índice]] multinivel, dinámico, con un límite máximo y mínimo en el número de claves por nodo.

#### Operaciones
Las operaciones son idénticas al [[B Tree|árbol B]] excepto que en la eliminación solo se eliminan los valores en las hojas, los de los nodos interiores permanecen. Cuando se inserta en un nodo hoja lleno este se divide en dos, pero ahora el primero contendrá d claves y el segundo d+1 y lo que subirá al padre será una copia de la clave central.