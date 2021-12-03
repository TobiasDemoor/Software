La organización de archivos consiste en abordar técnicas de [[organización de datos]] en archivos con el objetivo de optimizar la eficiencia de almacenamiento, recuperación y resguardo de los datos, comenzando con las bases conceptuales y procedimentales sobre las que se apoyarán dichas técnicas.

## Conceptos de organización de archivos
Dónde almacenar registros nuevos y cómo encontrar registros dentro del [[archivo]] para eliminarlos, modificarlos o recuperarlos para consulta. Son los modos de disponer los registros del fichero en el soporte.

Se define la estructura de archivos como la forma en cómo están constituidos físicamente los archivos. Y a la organización de archivos como a la forma de administración de los archivos, en función de las relaciones de los registros.

Desde el punto de vista de la organización existen tres modos principales:

- Secuencial: Un [[registro]] a continuación de otro.
- Directo: Los registros binarios no se disponen en el soporte atendiendo a un algoritmo de cálculo.
- Indexado: Los registros generalmente se almacenan secuencialmente y van con un [[índice]].
## Primitivas de organización de archivos
- De creación: creación y carga inicial sin validación de unicidad ni búsqueda de espacio libre.
- De actualización de registros: inserción con validación de unicidad y búsqueda de espacio libre, modificación y supresión.
- De recuperación de registros: consulta o recuperación unitaria de registros y reporte o recuperación comprensiva.
- De mantenimiento: reestructuración (reconstrucción), depuración (archivos transaccionales) y respaldo.
## Criterios para elegir un tipo de organización
Se pueden considerar tres criterios básicos:

- Rápido acceso: el costo en tiempo de acceso al dato.
- Economía de almacenamiento: el costo en tamaño de uso del espacio disponible.
- Facilidad de uso: complejidad algorítmica.

La elección de la organización determina el [[Performance|rendimiento]] relativo del sistema.

Algunas medidas de rendimiento son:

- Almacenamiento requerido por un registro.
- Tiempo de búsqueda de un registro.
- Tiempo requerido para leer todo el archivo.
- Tiempo requerido para insertar un registro.
- Tiempo para modificar un registro
## Organización de archivos secuenciales
Es la organización más simple y la primera en aparecer. La única cuando los únicos dispositivos de almacenamiento permanente eran las cintas magnéticas. Se basa en el acceso secuencial pero también puede optimizarse utilizando acceso relativo.

Los registros están grabados consecutivamente cuando el archivo se crea, y de igual forma deben ser accedidos consecutivamente cuando el archivo es procesado o tomado como entrada de datos. Los registros de un archivo secuencial quedan ordenados de acuerdo con el valor de algún campo o grupo de campos, denominados clave o llave.

*Beneficios:*

- Acceder al próximo registro es trivial.
- Con respecto a la actualización el reemplazo de campos de igual largo puede reescribirse dicho campo.
- Para agregar registros a un archivo secuencial hay dos opciones:
  - Crear un nuevo archivo.
  - Agregar al final del archivo.
- Para eliminar los registros estos se pueden marcar (necesidad de un campo extra) o se debe crear un nuevo archivo.
- Los archivos secuenciales ocupan un tamaño mínimo. Sólo el espacio requerido para el almacenamiento de los registros.
- Mientras que el patrón de acceso al archivo sea el mismo que el dado por el ordenamiento de los registros el tiempo de acceso será mínimo
### Registros ordenados por identificador
*Ventajas:*

- Optimizar búsquedas: elimina la necesidad de leer todo el archivo.
- Procesamiento coordinado con otros archivos (apareo).
- Cortes de control con un único recorrido (reportes).

*Desventajas:*

