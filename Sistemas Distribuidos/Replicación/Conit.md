Para definir inconsistencias se introduce una **unidad de consistencia** o **consistency unit**, abreviada a **conit**. Un conit especifica una unidad sobre la cual la consistencia debe ser medida.  Por ejemplo, en un sistema bursatil, un conit se podría definir como un registro representando una sola acción. Otro ejemplo es un reporte climático individual.

![[conit_1.png]]

Se define la **desviación de orden** de una réplica como la cantidad de operaciones pendientes a ser commiteadas en dicha réplica.

Se define la **desviación numérica** de una réplica como la tupla compuesta por la cantidad de operaciones faltantes en dicha réplica y la suma de dichos cámbios. Se pueden diseñar esquemas más sofisticados. Cabe destacar que para esto hace falta una comunicación entre las réplicas para que las otras estén al tanto de cuantas operaciones les faltan, se supone que esta comunicación es mucho menos costosa que la necesaria para aplicar efectivamente las operaciones.