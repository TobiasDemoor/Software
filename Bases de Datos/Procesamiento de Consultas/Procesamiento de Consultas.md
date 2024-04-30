Los lenguajes de consultas relacionales nos dan una interfaz declarativa de alto nivel para acceder a los datos almacenados en una base de datos. El **procesamiento de consultas** se refiere al conjunto de actividades que realiza un [[Motor de Base de datos]] para la extracción de datos de la base de datos a partir de una sentencia en un lenguaje de consulta.

Los pasos básicos son:
1. Parsing y traducción 
2. Optimización 
3. Generación de código 
4. Ejecución de la consulta

Estos pasos en general son realizados por diferentes componentes del motor. Los componentes clave son: el optimizador de consultas y el procesador de consultas.

La idea general es que luego del parsing se construya una expresión algebraica equivalente (o podría ser más de una), se analicen diferentes formas de resolver la consulta (estas formas se llaman **planes de ejecución**) evaluando sus costos, y se seleccione la más eficiente. Esto lo hace el componente generalmente llamado **Optimizador de Consultas**.

Luego, esta consulta es pasada al otro componente generalmente llamando **Procesador de Consultas**, que es el que se encarga de ejecutar físicamente la consulta de acuerdo al plan de ejecución, produciendo y devolviendo el resultado.

## Procesamiento de consultas
%%Base de datos II%%
Cada vez que el motor de BD recibe una consulta, ejecuta el siguiente proceso: 
1. La caché de consultas 
	- Se recibe la consulta
	- Se aplica un hash
	- Se verifica la existencia en el almacenamiento de consultas
	La caché de consultas es muy útil en tablas que no cambian frecuentemente y donde se realizan muchas peticiones idénticas, suele ser el caso de páginas web dinámicas que muestran el resultado almacenado en base de datos.
	
	La cache puede ser activada/desactiva en el motor de BD.
2. Parseado 
	El parseado es el análisis gramatical de una cadena de texto. El analizador de consultas se asegura de que la consulta sea sintácticamente y semánticamente correcta.
	**[[Sintaxis|Sintácticamente]]** se verifica que el lenguaje de alto nivel (SQL) se utilice correctamente, Se evalúa: 
	- consulta este bien estructurada 
	- clausulas correctamente definidas 
	- objetos referenciados sean válidos 
	- los nombres de los campos estén bien especificados, sin comas fuera de lugar, palabras reservadas, etc.
	**[[Semántica|Semánticamente]]** el motor de BD realiza una evaluación bastante limitada de la semántica. La semántica se refiere al significado de las cosas. El motor de BD evalúa si dentro de la cláusula de WHERE existen condiciones contradictorias, con el objetivo de simplificar la estructura de la consulta y evitar el trabajo de extraer datos que impliquen condiciones falsas.
3. Optimización 
    Primero realiza optimizaciones directas (Mejoras que siempre resultan en un mejor rendimiento, como simplificar $5*10$ en $50$).
    Posteriormente realiza optimizaciones más complejas (Por ejemplo simplificar las sentencias que disponen de subquery reescribiendolas utilizando join).
    La optimización de las consultas tiene lugar en el nivel del [[Álgebra Relacional|álgebra relacional]], donde el sistema intenta hallar una expresión que sea equivalente a la expresión dada, pero de ejecución más eficiente.
4. Planificación 
    Se utiliza la sentencia EXPLAIN (MySQL) y cada motor de BD tiene distintas implementaciones/soluciones.
    Hay que tener en cuenta que el planificador debe tomar una decisión muy rápida sobre el mejor camino a seguir. No puede probar todas las opciones porque pasaría más tiempo planificando que resolviendo. Debe tomar sus decisiones con información parcial sobre, por ejemplo, la efectividad de un índice, el orden más conveniente de realizar una cadena de joins, etc.
    El [[Optimizador de consultas]] de SQL elige, además del plan de ejecución con el costo de recursos mínimo, el plan que devuelve resultados al usuario con un costo razonable de recursos y con la mayor brevedad posible.
5. Ejecución
	Una vez realizadas las actividades anteriores, el motor de BD ejecuta las consultas y devuelve el resultado.   

## Optimizador de consultas
![[Optimizador de consultas]]

## Optimización de consultas
![[Optimización de consultas]]
