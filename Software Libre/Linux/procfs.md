El sistema de archivos proc actúa como una interfaz para las estructuras de datos internas del kernel. Puede usarse para obtener información sobre el sistema y para cambiar ciertos parámetros del kernel en tiempo de ejecución (sysctl).

#### Información útil
- /proc/PID/cmdline, el comando que inició originalmente el proceso.
- /proc/PID/cwd, un enlace simbólico al directorio de trabajo actual del proceso.
- /proc/PID/environment contiene los nombres y valores de las variables de entorno que afectan el proceso.
- /proc/PID/exe, un enlace simbólico al archivo ejecutable original, si aún existe (un proceso puede continuar ejecutándose después de que su ejecutable original haya sido eliminado o reemplazado).
- /proc/PID/fd, un directorio que contiene un enlace simbólico para cada descriptor de archivo abierto.
- /proc/PID/fdinfo, un directorio que contiene entradas que describen la posición y las banderas de cada descriptor de archivo abierto.
- /proc/PID/maps, un archivo de texto que contiene información sobre archivos y bloques mapeados (como heap y stack).
- /proc/PID/mem, una imagen binaria que representa la memoria virtual del proceso, solo se puede acceder mediante un proceso de rastreo.
- /proc/PID/status contiene información básica sobre un proceso, incluido su estado de ejecución y uso de memoria.