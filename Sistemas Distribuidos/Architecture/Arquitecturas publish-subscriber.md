A medida que los sistemas siguen creciendo y los procesos pueden unirse e irse más fácilmente, es importante tener una arquitectura donde las dependencias entre procesos sean lo más sueltas posibles. Una gran clase de [[Sistemas Distribuidos|sistemas distribuidos]] han adoptado una arquitectura en la que hay una gran separación entre **procesamiento** y **coordinación**. La idea es ver al sistema como una colección de procesos operando autónomamente. En este modelo, coordinación cubre la comunicacion y cooperación entre procesos. Forma el pegamento que une las actividades realizadas por procesos en un todo.

|                                  | Acoplado temporalmente | Desacoplado temporalmente   |
| -------------------------------- | ---------------------- | --------------------------- |
| **Acoplado referencialmente**    | Directa                | Mailbox                     |
| **Desacoplado referencialmente** | Basado en eventos      | Espacio de datos compartido |

Cuando los procesos están temporal y referencialmente [[Acoplamiento|acoplados]], la coordinación toma lugar de una manera **directa**. El acoplamiento referencial generalmente aparece en la forma de referencias explicitas en la comunicación. Por ejemplo un proceso solo se puede comunicar si sabe el nombre o el identificador del proceso con el que quiere intercambiar información. El acoplamiento temporal significa que los procesos que se están comunicando ambos tienen que estar ejecutandose. Un ejemplo concreto de este tipo de coordinación es una llamada telefónica.

Un tipo distinto de coordinación ocurre cuando los procesos están desacoplados temporalmente, pero acoplados referencialmente, a este lo llamamos **mailbox coordination**.

La combinación de acoplamiento temporal y desacoplamiento referencial forma el grupo de **coordinación basada en eventos**. En los sistemas referencialmente desacoplados, los procesos no se tienen que conocer explicitamente entre ellos. Lo único que un proceso puede hacer es publicar una notificación describiendo la ocurrencia de un evento y suscribirse a un tipo específico de notificación.

Un último caso es la combinación de desacoplamiento temporal y referencial, llegando al **espacio de datos compartido**. La idea central es que los procesos se comunican integramente a través de **tuplas**, las cuales son registros estructurados consistentes de un número de campos, similares a una fila de una tabla. Los procesos pueden colocar cualquier tipo de tupla en un shared data space. En orden de recolectar una tupla, un proceso provee un patrón de búsqueda que es comparado contra las tuplas. Cualquier tupla que coincida es retornada.

Estos dos últimos son **arquitecturas de publicación-suscripción**.

![[SSDD_arquitecturas_publicacion-suscripcion_1.png]]