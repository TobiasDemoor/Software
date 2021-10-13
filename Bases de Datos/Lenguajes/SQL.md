**SQL (Structured Query Language)** es un lenguaje de programación diseñado para administrar, y recuperar información de sistemas de gestión de base de datos relacionales ([[RDBMS]]). Es considerado un lenguaje estándar para BD relacionales.

El SQL está basado tanto en el enfoque procedural ([[Álgebra Relacional]]) como en el declarativo ([[Lenguajes Relacionales de Manejo de Datos|Cálculo Relacional]]). Estos lenguajes permiten la manipulación y recuperación de datos de la [[Bases de Datos|base de datos]].

Los estándares de SQL representan un kernel de funciones que van a ser implementados por los lenguajes comerciales.

## Selección
```SQL
SELECT [DISTINCT] <atributos>
FROM <tabla 1 [alias 1], tabla 2 [alias 2], ..., tabla N [alias N]>
[WHERE <condición>]
[GROUP BY <atributos>]
[HAVING <condicion sobre c/grupo]
[ORDER BY <atrib 1 [ASC/DESC], atrib 2 [ASC/DESC], ..., atrib M [ASC/DESC]>];
```

El valor que devuelve una sentencia yo no es una relación sino que es una tabla y por lo tanto puede haber filas repetidas, esto en contraste al [[Modelo Lógico Relacional]] teórico. Si se desea que el resultado sea un conjunto basta con agregar DISTINCT luego del SELECT.

## Operadores de conjunto
```SQL
<tabla 1> UNION <tabla 2>;

<tabla 1> INTERSECT <tabla 2>;

<tabla 1> EXCEPT <tabla 2>; -- (diferencia)
```
Estos operadores dan como resultado conjuntos y por lo tanto no hay filas repetidas. Si se desea que queden los repetidos frente a una unión se puede usar UNION ALL.

Para realizar un producto cartesiano basta con realizar un select con dos tablas en la lista de tablas.

## Operadores de junta
Junta interna:
```SQL
-- usamos esta para la materia
SELECT <atributos>
FROM <tabla 1> <alias 1>, <tabla 2> <alias 2>
WHERE <condición de junta>;

SELECT <atributos>
FROM <tabla 1> <alias 1>
INNER JOIN <tabla 2> <alias 2> ON <condición de junta>;

SELECT <atributos>
FROM <tabla 1> <alias 1>
NATURAL JOIN <tabla 2> <alias 2>;
```
Junta externa:
```SQL
SELECT <atributos>
FROM <tabla 1> <alias 1>
FULL OUTER JOIN <tabla 2> <alias 2> ON <condición de junta>;

SELECT <atributos>
FROM <tabla 1> <alias 1>
LEFT OUTER JOIN <tabla 2> <alias 2> ON <condición de junta>;

SELECT <atributos>
FROM <tabla 1> <alias 1>
RIGHT OUTER JOIN <tabla 2> <alias 2> ON <condición de junta>;
```

## Consultas anidadas
```SQL
SELECT <atributos>
FROM  <tabla 1>
WHERE <atributo> IN <tabla 2>;
-- tabla 2 debe tener 1 columna (generada por subquery)
-- el dom(<atributo>) debe ser igual a dom(<tabla 2>)
-- se puede negar

SELECT <atributos>
FROM <tabla 1> <alias 1>
WHERE EXISTS (
	SELECT *
	FROM <tabla 2> <alias 2>
	WHERE <condición(alias 1)>
);
-- la condición de la subquery es función de la tupla externa
-- se puede negar
```

## Comparación de conjuntos
```SQL
SELECT <atributos>
FROM  <tabla 1> <alias 1>
WHERE <atributo> <op comparación> ANY <tabla 2>;
-- tabla 2 debe tener 1 columna (generada por subquery)
-- el dom(<atributo>) debe ser igual a dom(<tabla 2>)
/*
	se lee como seleccionar si alguna tupla de tabla 2
	cumple con la condición
*/

SELECT <atributos>
FROM  <tabla 1> <alias 1>
WHERE <atributo> <op comparación> ALL <tabla 2>;
-- tabla 2 debe tener 1 columna (generada por subquery)
-- el dom(<atributo>) debe ser igual a dom(<tabla 2>)
/*
	se lee como seleccionar si todas las tuplas de tabla 2
	cumplen con la condición
*/
```

## Funciones de agregación
```SQL
SELECT 
	COUNT(*),	-- cuenta tuplas en general
	COUNT([DISTINCT] <atributo>),
	SUM([DISTINCT] <atributo>),
	AVG([DISTINCT] <atributo>),
	MIN(<atributo>),
	MAX(<atributo>)
FROM <tabla>;
```

