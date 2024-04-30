---
aliases: ["desnormalización"]
---
A veces es necesario usar **[[Redundancia de datos|redundancia]] controlada** para mejorar la [[Performance|performance]] de las queries sobre una [[Bases de Datos|base de datos]]. Por ejemplo, pordemos almacenar el nombre del estudiante y el código de curso de manera redundante en el reporte de nota, porque cada vez que se quiera consultar el reporte de nota se quiere levantar el nombre del estudiante y el código del curso. Localizando la información junta, no se tiene que buscar a través de múltiples archivos para recolectar la información. Esto es conocido como desnormalización o **denormalization**.

El [[DBMS|DBMS]] debería ser capaz de controlar esta redundancia de manera de evitar inconcistencias.

### Principios
- Es una estrategia utilizada en una base de datos previamente [[Normalización|normalizada]] (siempre).
- Se basa en introducir redundancias controladas.
- Su objetivo es mejorar las prestaciones ([[Performance]]). La desnormalización busca mejorar tiempos en operaciones de consulta, reduciendo el número de tablas involucradas.

### Factores
- La desnormalización hace que la implementación sea más compleja (esto ya que se debe mantener cierta sincronización entre tablas).
- La desnormalización hace que se sacrifique la flexibilidad.
- La desnormalización introduce redundancia en la base de datos.
- La desnormalización puede hacer que los accesos a datos sean más rápidos, pero relentiza las actualizaciones.

### ¿Cómo aplicar desnormalización?
1. Combinar relaciones 1 a 1: si se tienen dos tablas, automoviles y motores, con una relación 1 a 1 se puede desnormalizar uniendo en una sola tabla los atributos de ambas.
2. Duplicar atributos en relaciones 1 a N: si se tienen dos tablas, películas y adaptaciones, con una relación 1 a N, y se quiere saber el nombre original y fecha de estreno para las adaptaciones (atributos que están en la tabla películas) se pueden duplicar estos datos en la tabla adaptaciones para cada adaptación y así evitar realizar una unión.
3. Duplicar atributos en relaciones N a M: en una relación N aM se crea una nueva tabla para almacenar las ocurrencias de ambas tablas (join table), de modo que si se quiere obtener la información de la tabla intermedia, se tiene que realizar el JOIN de tres tablas. Para evitar algunos de estos JOIN se puede incluir algunos de los atributos de las tablas originales en la tabla intermedia.
4. Partir tablas: las tablas se pueden partir horizontalmente (por casos) o verticalmente (por atributos) de modo que a partir de una tabla grande, que tiene datos que no se acceden con frecuencia, se obtengan tablas más pequeñas, algunas de las cuales contienen sólo datos que sí se acceden muy a menudo.
5. Introducir datos derivados: se trata de datos calculados a partir de otros datos. Esto trae con sí las ventajas de que se minimizan los cálculos en tiempo de ejecució y se minimizan la cantidad de tablas en la unión. Y también las desventajas de necesitar mayores controles en las actualizaciones y que estas tomen más tiempo.
6. Agregar nuevas tablas: es un recurso utilizado para generar resultados temporales o resultados calculados. Generalmente se aplica cuando existe una alta tasa de consulta de datos resumen con una baja o nula frecuencia de actualización. Por ejemplo consultar la ganancia histórica de la empresa. En estos casos es necesario analizar la frecuencia de generación (diaria, mensual, on demand, event oriented) y el tipo de generación (completa, incremental)

### Situaciones en las que se debería pensar en desnormalización
- **Tener precalculados valores que utilizamos con frecuencia**: evitar generar datos en vivo. 
- **Aceleración de presentación de informes**: si necesitamos algunas estadísticas con mucha frecuencia, crearlas a partir de datos en vivo requiere mucho tiempo y puede afectar al rendimiento general del sistema. 
- **Mejorar el rendimiento de las consultas**: algunas consultas pueden utilizar varias tablas para acceder a los datos que con frecuencia necesitamos.
- **Mantenimiento de un histórico**: Los detalles de ciertas consultas deben contener valores que eran reales en el momento en que se generaron. No seríamos capaces de recrear los datos del pasado correctamente si esto no es así. Podríamos resolver este problema agregando una tabla que contiene el historial de estos cambios.
- **Información de resumen preconstruida**: Util para informes, data warehouse, data mining o cubos OLAP.
