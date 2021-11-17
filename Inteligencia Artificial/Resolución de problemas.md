Resolver un problema determinado en un dominio D, bajo un conjunto de ciertas condiciones C, significa encontrar una solución x $\in$ X que satisfaga el conjunto de condiciones C, donde X es el conjunto de todas las soluciones posibles a dicho problema.

Este proceso de solucionar un problema se realiza mediante una búsqueda en el espacio de búsqueda que contiene X. Existen dos esquemas básicos de solución de problemas:
- **Esquema de reducción** Representación arborescente Y/O 
- **Esquema de producción** Cambio de estados ó Hallar el camino.

## Representación arborescente Y/O
En este esquema el problema se descompone en varios subproblemas, los cuales se resuelven de manera independiente y luego se combinan sus soluciones para obtener la solución del problema original.

En esta representación: 
1. La **raíz del árbol** está etiquetada con el **problema inicial**. 
2. Si un nodo etiquetado con un problema se reduce a **subproblemas**, ellos se unen en un **manojo**. 
3. Si un nodo etiquetado con un problema empareja con un **aserto**, se une a un **nodo vacío**.

![[res_de_problemas_ejemplo_repr_arborescente.png]]

## Cambio de estados
Para resolver un problema es necesario definir el problema con precisión ¿Qué quiero, dónde estoy, qué puedo hacer?

Componentes que determinan la existencia de un problema:
1. Objetivo o meta a alcanzar: Soluciones aceptables 
2. Conjunto de acciones posibles: Deben producir un cambio en el estado de un problema. El espacio de estados debe ser limitado 
3. Situación inicial

## Estrategias de búsqueda
En definitiva, no sólo basta plantear los problemas de una manera formal, sino que hace falta encontrar la forma apropiada de decidir las reglas a aplicar desde el estado inicial para llegar al estado final y el orden en que éstas se aplican. Se necesitan **estrategias de búsqueda**.

Las estrategias de búsqueda definen el orden para la expansión de nodos (qué N se extrae, dónde se inserta Ni ) Cada estrategia hay que evaluarla según:
- la **completitud** de la solución ¿encuentra la solución, si ésta existe? 
- la **complejidad temporal** ¿cuántos nodos se han generado?
-  la **complejidad espacial** ¿cuántos nodos como máximo se han guardado en memoria? 
-  la **optimalidad** de la solución ¿encuentra la solución de menor coste?
-  **Parámetros de evaluación:** Factor de ramificación (b), profundidad de la solución (d), máxima profundidad (m)

### Complejidad
![[Análisis computacional]]

### Tipos de estrategias de búsqueda
- Estrategias sin información del dominio o búsqueda a ciegas (*uninformed strategies*). Sólo emplean la información en la definición del problema. 
- Estrategias con información del dominio o estrategias heurísticas (*informed strategies*). Emplean información del espacio de búsqueda para evaluar cómo va el proceso, se utiliza una función de evaluación (heurístico) de cada nodo (el coste de llegar a él).