## Agrupamiento
```SQL
SELECT <agregaciones de atributos o atributos agrupados>
FROM <tabla>
GROUP BY <lista de atributos de agrupación>
[HAVING <condición sobre c/grupo>];
```
El resultado se compone de una fila por cada grupo que cumple la condición. Las columnas resultantes tienen que estar en la lista de atributos de agregación o tienen que ser funciones de agregación.

## División
```SQL
-- Ejemplo
SELECT E.nombre
FROM EMPLEADO E
WHERE NOT EXISTS (
	SELECT * FROM PLANTA P
	WHERE NOT EXISTS (
		SELECT * FROM TRABAJA T
		WHERE T.nro-planta = P.nro-planta
			AND t.nro-leg = E.nro-leg
	)
)

/*
	Se lee: seleccionar los nombres de los empledos tal que no
	exista una planta en plantas que no tenga vinculado al
	empleado con dicha planta.
*/
```

## Stored Procedures
Un **stored procedure** es un programa almacenado físicamente en una BD que es ejecutado directamente en el motor de BD. Su implementación varía de un DBMS a otro. Los stored procedures no retornan valores, los parámetros de un stored procedure si pueden retornar valores aunque no está bien visto.

```SQL
delimiter && -- cambia el delim de fin de linea para poder utilizar ; en el SP
CREATE PROCEDURE sp_name
	([parameter [,...]])
	routine_body
&&
delimiter ;
/*
	parameter: [IN|OUT|INOUT] param_name param_type (por defecto son IN)
	routine_body: comandos SQL válidos (si son más de uno usar BEGIN END)
*/

CALL sp_name; -- para ejecutarlo
```

## Funciones
Una **función** es una rutina creada para tomar unos parámetros, procesarlos y retornar en un salida que es ejecutada directamente en el motor de BD. Su implementación varía de un DBMS a otro.

```SQL
CREATE FUNCTION fun_name
	([parameter[,...]])
	RETURNS return_type
	routine_body

/*
	parameter: [IN|OUT|INOUT] param_name param_type (por defecto son IN)
	routine_body: comandos SQL válidos con un RETURNS obligatorio
*/

SELECT fun_name -- para ejecutarla
```

## Vistas
Una **vista** es una tabla virtual. Se almacenan en el servidor con lo que el consumo de recursos y eficacia siempre serán más óptimos. Se pueden utilizar en otras consultas y no aceptan parámetros.

```SQL
CREATE [OR REPLACE] VIEW view_name
	[column_list]
	AS query

/*
	OR REPLACE: Reemplaza una vista existente en caso de coincidir en nombre
	column_list: Listado de columnas a crear
	query: Información que contendrá la vista
*/

SELECT * FROM view_name -- se consulta como a una tabla
```

Su uso más frecuente es para reportes o llenado de grillas. Tiene un nivel de acoplamiento alto con la estructura de las tablas.

## Triggers
El **trigger** o **disparador** es un objeto de la BD que está asociado con tablas (no vistas) y se activa cuando ocurre un evento en particular para esa tabla. Los eventos pueden ser INSERT, UPDATE y DELETE. Y se puede invocar antes (BEFORE) o después del evento (AFTER). No puede haber dos disparadores en una misma tabla que correspondan al mismo momento y sentencia.

```SQL
CREATE TRIGGER trig_name
	trig_moment trig_event
	ON table_name FOR EACH ROW
		trig_body

/*
	trig_moment: el momento en que el trigger entra en acción (BEFORE o AFTER)
	trig_event: la sentencia que activa al trigger (INSERT, UPDATE o DELETE)
	trig_body: la sentencia que se ejecuta cuando se activa el trigger.
*/
```

El trigger no puede referirse a tablas directamente por su nombre (depende versión MySQL). Sin embargo, se pueden emplear las palabras clave OLD y NEW.
* **OLD** se refiere a un registro existente que va a borrarse o que va a actualizarse antes de que esto ocurra.
* **NEW** se refiere a un registro nuevo que se insertará o a un registro modificado luego de que ocurre la modificación.

Estas palabras clave se pueden utilizar según la sentencia:
* **INSERT**: NEW.nom_col; ya que no hay una versión anterior del registro.
* **DELETE**: OLD.nom_col, porque no hay un nuevo registro
* **UPDATE**:
	* OLD.nom_col para referirse a las columnas del registro antes de que sea actualizado.
	* NEW.nom_col para referirse a las columnas del registro luego de actualizarlo.

El trigger no puede invocar stored procedures y tampoco puede utilizar sentencias que inicien o finalizen una transacción.

Pueden surgir conflictos relacionados a las transacciones. No es recomendable que haya lógica de negocios en los triggers, si puede ser recomendable que haya validaciones o lógica de integridad (cuando resulta imposible implementar un FK por ejemplo) y cuando se desea realizar algún tipo de cálculo para resumir una cuenta (cuando se tiene una relación entre entidades fuerte).