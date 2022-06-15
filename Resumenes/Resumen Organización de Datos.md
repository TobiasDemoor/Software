# Organización de Datos
![[Organización de Datos]]

# Organización de archivos
![[Organización de archivos]]

# Árboles
![[Árboles]]

# Motores de búsqueda
![[Motores de búsqueda]]

# File systems
> *“El conjunto de programas del sistema operativo encargados de proveer la visión lógica de la información almacenada a usuarios y programas conforman el Sistema de Archivo.”*

“ Un archivo me permite estructurar datos, un sistema de archivo me permite estructurar archivos”

Es el que indica como se organiza la información dentro de los medios físicos. Sus funciones son el guardado y recuperación de la información; la administración del espacio libre y el guardado de los atributos de seguridad del sistema operativo. Estos programas se encargan de:

- Identificar y localizar archivos.
- Seguridad.
- Asignación de espacio.
- Coordinación de transferencia (sistema multiusuario).

Los sistemas de archivos pueden ser clasificados por medio, de red y de propósito especial.

- Discos de plato magnético o Flash (acceso aleatorio): [[FAT]], [[NTFS]], HFS+, UFS, [[EXT|EXT2/3/4]], XFS, BRTFS, Veritas File system, ZFS, ReiserFS
- Discos Ópticos: ISO9660, UDF
- Flash file System (Especialmente embebidos): JFFS, UBIFS, LogFS, F2FS, SquashFS
- Network File System: [[NFS]], AFS (Sistema de compartición de Apple), SMB (Sistema de compartición de Microsoft), [[FTP]], Webdav, SSHFS.
- Sistemas de archivos en Cluster: 
  - Shared-disk / storage area network: GFS2 (Red hat), GPFS (IBM), CSV (Microsoft), OCFS (Oracle)
  - Distributed file systems: GFS (Google), HDFS (Apache), Ceph (Red Hat), DFS (Microsoft), [[GlusterFS]] (Red Hat)
- Especiales:
  - procfs --> Mapeo de procesos y estructuras en Linux
  - configfs y sysfs --> Muestra como archivos los parámetros de consulta y configuración de un Linux
  - devfs --> los archivos en este FS representan a dispositivos. Y permite utilizar las primitivas de cualquier FS para acceder al dispositivo.
  - Superpuestos --> [[UnionFS|OverlayFS]], [[UnionFS]], aufs
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
![[FAT]]

## Sistemas de archivos UNIX (Ext2/3/4)
![[EXT]]

## NTFS
![[NTFS]]

## VFS
![[VFS]]

## FUSE
![[FUSE]]

# XML
![[XML]]

# JSON
![[JSON]]

# Compresión
![[Compresión]]

# Seguridad Informática
La seguridad es una característica o cualidad que implica que un sistema este libre de peligro, daño o riesgo. La seguridad es una utopía, una característica inalcanzable, una tendencia. La fiabilidad es la probabilidad que un sistema actúe de acuerdo a lo esperado. Fundamentalmente cuando hablamos de seguridad informática lo que **queremos proteger es la información**.

Los tipos de ataques posibles son:

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
![[Criptología]]