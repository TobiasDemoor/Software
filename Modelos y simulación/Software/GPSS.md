## Entidades
### Entidades permanentes
Son aquellas que permanecen en el modelo.
 | Entidades en GPSS | Ejemplos                               |
 | ----------------- | -------------------------------------- |
 | Facilities        | Empleado, Procesador, Impresora...     |
 | Storages          | Cajas, Memoria, Almacén, Habitación... |
 | Queues            | Fila de espera                         |

### Entidades transitorias (Transacciones)
Son aquellas que ingresan, transitan a través del modelo y luego salen. Estas se llaman **transacciones** en GPSS. Por ejemplo, clientes, procesos, jefes, documentos, pasajeros, etc.

Estas transacciones pueden tener atributos propios que se llaman **parámetros de transacción**. Estos se crean con el primer uso, sea una asignación o una consulta.

## SNA
![[SNA]]

## SaveValue
![[SaveValue]]

## Variables
En GPSS una variable es una entidad que permite realizar un cálculo matemático y devolver el resultado del mismo.
Sus operadores son:
```
+ suma
- resta
# multiplicación
/ división entera
@ módulo
```
Permite el uso de paréntesis.
RN es un conjunto de series que generan números aleatorios (entre 1 y 999), para acceder a distintas series se agrega un número (RN1, RN2, RN3, ...). Históricamente RN1 se utiliza para los generate.

Se accede al valor de una variable utilizando el [[SNA]] V.