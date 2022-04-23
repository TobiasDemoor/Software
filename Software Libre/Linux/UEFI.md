Es una especificación que define una interfaz entre el sistema operativo y el firmware.

Unified Extensible Firmware Interface. Tiene soporte para leer tanto la tabla de particiones como los sistemas de archivo. No carga ningún código de arranque desde la Master Boot Record ([[MBR]]), sino que el arranque depende de las entradas en la NVRAM (memoria de acceso aleatorio no volátil).
- Puede leer FAT12/15/32.
- Permite añadir drivers para sistemas de archivos adicionales. Apple agrega para HFS+ o APFS.
- UEFI lanza aplicaciones EFI, como los bootloaders, boot managers, UEFI Shell, etc.
	- Estas aplicaciones se almacenan en la partición EFI.
	- Se pueden lanzar agregando una entrada en la NVRAM.
- Tiene soporte para arranque [[BIOS]] con el módulo de soporte de compatibilidad (CSM).
	- Si el CSM está activado, UEFI generará entradas de arranque CSM para todos los dispositivos.
	- Si se bootea desde alguna de estas entradas CSM, el CSM intentará arrancar desde el código presente en el [[MBR]] del dispositivo.
- Fue desarrollada inicialmente por Intel en el 2002.
- Soporte completo para la Tabla de particiones GUID ([[GPT]]), se pueden crear hasta 128 particiones por disco, con una capacidad total de 8 ZB.1