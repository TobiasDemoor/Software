---
aliases: ["idempotente"]
---
Propiedad de una operación o función. Que al aplicarse repetidamente el resultado siempre es el mismo (una consulta es una opración idempotente).

Las operaciones idempotentes son operaciones que pueden ser repetidas múltiples veces y no se acumula su resultado (realizarla 1 o más veces no altera el estado final). Por ejemplo, consultar el saldo de una cuenta es naturalmente una operación idempotente. Algunas otras operaciones deben ser forzadas (transferencias bancarias, por ejemplo).