- Problemas de inserción: altas implican nuevo archivo o deben diferirse.
- Bajas costosas: bajas lógicas con necesidad de reestructuración o bajas físicas con reconstrucción del archivo o diferidas.
### Primitivas con registros desordenados
- Creación: creación y carga sin validación de unicidad ni búsqueda de espacio libre.
- Actualización de registros:
  - Inserción: se busca si el registro existe y si no existe se graba el nuevo buscando el espacio libre.
  - Modificación: se recupera el registro buscado, se actualiza, se vuelve al comienzo de la unidad recién leída (registro o bloque) y escribe la unidad modificada.
  - Eliminación (LF): se Busca el registro a eliminar; se toma su posición; se graba el ultimo registro del archivo en la posición a eliminar y trunca el archivo.
  - Eliminación (LV): se compacta el bloque donde se encontró el registro; se actualiza el Espacio Libre del bloque y se reescribe el bloque.
- Recuperación de registros: posicionamiento al inicio del archivo y lectura secuencial de registros hasta encontrar el buscado o llegar al final del archivo. Solo búsqueda lineal.
### Primitivas con registros ordenados
- Creación: registros a cargar ya están validados y ordenados por identificador ordenamiento externo de un archivo desordenado.
- Actualización de registros:
  - Inserción (directa): hay que crear un archivo nuevo, copiar los registros con identificadores menores al del registro a insertar, agregar el registro nuevo, copiar el resto de los registros con identificadores mayores, borrar el archivo viejo y renombrar el archivo nuevo con el nombre del viejo.
  - Inserción (por novedades): crear un nuevo archivo con las altas ordenadas; luego insertar por mezcla.
  - Modificación: posiciona el registro por el identificador, desde el comienzo de la unidad al registro y se escribe.
  - Eliminación (directa): hay que crear un archivo nuevo, copiar los registros con identificadores menores al del registro a eliminar, copiar el resto de los registros con identificadores mayores, borrar el archivo viejo y renombrar el archivo nuevo con el nombre del viejo.
  - Eliminación (por novedades): Dos opciones
    - Ubicar el registro por el identificador, cambiar signo del Identificador.
    - Ubicar el registro por el identificador, campo de marcado (costo x bits).
  - Eliminación (por marcado): ubicar el registro por el identificador, cambiar signo del Identificador
- Recuperación de registros: consulta o recuperación unitaria. Búsqueda Lineal o Binaria.
- Mantenimiento: hacer siempre copia de respaldo. En al caso de eliminación por marcado hay que cada tanto depurar o compactar.
### Corte de control
Es un proceso en el cual partiendo de registros ordenados por uno o más campos, se los procesa en categorías determinadas por los criterios de ordenamiento. En otras palabras, se procesa un conjunto ordenado de registros en subconjuntos determinados por los criterios de orden.

La aplicación más común para la cual se realiza el corte de control es para generar reportes que acumulen cantidades. Se utilizan contadores, sumadores, promedios, se informan subtotales por niveles y totales generales.
### Apareo de archivos
A partir de dos archivos (uno principal y otro relacionado) y tienen alguna información que los enlace, generar un tercero (o una salida por pantalla), como una mezcla de los dos. Puede ser intersección, unión o diferencia.
### Ordenamiento de archivos
*Clasificación:*

- Según lugar: internos (dentro de la memoria interna) o externos (en la memoria externa)
- Según tiempo: natural (tiempo mínimo: entrada ordenada) o no natural (tiempo mínimo: entrada inversa)
- Según estabilidad: estables (mantiene el orden por clave principal) o inestables (ordena por más de una clave).

El problema que surge al ordenar archivos es que la memoria principal no alcanza. El ordenamiento externo se requiere cuando la información a procesar no cabe en la memoria principal de una computadora (RAM). Hay que utilizar memoria externa y el proceso es más lento. Los métodos de ordenamiento externos más comunes son el de mezcla directa (merge sort) y el de mezcla natural (natural merge sort).
## Organización de archivos directos
El archivo y los registros tienen longitud fija y los registros tienen una clave primaria asociada. Cada registro del archivo posee un atributo extra que indica si el mismo está “libre”, “ocupado” o “borrado”. Para realizar altas bajas y modificaciones de registros en el archivo, se debe calcular su posición en el mismo con una función de hashing. Si dos registros hashean a la misma posición la colisión debe resolverse.

