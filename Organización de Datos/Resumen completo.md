# Organización de Datos
`	`Técnicas de representación y almacenamiento de datos en archivos para su recuperación, resguardo y transmisión en formas eficientes y seguras.

`	`*Tipo de Dato Abstracto (TDA):* Modelo formal de un ente junto con un conjunto de operaciones definidas sobre el modelo que nos permite procesarlo.

`	`*Estructuras de datos:* Organización lógica de la información con que representamos los datos.
# Conceptos fundamentales
## Dato
`	`Representación de una cosa real o ideal o de un evento ocurrido o programado para que ocurra, en una unidad lógica de manipulación llamada registro, en términos de características descriptivas (atributos) que se representan en unidades llamadas campos.
## Archivo de Datos
`	`Unidad lógica de almacenamiento permanente de registros, administrada por un sistema operativo. Dentro de un archivo los registros pueden organizarse en otras unidades lógicas llamadas bloques o páginas.
## Clasificación de archivos por función
- Archivos de datos maestros:

Datos de un sistema de información que representan entidades de existencia real o ideal, por ejemplo, productos o servicios, o valores de referencia para determinar características o atributos de otros datos (dominios de atributos definidos por extensión).

- Archivos de datos transaccionales:

Registros de hechos o eventos relacionados con datos maestros, por ejemplo, de ventas de productos o de prestaciones de servicios.

- Archivos de reporte:

Información editada para su presentación al usuario (en general en formatos pdf, html o de texto).

- Archivos de trabajo:

Resultados parciales o intermedios de procesamiento, o datos de intercambio entre programas.

- Archivos de control de datos:

Para almacenar metadatos (definiciones de datos), administrar espacios libres, registrar identificadores de registro vacantes o acceder al contenido de otro Archivo (índices y tablas de acceso).

- Archivos de intercambio de datos:

Representar datos en formatos estándar de manera que puedan ser procesados libremente conociendo el estándar.

Generalmente son archivos de texto, con alguna convención para rotular o delimitar datos, que pueden incluir o no definiciones sobre la estructura de la información contenida. (un estándar actual es el XML: eXtensible Markup Language).

- Archivos de recursos de programa:

También conocidos como de Unidades Grandes de Información. (imágenes, audio, vídeo).

- Archivos de productos de programas:

Son archivos con tipo asociado a un programa o aplicación (.doc, .xls, etc.).

- Archivos de empaquetado de archivos:

Se utilizan para agrupar, normalmente en forma comprimida, archivos y directorios, con propósitos de trasmisión o respaldo (.zip, .rar, etc.).
## Clasificación de archivos por tipos de datos
- Texto
- Binarios
- Tipificados y sin tipo
## Clasificación de archivos por tipo de registros
- Registros de longitud fija
- Registros de longitud variable
## Clasificación de archivos por tipo de acceso
- Secuencial
- Directo
- Indexado
- Relativos
- Stream (flujo de datos)
## Sistema operativo
Es el responsable del manejo de recursos de una computadora. Los recursos pueden ser físicos (el hardware) o lógicos (carpetas y archivos).

Provee una interfaz controlada entre usuarios y aplicaciones, a nivel lógico, y dispositivos de almacenamiento secundario, a nivel físico.
### Sistema de archivo
Los usuarios y programas tienen una visión lógica de la Información almacenada, y los dispositivos de almacenamiento tienen una visión física. El sistema operativo es el mediador.

El conjunto de programas del sistema operativo encargados de proveer la visión lógica de la información almacenada a usuarios y programas conforman: el Sistema de Archivo.
### Funciones de un sistema operativo
- Identificación y ubicación de archivos (Directorio Estructura Jerárquica o catalogo)
- Brindar seguridad (Usuarios y Grupos; permiso de acceso a los datos)
- Asignación de espacio en dispositivos de almacenamiento (Administra lo que ocupa cada archivo, y las Unidades de asignación libre)
- Coordinación de transferencia (Atender y resolver las solicitudes simultaneas; Priorizar lectura/escritura de registros)
- Administrar la comunicación entre la CPU y los dispositivos de almacenamiento (Administrar el acceso concurrente de procesos a un mismo registro físico)
## Visión lógica de archivos
Atributos: Nombre, tamaño, fecha/hora, dueño, grupo, indicadores, etc.

Operaciones: Crear, eliminar, abrir, cerrar, leer, escribir, escribir al final, posicionarse, obtener atributos, definir atributos, renombrar.
# Organización de archivos
`	`La organización de archivos consiste en abordar técnicas de organización de datos en archivos con el objetivo de optimizar la eficiencia de almacenamiento, recuperación y resguardo de los datos, comenzando con las bases conceptuales y procedimentales sobre las que se apoyarán dichas técnicas.
## Diseño de datos
`	`*Atributos:* especificación que define una propiedad de un objeto, elemento o archivo. También puede referirse a el valor específico para una instancia determinada de los mismos.

`	`*Tipos de atributos:*

