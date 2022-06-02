---
aliases: ["árboles B", "árbol B"]
---
Los sistemas de almacenamiento masivo suelen tener un tiempo de acceso mucho mayor que el tiempo de transferencia: la localización de un elemento es mucho más costosa que la lectura secuencial de datos, una vez localizados. Esto supone un problema para estructuras enlazadas, como los [[árboles AVL]], donde las operaciones acceden a bastantes nodos de pequeño tamaño. Para grandes volúmenes se datos, sería conveniente reducir el número de accesos, a cambio de que esos accesos contuvieran elementos de mayor tamaño.

> **Árboles (a, b)**
> Los árboles (a, b) son [[árboles]] generales donde cada nodo interno puede tener un número de hijos *m+1* en el rango \[a, b]. Cada nodo almacena *m* claves (elementos comparables por ≤), ordenadas de menor a mayor que sirven para que se pueda usar como árbol de búsqueda.

Un árbol B de orden d es un árbol (d+1, 2d+1) con las propiedades adicionales siguientes:

- La raíz puede tener cualquier número de claves.
- Todas las hojas se encuentran a la misma profundidad *h*.

La segunda propiedad garantiza que un árbol B es un árbol equilibrado: su altura es logarítmica respecto al número de claves almacenadas.

### Operaciones
- Si un nodo supera el número máximo de claves (2d), el nodo se divide, transfiriendo su clave en posición media al padre.
- Si un nodo queda por debajo del número mínimo de claves (d-1):
  - Se intenta una transferencia con el hermano izquierdo o derecho, el que contenga más claves.
  - Si no es posible (ambos tienen d hijos o no existen), se produce una fusión con el hermano izquierdo (o derecho si no existe). La fusión toma un elemento del padre por lo que éste a su vez puede necesitar transferencias o fusiones (y así con los ascendientes).
 
### Árboles B+
![[B+ Tree]]

### Árboles B\*
En un árbol B\* de orden d

- Cada nodo tiene un máximo de 2d+1 descendientes y un mínimo de 2d+1.23 .
- Cada nodo excepto la raíz tiene al menos 2d.23 claves y no más de 2d.
- La raíz tiene al menos dos descendientes (a menos que sea hoja).

#### Operaciones
- Si un nodo cae por debajo del límite inferior:
  - Se intenta trasladar nodos de sus hermanos (del que tenga más nodos primero intentando con sus hermanos adyacentes).
  - Si no se puede se fusionan 3 hermanos en 2.
- Si un nodo supera el límite superior:
  - Se intenta trasladar nodos a sus hermanos (al que tenga menos nodos primero intentando con sus hermanos adyacentes).
  - Si no se puede se dividen 2 hermanos en 3.