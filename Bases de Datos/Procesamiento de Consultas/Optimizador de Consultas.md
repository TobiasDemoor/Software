El **optimizador de consultas** es el responsable de generar el plan, que va a ser el input del motor de ejecución. Debe ser un plan eficiente de ejecución de una consulta [[SQL]], perteneciente al espacio de los posibles planes de ejecución de esa consulta.

La cantidad de posibles planes de ejecución para una consulta puede ser grande, ya sea porque [[Álgebra Relacional|algebraicamente]] se la puede escribir de diferentes maneras lógicamente equivalentes, o porque hay más de un algoritmo disponible que implemente una expresión algebraica dada. Como el procesamiento de cada plan de ejecución puede tener un rendimiento diferente, la tarea del optimizador es realmente importante a efectos de encontrar una buena solución.

Típicamente, a partir de una consulta en lenguaje SQL, construye una expresión en álgebra relacional de la siguiente manera:
1. Realiza el producto cartesiano de las tablas del FROM de izquierda a derecha. 
2. Realiza un select con las condiciones de la cláusula WHERE. 
3. Realiza una proyección con las columnas de la cláusula SELECT.

Una vez obtenida la expresión, pasa a armar un plan de ejecución de la consulta construyendo un árbol, el cual consta de expresiones de álgebra relacional, donde las relaciones son las hojas y los nodos internos, las operaciones algebraicas. Es importante notar que una misma consulta puede tener varios planes de ejecución (es decir, varios árboles pueden producir los mismos resultados).

En general, el objetivo principal es **minimizar la cantidad de accesos a disco**. El optimizador construye diferentes planes basándose en:
* Los distintos algoritmos implementados en el procesador de consultas y disponibles al optimizador que implementan las operaciones de álgebra relacional (Proyección, Selección, Unión, Intersección, Resta, Join).
* Información acerca de:
	* La estructura física de los datos (ordenamiento, clustering, hashing).
	* La existencia de [[Índice|índices]] e información sobre ellos (ej : nro de niveles que posee).
	* Estadísticas guardadas en el [[catálogo]] (esta información no está “al día” constantemente por razones de eficiencia, sino que se actualiza periódicamente):
		* Tamaño de archivos y factor de bloqueo. 
		* Cantidad de tuplas de la relación 
		* Cantidad de bloques que ocupa la relación 
		* Cantidad de valores distintos de una columna (esto permite estimar la selectividad de una operación)
* Ciertas heurísticas que le permiten encontrar planes de ejecución sin necesidad de generar en forma completa el espacio de búsquedas (como podría ser tratar de armar planes que realicen cuanto antes las operaciones más restrictivas y maximicen el uso de índices y de las estructuras físicas existentes)

Una vez construidos los diferentes planes alternativos, el optimizador selecciona el que sea más eficiente, el cual es su output.