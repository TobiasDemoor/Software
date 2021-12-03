La idea fundamental es guardar la mayor cantidad de datos posibles en la menor cantidad de espacio posible y que dado el archivo comprimido pueda recuperarse el archivo original. Hay dos tipos principales de algoritmos de compresión, sin pérdida (lossless) y con pérdida (lossy). También se pueden clasificar según como procesan los datos de entrada como:

- Algoritmos estáticos: leen una vez el archivo para recolectar estadísticas y luego otra vez para comprimirlo.
- Algoritmos semi-estáticos: levantan en memoria un bloque del archivo, lo procesan en forma estática y luego graban el bloque comprimido. Solo hacen una lectura del archivo original pero cada bloque es procesado dos veces (en memoria).
- Algoritmos dinámicos: leen una vez el archivo de entrada y lo van comprimiendo a medida que lo leen.

## Compresión lossless
### Compresión RLE
El método de compresión RLE (Run Length Encoding) es utilizado por muchos formatos de imagen (BMP, PCX, TIFF). Se basa en la repetición de elementos consecutivos. El principio fundamental consiste en codificar un primer elemento al dar el número de repeticiones de un valor y después el valor que va a repetirse. Para que la compresión RLE sea efectiva está regida por reglas particulares, estas son:

- Si se repiten tres o más elementos consecutivamente, se utiliza el método de compresión RLE.
- De lo contrario se inserta un carácter de control (/x00) seguido del número de elementos de la cadena no comprimida y después la última.
- Si el número de elementos de la cadena es extraño, se agrega el carácter de control (/x00) al final.
- Finalmente, se definen los caracteres de control específicos según el código.

Su principal ventaja radica en que RLE se puede usar aún cuando no se pueda analizar el texto o imagen completa a enviar.

### Compresión estadística
Los compresores estadísticos conforman la columna vertebral de la compresión de datos. La idea básica es en base a las probabilidades de entrada reducir el tamaño esperado de la salida. El objetivo de la compresión estadística es en definitiva determinar cual deberá ser la longitud de los códigos correspondientes a los caracteres de un archivo, el valor de los códigos puede ser cualquiera siempre y cuando se respeten las longitudes.

#### *Huffman estático*
Este algoritmo desarrollado por Huffman en 1952 es el más popular y utilizado de los compresores estadísticos. El método es:

1. Armar Histograma
1. Agrupar de a dos caracteres siempre que su frecuencia de aparición sea menor a todos y se arma un nuevo símbolo, con la frecuencia de aparición de los dos anteriores.
1. Repetir el punto dos hasta que quede un [[Árboles binarios|árbol binario]] donde el nodo principal tenga cadena con todos los caracteres.

El descompresor deberá primero recuperar el árbol y luego ir descomprimiendo.

## Compresión lossy
La compresión con pérdida es una necesidad al empezar a tratar con contenido audiovisual. Sin este tipo de compresión la transmisión de este tipo de contenido (en particular videos) sería terriblemente costosa.