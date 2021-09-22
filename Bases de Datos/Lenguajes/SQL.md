**SQL (Structured Query Language)** es un lenguaje de programación diseñado para administrar, y recuperar información de sistemas de gestión de base de datos relacionales ([[RDBMS]]). Es considerado un lenguaje estándar para BD relacionales.

El SQL está basado tanto en el enfoque procedural ([[Álgebra Relacional]]) como en el declarativo ([[Lenguajes Relacionales de Manejo de Datos|Cálculo Relacional]]). Estos lenguajes permiten la manipulación y recuperación de datos de la [[Bases de Datos|base de datos]].

## Selección
```SQL
SELECT <atributos>
FROM <tabla 1 [alias 1], tabla 2 [alias 2], ..., tabla N [alias N]>
[WHERE <condición>]
[GROUP BY <atributos>]
[HAVING <condicion sobre c/grupo]
[ORDER BY <atrib 1 [ASC/DESC], atrib 2 [ASC/DESC], ..., atrib M [ASC/DESC]>];
```

El valor que devuelve una sentencia yo no es una relación sino que es una tabla y por lo tanto puede haber filas repetidas, esto en contraste al [[Modelo Lógico Relacional]] teórico.

## Operadores de conjunto
```SQL
<tabla 1> UNION <tabla 2>;

<tabla 1> INTERSECT <tabla 2>;

<tabla 1> EXCEPT <tabla 2>; (diferencia)
```
Estos operadores dan como resultado conjuntos y por lo tanto no hay filas repetidas. Si se desea que queden los repetidos frente a una unión se puede usar UNION ALL.

Para realizar un producto cartesiano basta con realizar un select con dos tablas en la lista de tablas.

## Operadores de junta
Junta interna:
```SQL
SELECT <atributos>
FROM <tabla 1> <alias 1>, <tabla 2> <alias 2>
WHERE <condición de junta>;		-- usamos esta en papel

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

SELECT <atributos>
FROM  <tabla 1> <alias 1>
WHERE <atributo> <op comparación> ALL <tabla 2>;
-- tabla 2 debe tener 1 columna (generada por subquery)
-- el dom(<atributo>) debe ser igual a dom(<tabla 2>)
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
	Se lee: Los nombres de los empledos tal que no exista una planta en plantas
 	que no tenga vinculado al empleado con esa planta.
*/
```

## Notas
Los estándares de SQL representan un kernel de funciones que van a ser implementados por los lenguajes comerciales.
