---
aliases: ["modelo de consistencia", "modelos de consistencia"]
---
Un **modelo de consistencia** o **consistency model** es escencialemente un contrato entre procesos y el almacen de datos. Se dice que si los procesos están de acuerdo en obedecer ciertas reglas, el almacen promete funcionar correctamente. Normalmente un proceso que realiza una operación de lectura sobre un ítem espera que la operación retorne un valor que muestre los resultados de la última operación de escritura sobre estos datos.