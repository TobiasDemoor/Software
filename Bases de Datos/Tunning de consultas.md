Existen distintas reglas que todo administrador de BD debe conocer para poder optimizar las consultas [[SQL]]. Es importante aclarar que estas reglas no pertenecen al estándar SQL, motivo por lo cual las mismas varían en función: 
- del motor de BD 
- el tipo de índice definido 
- la magnitud de la BD

### Reglas de optimización
#### Regla 1: Evitar el uso de SELECT *
Evitar el uso de SELECT * ya que le obligará al motor de BD a leer toda la estructura de la tabla antes de ejecutar la consulta. Además, posiblemente estemos transfiriendo un conjunto mayor al que estamos necesitando.

#### Regla 2: SELECT tabla.campo
En consultas multitablas, es conveniente especificar la tabla de cada atributo en el SELECT Debemos evitar que el motor tenga que buscar a que tabla pertenece el campo especificado en el SELECT de la consulta.

#### Regla 3: Evitar el uso de funciones en los predicados
```MySQL
SELECT * FROM clientes WHERE PTRIM(nombre) = 'Pedro'
```
En este caso el índice sobre 'nombre' no será utilizado; por lo que se accederá a toda la tabla clientes (es decir que se recorrerá toda la tabla).

#### Regla 4: El índice no será utilizado cuando la columna indexada es comparada con el valor nulo
```MySQL
SELECT * FROM clientes WHERE nro_cliente IS NOT NULL

SELECT * FROM clientes WHERE nro_cliente > -1
```
Para que se pueda utilizar el índice sobre 'nro_cliente' se debe modificar la sentencia

Observaciones: 
- Esta modificación tendrá sentido si los números de cliente no son negativos. 
- Esta regla no es aplicable a todos los motores de BD.

####  Regla 5: No se utilizará el índice si la columna indexada es comparada por diferencia (!= o NOT)
```MySQL
SELECT * FROM clientes WHERE nro_cliente != 1000 

SELECT * FROM clientes WHERE nro_cliente < 1000 OR nro_cliente > 1000
```

La segunda sentencia utiliza el índice, en cambio la primer sentencia no hace uso del índice. De ser posible evitar el uso del operador NOT ya que demanda de un procesamiento extra.

#### Regla 6: Evite el uso del caracter comodín (%) al principio de un predicado
En la sentencia LIKE, el índice es utilizado únicamente cuando el primer carácter de la izquierda es distinto de %.

```MySQL
SELECT * FROM clientes WHERE nombre LIKE 'Suarez%'

SELECT * FROM clientes WHERE nombre LIKE '%Suarez'
```

En la primer sentencia se utilizaría el índice, en cambio en la segunda sentencia no se utilizaría el índice, motivo por lo cual se recorrería toda la tabla. Si es necesario su uso, tener en cuenta que es mejor usar ‘valor%’ que ‘%valor’ o ‘%valor%’.

#### Regla 7: Si un atributo en común entre dos tablas no está indexado, el optimizador ordena cada tabla con un recorrido secuencial y después las fusiona verificando la condición de combinación
```MySQL
SELECT * FROM cliente, pedidos WHERE cliente.nro_cli = pedido.nro_cli
```
Si no existen índices en ninguna de las tablas, este proceso es que es muy largo.

#### Regla 8: Cuando uno de los dos campos de las tablas que se combinan está indexado, el optimizador elige como tabla directriz aquella que no disponga de índice. Esta tabla es la que será utilizada para recorrer secuencialmente
```MySQL
SELECT * FROM cliente, pedidos WHERE cliente.nro_cli = pedido.nro_cli
```
Si existe índice sobre el campo nro_cli de la tabla pedidos, entonces se recorre la tabla clientes secuencialmente y con cada nro_cli se accede por índice a la tabla pedidos.

#### Regla 9: >= es mejor que >
```MySQL
SELECT * FROM articulos WHERE codigo >= 1000 SELECT * FROM articulos WHERE codigo > 999
```
La primera sentencia es mejor que la segunda, ya que en el primer caso el motor saltará directamente al valor 1000 mientras que en el segundo comparará todos los registros hasta encontrar el valor 1000.

#### Regla 10: Evitar la cláusula DISTINCT
```MySQL
SELECT DISTINCT codigo FROM articulos
```
Internamente se tendrá que ordenar la salida para eliminar los valores repetidos. Es una de las sentencias que más necesita hacer I/O en el disco y forzar bastante el procesador. Es conveniente evitar esta cláusula.

#### Regla 11: Utilizar los primeros campos de los índices compuestos
Si se tiene un índice compuesto por los campos A, B y C.
```MySQL
WHERE A=1 
WHERE A>=12 and A<=15 
WHERE A=1 and B<15 

WHERE B=1 
WHERE B>=12 and B<=15 
WHERE C=1 and B<15
```
En los primeros casos se utiliza el índice, en cambio en los segundos casos no se utiliza el índice. **Debemos considerar el orden de los campos a momento de definir un índice.**

#### Regla 12: Evitar el uso de la cláusula NOT IN
Se deberá filtrar por el complemento de los valores incluidos en NOT IN. En el caso de que el conjunto de valores del complemento buscado sea mayor al conjunto de los valores incluidos en NOT IN la consulta será más lerda.
```MySQL
SELECT * FROM ventas WHERE dia not IN (‘Lunes’,’Martes’)

SELECT * FROM ventas WHERE dia IN (‘Miercoles’, ‘Jueves’, ‘Viernes’, ‘Sabado’, ‘Domingo’)
```
En este caso, la segunda consulta será más lerda que la primera, no obstante debemos tratar de evitar la cláusula NOT IN. NOT IN hace un escaneo completo en la tabla descartando opciones a omitir

#### Regla 13: Evitar uniones de tablas mediante campos de texto
```MySQL
SELECT * FROM ventas, clientes WHERE ventas.nombre=clientes.nombre
```

#### Regla 14: Evitar la creación de tablas temporales
Las tablas temporales producen un procesamiento adicional y consumo extras de E/S, motivo por lo cual el[[ Optimizador de Consultas]] debe decidir si debe crear o no tablas temporales. 
- Para el caso de la cláusula **GROUP BY**, siempre se debe crear una tabla temporal para realizar el agrupamiento. 
- Para el caso de la cláusula **DISTINCT**, se debe crear una tabla que ordene los valores y elimine los duplicados. Si existe un índice único no es necesario. 
- Para el caso de la cláusula **ORDER BY**, la utilización de una tabla dependerá de los índices sobre la tabla.