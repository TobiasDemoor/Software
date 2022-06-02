---
aliases: ["árbol"]
---
Los árboles representan estructuras no lineales (porque a cada elemento del árbol puede seguirle varios elementos) y dinámicas (puesto que la estructura del árbol puede variar durante la ejecución del programa). Un árbol es una estructura jerárquica aplicada sobre una colección de elementos u objetos llamados nodos; uno de los cuales se denomina raíz.

## Características
- Todo árbol que no es vacío tiene un único nodo raíz.
- Si un nodo X es descendiente directo de un nodo Y decimos que X es hijo de Y.
- Si un nodo X es antecesor directo de un nodo Y decimos que X es padre de Y.
- Todos los nodos de un mismo padre son hermanos.
- Todo nodo que no tiene hijos es un nodo terminal.
- Todo nodo que no es raíz ni terminal es un nodo interior.
- Grado es el número de descendientes directos de un determinado nodo.
- Grado de un árbol es el máximo grado de todos los nodos del árbol.
- Nivel es el número de nodos que deben ser recorridos como mínimo para llegar a un determinado nodo (desde la raíz).
- Altura de árbol es el máximo número de niveles entre todas las ramas del árbol más 1.

## Recorridos
### En profundidad
- Preorden: primero la raíz, luego preorden subárbol izquierdo y finalmente preorden subárbol derecho.
- Postorden: primero postorden subárbol izquierdo, luego postorden subárbol derecho y finalmente la raíz.
- Inorden: primero inorden subárbol izquierdo, luego la raíz y finalmente inorden subárbol derecho.

### En anchura
- Por niveles: se etiquetan los nodos según su profundidad. Se recorren ordenados de menor a mayor nivel, igualdad de nivel se recorren de izquierda a derecha.

## Árboles degenerados
Son árboles donde cada nodo tiene un solo hijo motivo por el cual se comporta como una lista, motivo por el cual pierde la eficiencia que tienen los árboles respecto de las listas.

## Árbol binario
![[Árboles binarios]]

## Árboles B
![[B Tree]]

## Árboles hilvanados
Un árbol hilvanado es un árbol binario en el que cada hijo izquierdo de valor nulo es sustituido por un enlace o hilván al nodo que le antecede en orden simétrico (inorden) (excepto el primer nodo en orden simétrico) y cada hijo derecho de valor nulo es sustituido por un enlace o hilván al nodo que le sigue en el recorrido en orden simétrico (excepto el último nodo en orden simétrico). Cada nodo del árbol hilvanado contiene una referencia a su información, un apuntador a su hijo izquierdo, un indicador izquierdo (indica si tiene un hijo izquierdo), un apuntador a su hijo derecho y un indicador derecho (indica si tiene un hijo derecho).