---
aliases: [árbol binario]
---
Los árboles binarios son [[árboles]] de grado 2, un árbol donde cada nodo puede tener como máximo 2 subárboles, siendo necesario distinguir entre el subárbol derecho y el subárbol izquierdo.

*Árboles distintos*:  son distintos cuando sus estructuras son diferentes.

*Árboles similares:* son similares cuando sus estructuras son idénticas pero la información que contienen los nodos difiere entre sí.

*Árboles equivalentes:* son equivalentes cuando son similares y además los nodos contienen la misma información.

*Árbol estricto:* si un subárbol está vacío el otro también. Cada nodo puede tener 0 o 2 hijos.

*Árbol lleno:* árbol estricto donde en cada nodo la altura del subárbol izquierdo es igual a la del subárbol derecho y ambos subárboles son árboles llenos.

*Árbol completo:* árbol lleno hasta el penúltimo nivel. En el último nivel los nodos están agrupados a la izquierda.

### Montículo binario
Es un árbol binario completo cuyos nodos almacenan elementos comparables mediante ≤ y donde todo nodo cumple la propiedad del montículo (para un montículo de mínimos: todo nodo es menor que sus descendientes).

Si un solo elemento no cumple la propiedad del montículo es posible reestablecerla mediante ascensos sucesivos en el árbol (intercambiándose con su padre) o mediante descensos sucesivos (intercambiándose con el menor de sus hijos). Para insertar un nuevo nodo se sitúa al final y se asciende hasta que cumpla con la propiedad. Para eliminar la raíz se intercambia con el último elemento y este se desciende hasta que cumpla la propiedad. Para la búsqueda se comporta como un vector desordenado.

Un montículo es una estructura muy útil para representar una cola de prioridad.

### Árbol binario de búsqueda (BB)
![[Árbol binario de búsqueda]]

### Árboles balanceados
Un árbol balanceado intenta mantener la menor profundidad en sus dos subárboles. El balanceo o equilibrio de un árbol, hace que algunas operaciones sean más eficientes, sobre todo las búsquedas. Un árbol está balanceado cuando la longitud de la trayectoria más corta hacia una hoja no difiere de la longitud de la trayectoria más larga.

### Árboles AVL (Adelson-Velski & Landis)
![[Árboles AVL]]

### Problema de los árboles binarios
El recorrido de árboles con programas recursivos resulta costoso ya que implica un gato adicional de memoria y tiempo de ejecución. Los árboles binarios suelen tener muchos punteros en NULL. Si un árbol tiene n nodos, existen 2n enlaces, donde n+1 son enlaces vacíos.