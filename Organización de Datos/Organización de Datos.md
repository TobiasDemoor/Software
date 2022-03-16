Técnicas de representación y almacenamiento de datos en archivos para su recuperación, resguardo y transmisión en formas eficientes y seguras.

*Tipo de Dato Abstracto (TDA):* Modelo formal de un ente junto con un conjunto de operaciones definidas sobre el modelo que nos permite procesarlo.

*Estructuras de datos:* Organización lógica de la información con que representamos los datos.
## Conceptos fundamentales
### Dato
Representación de una cosa real o ideal o de un evento ocurrido o programado para que ocurra, en una unidad lógica de manipulación llamada [[registro]], en términos de características descriptivas (atributos) que se representan en unidades llamadas campos.
### Archivo de Datos
Unidad lógica de almacenamiento permanente de registros, administrada por un [[Sistemas Operativos|sistema operativo]]. Dentro de un [[archivo]] los registros pueden organizarse en otras unidades lógicas llamadas bloques o páginas.
### Clasificación de archivos por función
- Archivos de datos maestros:
	Datos de un [[sistema de información]] que representan entidades de existencia real o ideal, por ejemplo, productos o servicios, o valores de referencia para determinar características o atributos de otros datos (dominios de atributos definidos por extensión).

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

Generalmente son archivos de texto, con alguna convención para rotular o delimitar datos, que pueden incluir o no definiciones sobre la estructura de la información contenida. (un estándar actual es el [[XML]]).

- Archivos de recursos de programa:
También conocidos como de Unidades Grandes de Información. (imágenes, audio, vídeo).

- Archivos de productos de programas:
Son archivos con tipo asociado a un [[programa]] o aplicación (.doc, .xls, etc.).

- Archivos de empaquetado de archivos:
Se utilizan para agrupar, normalmente en forma comprimida, archivos y directorios, con propósitos de trasmisión o respaldo (.zip, .rar, etc.).

### Clasificación de archivos por tipos de datos
- Texto
- Binarios
- Tipificados y sin tipo

### Clasificación de archivos por tipo de registros
- Registros de longitud fija
- Registros de longitud variable

### Clasificación de archivos por tipo de acceso
- Secuencial
- Directo
- Indexado
- Relativos
- Stream (flujo de datos)

### Sistema operativo
El [[Sistemas Operativos|sistema operativo]] es el responsable del manejo de recursos de una computadora. Los recursos pueden ser físicos (el hardware) o lógicos (carpetas y archivos).

Provee una interfaz controlada entre usuarios y aplicaciones, a nivel lógico, y dispositivos de almacenamiento secundario, a nivel físico.

#### Sistema de archivo
Los usuarios y programas tienen una visión lógica de la Información almacenada, y los dispositivos de almacenamiento tienen una visión física. El sistema operativo es el mediador.

El conjunto de programas del sistema operativo encargados de proveer la visión lógica de la información almacenada a usuarios y programas conforman: el [[Sistemas de archivos|sistema de archivo]].

#### Funciones de un sistema operativo
- Identificación y ubicación de archivos (Directorio Estructura Jerárquica o catalogo)
- Brindar [[Seguridad]] (Usuarios y Grupos; permiso de acceso a los datos)
- Asignación de espacio en dispositivos de almacenamiento (Administra lo que ocupa cada archivo, y las Unidades de asignación libre)
- Coordinación de transferencia (Atender y resolver las solicitudes simultaneas; Priorizar lectura/escritura de registros)
- Administrar la comunicación entre la CPU y los dispositivos de almacenamiento (Administrar el acceso concurrente de procesos a un mismo registro físico)

## Visión lógica de archivos
Atributos: Nombre, tamaño, fecha/hora, dueño, grupo, indicadores, etc.

Operaciones: Crear, eliminar, abrir, cerrar, leer, escribir, escribir al final, posicionarse, obtener atributos, definir atributos, renombrar.

## Diseño de datos
*Atributos:* especificación que define una propiedad de un objeto, elemento o archivo. También puede referirse a el valor específico para una instancia determinada de los mismos.

*Tipos de atributos:*

- Simple: una propiedad (por ejemplo, nombre, apellido, peso, altura.
- Compuestos; una propiedad compuesta (por ejemplo, fecha -> día, mes, año)
- Opcional: puede o no estar al momento de registrarse.
- Polivalentes: Depende de una lista de valores del mismo tipo.
- Externos; relacionan un dato con otro u otros del mismo conjunto o un conjunto externo.

*Identificador:* Cada cosa o evento debe poder distinguirse de los demás. Debe haber uno o más atributos que identifiquen unívocamente a los datos. Un conjunto de datos puede tener más de un identificador.
### Diseño conceptual
La definición conceptual de datos implica la definición de atributos, sin especificar tipos o dominios. Para cada atributo se indica la identidad (nombre). La estructura (en caso de que sean compuestos). La cardinalidad. Y también se puede definir la extensión.

*Los calificadores:*

- i: identificador.
- ie: identificador externo.
- d: definido por extensión en otro archivo.
- ?: opcional
- \*: ninguno o varios (0 a N)
- +: uno o más
### Definición lógica
Para cada atributo (dentro de un archivo). Implica la definición de bloques o unidades de organización. Especificando tipos o dominios para atributos, y la determina la convención de almacenamiento y recuperación. Es independiente del lenguaje de programación.

**Tipos de valores convencionales**
|     |                      |                                                                     |
|:---:| -------------------- | ------------------------------------------------------------------- |
| En  | Enteros              | Complemento a dos en n bytes                                        |
| Fn  | Fraccionarios        | Punto flotante en n bytes                                           |
| Cn  | Caracteres           | Con longitud exacta n                                               |
| CV  | Caracteres Variables | Hasta 255, con prefijo de longitud                                  |
|  T  | Texto                | Cantidad ilimitada de caracteres, incluyendo caracteres de control. |
|  L  | Lógicos              | 0: Falso o No, 1: Verdadero o Sí                                    |
|  B  | Binario              | Imagen, audio, video, etc.                                          |


## Organización de registros
### Registros de longitud fija
Son elementos del mismo tamaño y almacenan la información en los archivos mediante un encabezado. Se introducen una a uno los registros ubicados en posiciones consecutivas. En el tamaño del campo produce un desperdicio de espacio. Facilita la dirección y extracción de la información del campo.
### Registros de longitud variable
Almacenan elementos de varios tipos en un archivo y permite uno o más campos de longitudes variables y los campos pueden ser repetidos. La longitud de los registros debe estar definida correctamente para poder leer y escribir de forma efectiva. Aquí hay un aprovechamiento del espacio, pero se complica la localización y extracción de información.
### Independencia lógica de datos
*Datos lógicamente dependientes:* Dependen de una aplicación propietaria (sólo la aplicación conoce la estructura y organización de los registros).

*Datos lógicamente independientes:* Hay una definición de los datos (metadatos) pública y en una convención estándar (por ejemplo, [[XML]] o [[JSON]])