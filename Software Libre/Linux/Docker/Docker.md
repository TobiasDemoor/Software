Docker es una plataforma de [[Containers|containers]] de [[Software Libre|código abierto]]. Docker permite a los desarrolladores empaquetar aplicaciones en contenedores, componentes ejecutables estandarizados que combinan el código fuente de la aplicación con todas las bibliotecas y dependencias del sistema operativo (SO) necesarias para ejecutar el código en cualquier entorno.

### ¿Por qué usar docker?
**Creación de contenedores automatizada**: Docker puede crear automáticamente un contenedor basado en el código fuente de la aplicación.

**Control de versiones de contenedores**: Docker puede rastrear versiones de una imagen de contenedor, revertir a versiones anteriores y rastrear quién creó una versión y cómo. Incluso puede cargar solo los deltas entre una versión existente y una nueva. 

**Reutilización de contenedores**: los contenedores existentes se pueden utilizar como imágenes base, esencialmente como plantillas para crear nuevos contenedores. 

**Bibliotecas de contenedores compartidos**: los desarrolladores pueden acceder a un registro de código abierto que contiene miles de contenedores aportados por los usuarios ([Docker Hub](https://hub.docker.com/)).

### Terminología
- **Dockerfile**: cada contenedor de Docker comienza con un archivo de texto que **contiene instrucciones sobre cómo crear la imagen del contenedor de Docker**. El Dockerfile automatiza el proceso de creación de imágenes de Docker. Es esencialmente una lista de comandos que Docker Engine ejecutará para ensamblar la imagen.
- **Imágenes docker**: contienen código fuente de la aplicación ejecutable, así como todas las herramientas, bibliotecas y dependencias que el código de la aplicación necesita para ejecutarse como contenedor. **Cuando ejecuta la imagen de Docker, se convierte en una instancia (o varias instancias) del contenedor**. Las imágenes de Docker se componen de capas y cada capa corresponde a una versión de la imagen. Siempre que un desarrollador realiza cambios en la imagen, se crea una nueva capa superior. Las capas anteriores se guardan para reversiones o para reutilizarlas en otros proyectos.
- **Contenedores Docker**: son **instancias en vivo y en ejecución de imágenes de Docker**. Si bien las imágenes de Docker son archivos de solo lectura, los contenedores son contenido ejecutable, efímero y en vivo. Los usuarios pueden interactuar con ellos y los administradores pueden ajustar su configuración y condiciones.
- **Docker Hub**: es el repositorio público de imágenes de Docker que se autodenomina la "biblioteca y comunidad de imágenes de contenedores más grande del mundo". Contiene más de 100.000 imágenes de contenedores procedentes de proveedores de software comercial, proyectos de código abierto y desarrolladores individuales. Todos los usuarios de Docker Hub pueden compartir sus imágenes a voluntad. También pueden descargar imágenes base predefinidas para usarlas como punto de partida para cualquier proyecto de contenedorización

### Plataforma y arquitectura de Docker
![[SL_Docker.png]]

> Para que Docker funcione como lo hace se tubieron que agregar features al kernel de [[Linux]] estas son:
> 	- cgroups
> 	- namespaces

#### Docker namespaces
Los espacios de nombres son los componentes principales de los contenedores Docker. Hay varios tipos de espacios de nombres, y cada uno de ellos actúa como un bloque aislante de una aplicación a otra. La creación de espacios de nombres ocurre a través de la llamada al sistema de clonación clone() y derivadas. Algunos de los espacios de nombres utilizados por Docker incluyen: PID, espacio de nombres de red, IPC, MNT, UTS, Espacio de nombre de usuario.

##### PID namespace
Aíslan el número de identificación del proceso. Eso significa que los procesos que utilizan diferentes espacios de nombres PID pueden tener el mismo PID.

Los PID en un nuevo espacio de nombres PID comienzan en 1, algo así como un sistema independiente, y las llamadas a fork, vfork o clone producirán procesos con PID que son únicos dentro del espacio de nombres. Como se mencionó, los espacios de nombres PID permiten que cada contenedor tenga un conjunto aislado de PID. Cada PID crea una jerarquía de procesos única. Un espacio de nombres "principal" (principal) puede administrar los espacios de nombres "secundarios" y realizar acciones para modificar su funcionalidad. Sin embargo, un espacio de nombres secundario no puede ver ni realizar ninguna acción en particular en el nodo del espacio de nombres principal.

##### El espacio de nombres de red
El espacio de nombres de la red es una copia lógica de la pila de la red. Tiene bloques de construcción individuales como reglas de firewall, interfaces de red y tablas de enrutamiento. La ubicación predeterminada para los espacios de nombres de red es: /var/run/netns/NAME.

Los espacios de nombres de red permiten crear múltiples interfaces de red en cada contenedor, lo que permite que los servicios se comuniquen en sus respectivos puertos.

##### IPC namespaces
Un recurso de [[IPC]] inicializado por un contenedor puede ser consumido o terminado por otro contenedor. Si esto sucede, la aplicación vinculada al recurso de IPC en el primer contenedor falla. Ahí es donde entra en juego el espacio de nombres de IPC: evita que los procesos que se ejecutan en un espacio de nombres accedan a otros recursos de otro espacio de nombres de IPC.

##### MNT namespaces
Sin el espacio de nombres mnt, solo puede usar la operación chroot para verificar las rutas relativas de un sistema en particular desde un directorio/espacio de nombres “chrooted”. Con el espacio de nombres mnt, un solo contenedor puede tener su propio conjunto individual de directorios raíz montados y árbol del sistema de archivos.

#### cgroups
![[cgroups]]

#### UnionFS
![[UnionFS]]

### Implementación y orquestado
![[Docker Compose]]


![[Kubernetes]]

### Ejemplos
```sh
# levanta un container con ubuntu 20.04 y ejecuta el comando echo 'Hola mundo'
$ docker container run ubuntu:20.04 /bin/echo 'Hola mundo'
# levanta un container con ubuntu 20.04 asigna una pts dentro del container (-t), 
# mantiene una conexión interactiva con la stdin del contenedor (-i) y ejecuta el
# bash
$ docker container run -t -i ubuntu:20.04 /bin/bash
```

```sh
# aquí primero creamos un volumen apache-data y luego levantamos un container
# con apache (httpd) que levanta el volumen y su puerto 80 es forwardeado al
# puerto 8080 de la máquina host
$ docker volume create apache-data
$ docker run -d --name apache-server -p 8080:80 -v apache-data:/usr/local/apache2/htdocs httpd
```