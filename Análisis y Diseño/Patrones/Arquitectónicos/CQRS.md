%%
[Learn Microsoft](https://learn.microsoft.com/es-mx/azure/architecture/patterns/cqrs)
[CQRS, Task Based UIs, Event Sourcing agh!](https://gist.github.com/meigwilym/025f08208b5640ad26bc410c8a83b10f)
%%
CQRS (*Comand Query Responsability Separation*) significa segregación de responsabilidades de comandos y consultas, un patrón que separa las operaciones de lectura y actualización de un almacén de datos. La implementación de CQRS en la aplicación puede maximizar el rendimiento, la escalabilidad y la seguridad. La flexibilidad creada al migrar a CQRS permite que un sistema evolucione mejor con el tiempo y evita que los comandos de actualización provoquen conflictos de combinación en el nivel de dominio.

CQRS es simplemente la creación de dos objetos donde antes había uno. La separación ocurre según los métodos son un *command* (cualquier método que modifica un estado) o un *query* (cualquier método que retorna un valor). Cuando se habla de CQRS por lo general se está hablando de aplicar el patrón al objeto que representa la interfaz de servicio de una aplicación.

Esta separación nos permite realizar muchas cosas interesantes desde el punto de vista arquitectónico. La más importante es que nos fuerza a romper con la fijación usual de que por contener ambos la misma información deben utilizar el mismo modelo de datos. Así mismo nos permite escalar los servicios de *command* y de *query* de manera independiente según sea necesario.