---
aliases: ["entity-attribute-value", "EAV", "object–attribute–value", "vertical database model", "open schema"]
---
Modelo entidad-atributo-valor (EAV) es un modelo de datos ([[Modelo Lógico Relacional]]) para codificar, de manera eficiente en espacio, entidades donde el número de atributos (propiedades, parámetros) que se pueden utilizar para describirlas es potencialmente vasto, pero el número que realmente se aplica a una entidad determinada es relativamente modesto. Estas entidades corresponden a la noción matemática de una matriz dispersa o rala.
S
Esta representación de datos es análoga a métodos eficientes en espacio para almacenar una matriz rala, donde solo se almacenan los valores no vacíos. En un modelo de datos EAV, cada par atributo-valor es un hecho que describe una entidad, y una fila en una tabla EAV almacena un solo hecho. Las tablas EAV a menudo se describen como "largas y estrechas": "largo" se refiere al número de filas, "estrecho" a las pocas columnas.

Los datos se registran en tres columnas:
- La _entidad_: el elemento que se está describiendo.
- El _atributo_ o _parámetro_: típicamente implementado como una clave externa en una tabla de definiciones de atributos. La tabla de definiciones de atributos podría contener las siguientes columnas: un ID de atributo, nombre de atributo, descripción, tipo de datos y columnas que ayudan a la validación de entrada, por ejemplo, longitud máxima de cadena y expresión regular, conjunto de valores permitidos, etc.
- El _valor_ del atributo.