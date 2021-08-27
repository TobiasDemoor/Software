## Arquitectura de tres schemas
El objetivo de la [[Software Architecture|arquitectura]] de tres schemas para [[Database System|sistemas de base de datos]] (**three-schema architecture**) es el de separar las aplicaciones de usuario de la base de datos física. En esta arquitectura los schemas pueden ser definidos en tres niveles:
1. El **nivel interno** tiene un **schema interno**, el cual describe la estructura de almacenamiento físico de la base de datos. El schema interno usa un modelo de datos físico y describe los detalles completos del almacenamiento y las rutas de acceso para la base de datos.
2. El **nivel conceptual** tiene un **schema conceptual**, el cual describe la estructura de toda la base de datos para una comunidad de usuarios. El schema conceptual oculta los detalles de las estructuras de almacenamiento físico y se concentra en describir las entidades, tipos de datos, relaciones, operaciones y [[Integrity constraints|restricciones]].
3. El **nivel externo** o de **vista** incluye un número de **schemas externos** o **vistas de usuario**. Cada schema externo describe la parte de la base de datos que es de interés para un grupo particular de usuarios y oculta el resto.

![[database_three_schema_architecture_1.png]]

### Data Independence
![[Data Independence]]