El envenenamiento de cache de [[DNS]] es un ataque donde los datos DNS falsificados se introducen en la caché de un RESOLVER DNS, lo que hace que el RESOLVER devuelva una dirección IP incorrecta para un dominio. Luego, si alguien consulta por ese dominio envenenado será dirigido a la IP falsa.

##### Variantes
- **Redirección al servidor de nombres del dominio objetivo:** redirigir el nombre del servidor del atacante del dominio hacia el servidor de nombres del dominio objetivo 
  Ahora ya puede asignarle a dicho servidor de nombres una dirección IP especificada por el atacante.
- **Redirigir el registro DNS a otro dominio objetivo:** Redirigir el servidor de nombres hacia otro dominio no relacionado a la petición original de una dirección IP especificada por el atacante.
- **Responder antes del servidor de nombres real:** Aplica Falsificación de DNS (DNS Forgery) Trata de hacer demorar la respuesta real hacia una consulta recursiva DNS hacia el servidor DNS.
  Las consultas DNS contienen un número identificador (nonce) de 16 bits.
  Si el atacante puede predecir exitosamente el valor de dicho número identificador y responde antes... ya esta!!!