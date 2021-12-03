Es un [[Sistemas de archivos|sistema de archivo]] basado en una tabla de asignación de archivos (FAT). El propósito de dicha tabla es realizar un seguimiento para saber dónde encontrar archivos en el disco.

El directorio raíz es “drive:\\”. El separador de directorios es usualmente “\\”, pero el sistema operativo también reconoce internamente una “/”. Las unidades físicas y virtuales son nombradas con una letra de dispositivo, en vez de ser fusionados. Esto significa que no hay un directorio raíz formal, sino que hay un directorio raíz independiente en cada unidad. Cada directorio puede contener otros directorios o archivos.

Limita el nombre de los archivos a 8 caracteres y la extensión a 3 caracteres.

El sistema de archivos FAT se compone de cuatro secciones:

- **El sector de arranque.**
Siempre es el primer sector de la partición (volumen) e incluye información básica, punteros a las demás secciones y la dirección de la rutina de arranque del sistema operativo.

- **La región FAT.**
Contiene dos copias de la tabla de asignación de archivos (por motivos de seguridad). Estos son mapas de la partición, indicando que clusters están ocupados por los archivos.

- **La región del directorio raíz.**
Es el [[índice]] principal de carpetas y archivos.

- **La región de datos.**
Es el lugar donde se almacena el contenido de archivos y carpetas. Por tanto, ocupa casi toda la partición. El tamaño de cualquier archivo o carpeta puede ser ampliado siempre que queden suficientes clusters libres. Cada cluster está enlazado con el siguiente mediante un puntero. Si un determinado cluster no se ocupa por completo su espacio remanente se desperdicia.

### Tabla de asignación (región FAT)
La tabla de asignación de archivos consta de una lista de entradas. Cada entrada contiene información sobre un clúster:

- La dirección del siguiente cluster en la cadena.
- Si es pertinente, la indicación de “fin de archivo” (que también es el fin de la cadena).
- Un carácter especial para indicar que el cluster es defectuoso.
- Un carácter especial para indicar que el cluster está reservado (es decir, ocupado por un archivo).
- El número cero para indicar que el cluster está libre (puede ser usado).
- El tamaño de estas entradas también depende de la variante FAT en uso: FAT16 usa entradas de 16 bits, FAT32 usa entradas de 32 bits, etc.

### Directorio Raíz
Este índice es un tipo especial de archivo que almacena las subcarpetas y archivos que componen cada carpeta. Cada entrada del directorio contiene el nombre del archivo o carpeta (máximo 8 caracteres), su extensión (máximo 3 caracteres), sus atributos (archivo, carpeta, oculto, del sistema, o volumen), la fecha y hora de creación, la dirección del primer cluster donde están los datos y por último, el tamaño que ocupa.

El directorio raíz ocupa una posición concreta en el sistema de archivos, pero los índices de otras carpetas ocupan la zona de datos como cualquier otro archivo. Los nombres largos se almacenan ocupando varias entradas en el índice para el mismo archivo o carpeta.