Para este tipo de organización, es conveniente que el medio de almacenamiento permita acceso directo. La memoria principal y los discos magnéticos son la mejor opción, las cintas son la peor.

Su complejidad es programar la relación existente entre el contenido de un registro y su posición física. Suele suceder que existan huecos libres dentro del medio magnético, y por lo tanto pueden existir huecos libres entre registros.
### Acceso directo
El acceso directo es el que permite acceder de manera rápida y simple a los registros de un archivo. Se debe aclarar que la secuencia u ordenamiento lógico de los registros no tiene, necesariamente, una relación con la secuencia física.

La forma de acceder a los registros es a través de la clave de dicho archivo. La clave o llave principal es el campo o la combinación de campos del archivo que permiten identificar o diferenciar plenamente cada registro de los demás.	
### Características que permitan acceso directo
- El conjunto de claves debe tener un orden ascendente, con pocos valores no utilizados, “bajar el desperdicio”.
- Ideal: La clave de los registros corresponden con los números de las direcciones.
- Existe una dirección de almacenamiento en el archivo por cada valor posible de la clave, y éstas no tiene valores duplicados.
- Los valores de las claves están en un rango acotado.
### Algoritmos de dispersión (hashing)
Técnica para generar una dirección base única para una clave dada. La dispersión se usa cuando se requiere acceso rápido a un registro. Técnica que convierte la clave del registro en un número aleatorio, el que sirve después para determinar donde se almacena el mismo.

Existen distintos métodos de construcción de funciones:

- Resto de división o módulo: la clave se divide entre el número de direcciones (debe tratarse de que sea número primo, pues tiende a distribuir residuos en forma más eficiente). Por ejemplo, Hk=k mod M.
- Multiplicación: se multiplica la llave por una constante y luego se multiplica por m. Por ejemplo, H(k) = m.(k A mod 1).
- Plegado FOLD & ADD: dividir la clave en partes iguales y sumarlas. La suma de las partes puede realizarse de dos formas:
  - Por desplazamiento: se suman las partes una a una.
  - Por fronteras: se invierte el orden de los dígitos de las partes alternadamente (en la base que se desee) y se suman.
- Compresión: dividir la clave en componentes, traducir su número de cotejo a binario y aplicar la operación XOR al resultado se le aplica la operación resto.
- Extracción: método de la mitad del cuadrado; si tenemos claves numéricas (si no se deben transformar), calculamos su cuadrado y nos quedamos con algún número de la zona central del resultado. Nos quedamos con tantos dígitos como necesitemos para mapear el array.
- Otros.
### Conceptos básicos
Las tablas hashing se aplican cuando el conjunto de claves posibles es mucho mayor que el de claves reales a almacenar.

Dado un conjunto de claves posibles X y un conjunto de direcciones de memoria D, una función de transformación H(x) es una aplicación suprayectiva del conjunto de claves posibles en el conjunto de direcciones de memoria H:X -> D.

- *Desbordamiento:* se dice que se ha producido un desbordamiento cuando una nueva clave se aplica a una dirección de memoria completamente ocupada.
- *Colisión:* se dice que se ha producido una colisión cuando dos claves distintas se aplican sobre la misma celda (las claves sinónimas producen colisiones).
- *Caso particular:* en el caso habitual en el que una celda contiene un único registro el desbordamiento y la colisión se producen simultáneamente.
- *Densidad de claves:* se denomina densidad de claves al cociente entre el número de claves en uso, m, y el número total de llaves posibles, n x.
- *Factor de carga o densidad de carga α:* se denomina al cociente entre el número de claves en uso y el número total de registros almacenables en la tabla de dispersión.
- *Hashing perfectas:* No producen colisiones. Se conoce perfectamente el espacio de claves.
- *Hashing imperfectas:* pueden producir colisiones.
### Colisiones
Hay varios métodos para reducir colisiones:

- *Propagar los registros:* buscar funciones que distribuyan muy aleatoriamente los registros podemos evitar agrupaciones de llaves que produzcan las mismas direcciones.
- *Usar memoria extra:* poner más espacio de direcciones posibles que registros a utilizar.
- *Colocar más de un registro en una dirección:* Este concepto se basa en cubetas de datos en cada dirección, ahí se colocan algunos (casi todos) los registros que colisionan de manera que al hacer una búsqueda debemos recuperar la cubeta entera ya ahí buscar por el registro deseado.

Hay varios métodos para resolver colisiones:

- *Direccionamiento abierto (progresive overflow):* en esta otra dirección distinta de la dirección de origen es encontrada en el archivo original. Para esto hay varios métodos:
  - *Sondeo lineal:* en el que el intervalo entre cada intento es constante Pi=Hk+c.
  - *Sondeo cuadrático*: En el que el intervalo entre los intentos aumenta linealmente (por lo que los índices descritos por una función cuadrática) Pi=Hk+a.i2+b.i+c.
  - *Doble hasheo*: en el que el intervalo entre intentos es constante para cada registro, pero es calculado por otra función hash Pi=Hk+i.g(k).
- *Separación de desborde (separate overflow area)*: en esta alguna dirección es encontrada para el valor fuera del área principal del archivo principal. En un área especial de desborde, exclusiva para registros que no pueden ser asignados a su dirección de origen.
- *Distribución en el almacenamiento por cubetas:* se asigna bloques de espacio para almacenar múltiples registros en lugar de asignar celdas individuales a registros. Cuando una cubeta es desbordada una nueva cubeta deberá ser asignada para el registro. Los métodos para el problema de desborde de cubetas son iguales al de las colisiones por celda. Si el direccionamiento abierto es usado se busca en la siguiente cubeta. También se puede hacer que cada cubeta sea un puntero a una lista de claves.
- *Encadenado de progresive overflow:* la idea se basa en crear una lista encadenada de sinónimos aplicando los mismos conceptos de distribución que el progresive overflow común.
- *Encadenado con separate overflow area:* se aplica nuevamente la idea de una lista encadenada, la diferencia es que se almacenan en un área de overflow. En el archivo de datos primarios solo se almacena la cabeza de la lista.
- *Scatter tables:* no existe un área primaria, solo apuntadores hacia las distintas cabeceras de listas de claves sinónimas.
## Organización de archivos indexados
Pueden verse como un conjunto de registros, los que pueden accederse mediante una clave.

*Área principal:* En esta área se almacenan los registros con los datos, al momento de crear el archivo.

*Área de índices:* Cada registro del área de índices consta de 2 campos: clave de los registros, puntero al registro en el área principal.

Anexar siempre genera un nuevo registro en ambas áreas. Eliminar basta con poner el puntero a nulo en el área de índices. Insertar puede hacerse como anexar o bien aprovechar una posición eliminada.

