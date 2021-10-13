Informalmente, un **modelo de datos** o **data model** es un tipo de  [[Data Abstraction|abstracción de datos]] que es usada para proveer una **representación conceptual**. El modelo de datos utiliza conceptos lógicos, tales como [[OOP|objetos]], sus propiedades, y sus interrelaciones, de manera que pueda ser más sencillo para la mayoría de los usuarios entender que los conceptos de almacenamiento. Por lo tanto, el modelo de datos *[[Ocultamiento de la información|oculta]]* detalles del almacenamiento e implementación que no son de interés para la mayoría de usuarios de [[Bases de Datos|base de datos]]. Los modelos de datos también suelen incluir un conjunto de **basic operations** para especificar consultas y modificaciones en la base de datos.

Además de las operaciones básicas, es común incluir conceptos en el modelo de datos que especifiquen el aspecto dinámico (**dynamic aspect**) o comportamiento (**behavior**) de la aplicación de base de datos. Esto permite al diseñador especificar un conjunto de operaciones válidas definidas por el usuario que son permitidas sobre los objetos de la base. En el modelo básico de datos relacionales, existen los **stored procedures** o **persistent stored modules** para añadir comportamiento a las relaciones.

Los modelos de datos se pueden clasificar según su nivel de [[Abstracción|abstracción]] en:
* **[[Modelo Conceptual|Conceptual data models]]**: de alto nivel, por ejemplo [[Modelo Entidad Relación]].
* **Physical data models**: de bajo nivel.
* **Representational data models** o implementation data models: en el medio de los anteriores, por ejemplo [[Modelo Lógico Relacional]], [[Modelo Orientado a Objetos]].

En un modelo de datos es importante distinguir entre la *descripción* de la [[Bases de Datos|base de datos]] y la *base de datos en sí*. La descripción de la base de datos es llamado **database schema** o esquema de base de datos, el cual es especificado durante el diseño de base de datos y no es esperado que cambie con frecuencia. Los datos en la bases de datos en un momento particular reciben el nombre de **database state** (estado de base de datos) o **snapshot** (foto).

### Modelo Conceptual
![[Modelo Conceptual]]

### Modelo Lógico Relacional
![[Modelo Lógico Relacional]]