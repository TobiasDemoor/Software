## Notas
[[Normalization]] [[Denormalization]]
Cuando se transforma el [[Diagrama Entidad Relación]] al [[Modelo Lógico Relacional]] se mide la **calidad del diseño**. Se estudian las **anomalías** del diseño.

Esquema de ejemplo:
PROVEEDOR(P-nro, P-nombre, P-dir, nro-Item, nombre-Item, precio)

Problemas o características no deseables:
* Redundancia (ej: los datos del proveedor aparecen replicados por cada item)
* Inconsistencia Potencial (ej: al estar replicados los datos del proveedor podrían quedar inconsistentes)
* Anomalías de Actualización
	* Inserción (ej: quiero dar de alta un proveedor que no provee ningún item, no puedo)
	* Modificación (ej: quiero modificar los datos de un proveedor tengo que modificar todas sus apariciones)
	* Borrado (ej: quiero borrar todos los items de un proveedor, se borran también los datos del proveedor)
La **redundancia** nos lleva a otra característica no deseable que es la **incosistencia potencial**

> La redundancia de las claves foráneas es una redundancia necesaria.

La desventaja principal de normalizar es que se requieren más operaciones de junta para levantar los datos deseados.

### Dependencia funcional (DF)
la dependencia funcional se define dentro de un esquema de relación
$X \rightarrow Y$ se lee "X determina funcionalmente a Y" o "Y depende funcionalmente de X"

Con el ejemplo anterior podémos establecer que el P-nro determina funcionalmente a P-nombre y P-dir

A partir de las dependencias funcionales que define el diseñador (F) se pueden inferir otras en base a las **reglas de inferencia**. El conjunto de todas esas DF's se denomina **CLAUSURA DE F** y se denota $\bf{F^+}$