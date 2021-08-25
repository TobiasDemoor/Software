---
cssclass: clean-embeds
---
# Base de Datos
>"Una base de datos es una fuente central de [[Dato, información y conocimiento|datos]] con el fin de que varios usuarios la compartan para su uso en varias aplicaciones" - (Kendall, 2005)

Se puede definir una base de datos como una colección de datos relacionados. Esta definición es muy general y usualemente el término *base de datos* es más restrictivo. Una base de datos tiene las siguientes propiedades:
- Una base de datos representa un aspecto del mundo real, a veces llamado minimundo o universo de discurso (universe of discourde, UoD). Y los cambios al minimundo son reflejados en la base de datos.
- Una base de datos es una colección logicamente coherente de datos con un significado inherente. Un conjunto de datos aleatorios no puede ser llamado correctamente una base de datos.
- Una base de datos es diseñada, construida y populada con datos para un propósito en especifico. Tiene un grupo de usuarios y de aplicaciones para el cual fue diseñado.

Una base de datos computarizada puede ser mantenida por un grupo de programas de aplicación desarrollados especificamente para la tarea o mediante un [[DBMS|sistema de gestión de base de datos]].

Cuando se define una base de datos no solo se define la estructura sino que también se definen reglas que restringen los datos que la van a componer. Si de alguna manera los datos que se encuentran en la base de datos no cumplen con estas reglas estaría en un **estado inconsistente**, los datos cumplen todas las reglas se dice que es una **base de datos legal**.

En comparación al esquema predecesor de procesamiento de archivos las carácteristicas del approach de base de datos son las siguientes:
 * **Naturaleza auto descriptiva del sistema de base de datos**
		Una característica fundamental del approach de base de datos es que el [[Database System|sistema de base de datos]] no solo contiene la base de datos en sí sino también la definición o descripción de la estructura y restricciones de la base de datos (meta-data). Es importante comentar que los sistemas NOSQL no requieren meta-data, sino que la información es almacenada como información auto descriptiva (**self-describing data**).
 * **Aislamiento entre Programas e Información, y Data Abstraction**
		En el procesamiento de archivos tradicional la estructura del almacenamiento está embebido en los programas de aplicación, por lo tanto cualquier cambio a la estructura requiere actualizar todos los programas que accedan al almacenamiento. En contraste los programas de acceso del [[DBMS|DBMS]] no requieren esos cambios en la mayoría de los casos. La estructura del almacenamiento está almacenada en el catálogo, separado de los programas de acceso. A esta propiedad se le llama **independencia programa-información** (**program-data independence**).
		![[Data Abstraction]]
 * **Soporte de multiples vistas de la información**
		Una base de datos suele tener muchos tipos de usuarios, cada uno de los cuales puede requerir una perspectiva o **vista** diferente de la base de datos. Una vista puede ser un subset de la base de datos o puede contener **información virtual** (**virtual data**) que es derivada de los archivos de base de datos pero no almacenada explicitamente.
 * **Sharing de información y procesamiento de transacciones multiusuario**
		Un [[DBMS|DBMS]] multiusuario debe permitir el acceso de multiples usuarios a la base de datos simultaneamente. Esto es esencial si se pretende integrar y mantener información para múltiples aplicaciones en una sola base de datos. El [[DBMS|DBMS]] debe incluir software de **control de concurrencia** para asegurar que varios usuarios intentando modificar la misma información lo hagan en forma controlada. El concepto de [[Transacciones|transacción]] es central para muchas aplicaciones de base de datos.

## Diseño de RDBs
Una técnica para diseñar bases de datos es la **Metodología de Diseño Lógico para Bases de Datos Relacionales** (Logical Relational Design Methodology, LRDM), que utiliza la técnica de [[Diagrama Entidad Relación|DER]] extendido. En líneas generales, los pasos para lograr un diseño de la Base de Datos Relacional con esta metodología son:
1. Construcción del Modelo Entidad Relación ([[Modelo Entidad Relación|MER]]) a partir de los [[Requerimientos|requerimientos]].
2. Transformación del MER a Relaciones
3. Normalización de las Relaciones.

[[Requerimientos|Requerimientos]] ←> Diseño conceptual ([[Modelo Entidad Relación|MER]]) ←> Diseño lógico ([[Modelo Relacional|MR]]) ←> Normalización ←> Diseño Físico ←> DB