El índice se puede organizar de diversas formas, las más típica son: secuencial, multinivel y árbol. Podremos procesar un fichero de forma secuencial o de forma directa según la clave de indexación, y esto independientemente de como esté organizado el fichero por sí mismo. Se pueden tener tantos índices como se quiera variando la clave que se emplee. El índice está formado por registros que contienen: clave de organización -> puntero(s) al fichero de datos.
### Concepto de índice
- *Índice denso:* hay una entrada de índice por cada dato.
- *Índice no denso:* hay solo entradas de índice para un subconjunto de claves (los datos deben estar parcialmente ordenados por la clave).
- *Índice primario:* se utiliza la clave primaria del dato.
- *Índice de agrupamiento:* se utiliza un campo de ordenación del dato.
- *Índice secundario:* se utiliza cualquier otro campo.
- *Índice multinivel:* si todavía el índice es muy grande se puede hacer un índice sobre el índice. Esto aumenta la eficiencia de la búsqueda, pero complica la gestión.
### Multilistas
Conjunto de nodos en que algunos tienen más de un puntero y pueden estar en más de una lista simultáneamente. Para casa tipo de nodo es importante distinguir los distintos campos punteros para realizar los recorridos adecuados y evitar confusiones. Es la estructura básica para sistemas de bases de datos en red. El método de búsqueda permite acceder a la información de manera ordenada a través de campos claves. Las Multilistas permiten llegar a un registro por diferentes caminos. El camino lo determina el campo clave sobre el cual se haga la búsqueda. En general las multilistas son recomendables cuando la búsqueda se hace sobre un solo atributo. En el caso de necesitarse una combinación de atributos es preferible usar listas invertidas.

*Entidad:* representa una “cosa”, “objeto” o “concepto” del mundo real con existencia independiente. Una entidad está descrita y se representa por sus características o atributos.

*Relación:* es una asociación o relación matemática entre varias entidades. Poseen una cardinalidad (uno a uno, uno a varios, varios a uno o varios a varios).

Para su implementación se requiere al menos una estructura para la entidad A, una para la entidad B, una estructura para la relación A-B y una para la multilista que los engloba. Para su implementación en un archivo se requiere al menos un archivo cabecera que almacena las direcciones de inicio de cada cadena de característica, también es recomendable que incluya un campo con la longitud de cadena para seleccionar el acceso de la cadena más corta cuando se conocen varias características y tendrá tantos registros como características tenga el modelo. También se necesita el archivo principal donde se almacenan los datos y los enlaces entre ellos.
### Índices invertidos
Estructura de datos de índice de una asignación de contenido, como palabras o números, a sus localizaciones en un archivo de base de datos o en un documento o conjunto de documentos. Permite rápidas búsquedas de texto completo a un buen costo de procesamiento cuando un documento se agrega a la base de datos. Es la estructura de datos más popular en sistemas de recuperación de documentos.

Hay dos variantes principales, a nivel índice de archivo invertido (o simplemente archivo invertido) que contiene una lista de referencias a los documentos de cada palabra y índice completo invertido (o lista invertida) que además contiene las posiciones de cada palabra dentro de un documento.
### Índices secundarios
Es un índice para claves que no sean primarias, o sea una clave para más de un registro, estos son llamados índices secundarios. En los índices primarios, el direccionamiento puede ser real (posición exacta en el disco) o relativo (en función de la posición del fichero). En los índices secundarios, el direccionamiento es simbólico (la clave proporciona la clave primaria del registro, y no su dirección ni física ni relativa). En definitiva, emplea punteros indirectos (Clave secundaria -> clave primaria). Con este direccionamiento se puede cambiar la posición física de un registro sin necesitar regenerar los índices.
### Archivos invertidos
A partir de un dato (clave secundaria) se obtiene una clave primaria que lleva a más datos (también se puede poner una referencia directa al dato). Hay dos tipos: totalmente invertidos (se obtienen todas las claves relacionadas) y parcialmente invertidos (solo se obtiene la primera de ellas). La información del índice no tiene porque estar en el dato.
## Organización de archivos secuenciales indexados
El índice se puede organizar de diversas formas, las más típicas son: secuencial, multinivel y árbol. Podremos procesar un fichero de forma secuencial o de forma directa según la clave de indexación, y esto independientemente de cómo esté organizado el fichero por sí mismo Se pueden tener tantos índices como se quiera variando la clave que se emplee. El índice está formado por registros que contienen: clave de organización -> puntero(s) al fichero de datos.  Toda la información está en un conjunto encadenado de bloques (conjunto secuencia) y el árbol de acceso (árbol B) está formado con copia de las llaves que actúan como separadores (conjunto índice).