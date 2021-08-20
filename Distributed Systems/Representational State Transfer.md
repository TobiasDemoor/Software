# Representational State Transfer (REST)
 Hay cuatro características claves de lo que se conoce como **RESTful architectures**:
 1. Los recursos son identificados mediante un esquema de naming único.
 2. Todos los servicios ofrecen la misma interfaz, consistente de como máximo 4 operaciones (PUT, GET, DELETE, POST).
 3. Los mensajes enviados para o desde el servicio son completamente auto descriptivos.
 4. Luego de ejecutar una operación en un servicio, ese [[Component|componente]] olvida todo sobre el solicitante (**stateless excecution**).

## Operaciones
|Operation | Description                                             |
|----------|---------------------------------------------------------|
|POST      | Crear un nuevo recurso                                  |
|GET       | Consultar el estado de un recurso en una representación |
|DELETE    | Eliminar un recurso                                     |
|PUT/PATCH | Modificar un recurso transfiriendole un nuevo estado    |
