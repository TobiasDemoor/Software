### Entidades
#### Entidades permanentes
Son aquellas que permanecen en el modelo.
 | Entidades en GPSS | Ejemplos                               |
 | ----------------- | -------------------------------------- |
 | Facilities        | Empleado, Procesador, Impresora...     |
 | Storages          | Cajas, Memoria, Almacén, Habitación... |
 | Queues            | Fila de espera                         |

#### Entidades transitorias
Son aquellas que ingresan, transitan a través del modelo y luego salen. Estas se llaman transacciones en GPSS. Por ejemplo, clientes, procesos, jefes, documentos, pasajeros, etc.

### Diagrama de Flujo de Transacciones (DFT)
El DFT especifica el comportamiento de las transacciones en el modelo. Está compuesto por **módulos enlazados** donde cada módulo representa “una acción” o comportamiento específico. 

Los **módulos son de una clase**, dicha clase representa un comportamiento genérico. Algunos módulos se utilizan para declarar entidades, como por ejemplo los storage. Pero algunas entidades se “instancian” automáticamente con el primer uso, como por ejemplo los facility. Durante la ejecución de la simulación las transacciones se “mueven” por el diagrama en forma concurrente.

![[MyS_DFT_ejemplo.png]]