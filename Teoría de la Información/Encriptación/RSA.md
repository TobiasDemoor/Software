Llamado así por sus inventores Ron Rivest, Adi Shamir y Leonard Adleman. Se basa en la dificultad para factorizar grandes números.

- Encriptación: $c = (m^e)\ mod\ n$
- Decrepitación: $m = (c^d)\ mod\ n$

Donde
- c: texto cifrado
- m: mensaje
- e: llave pública
- d: llave privada
- n = P\*Q (ya calculado)

> Las cuentas de exponenciación mod n pueden realizarse muy rápidamente utilizando el algorítmo square & multiply