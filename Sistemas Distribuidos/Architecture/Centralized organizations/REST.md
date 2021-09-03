Como una alternativa a la [[Architectural style#Object-based and Service-oriented architectures|vista centrada en servicios]], uno puede ver a un [[Sistemas Distribuidos|sistema distribuido]] como una gran colección de recursos que son administrados individualmente por [[Componente|componentes]]. Los recursos pueden ser añadidos o removidos por aplicaciones remotas y a su vez pueden ser consultados o modificados. Este approach fue muy adoptado para la Web y es conocido como **Representational State Transfer (REST)**.

 Hay cuatro características claves de lo que se conoce como **RESTful architectures**:
 1. Los recursos son identificados mediante un esquema de naming único ([[URL]]).
 2. Todos los servicios ofrecen la misma interfaz, consistente de como máximo 4 operaciones (PUT, GET, DELETE, POST).
 3. Los mensajes enviados para o desde el servicio son completamente auto descriptivos.
 4. Luego de ejecutar una operación en un servicio, ese [[Componente|componente]] olvida todo sobre el solicitante (**[[Servidor#Stateless vs stateful|stateless excecution]]**).

#### Operaciones
|Operation | Description                                             |
|----------|---------------------------------------------------------|
|PUT       | Crear un nuevo recurso ([[Idempotencia|idempotente]])   |
|GET       | Consultar el estado de un recurso en una representación |
|DELETE    | Eliminar un recurso                                     |
|POST      | Modificar un recurso transfiriéndole un nuevo estado    |
