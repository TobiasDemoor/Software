Device-mapper es una infraestructura en el kernel Linux 2.6 y posterior que proporciona una forma genérica para crear capas virtuales de dispositivos de bloques.

Device-mapper crypt proporciona cifrado transparente de dispositivos de bloque utilizando la API criptográfica del kernel. Esto permite cifrar nuestro sistema de archivos completo, es decir discos enteros, particiones, pen drives, etc.

El usuario puede básicamente especificar uno de los **cifrados simétricos que están disponibles en el kernel (como módulos)**, una clave (de cualquier tamaño permitido), un modo de generación y luego crear un nuevo dispositivo de bloques en /dev. Es un ejemplo de [[Cifrado de archivos|cifrado a nivel dispositivo de bloques]].

Las escrituras en este dispositivo serán encriptadas y se leerán descifradas. Puede montar su sistema de archivos como de costumbre o apilar el dispositivo dm-crypt con otro dispositivo como volumen RAID o LVM.

Algunas distribuciones de Linux admiten el uso de dm-crypt en el sistema de archivos raíz. Estas distribuciones usan initrd ([[Proceso de arranque]]) para solicitar al usuario que ingrese una frase de contraseña en la consola o que inserte una tarjeta inteligente antes del proceso de inicio normal. Es decir permiten arrancar un sistema operativo con el sistema de archivos casi completamente cifrado.

### cryptsetup
El mapeador de dispositivos dm-crypt reside completamente en el espacio del kernel y solo se ocupa del cifrado del dispositivos de bloque, **no interpreta ningún dato por sí mismo**. Se basa en las utilidades userspace para crear y activar volúmenes cifrados y administrar la autenticación.

Actualmente hay al menos dos interfaces disponibles: cryptsetup y cryptmount.

Ejemplo:
```sh
~$ dd if=/dev/urandom of=cifrado bs=1M count=100
~$ losetup -–find -- show cifrado
# anotar el ‘/dev/loopN’
~$ cryptsetup -v luksFormat --type luks2 /dev/loop0
~$ lsblk
~$ cryptsetup open /dev/loop0 mapeo
# ahora va a estar disponible en /dev/mapper/mapeo
~$ mkfs.ext4 /dev/mapper/mapeo
~$ mount /dev/mapper/mapeo /mnt
```