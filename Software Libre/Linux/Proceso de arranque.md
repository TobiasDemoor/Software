---
aliases: ["proceso de arranque"]
---

Cuando se inicia un sistema el procesador ejecuta código en un lugar bien conocido. En una computadora personal, este lugar se encuentra en la BIOS (basic input/output system), que se encuentra almacenado en flash en el motherboard.

![[SL_Linux_Proceso_de_arranque.png]]

El primer paso es la realización del POST (power-on self test). El trabajo del POST es chequear el hardware. El segundo paso de la BIOS es enumerar e inicializar los dispositivos locales.

Para bootear un sistema operativo, el runtime de la BIOS busca dispositivos activos y booteables en el orden de preferencia definido por la configuración del CMOS. Un disco booteable contiene un [[MBR]] (en caso de un sistema UEFI se tiene un [[GPT]]), este es un sector de 512 bytes que se ubica como el primer sector del cilindro 0 cabeza 0. Luego de que el MBR es cargado en memoria principal la BIOS cede el control.

El boot loader primario que reside en el MBR es una imagen de 512 bytes que contiene tanto código de programa como una pequeña tabla de particiones. Los primeros 446 bytes son el boot loader primario, los siguientes 64 bytes son la tabla de particiones, que contiene un registro por cada una de las 4 particiones (de aquí el límite). El MBR finaliza con 2 bytes que son definidos como el magic number (0xAA55). El magic number sirve como una validación del MBR.

![[SL_Linux_MBR.png]]

El trabajo del boot loader primario es buscar y cargar el boot loader secundario. Luogra esto buscando a través de la tabla de particiones por una partición activa. Cuando encuentra una partición activa, escanea las particiones restantes para asegurarse que están todas inactivas. Cuando esto está verificado se lee el registro de booteo de la partición activa, se carga en memoria principal y se ejecuta.

El objetivo del boot loader secundario es cargar el kernel y un RAM disk opcional en memoria principal.

Los boot loaders de primera y segunda etapa combinados son llamados Linux Loader (LILO) o Grand Unified Bootloader (GRUB). LILO es la solución original, GRUB es una solución que arregla varias desventajas de LILO y es lo que se usa actualmente.

GRUB tiene conocimiento de [[sistemas de archivos]], en vez de usar sectores crudos del disco (como hacía LILO) GRUB puede cargar el kernel de un sistema de archivos ext2 o ext3. Logra esto incluyendo una etapa intermedia, el MBR ejecuta una stage 1.5 que entiende un sistema de archivos particular (por ejemplo e2fs_stage1_5 para ext2 o ext3). Cuando el stage 1.5 se encuentra cargado y ejecutando el boot loader stage 2 puede ser cargado.

Con el boot loader de segunda etapa en memoria, el sistema de archivos es consultado y la imagen de kernel por defecto, junto con una imagen de *initrd* (initial RAM disk) son cargados en memoria.

El kernel utiliza *initrd* como sistema de archivos raíz temporal hasta que se termina el arranque y se monta el sistema de archivos raíz real. También contiene los drivers necesarios compilados en su interior, lo que le ayuda a acceder a las particiones del disco duro y otro hardware.

Debian generará una imagen *initrd* personalizada que contiene solo lo necesario para arrancar una máquina en particular, como ATA, SCSI y módulos del kernel del sistema de archivos.

%%Fuente: https://developer.ibm.com/articles/l-linuxboot/%%
