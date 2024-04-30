Una subconsulta es una a instrucción SELECT dentro de una instrucción SELECT, INSERT, UPDATE o DELETE, o en otra subconsulta. Las subconsultas son útiles cuando la consulta depende de los resultados de otra consulta.

```MySQL
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

### Consideraciones:
- Las subconsultas se deben incluir entre paréntesis.
- Dependiendo de donde se encuentre la subconsulta, puede devolver:
	- Un solo valor
	- Una lista de valores
	- Un conjunto de registros de varias columnas (tabla).
- Pueden existir subconsultas dentro de subconsultas
- Existen 3 tipos de subconsultas
	1. Uso de una subconsulta como una tabla derivada
	2. Uso de una subconsulta como una expresión
	3. Uso de una subconsulta para correlacionar datos

### Uso de una subconsulta como una tabla derivada
Una tabla derivada se crea al utilizar una subconsulta en lugar de una tabla en una cláusula FROM.
```MySQL
SELECT * FROM (SELECT fecha FROM ventas) AS t

SELECT * FROM (SELECT * FROM ventas WHERE cc = 2) AS t
```

- Es un conjunto de registros dentro de una consulta que funciona como una tabla 
- Ocupa el lugar de la tabla en la cláusula FROM 
- La nueva tabla generada en la subconsulta debe tener un alias (es necesario ya que el resultado de la subconsulta se almacena en memoria con este)
- La subconsulta puede devolver varias filas y varias columnas

### Uso de una subconsulta como una expresión
- Se ejecuta una vez por cada registro de la consulta de afuera
- La subconsulta devuelve una sola columna
```MySQL
SELECT 
	titulo,
	precio,
	(SELECT AVG(precio) FROM libros) AS prom
FROM libros
WHERE idlibro = 777
```

### Uso de una subconsulta para correlacionar datos
- SQL ejecuta la consulta interna por cada fila que selecciona la consulta externa 
- SQL compara los resultados de la subconsulta con los resultados externos a ella
```MySQL
SELECT ordenid, clienteid
FROM ordenes AS o
WHERE 20 < (
	SELECT sum(cantidad)
	FROM ordenes_detalle AS od
	WHERE o.ordenid = od.ordenid AND od.productoid = 23
)
```

### Cláusulas EXIST y NOT EXISTS
- Los operadores EXISTS y NOT EXISTS se pueden utilizar para determinar si hay datos en una lista de valores. 
- Los operadores EXISTS y NOT EXISTS devuelven TRUE o FALSE, en función de si la subconsulta devuelve filas o no
```MySQL
SELECT nombre, empleadoid 
FROM empleados AS e 
WHERE EXISTS (
	SELECT *
	FROM ordenes AS o
	WHERE e.empleadoid = o.empleadoid AND o.fecha = ‘2020-09-05'
)
```

### Cláusulas ANY y ALL
Los operadores de comparación que presentan una subconsulta se pueden modificar mediante las palabras clave ALL o ANY.

- `campo >ANY (subconsulta)` significa que el valor de campo debe ser mayor a alguno de los valores de la subconsulta.
- `campo >ALL (subconsulta)` significa que el valor de campo debe ser mayor a todos los valores de la subconsulta.

### Resumen
|               | Tabla derivada                | Expresión   | Correlacionar datos |
| ------------- | ----------------------------- | ----------- | ------------------- |
| Ubicación     | FROM                          | SELECT      | WHERE               |
| Resultados    | Varias filas, varias columnas | Una columna | Un valor            |
| # ejecuciones | Una vez                       | N veces     | N veces             |

