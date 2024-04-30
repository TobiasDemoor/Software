La teoría de normalización trata de brindar un criterio para elegir un diseño de [[Bases de Datos|BD]] frente a otros diseños alternativos. Cuando se transforma el [[Diagrama Entidad Relación]] al [[Modelo Lógico Relacional]] se mide la **calidad del diseño**.

## Anomalías
Se estudian las **anomalías** del diseño. Lo que buscamos son las "buenas propiedades" de los diseños de BD relacionales y evitar los problemas o características no deseables. Estos úlitmos se pueden clasificar de la siguiente manera:
- **[[Redundancia de datos|Redundancia]]** (ej: los datos del proveedor aparecen replicados por cada item)
- **Inconsistencia Potencial** (ej: al estar replicados los datos del proveedor podrían quedar inconsistentes)
- **Anomalías de Actualización**
	- **Inserción** (ej: quiero dar de alta un proveedor que no provee ningún item, no puedo)
	- **Modificación** (ej: quiero modificar los datos de un proveedor tengo que modificar todas sus apariciones)
	- **Borrado** (ej: quiero borrar todos los items de un proveedor, se borran también los datos del proveedor)

Esquema de ejemplo: PROVEEDOR(P-nro, P-nombre, P-dir, nro-Item, nombre-Item, precio)

> La **redundancia** nos lleva a otra característica no deseable que es la **incosistencia potencial**

> La redundancia de las claves foráneas es una redundancia necesaria.

## Dependencia funcional (DF)
![[Dependencia Funcional]]

## Formas Normales
![[Formas Normales]]

## Propiedades de las descomposiciones relacionales
![[Propiedades de las descomposiciones relacionales]]

## Síntesis Relacional
![[Síntesis Relacional]]

## Descomposición FNBC
![[Descomposición FNBC]]

## Notas
[[Normalización]] [[Denormalización]]
La desventaja principal de normalizar es que se requieren más operaciones de junta para levantar los datos deseados.

Para aplicar las definiciones de 2FN en adelante hace falta tener las claves candidatas definidas.