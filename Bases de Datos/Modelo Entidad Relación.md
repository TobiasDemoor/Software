# Modelo Entidad Relación (MER)
 Conjunto de herramientas conceptuales para describir los datos, sus relaciones y restricciones.
 Permite especificar el **diseño conceptual** de la [[Base de Datos|DB]], a través de un Diagrama Entidad Relación (DER) y especificaciones de **restricciones** que no se puedan expresar con los elementos del diagrama.
 Facilita la comunicación con el usuario ya que utiliza un lenguaje de alto nivel abstracción.

Elementos:
- **Entidad**: cosa u objeto del mundo real que es distinguible. Tiene asociado un conjunto de propiedades o atributos.
- **Conjunto de entidades**
- **Atributo**: propiedad descriptiva de las entidades. Asociado a un [[Dominio|dominio]], o conjunto de valores posibles que puede tomar.
- **Clave de un conjunto de entidades**: conjunto minimal (no tiene atributos redundantes) de atributos que permite distinguir unívocamente a una entidad de otra. Puede haber varias **claves candidatas** asociadas a un conjunto de entidades. Se elige una, denominada **clave primaria**, y se la denota subrayando sus atributos.
