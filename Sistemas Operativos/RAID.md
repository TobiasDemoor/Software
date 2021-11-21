La tecnología **RAID (Redundant Array of Independent Disks o Redundant Array of Inexpensive Disks)** permite simular un dispositivo de almacenamiento lógico utilizando en paralelo varios físicos.

Tiene como objetivos mejorar el [[Performance|rendimiento]] del almacenamiento, aumentando el **paralelismo de operaciones** y por consecuente mejorando la **tasa de transferencia**. Y además mejorar la **seguridad** aumentando la tolerancia a fallos mediante el uso de redundancia.

## Distribución de los datos
### Direccionamiento independiente
Las partes son tan grandes como cada uno de los discos a los que refieren. Antes, los discos tenían que ser exactamente los mismos. Hoy pueden ser “similares”.

### División por Bandas
Una banda es un fragmento que se utiliza para dividir el volumen lógico resultante de la “unión” de los dispositivos físicos.

#### Bandas finas
- Máxima división. Bandas de tamaño menor a los bloques de lectura/escritura de los dispositivos físicos.
- Todos los discos leen a la vez dado que si el SO solicita un bloque del dispositivo lógico tiene que rescatar fragmentos de todos los discos. Solo una operación a la vez, dado que todos están leyendo. Velocidad muy alta.
- Los discos más lentos hacen esperar a todos los demás. Problemas con la sincronización mecánica.
- Bueno para pocos usuarios y grandes archivos.
- Un sector “virtual” consta de pedazos de sectores de más de un disco, por lo que deben sincronizarse los mismos para que los tiempos de escritura de un sector (unidad mínima) sean siempre los mínimos.

#### Bandas gruesas
- Bandas de tamaño más grande.
- Cada disco puede leer una banda independientemente de los demás discos.
- Paralelismo entre operaciones.
- Bueno para muchos usuarios.

## Mecanismos de redundancia
### Espejado
- Si se rompe un disco, puedo seguir operando con su espejo. 
- Cada disco posee su espejo.
- Sumamente robusto. Alta velocidad de respuesta a errores.
- Sumamente costoso, utiliza el doble de datos.
- 
## Métodos de detección de errores
### XOR
Destina un disco para almacenar bloques de paridad (destinado a redundancia). Cada bloque es la función XOR de los bloques correspondientes a los otros discos. Por lo tanto, puede detectar errores a nivel bloque. 

Alto costo de resolución de errores, se debe hacer en frio.

a XOR b=c→a XOR c=b→b XOR c=a

### Hamming
Utilizando [[códigos de Hamming]] puedo detectar errores de bits en caliente. Tiene un costo de redundancia mayor al XOR pero es más eficiente. Obliga al sistema a utilizar bandas finas, por lo que el RAID debe utilizarse mediante placas de hardware.

## Implementación
La **implementación por software** consta de un programa que gestiona los discos rígidos haciendo uso del procesador. Por otro lado, si implementamos por hardware, una placa física es la encargada de gestionar las operaciones de E/S de los discos.

La **implementación por software** no tiene un incremento en rendimiento muy alto, por lo que es conveniente utilizarlo en casos donde no se priorice el rendimiento, pero si la alta disponibilidad de los datos.

## Niveles de RAID
### RAID 0 - Not redundant
- Distribuye las bandas secuencialmente en los discos. 
- Bandas gruesas a nivel bloque (bloque del raid = bloque del disco físico).
- No se desperdicia espacio dedicado a la redundancia.
- Si se produce algún error crítico, pierdo la información implicada. Robustez 0.
- Si dos peticiones refieren a dos bloques distintos, hay una gran posibilidad de que se encuentren en discos separados, de modo que pueden ser respondidas en paralelo.

### RAID 1 - Mirror
- Replica cada banda en otro disco. 100% de redundancia. 
- Bandas gruesas a nivel bloque.
- Alta robustez. Muy resistente a roturas, continúa en caliente.
- Necesito almacenar el doble de la información.
- Una petición puede ser respondida a partir del disco como de su espejo, por lo que aumentamos la probabilidad de responder en paralelo.

### RAID 2 - Hamming
- Basado en el código de corrección de Hamming.
- m bits de datos y n bits de redundancia.
- m + n discos.
- Con cada byte/palabra genera el código de hamming y distribuye secuencialmente los bits en los distintos discos.
- Puede detectar errores de 2 bit y corregir errores de 1 bit.
- Corrige errores en caliente.
- Bandas finas a nivel bit.
- Resiste la rotura de un disco y continúa funcionando en caliente.
- Es complejo, necesita sincronismo mediante hardware y tiene un nivel alto de redundancia.
- Se accede al disco de datos y al de paridad en paralelo, de modo que el controlador del arreglo de discos pueda detectar el error y corregirlo en el momento.

### RAID 3 - XOR (Bandas finas)
- Por cada n-1 bandas de datos agrega una de paridad.
- Como usa bandas finas, puede lograr tasas de transferencia muy altas.
- Requiere un solo disco de paridad.
- Cuando ocurre un error de disco, se accede al disco de paridad y los datos son reconstruidos con los demás dispositivos (propiedad xor).
- Bandas finas a nivel byte/palabra.
- Requiere sincronismo a nivel hardware.
- Debido a que toda operación de E/S requiere actividad de todos los discos en sincronización, se vuelve ideal para aplicaciones que demandan las tasas de transferencia más altas en largas lecturas o escrituras secuenciales.
- Corrección en frio (a veces puede haber reconstrucción en caliente si se detecta cual está roto por otro mecanismo).
- Barato y detecta el error en un disco. Tasa de transferencia alta.

### RAID 4 - XOR (Bandas gruesas)
- Por cada n-1 bandas de datos agrega una de paridad.
- Independencia entre los discos más acentuada, no total.
- Permite resolver peticiones en paralelo.
- Bandas gruesas a nivel bloque.
- Requiere cierto sincronismo a nivel hardware, dado que necesito escribir en paralelo al bloque de paridad correspondiente al respectivo offset. Puede suceder que se escriba en simultáneo en varios discos, por lo que se produce un cuello de botella con el disco de paridad.
- Cuando se escribe un bloque, se debe actualizar no solo los datos sino también los bits de paridad correspondientes.

### RAID 5 - XOR (distribuido)
- Distribuye los bloques de paridad a lo largo de todos los discos. 
- Reduce la posibilidad de cuello de botella en disco de paridad.
- Soporta la ruptura de un disco, no se pierden todos los datos.
- Para un arreglo de n discos, el bloque de paridad está en un disco diferente para los primeros n bloques de datos, luego el patrón se repite.

### RAID 6 - XOR (doble)
- Surge para soportar la ruptura de dos discos.
- Requiere N+2 discos.
- Se realizan dos cálculos de paridad diferentes y se almacenan en bloques separados en diferentes discos (P y Q en el gráfico). Uno de estos dos es utilizado en RAID 4 y 5.
- Más gasto en redundancia.
- Gran penalización de escritura, hay que actualizar dos bloques de paridad por bloque que se modifica.