- Simple: una propiedad (por ejemplo, nombre, apellido, peso, altura.
- Compuestos; una propiedad compuesta (por ejemplo, fecha -> día, mes, año)
- Opcional: puede o no estar al momento de registrarse.
- Polivalentes: Depende de una lista de valores del mismo tipo.
- Externos; relacionan un dato con otro u otros del mismo conjunto o un conjunto externo.

*Identificador:* Cada cosa o evento debe poder distinguirse de los demás. Debe haber uno o más atributos que identifiquen unívocamente a los datos. Un conjunto de datos puede tener más de un identificador.
### Diseño conceptual
`	`La definición conceptual de datos implica la definición de atributos, sin especificar tipos o dominios. Para cada atributo se indica la identidad (nombre). La estructura (en caso de que sean compuestos). La cardinalidad. Y también se puede definir la extensión.

*Los calificadores:*

- i: identificador.
- ie: identificador externo.
- d: definido por extensión en otro archivo.
- ?: opcional
- \*: ninguno o varios (0 a N)
- +: uno o más
### Definición lógica
`	`Para cada atributo (dentro de un archivo). Implica la definición de bloques o unidades de organización. Especificando tipos o dominios para atributos, y la determina la convención de almacenamiento y recuperación. Es independiente del lenguaje de programación.


| *Tipos de valores convencionales* |                      |                                                                                                                                          |
|:---------------------------------:| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
|                En                 | Enteros              | Complemento a dos en n bytes                                                                                                             |
|                Fn                 | Fraccionarios        | Punto flotante en n bytes                                                                                                                |
|                Cn                 | Caracteres           | Con longitud exacta n                                                                                                                    |
|                CV                 | Caracteres Variables | Hasta 255, con prefijo de longitud                                                                                                       |
|                 T                 | Texto                | Cantidad ilimitada de caracteres, incluyendo caracteres de control como salto de línea, retorno de carro, tabulación, fin de texto, etc. |
|                 L                 | Lógicos              | 0: Falso o No, 1: Verdadero o Sí                                                                                                         |
|                 B                 | Binario              | Imagen, audio, video, etc.                                                                                                               |
# Organización de registros
## Registros de longitud fija
`	`Son elementos del mismo tamaño y almacenan la información en los archivos mediante un encabezado. Se introducen una a uno los registros ubicados en posiciones consecutivas. En el tamaño del campo produce un desperdicio de espacio. Facilita la dirección y extracción de la información del campo.
## Registros de longitud variable
`	`Almacenan elementos de varios tipos en un archivo y permite uno o más campos de longitudes variables y los campos pueden ser repetidos. La longitud de los registros debe estar definida correctamente para poder leer y escribir de forma efectiva. Aquí hay un aprovechamiento del espacio, pero se complica la localización y extracción de información.
## Independencia lógica de datos
`	`*Datos lógicamente dependientes:* Dependen de una aplicación propietaria (sólo la aplicación conoce la estructura y organización de los registros).

`	`*Datos lógicamente independientes:* Hay una definición de los datos (metadatos) pública y en una convención estándar (por ejemplo, XML)
# Organización de archivos
## Conceptos de organización de archivos
`	`Dónde almacenar registros nuevos y cómo encontrar registros dentro del archivo para eliminarlos, modificarlos o recuperarlos para consulta. Son los modos de disponer los registros del fichero en el soporte.

`	`Se define la estructura de archivos como la forma en cómo están constituidos físicamente los archivos. Y a la organización de archivos como a la forma de administración de los archivos, en función de las relaciones de los registros.

Desde el punto de vista de la organización existen tres modos principales:

- Secuencial: Un registro a continuación de otro.
- Directo: Los registros binarios no se disponen en el soporte atendiendo a un algoritmo de cálculo.
- Indexado: Los registros generalmente se almacenan secuencialmente y van con un índice.
## Primitivas de organización de archivos
- De creación: creación y carga inicial sin validación de unicidad ni búsqueda de espacio libre.
- De actualización de registros: inserción con validación de unicidad y búsqueda de espacio libre, modificación y supresión.
- De recuperación de registros: consulta o recuperación unitaria de registros y reporte o recuperación comprensiva.
- De mantenimiento: reestructuración (reconstrucción), depuración (archivos transaccionales) y respaldo.
## Criterios para elegir un tipo de organización
`	`Se pueden considerar tres criterios básicos:

- Rápido acceso: el costo en tiempo de acceso al dato.
- Economía de almacenamiento: el costo en tamaño de uso del espacio disponible.
- Facilidad de uso: complejidad algorítmica.

La elección de la organización determina el rendimiento relativo del sistema.

Algunas medidas de rendimiento son:

- Almacenamiento requerido por un registro.
- Tiempo de búsqueda de un registro.
- Tiempo requerido para leer todo el archivo.
- Tiempo requerido para insertar un registro.
- Tiempo para modificar un registro
## Organización de archivos secuenciales
`	`Es la organización más simple y la primera en aparecer. La única cuando los únicos dispositivos de almacenamiento permanente eran las cintas magnéticas. Se basa en el acceso secuencial pero también puede optimizarse utilizando acceso relativo.

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
`	`*Ventajas:*

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
`	`*Clasificación:*

- Según lugar: internos (dentro de la memoria interna) o externos (en la memoria externa)
- Según tiempo: natural (tiempo mínimo: entrada ordenada) o no natural (tiempo mínimo: entrada inversa)
- Según estabilidad: estables (mantiene el orden por clave principal) o inestables (ordena por más de una clave).

El problema que surge al ordenar archivos es que la memoria principal no alcanza. El ordenamiento externo se requiere cuando la información a procesar no cabe en la memoria principal de una computadora (RAM). Hay que utilizar memoria externa y el proceso es más lento. Los métodos de ordenamiento externos más comunes son el de mezcla directa (merge sort) y el de mezcla natural (natural merge sort).
## Organización de archivos directos
`	`El archivo y los registros tienen longitud fija y los registros tienen una clave primaria asociada. Cada registro del archivo posee un atributo extra que indica si el mismo está “libre”, “ocupado” o “borrado”. Para realizar altas bajas y modificaciones de registros en el archivo, se debe calcular su posición en el mismo con una función de hashing. Si dos registros hashean a la misma posición la colisión debe resolverse.

Para este tipo de organización, es conveniente que el medio de almacenamiento permita acceso directo. La memoria principal y los discos magnéticos son la mejor opción, las cintas son la peor.

Su complejidad es programar la relación existente entre el contenido de un registro y su posición física. Suele suceder que existan huecos libres dentro del medio magnético, y por lo tanto pueden existir huecos libres entre registros.
### Acceso directo
`	`El acceso directo es el que permite acceder de manera rápida y simple a los registros de un archivo. Se debe aclarar que la secuencia u ordenamiento lógico de los registros no tiene, necesariamente, una relación con la secuencia física.

La forma de acceder a los registros es a través de la clave de dicho archivo. La clave o llave principal es el campo o la combinación de campos del archivo que permiten identificar o diferenciar plenamente cada registro de los demás.	
### Características que permitan acceso directo
- El conjunto de claves debe tener un orden ascendente, con pocos valores no utilizados, “bajar el desperdicio”.
- Ideal: La clave de los registros corresponden con los números de las direcciones.
- Existe una dirección de almacenamiento en el archivo por cada valor posible de la clave, y éstas no tiene valores duplicados.
- Los valores de las claves están en un rango acotado.
### Algoritmos de dispersión (hashing)
`	`Técnica para generar una dirección base única para una clave dada. La dispersión se usa cuando se requiere acceso rápido a un registro. Técnica que convierte la clave del registro en un número aleatorio, el que sirve después para determinar donde se almacena el mismo.

`	`Existen distintos métodos de construcción de funciones:

- Resto de división o módulo: la clave se divide entre el número de direcciones (debe tratarse de que sea número primo, pues tiende a distribuir residuos en forma más eficiente). Por ejemplo, Hk=k mod M.
- Multiplicación: se multiplica la llave por una constante y luego se multiplica por m. Por ejemplo, H(k) = m.(k A mod 1).
- Plegado FOLD & ADD: dividir la clave en partes iguales y sumarlas. La suma de las partes puede realizarse de dos formas:
  - Por desplazamiento: se suman las partes una a una.
  - Por fronteras: se invierte el orden de los dígitos de las partes alternadamente (en la base que se desee) y se suman.
- Compresión: dividir la clave en componentes, traducir su número de cotejo a binario y aplicar la operación XOR al resultado se le aplica la operación resto.
- Extracción: método de la mitad del cuadrado; si tenemos claves numéricas (si no se deben transformar), calculamos su cuadrado y nos quedamos con algún número de la zona central del resultado. Nos quedamos con tantos dígitos como necesitemos para mapear el array.
- Otros.
### Conceptos básicos
`	`Las tablas hashing se aplican cuando el conjunto de claves posibles es mucho mayor que el de claves reales a almacenar.

`	`Dado un conjunto de claves posibles X y un conjunto de direcciones de memoria D, una función de transformación H(x) es una aplicación suprayectiva del conjunto de claves posibles en el conjunto de direcciones de memoria H:X -> D.

- *Desbordamiento:* se dice que se ha producido un desbordamiento cuando una nueva clave se aplica a una dirección de memoria completamente ocupada.
- *Colisión:* se dice que se ha producido una colisión cuando dos claves distintas se aplican sobre la misma celda (las claves sinónimas producen colisiones).
- *Caso particular:* en el caso habitual en el que una celda contiene un único registro el desbordamiento y la colisión se producen simultáneamente.
- *Densidad de claves:* se denomina densidad de claves al cociente entre el número de claves en uso, m, y el número total de llaves posibles, n x.
- *Factor de carga o densidad de carga α:* se denomina al cociente entre el número de claves en uso y el número total de registros almacenables en la tabla de dispersión.
- *Hashing perfectas:* No producen colisiones. Se conoce perfectamente el espacio de claves.
- *Hashing imperfectas:* pueden producir colisiones.
### Colisiones
`	`Hay varios métodos para reducir colisiones:

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
`	`Pueden verse como un conjunto de registros, los que pueden accederse mediante una clave.

`	`*Área principal:* En esta área se almacenan los registros con los datos, al momento de crear el archivo.

`	`*Área de índices:* Cada registro del área de índices consta de 2 campos: clave de los registros, puntero al registro en el área principal.

`	`Anexar siempre genera un nuevo registro en ambas áreas. Eliminar basta con poner el puntero a nulo en el área de índices. Insertar puede hacerse como anexar o bien aprovechar una posición eliminada.

`	`El índice se puede organizar de diversas formas, las más típica son: secuencial, multinivel y árbol. Podremos procesar un fichero de forma secuencial o de forma directa según la clave de indexación, y esto independientemente de como esté organizado el fichero por sí mismo. Se pueden tener tantos índices como se quiera variando la clave que se emplee. El índice está formado por registros que contienen: clave de organización -> puntero(s) al fichero de datos.
### Concepto de índice
- *Índice denso:* hay una entrada de índice por cada dato.
- *Índice no denso:* hay solo entradas de índice para un subconjunto de claves (los datos deben estar parcialmente ordenados por la clave).
- *Índice primario:* se utiliza la clave primaria del dato.
- *Índice de agrupamiento:* se utiliza un campo de ordenación del dato.
- *Índice secundario:* se utiliza cualquier otro campo.
- *Índice multinivel:* si todavía el índice es muy grande se puede hacer un índice sobre el índice. Esto aumenta la eficiencia de la búsqueda, pero complica la gestión.
### Multilistas
`	`Conjunto de nodos en que algunos tienen más de un puntero y pueden estar en más de una lista simultáneamente. Para casa tipo de nodo es importante distinguir los distintos campos punteros para realizar los recorridos adecuados y evitar confusiones. Es la estructura básica para sistemas de bases de datos en red. El método de búsqueda permite acceder a la información de manera ordenada a través de campos claves. Las Multilistas permiten llegar a un registro por diferentes caminos. El camino lo determina el campo clave sobre el cual se haga la búsqueda. En general las multilistas son recomendables cuando la búsqueda se hace sobre un solo atributo. En el caso de necesitarse una combinación de atributos es preferible usar listas invertidas.

`	`*Entidad:* representa una “cosa”, “objeto” o “concepto” del mundo real con existencia independiente. Una entidad está descrita y se representa por sus características o atributos.

`	`*Relación:* es una asociación o relación matemática entre varias entidades. Poseen una cardinalidad (uno a uno, uno a varios, varios a uno o varios a varios).

`	`Para su implementación se requiere al menos una estructura para la entidad A, una para la entidad B, una estructura para la relación A-B y una para la multilista que los engloba. Para su implementación en un archivo se requiere al menos un archivo cabecera que almacena las direcciones de inicio de cada cadena de característica, también es recomendable que incluya un campo con la longitud de cadena para seleccionar el acceso de la cadena más corta cuando se conocen varias características y tendrá tantos registros como características tenga el modelo. También se necesita el archivo principal donde se almacenan los datos y los enlaces entre ellos.
### Índices invertidos
`	`Estructura de datos de índice de una asignación de contenido, como palabras o números, a sus localizaciones en un archivo de base de datos o en un documento o conjunto de documentos. Permite rápidas búsquedas de texto completo a un buen costo de procesamiento cuando un documento se agrega a la base de datos. Es la estructura de datos más popular en sistemas de recuperación de documentos.

`	`Hay dos variantes principales, a nivel índice de archivo invertido (o simplemente archivo invertido) que contiene una lista de referencias a los documentos de cada palabra y índice completo invertido (o lista invertida) que además contiene las posiciones de cada palabra dentro de un documento.
### Índices secundarios
`	`Es un índice para claves que no sean primarias, o sea una clave para más de un registro, estos son llamados índices secundarios. En los índices primarios, el direccionamiento puede ser real (posición exacta en el disco) o relativo (en función de la posición del fichero). En los índices secundarios, el direccionamiento es simbólico (la clave proporciona la clave primaria del registro, y no su dirección ni física ni relativa). En definitiva, emplea punteros indirectos (Clave secundaria -> clave primaria). Con este direccionamiento se puede cambiar la posición física de un registro sin necesitar regenerar los índices.
### Archivos invertidos
`	`A partir de un dato (clave secundaria) se obtiene una clave primaria que lleva a más datos (también se puede poner una referencia directa al dato). Hay dos tipos: totalmente invertidos (se obtienen todas las claves relacionadas) y parcialmente invertidos (solo se obtiene la primera de ellas). La información del índice no tiene porque estar en el dato.
## Organización de archivos secuenciales indexados
El índice se puede organizar de diversas formas, las más típicas son: secuencial, multinivel y árbol. Podremos procesar un fichero de forma secuencial o de forma directa según la clave de indexación, y esto independientemente de cómo esté organizado el fichero por sí mismo Se pueden tener tantos índices como se quiera variando la clave que se emplee. El índice está formado por registros que contienen: clave de organización -> puntero(s) al fichero de datos.  Toda la información está en un conjunto encadenado de bloques (conjunto secuencia) y el árbol de acceso (árbol B) está formado con copia de las llaves que actúan como separadores (conjunto índice).
# Árboles
`	`Los árboles representan estructuras no lineales (porque a cada elemento del árbol puede seguirle varios elementos) y dinámicas (puesto que la estructura del árbol puede variar durante la ejecución del programa). Un árbol es una estructura jerárquica aplicada sobre una colección de elementos u objetos llamados nodos; uno de los cuales se denomina raíz.
## Características
- Todo árbol que no es vacío tiene un único nodo raíz.
- Si un nodo X es descendiente directo de un nodo Y decimos que X es hijo de Y.
- Si un nodo X es antecesor directo de un nodo Y decimos que X es padre de Y.
- Todos los nodos de un mismo padre son hermanos.
- Todo nodo que no tiene hijos es un nodo terminal.
- Todo nodo que no es raíz ni terminal es un nodo interior.
- Grado es el número de descendientes directos de un determinado nodo.
- Grado de un árbol es el máximo grado de todos los nodos del árbol.
- Nivel es el número de nodos que deben ser recorridos como mínimo para llegar a un determinado nodo (desde la raíz).
- Altura de árbol es el máximo número de niveles entre todas las ramas del árbol más 1.
## Recorridos
### En profundidad
- Preorden: primero la raíz, luego preorden subárbol izquierdo y finalmente preorden subárbol derecho.
- Postorden: primero postorden subárbol izquierdo, luego postorden subárbol derecho y finalmente la raíz.
- Inorden: primero inorden subárbol izquierdo, luego la raíz y finalmente inorden subárbol derecho.
### En anchura
- Por niveles: se etiquetan los nodos según su profundidad. Se recorren ordenados de menor a mayor nivel, igualdad de nivel se recorren de izquierda a derecha.
## Árboles degenerados
`	`Son árboles donde cada nodo tiene un solo hijo motivo por el cual se comporta como una lista, motivo por el cual pierde la eficiencia que tienen los árboles respecto de las listas.
## Árbol binario
`	`Los árboles binarios son árboles de grado 2, un árbol donde cada nodo puede tener como máximo 2 subárboles, siendo necesario distinguir entre el subárbol derecho y el subárbol izquierdo.

`	`*Árboles distintos*:  son distintos cuando sus estructuras son diferentes.

`	`*Árboles similares:* son similares cuando sus estructuras son idénticas pero la información que contienen los nodos difiere entre sí.

`	`*Árboles equivalentes:* son equivalentes cuando son similares y además los nodos contienen la misma información.

`	`*Árbol estricto:* si un subárbol está vacío el otro también. Cada nodo puede tener 0 o 2 hijos.

`	`*Árbol lleno:* árbol estricto donde en cada nodo la altura del subárbol izquierdo es igual a la del subárbol derecho y ambos subárboles son árboles llenos.

`	`*Árbol completo:* árbol lleno hasta el penúltimo nivel. En el último nivel los nodos están agrupados a la izquierda.
### Montículo binario
`	`Es un árbol binario completo cuyos nodos almacenan elementos comparables mediante ≤ y donde todo nodo cumple la propiedad del montículo (para un montículo de mínimos: todo nodo es menor que sus descendientes).

`	`Si un solo elemento no cumple la propiedad del montículo es posible reestablecerla mediante ascensos sucesivos en el árbol (intercambiándose con su padre) o mediante descensos sucesivos (intercambiándose con el menor de sus hijos). Para insertar un nuevo nodo se sitúa al final y se asciende hasta que cumpla con la propiedad. Para eliminar la raíz se intercambia con el último elemento y este se desciende hasta que cumpla la propiedad. Para la búsqueda se comporta como un vector desordenado.

`	`Un montículo es una estructura muy útil para representar una cola de prioridad.
### Árbol binario de búsqueda (BB)
`	`Un árbol binario con raíz R es de búsqueda cuando no es vacío, si tiene un subárbol izquierdo, la raíz del subárbol izquierdo es menor a R y a la vez el subárbol izquierdo también es de búsqueda y si tiene un subárbol derecho, la raíz del subárbol derecho es mayor a R y a la vez el subárbol derecho también es de búsqueda. Tiene la propiedad que todo nodo es mayor que los nodos de su subárbol izquierdo y menor que los nodos de su subárbol derecho.  Para poder usar un árbol binario de búsqueda es necesario que los elementos que insertemos sean comparables.

Se define árbol equilibrado como aquél que garantiza que su altura es logarítmica respecto a la cantidad de elementos. El que un árbol BB esté equilibrado o no depende de la secuencia de inserciones.
### Árboles balanceados
`	`Un árbol balanceado intenta mantener la menor profundidad en sus dos subárboles. El balanceo o equilibrio de un árbol, hace que algunas operaciones sean más eficientes, sobre todo las búsquedas. Un árbol está balanceado cuando la longitud de la trayectoria más corta hacia una hoja no difiere de la longitud de la trayectoria más larga.
### Árboles AVL (Adelson-Velski & Landis)
`	`Un árbol AVL es un árbol binario de búsqueda (ABB) que tiene como característica que siempre está balanceado. Cuando se realiza una inserción o una eliminación, se comprueba si el árbol está desequilibrado y se realiza el balanceo. Todo árbol AVL tiene altura logarítmica (el árbol AVL con mayor desequilibro es el llamado árbol Fibonacci).

`	`Un árbol binario es un AVL si y sólo si cada uno de sus nodos tiene un factor de equilibrio (altura del subárbol derecho menos altura del subárbol izquierdo) de -1, 0 o 1.
### Problema de los árboles binarios
`	`El recorrido de árboles con programas recursivos resulta costoso ya que implica un gato adicional de memoria y tiempo de ejecución. Los árboles binarios suelen tener muchos punteros en NULL. Si un árbol tiene n nodos, existen 2n enlaces, donde n+1 son enlaces vacíos.
## Árboles (a, b)
`	`Los árboles (a, b) son árboles generales donde cada nodo interno puede tener un número de hijos *m+1* en el rango [a, b]. Cada nodo almacena *m* claves (elementos comparables por ≤), ordenadas de menor a mayor que sirven para que se pueda usar como árbol de búsqueda.
## Árboles B
[[B Tree]]
`	`Los sistemas de almacenamiento masivo suelen tener un tiempo de acceso mucho mayor que el tiempo de transferencia: la localización de un elemento es mucho más costosa que la lectura secuencial de datos, una vez localizados. Esto supone un problema para estructuras enlazadas, como los árboles AVL, donde las operaciones acceden a bastantes nodos de pequeño tamaño. Para grandes volúmenes se datos, sería conveniente reducir el número de accesos, a cambio de que esos accesos contuvieran elementos de mayor tamaño.

`	`Un árbol B de orden d es un árbol (d+1, 2d+1) con las propiedades adicionales siguientes:

- La raíz puede tener cualquier número de claves.
- Todas las hojas se encuentran a la misma profundidad *h*.

La segunda propiedad garantiza que un árbol B es un árbol equilibrado: su altura es logarítmica respecto al número de claves almacenadas.
### Operaciones
- Si un nodo supera el número máximo de claves (2d), el nodo se divide, transfiriendo su clave en posición media al padre.
- Si un nodo queda por debajo del número mínimo de claves (d-1):
  - Se intenta una transferencia con el hermano izquierdo o derecho, el que contenga más claves.
  - Si no es posible (ambos tienen d hijos o no existen), se produce una fusión con el hermano izquierdo (o derecho si no existe). La fusión toma un elemento del padre por lo que éste a su vez puede necesitar transferencias o fusiones (y así con los ascendientes).
## Árboles B+
`	`Sólo las hojas contienen elementos, los nodos internos contienen claves para dirigir la búsqueda (esas claves se encuentran también en los nodos hoja). Los nodos hoja forman una lista enlazada (simple o doble).

`	`Se utilizan en archivos secuenciales indexados, permiten una mejor recorrida por algún tipo de orden. Es un índice multinivel, dinámico, con un límite máximo y mínimo en el número de claves por nodo.
### Operaciones
`	`Las operaciones son idénticas al árbol B excepto que en la eliminación solo se eliminan los valores en las hojas, los de los nodos interiores permanecen. Cuando se inserta en un nodo hoja lleno este se divide en dos, pero ahora el primero contendrá d claves y el segundo d+1 y lo que subirá al padre será una copia de la clave central.
## Árboles B\*
En un árbol B\* de orden d

- Cada nodo tiene un máximo de 2d+1 descendientes y un mínimo de 2d+1.23 .
- Cada nodo excepto la raíz tiene al menos 2d.23 claves y no más de 2d.
- La raíz tiene al menos dos descendientes (a menos que sea hoja).
### Operaciones
- Si un nodo cae por debajo del límite inferior:
  - Se intenta trasladar nodos de sus hermanos (del que tenga más nodos primero intentando con sus hermanos adyacentes).
  - Si no se puede se fusionan 3 hermanos en 2.
- Si un nodo supera el límite superior:
  - Se intenta trasladar nodos a sus hermanos (al que tenga menos nodos primero intentando con sus hermanos adyacentes).
  - Si no se puede se dividen 2 hermanos en 3.
## Árboles hilvanados
`	`Un árbol hilvanado es un árbol binario en el que cada hijo izquierdo de valor nulo es sustituido por un enlace o hilván al nodo que le antecede en orden simétrico (inorden) (excepto el primer nodo en orden simétrico) y cada hijo derecho de valor nulo es sustituido por un enlace o hilván al nodo que le sigue en el recorrido en orden simétrico (excepto el último nodo en orden simétrico). Cada nodo del árbol hilvanado contiene una referencia a su información, un apuntador a su hijo izquierdo, un indicador izquierdo (indica si tiene un hijo izquierdo), un apuntador a su hijo derecho y un indicador derecho (indica si tiene un hijo derecho).
# Motores de búsqueda
`	`Es un sistema que construye un índice a partir de texto y responde a consultas utilizando este índice. Utilizan índices invertidos. El archivo invertido se crea siguiendo cuatro pasos principales: parseo, ordenamiento, agrupamiento, y generación del diccionario y posting.

1. Parseo: a cada documento se le extrae los términos y un id documento.
1. Ordenamiento: se ordena al archivo creado por términos manteniendo los duplicados.
1. Agrupamiento: corte de control por término y documento.
1. Diccionario y posting: generación de ambos archivos. El diccionario (archivo inverso con índice no denso) agrupa por término, informa frecuencia total y direcciona al posting. El posting (archivo con lista inversa) direcciona a los documentos, informa la frecuencia y contiene listas enlazadas.

Existen distintas variantes de búsqueda:

- Modelo booleano: indica si un documento dado contiene o no a un término.
- Modelo vectorial: relaciona un conjunto dado de documentos (D) con el conjunto de todos los términos relevantes del conjunto D (T). A diferencia del modelo booleano este si informa la frecuencia.
- Frases y términos: para cada término se debe tener la lista de posiciones donde aparece en el documento.
## Consulta con patrones
`	`Hay varias alternativas:

- Fuerza bruta: recorrido secuencial del léxico.
- Índice secundario de n-gramas: por cada término que se agrega al índice invertido, se indexan en el secundario todos sus n-gramas.
- Índice secundario de léxico rotado: por cada término que se agrega al índice invertido, se agregan al secundario todas sus rotaciones.

Los índices secundarios permiten buscar en el invertido todos los términos que cumplan con el patrón de búsqueda.

*Distancia de edición de Levenshtein:* Número mínimo de operaciones requeridas para transformar una cadena de caracteres en otra.
# File systems
> `	`*“El conjunto de programas del sistema operativo encargados de proveer la visión lógica de la información almacenada a usuarios y programas conforman el Sistema de Archivo.”*

“ Un archivo me permite estructurar datos, un sistema de archivo me permite estructurar archivos”

Es el que indica como se organiza la información dentro de los medios físicos. Sus funciones son el guardado y recuperación de la información; la administración del espacio libre y el guardado de los atributos de seguridad del sistema operativo. Estos programas se encargan de:

- Identificar y localizar archivos.
- Seguridad.
- Asignación de espacio.
- Coordinación de transferencia (sistema multiusuario).

Los sistemas de archivos pueden ser clasificados por medio, de red y de propósito especial.

- Discos de plato magnético o Flash (acceso aleatorio): FAT, NTFS, HFS+, UFS, EXT2/3/4, XFS, BRTFS, Veritas File system, ZFS, ReiserFS
- Discos Ópticos: ISO9660, UDF
- Flash file System (Especialmente embebidos): JFFS, UBIFS, LogFS, F2FS, SquashFS
- Network File System: NFS, AFS (Sistema de compartición de Apple), SMB (Sistema de compartición de Microsoft), FTP, Webdav, SSHFS.
- Sistemas de archivos en Cluster: 
  - Shared-disk / storage area network: GFS2 (Red hat), GPFS (IBM), CSV (Microsoft), OCFS (Oracle)
  - Distributed file systems: GFS (Google), HDFS (Apache), Ceph (Red Hat), DFS (Microsoft), GlusterFS (Red Hat)
- Especiales:
  - procfs --> Mapeo de procesos y estructuras en Linux
  - configfs y sysfs --> Muestra como archivos los parámetros de consulta y configuración de un Linux
  - devfs --> los archivos en este FS representan a dispositivos. Y permite utilizar las primitivas de cualquier FS para acceder al dispositivo.
  - Superpuestos --> overlayFS, UnionFS, aufs
## Aspectos a evaluar en un sistema de archivos
- Manejo de espacio.
  - Manejo de nombres de los objetos (directorio y archivos).
  - La estructura de directorios utilizados.
  - Metadata que se le puede asociar a los objetos (directorio y archivos).
- Utilidades: creación, chequeos, defrag, tunning, resize, undelete, etc.
- Mecanismos de permisos y restricción.
  - ACL
  - Capacidades
- Integridad de la información
- Limitaciones impuestas por diseño.
- Extras
  - Encriptación a nivel archivo o directorio.
  - Compresión a nivel archivo o directorio
  - Deduplicación (el problema principal es que si se rompe la información se rompe para todas sus referencias)
## FAT
El sistema de archivos FAT se compone de cuatro secciones:

- **El sector de arranque.**

Siempre es el primer sector de la partición (volumen) e incluye información básica, punteros a las demás secciones y la dirección de la rutina de arranque del sistema operativo.

- **La región FAT.**

Contiene dos copias de la tabla de asignación de archivos (por motivos de seguridad). Estos son mapas de la partición, indicando que clusters están ocupados por los archivos.

- **La región del directorio raíz.**

Es el índice principal de carpetas y archivos.

- **La región de datos.**

Es el lugar donde se almacena el contenido de archivos y carpetas. Por tanto, ocupa casi toda la partición. El tamaño de cualquier archivo o carpeta puede ser ampliado siempre que queden suficientes clusters libres. Cada cluster está enlazado con el siguiente mediante un puntero. Si un determinado cluster no se ocupa por completo su espacio remanente se desperdicia.
### Tabla de asignación (región FAT)
`	`La tabla de asignación de archivos consta de una lista de entradas. Cada entrada contiene información sobre un clúster:

- La dirección del siguiente cluster en la cadena.
- Si es pertinente, la indicación de “fin de archivo” (que también es el fin de la cadena).
- Un carácter especial para indicar que el cluster es defectuoso.
- Un carácter especial para indicar que el cluster está reservado (es decir, ocupado por un archivo).
- El número cero para indicar que el cluster está libre (puede ser usado).
- El tamaño de estas entradas también depende de la variante FAT en uso: FAT16 usa entradas de 16 bits, FAT32 usa entradas de 32 bits, etc.
### Directorio Raíz
`	`Este índice es un tipo especial de archivo que almacena las subcarpetas y archivos que componen cada carpeta. Cada entrada del directorio contiene el nombre del archivo o carpeta (máximo 8 caracteres), su extensión (máximo 3 caracteres), sus atributos (archivo, carpeta, oculto, del sistema, o volumen), la fecha y hora de creación, la dirección del primer cluster donde están los datos y por último, el tamaño que ocupa.

`	`El directorio raíz ocupa una posición concreta en el sistema de archivos, pero los índices de otras carpetas ocupan la zona de datos como cualquier otro archivo. Los nombres largos se almacenan ocupando varias entradas en el índice para el mismo archivo o carpeta.
## Sistemas de archivos UNIX (Ext2/3/4)
El superbloque tiene información del sistema de archivos en conjunto, como su tamaño (la información precisa aquí depende del sistema de archivos). Un nodo-i tiene toda la información de un archivo, salvo su nombre. El nombre se almacena en el directorio, junto con el número de nodo-i. Una entrada de directorio consiste en un nombre de archivo y el número de nodo-i que representa el archivo.

El nodo-i contiene los números de varios bloques de datos, que se utilizan para almacenar los datos en el archivo. Sólo hay espacio para unos pocos números de **bloques de datos** en el nodo-i; en cualquier caso, si se necesitan más, se colocan más espacios para punteros a los bloques de forma dinámica. Estos bloques colocados dinámicamente son **bloques indirectos**; el nombre indica que, para encontrar el bloque de datos, primero hay que encontrar su número en un bloque indirecto.

- **Superblock:**  contiene toda la información de la configuración del sistema de archivo. Contiene información del total de nodos-i (inodos) y bloques del sistema de archivos y cuántos están libres, cuándo fue montado, etc.
- **Inode:** cada archivo está representado por una estructura llamado un inode. Cada inode contiene la descripción del fichero, tipo de archivo, los derechos de acceso, marcas de tiempo, el tamaño y los punteros a los bloques de datos. El **bloque de indirección** es un inode que se usa para apuntar a otros inodos cuando la cantidad de inodos se acaba.
- **Directorios:** los directorios se estructuran en un árbol jerárquico. Cada directorio puede contener archivos o directorios. Los directorios son un tipo especial de archivos.
- **Enlaces:** los sistemas de archivos UNIX implementan el concepto de enlace. Varios nombres se pueden asociar con un inode. El inode contiene un campo que contiene el número asociado con el archivo.
- **Archivos especiales de dispositivo:** en los sistemas operativos tipo UNIX, los dispositivos pueden acceder a través de ficheros especiales. Un archivo especial de dispositivo no utiliza ningún espacio en el sistema de ficheros. Es sólo un punto de acceso al controlador de dispositivo. (Existen dos tipos de archivos especiales: character/block special files. La primera permite operaciones I/O en modo caracteres mientras que el segundo requiere datos a escribir en modo bloque a través de las funciones de caché del buffer. Cuando una solicitud de I/O se realiza en un archivo especial, se envía a un (pseudo) controlador de dispositivo. Un archivo especial hace referencia a un número importante, que identifica el tipo de dispositivo y un número que identifica la unidad.
### Fuentes
- <https://ext4.wiki.kernel.org/index.php/Ext4_Disk_Layout>
- <http://web.mit.edu/tytso/www/linux/ext2intro.html>
- <http://www.nongnu.org/ext2-doc/ext2.html#DEFINITIONS>
- <http://upload.wikimedia.org/wikipedia/commons/a/a2/Ext2-inode.gif>
- <http://cs.smith.edu/~nhowe/262/oldlabs/img/ext2.png>
- <https://www.cs.cmu.edu/~mihaib/fs/fs.html>
## NTFS
Organización de volumen NTFS, se tiene cuatro estructuras básicas:

- NTFS Boot Sector: almacena información sobre el diseño del volumen, las estructuras del sistema de archivos y en algunos Windows server el código de arranque.
- Master file table (MTF): contiene la información necesaria para recuperar los archivos de la partición NTFS, como los atributos de un archivo.
- File system data: almacena los datos que no se encuentran dentro de la MTF.
- Master file table copy: copia del MFT.

[Estructura NTFS](https://technet.microsoft.com/en-us/library/cc781134\(WS.10\).aspx)

`	`MFT (Metadata File Table):

- Habrá una file o record (entrada en la tabla) por cada archivo que exista en el sistema de archivos.
- Ahora bien, el concepto de archivo es bastante amplio: toda entidad almacenada individualmente es un archivo. La propia MFT es considerada un archivo y tiene su propia entrada en la MFT.
- Las primeras 16 entradas de la MFT están reservadas para almacenar archivos del sistema, es decir, información sobre el propio sistema de archivos. El resto de entradas se corresponden con los archivos y carpetas de datos.

Fuentes

- <http://ftp.kolibrios.org/users/Asper/docs/NTFS/ntfsdoc.html>
- <https://technet.microsoft.com/en-us/library/cc781134%28v=ws.10%29.aspx>
- <http://www.tuxera.com/community/ntfs-3g-manual/>
## VFS
`	`Es una capa virtual que sirve de capa de abstracción del sistema de archivo real. Esta capa es la que utiliza el usuario para acceder al sistema de archivo real. Esta capa permite controlar y/o manejar de la misma manera un sistema de archivo local como un sistema de archivo de red. El primer mecanismo de sistema de archivo virtual en un sistema UNIX fue introducido en el SunOS de 1985. Esto permitía acceder a su sistema de archivo local llamado UFS como acceder a sistemas remotos NFS de forma transparente.

`	`Podría decirse que el servicio más importante que la capa VFS ofrece es una caché de datos I/O uniforme. Linux mantiene cuatro cachés de datos de I/O: page cache, inode cache, buffer cache y directory cache. El page cache combina datos de la memoria y archivos virtuales. El buffer cache es una interfaz con el dispositivo de bloques y cachea los meta-datos de discos de bloques. El inode cache mantiene el acceso reciente a los inodos de archivo. El directory cache (d-cache) mantiene en la memoria de un árbol que representa una parte de la estructura de directorios del sistema de archivos. 

La estructura de VFS de Linux se parece a la estructura de ext2.
### VFS Superblock
`	`Todo sistema de archivo montado está representado por el VFS superblock. El VFS contiene:

- Device: este es el identificador de dispositivo. Por ejemplo, ‘/dev/sda1’.
- Inode pointers: apunta al primer inode del sistema de archivo. El puntero de inode cubierto representa al inode del directorio donde está montado dentro del sistema. Si es el root file system no tiene puntero cubierto (covered pointer).
- Blocksize: es el tamaño de bloque en el sistema de archivo.
- Superblock operations: apunta a el grupo de rutinas del superbloque. Entre otras cosas estas rutinas son las que permite la lectura y escritura de inodos y superbloques.
- File system type: es el puntero a los datos de estructura del tipo de sistema de archivo.
- File system specific: es el puntero a la información necesaria para este sistema de archivos.
### VFS Inode
`	`Como el sistema de archivos ext2, todo archivo, directorio y otro es representado por algún VFS inode. La información de cada inode VFS es construida desde la información extraída del sistema de archivo mediante rutinas específicas. Cada VFS inode existe solo en memoria del sistema y es mantenida dentro del inode cache. VFS inode contiene los siguientes datos:

- Device: es el identificador de dispositivo donde se encuentra el inode real.
- Inode number: Es un número único de inode dentro del sistema de archivo. Es una combinación entre el dispositivo y el número de inode.
- Mode: como el ext2 este campo describe los permisos al inode.
- Times: de creación, modificación y de escritura.
- Blocksize: tamaño de bloques.
- Inode operations: es un puntero a las direcciones de los procedimientos de inode.
- Count: es el número de componentes de sistema que están usando este inode. Cuando la suma llega a cero puede ser descartado o reusado.
- Lock: este campo es usado cuando el inode es lockeado cuando es usado por el sistema.
- Dirty: indica si el inode VFS ha sido escrito y el sistema de archivo por debajo necesita modificado.
### Registro de sistema de archivos
En Linux todo nuevo sistema de archivo debe ser registrado. Los sistemas de archivos pueden ser creados como módulos y cargados bajo demanda. Cuando son cargados el kernel registra el sistema de archivo. Uno puede ver si el archivo está registrado haciendo un cat al archivo /proc/filesystems.
### Bibliografía
- <http://www.ibm.com/developerworks/library/l-fuse/>
- <http://www.tldp.org/LDP/tlk/fs/filesystem.html>
- <http://www.tldp.org/LDP/khg/HyperNews/get/fs/vfstour.html>
- <https://kaiwantech.files.wordpress.com/2009/08/vfs_msdos_31.png>
- <http://www.inf.fu-berlin.de/lehre/SS01/OS/Lectures/Lecture16.pdf>
- The Linux VFS, Chapter 4 of Linux File Systems by Moshe Bar (McGraw-Hill, 2001). ISBN 0-07-212955-7
- Chapter 12 of Understanding the Linux Kernel by Daniel P. Bovet, Marco Cesati (O'Reilly Media, 2005). ISBN 0-596-00565-2
## FUSE
`	`FUSE permite implementar un Sistema de archivo funcional en le espacio de usuario de programas. Las características que incluyen son:

- Una librería simple.
- El módulo está incorporado al kernel.
- Correr el sistema de archivo en “userspace”, esto implica que no necesita ser usuario privilegiado.
- Corre en Linux 2.4.X en adelante.
- Ha probado ser estable.

FUSE fue desarrollado para soportar el sistema de archivo AVFS, posteriormente se convirtió en un proyecto aparte.
### Bibliografía
- <http://fuse.sourceforge.net/>
- <http://fuse.sourceforge.net/doxygen/null_8c.html>
- <https://code.google.com/p/pngdrive/>
- <http://www.buanzo.com.ar/lin/FUSE.html>
# XML
`	`XML es un subconjunto de SGML (Standard Generalised Mark-up Language), simplificado y adaptado a internet. XML es un meta-lenguaje que nos permite definir lenguajes de marcado adecuados a usos determinados. XML es el lenguaje sobre el cual está construido HTML. XML no es un lenguaje para hacer páginas web.

`	`XML sirve para representar información estructurada en la web (todos documentos), de modo que esta información pueda ser almacenada, transmitida, procesada, visualizada e impresa, por diversos tipos de aplicaciones y dispositivos.
## Características
- XML es un subconjunto de SGML que incorpora las tres características más importantes de este:
  - Extensibilidad
  - Estructura
  - Validación
- Basado en texto.
- Orientado a los contenidos no a la presentación.
- Las etiquetas se definen para crear los documentos, no tienen un significado preestablecido.
## Ventajas del XML
1. Es fácilmente procesable.
1. Separa radicalmente el contenido y el formato de presentación.
1. Diseñado para cualquier lenguaje y alfabeto.
## Estructura de un documento XML
`	`Un documento está formado por datos y marcas. Las marcas son las etiquetas. Dentro del documentos existen dos partes:

- Prólogo: indica los datos de la versión y encoding del documento junto con datos otros datos generales.
- Cuerpo: contiene la información a transmitir.

En un documento XML existen los siguientes componentes:

1. Elementos: pieza lógica del marcado, se representa con una cadena de texto (dato) encerrada entre etiquetas. Pueden existir elementos vacíos (<br/>). Los elementos pueden contener atributos.
1. Instrucciones: ordenes especiales para ser utilizadas por la aplicación que procesa: 		<?xml-stylesheet type=”text/css” href =” estilo.css” >
1. Las instrucciones XML: comienzan por <? y terminan por ?>.
1. Comentarios: información que no forma parte del documento. Comienzan por <!-- y terminan por -->.
1. Declaraciones de tipo: especifican información acerca del documento:		<!DOCTYPE persona SYSTEM “persona.dtd”>
1. Secciones CDATA: se trata de un conjunto de caracteres que no deben ser interpretados por el procesador:

<![CDATA[ aquí se puede meter cualquier carácter, como <, &, >, sin que sean interpretados como marcación]]>
## Árbol de análisis
`	`Estructura que muestra los objetos que forman el documento y las relaciones entre ellos. A los componentes de un documento se les llama “objetos” (elementos, comentarios y cadenas de texto). El propio documento es un objeto. A cada objeto del árbol se le denomina “nodo”. Al nodo principal que contiene a los demás se le llama nodo “raíz”. Cuando un nodo contiene a otro se le denomina “rama”. Los nodos finales, que no contienen a otros nodos, se llaman “hojas”.
## Sobre el diseño
`	`A la hora de diseñar se nos plantean dudas entre escoger atributo o elemento. Hay que tener en cuenta lo siguiente:

1. Los atributos no pueden contener subelementos ni subatributos.
1. Los atributos no se organizan en ninguna jerarquía por lo que la representación es mucho más reducida que los elementos.
1. La utilización de los atributos será una mera modificación de los elementos a los que se aplica, la información que deben de contener debe ser de poca entidad, sencilla y sin estructura.

Aun así, muchas veces llegamos a la misma conclusión utilizando atributos y elemento.
## Definición de reglas de construcción de XML
`	`Para definir y validar un XML se puede utilizar las DTD y/o los esquemas XML (XML Schema Definition o XSD).
### DTD (Document type data)
`	`Define los elementos, atributos, entidades y notaciones que pueden utilizarse para construir un tipo de documentos, así como las reglas para su utilización:

- Mediante ellas se comprueba la validez de un documento.
- Tienen su origen en SGML.
- Posee una sintaxis especializada.

Al definir el lenguaje XML ya nos referimos a la definición del tipo de documento que, en resumen, cumple con las siguientes funciones:

- Una DTD especifica la clase de documento
  - Describe un formato de datos.
  - Usa un formato común de datos entre aplicaciones.
  - Verifica los datos al intercambiarlos.
  - Verifica un mismo conjunto de datos.
- Una DTD describe
  - Elementos: cuáles son las etiquetas permitidas y cuál es el contenido de cada etiqueta.
  - Estructura: en qué orden van las etiquetas en el documento.
  - Anidamiento: qué etiquetas van dentro de cuáles.

Los elementos en una DTD son los siguientes:

- Elementos con “contenido ELEMENT”: Un elemento tiene contenido ELEMENT, si solo puede contener a otros elementos, opcionalmente separados por espacios en blanco.
- Elementos con “contenido TEXT”: Un elemento tiene contenido TEXT, si solo puede contener texto (PCDATA = printable character data).
- Elementos con “contenido MIXED”: Un elemento tiene contenido MIXED, si puede contener texto u otros elementos.
- Elementos con “contenido EMPTY”: Un elemento tiene contenido EMPTY, si no puede contener otros elementos.

Así pues, la DTD especifica la clase de documento XML. Una DTD indica sólo qué elementos, atributos, etc. tiene un documento y cómo se anidan, pero no dice nada acerca de tipos de dato. El único tipo de dato que conoce es PCDATA (texto plano), por tanto, las DTDs se quedan algo cortas y cuando se necesita algo más potente y rígido, se usa XSD.
### XML Schema Definition
`	`Tiene la misma finalidad que las DTDs, de hecho, es la evolución de la DTD descripta por la W3C. Describen los elementos y atributos que se pueden utilizar para construir documentos CML y las reglas de utilización. Permiten asociar tipos de datos con los elementos. Se crean utilizando la sintaxis XML.

`	`Surgen para dar respuesta a las limitaciones de las DTDs. Se basa en el vocabulario XML-Data que se utiliza para describir la estructura de los documentos. A la tecnología para la creación de esquemas se le conoce como XML Schema. IE 5.0 no realiza validación del documento a través del esquema.

Elementos:

- Schema: es el elemento raíz del documento, actúa como contenedor para el resto de los elementos. Contiene los atributos:
  - name: nombre del esquema
  - xmlns: espacio de nombres del esquema. Hace referencia a la DTD donde se definen los elementos del esquema. Su valor se establece a 		urn:schemas-microsoft-com:xml-data
- ElementType: define los tipos de elementos que se utilizarán para la elaboración de documentos que sigan el esquema. Contiene los atributos:
  - name: nombre del elemento
  - content: contenido del elemento:
    - eltOnly: solo puede contener elementos secundarios.
    - textOnly solo puede contener texto.
    - mixed: puede contener texto y elementos secundarios.
    - Empy: sin contenido.
  - order: orden y frecuencia del grupo de elementos secundarios del elemento:
    - one: solo se permite una serie de elementos.
    - seq: los elementos deben producirse en la secuencia especificada.
    - many: los elementos pueden aparecer las veces que sea en cualquier orden.
  - dt:type: establece el tipo de contenido del elemento.
- element: declara el modelo de contenido para un elemento. Dispone de los atributos:
  - type: tipo de elemento. Es el nombre con el que ha sido declarado ElementType.
  - minOcurrs: mínimo número de veces que el elemento puede aparecer. Su valor es 0 o 1.
  - maxOcurrs: máximo número de veces que el elemento puede aparecer. Puede ser 1 o \*.
- AttributeType: se utiliza para definir los tipos de atributos que van a ser utilizados en los elementos. Los atributos son:
  - name: nombre del atributo.
  - dt:types: tipo de datos del atributo.
  - dt:values: lista posible de valores de un atributo enumerado. Aplica dt:type a enumeration.
  - default: valor predeterminado.
  - required: indica si el atributo es o no obligatorio. Su valor es yes o no.
  - type: nombre del atributo.
  - default: valorpredeterminado.
  - required: si es o no obligatorio.
- attribute:se utiliza para declarar el modelo de contenido de un elemento. Sus atributos son:
  - type: nombre del atributo.
  - default: valor predeterminado.
  - required: si es o no obligatorio.

Los tipos de datos de XSD están definidos en el espacio de nombres urn:schema-microsoft-com:datatypes. Entre los tipos de datos más importantes están:

- char: carácter.
- string: cadena de caracteres.
- boolean: booleano 0 o 1.
- int: número entero.
- float: número real.
- date: fecha.
- time: hora.
- uri: identificador uniforme de recursos.
- enumeration: tipo enumerado, sólo válido para atributos.
- ID: atributo de tipo identificador.

Ejemplo:

<Schema xmlns="urn:schemas-microsoft-com:xml-data" xmlns:dt="urn:schemas-microsoft-com:datatypes">

<AttributeType name='id' dt:type='string' required='yes'/>

<ElementType name='nombre' content='textOnly'/>

<ElementType name='persona' content='mixed'>

<attribute type='id'/>

<element type='nombre'/>

</ElementType>

<ElementType name='documento' content='eltOnly'>

<element type='persona'/>

</ElementType>

</Schema>

Estándares relacionados con XML:

- [XPath](https://www.w3.org/TR/xpath20/): es un lenguaje de expresión que permite procesar valores conforme a los modelos de datos XML.
- [XPointer](https://www.w3.org/TR/xptr/) (the XML pointer language): permite armar hipervinculos que apuntan a partes específicas de fragmentos de documents XML.
- [XLink](https://www.w3.org/TR/xlink11/) (the XML linking language): define el método para crear links dentro de los documentos XML.
- [XSLT](https://www.w3.org/TR/xslt20/): permite las transformaciones de documentos CML a otros formatos como por ejemplo XHTML.
- [DOM](https://www.w3.org/TR/dom41/): define el estándar para acceder y manipular los documentos CML. El DOM presenta un documento XML como una estructura de árbol. El DOM es separado por la W3C en tres diferentes partes:
  - CORE DOM: define el modelo estándar para cualquier documento estructurado.
  - XML DOM: el modelo estándar para documentos XML.
  - HTML DOM: el modelo estándar para documentos HTML.
# JSON
`	`JSON (JavaScript Object Notation) es un formato ligero de intercambio de datos. Es una alternativo para el XML, es más simple ya que está construido por dos estructuras:

- Una colección de pares nombre/valor. En varios lenguajes esto es conocido como un objeto, registro, estructura, diccionario, tabla hash, lista de claves o un arreglo asociativo.
- Una lista ordenada de valores. En la mayoría de los lenguajes esto se implementa como arreglos, vectores, listas o secuencias.

Los tipos de dato de JSON son:

- **Objeto:** es un conjunto desordenados de pares nombre/valor. Comienza con llave de apertura y termina con llave de cierre. Cada nombre es seguido por dos puntos y los pares son separados por comas.
- **Arreglo:** es una colección de valores. El arreglo empieza con corchete y termina con el corchete de cierre. Los valores se separan por coma.
- **Valor:** un valor puede ser una cadena de caracteres con comillas dobles, un número, un boolean (true o false), un null, un objeto o un arreglo. Estas estructuras pueden anidarse.
# Compresión
`	`La idea fundamental es guardar la mayor cantidad de datos posibles en la menor cantidad de espacio posible y que dado el archivo comprimido pueda recuperarse el archivo original. Hay dos tipos principales de algoritmos de compresión, sin pérdida (lossless) y con pérdida (lossy). También se pueden clasificar según como procesan los datos de entrada como:

- Algoritmos estáticos: leen una vez el archivo para recolectar estadísticas y luego otra vez para comprimirlo.
- Algoritmos semi-estáticos: levantan en memoria un bloque del archivo, lo procesan en forma estática y luego graban el bloque comprimido. Solo hacen una lectura del archivo original pero cada bloque es procesado dos veces (en memoria).
- Algoritmos dinámicos: leen una vez el archivo de entrada y lo van comprimiendo a medida que lo leen.
## Compresión lossless
### Compresión RLE
`	`El método de compresión RLE (Run Length Encoding) es utilizado por muchos formatos de imagen (BMP, PCX, TIFF). Se basa en la repetición de elementos consecutivos. El principio fundamental consiste en codificar un primer elemento al dar el número de repeticiones de un valor y después el valor que va a repetirse. Para que la compresión RLE sea efectiva está regida por reglas particulares, estas son:

- Si se repiten tres o más elementos consecutivamente, se utiliza el método de compresión RLE.
- De lo contrario se inserta un carácter de control (/x00) seguido del número de elementos de la cadena no comprimida y después la última.
- Si el número de elementos de la cadena es extraño, se agrega el carácter de control (/x00) al final.
- Finalmente, se definen los caracteres de control específicos según el código.

Su principal ventaja radica en que RLE se puede usar aún cuando no se pueda analizar el texto o imagen completa a enviar.
### Compresión estadística
`	`Los compresores estadísticos conforman la columna vertebral de la compresión de datos. La idea básica es en base a las probabilidades de entrada reducir el tamaño esperado de la salida. El objetivo de la compresión estadística es en definitiva determinar cual deberá ser la longitud de los códigos correspondientes a los caracteres de un archivo, el valor de los códigos puede ser cualquiera siempre y cuando se respeten las longitudes.
#### *Huffman estático*
`	`Este algoritmo desarrollado por Huffman en 1952 es el más popular y utilizado de los compresores estadísticos. El método es:

1. Armar Histograma
1. Agrupar de a dos caracteres siempre que su frecuencia de aparición sea menor a todos y se arma un nuevo símbolo, con la frecuencia de aparición de los dos anteriores.
1. Repetir el punto dos hasta que quede un árbol binario donde el nodo principal tenga cadena con todos los caracteres.

El descompresor deberá primero recuperar el árbol y luego ir descomprimiendo.
## Compresión lossy
`	`La compresión con pérdida es una necesidad al empezar a tratar con contenido audiovisual. Sin este tipo de compresión la transmisión de este tipo de contenido (en particular videos) sería terriblemente costosa.
# Seguridad Informática
`	`La seguridad es una característica o cualidad que implica que un sistema este libre de peligro, daño o riesgo. La seguridad es una utopía, una característica inalcanzable, una tendencia. La fiabilidad es la probabilidad que un sistema actúe de acuerdo a lo esperado. Fundamentalmente cuando hablamos de seguridad informática lo que **queremos proteger es la información**.

`	`Los tipos de ataques posibles son:

1) **Interrupción:** que un objeto del sistema se pierda, se torne inutilizable o no esté disponible.
1) **Interceptación:** acceso no autorizado a la información en tránsito. Llamado *sniffing*, vulnera la privacidad de la información.
1) **Modificación:** consiste en interceptar y modificar la información. Llamado *spoofing*, vulnera la integridad de los datos.
1) **Fabricación:** consta de fabricar un objeto original. Vulnera la autenticidad.

Nos queremos proteger de:

- Personas:
  - Personal (accidentes por error o desconocimiento)
  - Exempleados
  - Atacantes no destructivos (curiosos)
  - Crackers (scanners, exploits)
  - Terroristas (ataques a DB, WEBS)
  - Intrusos remunerados (pagados por otras empresas)
- Amenazas lógicas:
  - Software incorrecto (bugs)
  - Herramientas de seguridad (Nessus, SATAN, etc.)
  - Backdoors
  - Bombas lógicas
  - Canales cubiertos
  - Virus
  - Worms
  - Troyanos
  - Programas conejo o bacteria
  - Técnicas Salami
- Catástrofes:
  - Naturales (Entorno geográfico)
  - Artificiales (Infraestructura)

Para protegernos hay 5 pasos:

- Prevención.
- Detección.
- Recuperación.
- Análisis forense.
# Criptología
`	`La criptología estudia los problemas teóricos en la seguridad en el intercambio de mensajes. Tiene dos ramas, la criptografía (el arte de escribir mensajes secretos) y el criptoanálisis (el arte de descifrar mensajes secretos).
## Criptosistemas
`	`Se define a un criptosistema como la quíntupla (M, C, K, E, D), donde:

- M representa el conjunto de todos los mensajes sin cifrar (lo que se denomina texto plano o plain text) que pueden ser enviados.
- C representa el conjunto de todos los posibles mensajes cifrados (o criptogramas).
- K representa el conjunto de claves que se pueden emplear en el criptosistema.
- E es el conjunto de transformaciones de cifrado o familia de funciones que se aplica a cada elemento de M para obtener un elemento de C. Existe una transformación diferente Ek para cada valor posible de la clave k.
- D es el conjunto de transformaciones de descifrado, análogo a E.
### Criptosistemas de clave simétrica o privada
`	`**Emplean la misma clave k tanto para cifrar como para descifrar.** El problema es que para ser empleados en comunicaciones la clave k debe estar tanto en el emisor como en el receptor.
### Criptosistemas de clave asimétrica o pública
`	`**Emplean una doble clave (kp, kP)**.

kp se conoce como clave privada y sirve para la transformación de descifrado (D).

Kp se conoce como clave pública y sirve para la transformación de cifrado (E).

Estos criptosistemas deben cumplir además que el conocimiento de la clave pública no permita calcular la clave privada. Pueden emplearse para establecer comunicaciones seguras por canales inseguros.
## Esteganografía
`	`Consiste en ocultar en el interior de una información, aparentemente inocua, otro tipo de información (cifrada o no). Permite burlar diferentes sistemas de control y encubrir mensajes cifrados. La técnica se conoce como *chaffing and winnowing*, que se traduciría como separar la paja del trigo.
## Criptoanálisis
`	`La idea es comprometer la seguridad de un criptosistema. Se puede hacer de dos formas, descifrando el mensaje sin conocer la llave, o bien obteniendo a partir de uno o más criptogramas la clave que ha sido empleada en su codificación. No es criptoanálisis el descubrimiento de un algoritmo secreto de cifrado, suponemos, por el contrario, que **los algoritmos son siempre conocidos.**
## Criptosistemas específicos
### El cuadrado de Polibio
`	`Es un algoritmo trivial donde cada letra del alfabeto es reemplazada por las coordenadas de su posición en un cuadrado. El cuadrado básico es de 5x5 (agrupando i y j) y se puede extender a 6x6 para agregar cifras y signos de puntuación.
### Método de los confederados
`	`Es un tipo de sustitución poli alfabética. Básicamente, se escoge una clave, que se va “sumando” al texto llano para dar lugar al texto cifrado. Para sumar se suman los índices de las letras (A=1, B=1, etc.). Los espacios se pueden ignorar.
### Cifrados mono-alfabéticos
`	`Sin desordenar los símbolos dentro de un mensaje, establecen una correspondencia única para todos ellos en todo el texto.
#### *Cifrado de cesar*	
`	`Se establece una correspondencia de una letra a la otra según un salto fijo.
#### *Cifrado de cesar con salto y palabra*
`	`Consiste en utilizar un salto y una palabra clave. Para escribir el diccionario de destino primero se coloca una palabra elegida, sin repetir caracteres, y luego se completa el abecedario. Después de esto se efectúa un cifrado de Cesar común con el alfabeto de destino modificado.
### Cifrados poli-alfabéticos
`	`La sustitución aplicada a cada carácter varía en función de la posición que ocupe éste dentro del texto plano. 
#### *Sistema Vigénere*
`	`Matriz de 26x26 (a..z) desplazada de a 1 por fila. La clave es una palabra de K letras. Teniendo una frase a encriptar y la clave se toman los primeros caracteres de ambas palabras colocando la letra de la palabra para determinar la fila y la de la clave la columna. El carácter resultante va al criptograma, se avanza en ambas palabras. Al terminar la palabra clave se vuelve a su inicio.

`	`Esto es equivalente a sumar los índices letra por letra con los índices comenzando en 0.
### Cifrado de trasposición
`	`La idea es no sustituir unos símbolos por otros, sino que cambia su orden dentro del texto.
## Algoritmos simétricos de cifrado (criptografía moderna)
`	`La gran mayoría de los algoritmos de cifrado simétricos se apoyan en los conceptos de confusión y difusión inicialmente propuestos por Shannon. Para conseguir algoritmos fuertes sin necesidad de almacenar tablas enormes es intercalar confusión (sustituciones simples, con tablas pequeñas) y difusión (permutaciones). En muchos casos el criptosistema no es más que un paso simple de sustitución-permutación repetido n veces, como ocurre con DES (Data Encryption Standard).
## Algoritmos asimétricos de cifrado
`	`Constan de dos claves diferentes denominadas clave privada y clave pública. Una de ellas se emplea para codificar, mientras que la otra se usa para decodificar. Dependiendo de la aplicación que le demos al algoritmo la clave pública será la de cifrado o viceversa. En el caso de comunicación privada se cifra con la clave pública y en caso de autenticación se cifra con la clave privada.
### Autenticación
La segunda aplicación de los algoritmos asimétricos es la autentificación de mensajes con ayuda de funciones resumen. Las funciones resumen permiten obtener una firma a partir de un mensaje.
### El algoritmo RSA
`	`Llamado así por sus inventores Ron Rivest, Adi Shamir y Leonard Adleman. Se basa en la dificultad para factorizar grandes números.

- Encriptación: c = me (mod n)
- Decrepitación: m=cd (mod n)

Donde c: texto cifrado, m: mensaje, e: llave pública, d: llave privada, n = P\*Q (ya calculado)
### La propagación de la confianza
- Infraestructura de clave pública o PKI.
  - ` `Entidades emisoras de certificados (Autoridades de certificación o CA del inglés Certification Authority)
- Establecimiento de una red de confianza.
  - No hay nodos aparte de los usuarios.
  - Los usuarios recogen claves públicas de otros usuarios y aseguran su autenticidad.
- Criptografía basada en identidad.
  - PKG (acrónimo de Private Key Generator)
  - Hay un Generador que reparte las Caves Publicas y privada a quien corresponda.
- Criptografía basada en certificados.
  - En este modelo el usuario posee una clave privada y otra pública.
  - La clave pública la envía a una Autoridad de certificación que basándose en criptografía basada en identidad genera un certificado que asegura la validez de los datos.
- Criptografía sin certificados.
  - KGC (acrónimo de Key Generator Center) es una clave parcial.
  - La clave privada completa se genera a partir de la clave privada parcial y un valor generado aleatoriamente por el usuario
# Firma Digital
`	`El objetivo es poder enviar un documento firmado a través de medios electrónicos de manera que ese documento cuente, por lo menos, con las mismas características técnicas de seguridad y legales que tiene un documento firmado holográficamente.

`	`La firma digital es una solución tecnológica que permite autenticar el origen y verificar la integridad del contenido de un mensaje de tal manera que ambas características sean demostrables ante terceros. Es el resultado de aplicarle a un documento digital un procedimiento matemático que requiere información de exclusivo conocimiento del firmante, encontrándose ésta bajo su absoluto control. Debe ser susceptible de verificación por terceras partes, de manera tal que dicha verificación permita simultáneamente identificar al firmante y detectar cualquier alteración del documento digital posterior a su firma.

`	`Propiedades:

- **Autenticidad:** poder atribuir el documento únicamente a su autor de forma fidedigna, de manera de poder identificarlo.
- **Integridad:** estar vinculada a los datos del documento digital poniendo en evidencia su alteración luego de que fue firmado.
- **Exclusividad:** garantizar que la firma se encuentre bajo el absoluto y exclusivo control del firmante.
- **No repudio:** garantizar que el emisor no pueda negar o repudiar su autoría o existencia; ser susceptible de verificación ante terceros.
- **Validez:** haber sido producida con un certificado emitido por un Certificador Licenciado.
## Las firmas
`	`Se requiere:

- **Atribuir** el documento a su autor (una persona) en forma fehaciente (autenticar al autor).
- **Verificar** la no alteración del contenido del documento luego de que fue firmado (integridad del contenido).
- **Garantizar** el no repudio.
## Firma electrónica
`	`Se entiende por firma electrónica al conjunto de datos electrónicos integrados, ligados o asociados de manera lógica a otros datos electrónicos, utilizado por el signatario como su medio de identificación, que carezca de algunos de los requisitos legales para ser considerada una firma digital.

`	`Un documento firmado digitalmente que no tenga un certificado emitido por un certificador licenciado es una firma electrónica pero no es una firma digital.
## Ley N ° 25.506 de firma digital.
`	`Establece una infraestructura de firma digital nacional.

- Autoridad de aplicación: Ministerio de modernización.
- Certificadores licenciados: sistema de acreditación obligatorio.
- Firma digital: presunción de autoría e integridad, salvo prueba en contrario.
- Principio de equivalencia funcional.
- Firma electrónica: se invierte la carga probatoria.
- Despapelización del Estado.
- Neutralidad tecnológica.
- Reconocimiento de certificados extranjeros.
- Protección del suscriptor del certificado (quien firma).
## Certificado de clave pública
`	`Los certificados de clave pública son documentos digitales firmados digitalmente por una autoridad certificante que vinculan la clave pública de una persona a sus datos de identidad.
## Gobierno electrónico
`	`“el Gobierno Electrónico es el uso de las tecnologías de la información y de la comunicación, en los órganos de la Administración Pública, para mejorar la información y los servicios ofrecidos a los ciudadanos, orientar la eficacia y la eficiencia de la gestión pública e incrementar sustantivamente la transparencia del sector público y de la activa participación de los ciudadanos “	*(Carta Iberoamericana de Gobierno Electrónico)*



# Notas
`	`**Identificar cuellos de botella**

`	`**Hacer coincider sistema block size on physical block size**
## Sistemas de archivos
Estructuras de almacenamiento de datos en bloques

Hay Sistemas de archivo para cada contexto

Básicamente genera una visión lógica de toda la información almacenada y mapeandola a una estructura.

Los sistemas de archivo afectan en la performance por la burocracia

Seguridad: El sistema de archivos le indica al sistema op a que puede acceder un usuario o no.

FAT: 

Los nombres de archivos están en bloques directorios

dd if=/dev/zero of=mivfat.raw bs=4k count=1k fat=16

ls -l

ls -lh

mkf

mkfs.vfat mivfat.raw

mcview mivfat.raw

mkdir mnt

sudo mount mivfat.raw mnt -o loop

dd if=/dev/urandom of=archivo1.txt bs=512 count=2

dd if=/dev/urandom of=archivo2.txt bs=512 count=4

mkdir hola

dd if=/dev/urandom of=./hola/archivo.txt bs=512 count=4

EXT:

Los nombres de archivos están en bloques directorios

NTFS: todo es un archive excepto el bootsector

La MFT está compuesta por registros de 1k

1/12/20

La seguridad la buscamos

Para pensar en la seguridad primero pensar en una persona y luego trasladarlo al sistema que importa

intersepción: sniffing -> privacidad

modificación: spoofing -> integridad

fabricación -> autenticidad

firma digital, se hashea el mensaje y se encripta con ka clave priv

\*\*establecimiento de una red de confianza\*\*, no web

huella == digesto (hashing del documento)



10/12/2020

Tecnológicos: autenticidad, integridad

Exclusividad depende del ser humano

Validez: certificado -> tecnológico, autoridad certificada -> legal

Firma digital = firma electrónica + legales

Encriptar aumenta mucho el tamaño del documento

Si cifro un documento entero puede ser vulnerable al criptoanálisis.
