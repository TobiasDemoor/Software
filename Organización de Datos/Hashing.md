---
aliases: ["hash"]
---
Una funcion hash tiene como entrada un conjunto de elementos, que suelen ser cadenas, y los convierte en un rango de salida finito, normalmente cadenas de longitud fija. Existen distintos métodos de construcción de funciones:

- Resto de división o módulo: la clave se divide entre el número de direcciones (debe tratarse de que sea número primo, pues tiende a distribuir residuos en forma más eficiente). Por ejemplo, Hk=k mod M.
- Multiplicación: se multiplica la llave por una constante y luego se multiplica por m. Por ejemplo, H(k) = m.(k A mod 1).
- Plegado FOLD & ADD: dividir la clave en partes iguales y sumarlas. La suma de las partes puede realizarse de dos formas:
  - Por desplazamiento: se suman las partes una a una.
  - Por fronteras: se invierte el orden de los dígitos de las partes alternadamente (en la base que se desee) y se suman.
- Compresión: dividir la clave en componentes, traducir su número de cotejo a binario y aplicar la operación XOR al resultado se le aplica la operación resto.
- Extracción: método de la mitad del cuadrado; si tenemos claves numéricas (si no se deben transformar), calculamos su cuadrado y nos quedamos con algún número de la zona central del resultado. Nos quedamos con tantos dígitos como necesitemos para mapear el array.
- Otros.

#### Conceptos básicos
Las tablas hashing se aplican cuando el conjunto de claves posibles es mucho mayor que el de claves reales a almacenar.

Dado un conjunto de claves posibles X y un conjunto de direcciones de memoria D, una función de transformación H(x) es una aplicación suprayectiva del conjunto de claves posibles en el conjunto de direcciones de memoria H:X -> D.

- *Desbordamiento:* se dice que se ha producido un desbordamiento cuando una nueva clave se aplica a una dirección de memoria completamente ocupada.
- *Colisión:* se dice que se ha producido una colisión cuando dos claves distintas se aplican sobre la misma celda (las claves sinónimas producen colisiones).
- *Caso particular:* en el caso habitual en el que una celda contiene un único registro el desbordamiento y la colisión se producen simultáneamente.
- *Densidad de claves:* se denomina densidad de claves al cociente entre el número de claves en uso, m, y el número total de llaves posibles, n x.
- *Factor de carga o densidad de carga α:* se denomina al cociente entre el número de claves en uso y el número total de registros almacenables en la tabla de dispersión.
- *Hashing perfectas:* No producen colisiones. Se conoce perfectamente el espacio de claves.
- *Hashing imperfectas:* pueden producir colisiones.
