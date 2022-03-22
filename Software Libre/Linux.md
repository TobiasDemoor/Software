---
aliases: ["GNU/Linux"]
---
> Se le dice Linux para abreviar pero el nombre completo es GNU/Linux, ya que Linux es solo el kernel de dicho SO.

### Distribuciones GNU/Linux
Una distribución de Linux (a menudo abreviada como distribución) es un sistema operativo creado a partir de una colección de software que se basa en el kernel de Linux y, a menudo, en un sistema de gestión de paquetes. Los usuarios de Linux generalmente obtienen su sistema operativo descargando una de las distribuciones de Linux, que están disponibles para una amplia variedad de sistemas.

Una distribución típica de Linux comprende un kernel de Linux, herramientas y bibliotecas [[Proyecto GNU|GNU]], software adicional, documentación, un sistema de ventanas (el más común es el sistema X Window), un administrador de ventanas y un entorno de escritorio.

La diferencia más importante entre distribuciones es el gestor de paquetes. El **gestor de paquetes** es el software que permite al usuario instalar y desinstalar paquetes, verificando e instalando dependencias y verificando su integridad. En los derivados de debian el gestor de paquetes es dpkg con apt encima.

>El sistema operativo no es solo el kernel

>Por el lado de la seguridad las librerías son un problema. Una solución a esto es lo que hace android (y snap) de utilizar sandboxing y hacer correr esta librería en su propio sandbox. El uso de sandboxes tiene un detrimento en la eficiencia ya que se deben correr varias instancias de la misma librería.

### Linux Filesystem Hierarchy (HFS)
Linux tiene su sistema de archivos estándar, que determina dónde se ubican los archivos. 
- En /bin se almacenan los archivos binarios.
- En /dev se encuentran los dispositivos.
- En /etc se encuentran los archivos de configuración.
- En /media se montan los dispositivos externos.
- En /mnt se montan los dispositivos internos.
- En /proc se almacena la información de los procesos en ejecución.
- En /tmp se almacenan los archivos temporales.
- En /usr se almacenan los archivos de usuario.
- En /var se almacenan los archivos de tamaño variable.

### Package manager
Un **gestor de paquetes** se ocupa de paquetes, distribuciones de software y archivos en almacenamiento. Los paquetes fundamentalmente resuelven las dependencias necesarias para que el software se ejecute correctamente. Tras la instalación, los metadatos se almacenan en una base de datos de paquetes local. Trabajan en estrecha colaboración con repositorios de software, administradores de repositorios binarios y tiendas de aplicaciones.