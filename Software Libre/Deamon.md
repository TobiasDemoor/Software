---
aliases: ["deamon"]
---
Un deamon es un [[Proceso|proceso]] de **larga duración** (a menudo, se crea un deamon al iniciar el sistema y se ejecuta hasta que el sistema está apagado) que **se ejecuta en segundo plano** y **no tiene terminal de control**. La falta de una terminal de control asegura que el kernel nunca genere automáticamente señales de control de trabajo o relacionadas con la terminal (como SIGINT, SIGTSTP y SIGHUP) para un deamon.

Muchos daemons estándar se ejecutan como procesos con [[Permisos|privilegios]] (es decir, ID de usuario efectivo de 0). Esto no es lo ideal.

> Es una convención (no observada universalmente) que los demonios tienen nombres que terminan con la letra d.

En [[Linux]], ciertos demonios se ejecutan como subprocesos del kernel. El código de estos demonios es parte del kernel y, por lo general, se crean durante el inicio del sistema. Cuando se enumeran usando ps, los nombres de estos demonios están entre corchetes (\[]). Un ejemplo es \[kthreadd], que se utiliza para crear nuevos threads.

### Ejemplos de deamons
- **cron**: un deamon que ejecuta comandos a una hora programada. (clasificación polémica)
- **sshd**: el deamon de shell seguro, que permite inicios de sesión desde hosts remotos utilizando un protocolo de comunicaciones seguro
- **httpd**: el deamon del servidor HTTP (Apache), que sirve a las páginas web.
- **inetd**: ex deamon superservidor de Internet, que escuchaba las conexiones de red entrantes en los puertos TCP / IP especificados y lanza los programas de servidor adecuados para manejar estas conexiones.

### Cómo crear un deamon
#### Paso 1
Llamar a [[fork()]], después de lo cual el padre sale y el hijo continúa. (Como consecuencia, el daemon se convierte en un hijo del proceso init por el mecanismo de [[Procesos huérfanos|re-crianza]]).
Este paso se realiza por dos razones: 
- Suponiendo que el daemon se inició desde la línea de comandos, el shell notará la terminación del padre, que luego muestra otro prompt y deja que el hijo continúe en segundo plano.
- Se garantiza que el proceso hijo no será un líder de grupo de procesos, ya que heredó su ID de grupo de procesos de su padre y obtuvo su propio pID único, que difiere del ID de grupo de procesos heredado. Esto es necesario para poder realizar con éxito el siguiente paso.

#### Paso 2
El proceso hijo llama a [[setsid()]] para iniciar una nueva sesión y liberarse a sí mismo de cualquier asociación con una terminal.

#### Paso 3
Setear el umask para asegurarse de que, cuando el demonio crea archivos y directorios, tengan los permisos solicitados.

#### Paso 4
Cambiar el directorio de trabajo actual del proceso, generalmente al directorio raíz (/). Esto es necesario porque un demonio normalmente se ejecuta hasta que se apaga el sistema; si el directorio de trabajo actual del demonio está en un sistema de archivos que no sea el que contiene /, entonces ese sistema de archivos no se podría desmontar.

Crond históricamente usa /var/spool/cron por ejemplo.

#### Paso 5
Cerrar todos los descriptores de archivos abiertos que el daemon haya heredado de su padre. (Un daemon puede necesitar mantener abiertos ciertos descriptores de archivos heredados, por lo que este paso es opcional). Esto se hace por una variedad de razones. Dado que el demonio ha perdido su terminal de control y se está ejecutando en segundo plano, no tiene sentido que el demonio mantenga abiertos los descriptores de archivo 0, 1 y 2 que se refieren a la terminal.

#### Paso 6
Después de haber cerrado los descriptores de archivo 0, 1 y 2, un daemon normalmente abre /dev/null y usa dup2() (o similar) para hacer que todos esos descriptores se refieran a este dispositivo. Esto por dos razones:
- Asegura que si el daemon llama a funciones de biblioteca que realizan E/S en estos descriptores, esas funciones no fallarán inesperadamente.
- Evita la posibilidad de que el daemon abra más tarde un archivo usando el descriptor 1 o 2, por una función de biblioteca que espera tratar estos descriptores como salida estándar y error estándar.

%%Ejemplos:
https://github.com/pasce/daemon-skeleton-linux-c (ejemplo en C)
https://www.jejik.com/articles/2007/02/a_simple_unix_linux_d (ejemplo en Python)
%%

### Doble fork
No es [[fork()]] el que desprende del terminal de control. Es el [[setsid()]] el que lo hace. Pero setsid() fallará si lo llama un líder de grupo de proceso. Por lo tanto, se debe realizar una fork() inicial antes de setsid() para garantizar que se llame a setsid() desde un proceso que no es un líder de grupo de procesos. El segundo fork() asegura que el proceso final (el que será el demonio) no sea un líder de sesión. Solo los líderes de sesión pueden adquirir una terminal de control, por lo que este segundo fork() garantiza que el daemon no volverá a adquirir una terminal de control. Esto es cierto para cualquier sistema operativo POSIX.
%%Fuente: https://stackoverflow.com/questions/881388/what-is-the-reason-for-performing-a-double-fork-when-creating-a-daemon%%

### El pidfile
El pidfile es una herramienta que se utiliza para que un deamon pueda saber si ya hay una instancia corriendo (si no se utilizara [[systemd]]). Consiste en crear un archivo en un lugar conocido que incluya el pid del deamon en ejecución. Entonces al iniciar un deamon puede buscar en el directorio conocido si existe el archivo, si no existe no hay un deamon corriendo, y si existe pero el pid no está asociado a ningún proceso tampoco hay uno corriendo. Al iniciar el deamon luego del chequeo genera este archivo, y antes de finalizar en lo posible elimina el archivo.
