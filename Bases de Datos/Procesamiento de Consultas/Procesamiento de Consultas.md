Los lenguajes de consultas relacionales nos dan una interfaz declarativa de alto nivel para acceder a los datos almacenados en una base de datos. El **procesamiento de consultas** se refiere al conjunto de actividades que realiza un [[Motor de Base de datos]] para la extracción de datos de la base de datos a partir de una sentencia en un lenguaje de consulta.

Los pasos básicos son:
1. Parsing y traducción 
2. Optimización 
3. Generación de código 
4. Ejecución de la consulta

Estos pasos en general son realizados por diferentes componentes del motor. Los componentes clave son: el optimizador de consultas y el procesador de consultas.

La idea general es que luego del parsing se construya una expresión algebraica equivalente (o podría ser más de una), se analicen diferentes formas de resolver la consulta (estas formas se llaman **planes de ejecución**) evaluando sus costos, y se seleccione la más eficiente. Esto lo hace el componente generalmente llamado **Optimizador de Consultas**.

Luego, esta consulta es pasada al otro componente generalmente llamando **Procesador de Consultas**, que es el que se encarga de ejecutar físicamente la consulta de acuerdo al plan de ejecución, produciendo y devolviendo el resultado.

## Optimizador de Consultas
![[Optimizador de Consultas]]

## Optimización de Consultas
![[Optimización de Consultas]]