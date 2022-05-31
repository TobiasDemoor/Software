---
aliases: ["criptosistemas", "criptosistema"]
---
Se define a un criptosistema como la quíntupla (M, C, K, E, D), donde:

- M representa el conjunto de todos los mensajes sin cifrar (lo que se denomina texto plano o plain text) que pueden ser enviados.
- C representa el conjunto de todos los posibles mensajes cifrados (o criptogramas).
- K representa el conjunto de claves que se pueden emplear en el criptosistema.
- E es el conjunto de transformaciones de cifrado o familia de funciones que se aplica a cada elemento de M para obtener un elemento de C. Existe una transformación diferente Ek para cada valor posible de la clave k.
- D es el conjunto de transformaciones de descifrado, análogo a E.
  
### Criptosistemas de clave simétrica o privada
**Emplean la misma clave k tanto para cifrar como para descifrar.** El problema es que para ser empleados en comunicaciones la clave k debe estar tanto en el emisor como en el receptor.

### Criptosistemas de clave asimétrica o pública
**Emplean una doble clave (kp, kP)**.

kp se conoce como clave privada y sirve para la transformación de descifrado (D).

Kp se conoce como clave pública y sirve para la transformación de cifrado (E).

Estos criptosistemas deben cumplir además que el conocimiento de la clave pública no permita calcular la clave privada. Pueden emplearse para establecer comunicaciones seguras por canales inseguros.