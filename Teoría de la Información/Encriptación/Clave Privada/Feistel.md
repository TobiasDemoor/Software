Muchos de los cifrados de producto tienen en común que dividen un bloque de longitud n en dos mitades, L y R. Los cifrados de este tipo son los Fesitel y se componen por iteraciones de 3 pasos:
1. Seleccionar cadena, N de 64 o 128 bits dividir en L y R, de igual longitud (N/2).
2. Se toma una función, F, y una clave Ki.
3. Se realizan una serie de operaciones con F y Ki y con L o R (solo uno de ellas) La cadena obtenida intercambia por la cadena sin operar y se hace nueva ronda.

![[TI_Encriptacion_Feistel.png]]

Este tipo de cifrado es utilizado por [[DES]], Lucifer, FEAL, CAST y Blowfish entre otros criptosistemas.