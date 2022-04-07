El cifrado de archivos implica **[[Criptología|cifrar]] a nivel de los datos almacenados en un equipo**. Cuando se cifra un archivo o directorio, su contenido se codifica y solamente quien tenga la clave de cifrado correcta podrá decodificarlo y leerlo. Esto ayuda a aumentar la seguridad de los archivos y directorios individuales.

El cifrado de archivos es útil para evitar la visualización no autorizada de los datos cuando la computadora o el disco:
- Están ubicados en un lugar al que las personas no confiables podrían tener acceso mientras estás fuera
- Pueden ser perdidos o robados, como en el caso de las computadoras portátiles, netbooks o dispositivos de almacenamiento externo.
- Van a estar en un taller de reparaciones.
- Van a ser descartados después de su fin de vida útil (la mejor solución a esto es la destrucción física).

Sin embargo el cifrado de archivos no protege contra todas las amenazas. El dispositivo sigue siendo vulnerable mientras se está ejecutando después de haber sido desbloqueado (si un atacante entra en ese momento tiene acceso a toda la información). Pueden obtener acceso físico a la computadora mientras se está ejecutando y si tienen los recursos realizar un ataque de [[Cold boot|arranque en frío]]. Entre otros ataques que aún siguen siendo posibles.

Existen dos técnicas comunes para proteger criptográficamente el almacenamiento:
- Cifrado de directorios. Dentro de esta es común el cifrado solo de datos de usuario.
- Cifrado de particiones o discos completos

En ambos casos todos los datos que se escriben se cifran automáticamente y se descifran sobre la marcha cuando se leen de nuevo. Los archivos solo están disponibles para el sistema operativo y las aplicaciones en forma legible mientras el sistema se ejecuta y desbloquea por un usuario de confianza. Una persona no autorizada que mira los contenidos del disco directamente, solo encontrará datos confusos de aspecto aleatorio en lugar de los archivos reales.

El **cifrado solo de datos de usuario** no es muy seguro ya que en los sistemas modernos, hay muchos procesos en segundo plano que pueden almacenar o ubicar en caché información sobre los datos del usuario o partes de los mismos en áreas no encriptadas del disco duro, como:
- particiones swap (un remedio potencial para esto es deshabilitar el swap o usar un swapping cifrado).
- archivos temporales /tmp (un remedio potencial es evitar las aplicaciones que los generan o montar el /tmp dentro de un ramdisk)
- archivos variables /var (archivos de log, bases de datos y similares)

El **cifrado completo del sistema** es definido como el cifrado completo de archivos sistema operativo y los datos del usuario. El cifrado del sistema ayuda a abordar algunas de las deficiencias del cifrado solo de datos de usuario.

El cifrado completo tiene como ventajas que impide el acceso físico no autorizado (y modificación) de los archivos del sistema operativo y el acceso físico no autorizado a datos privados que el sistema puede almacenar en cache. 

También tiene como desventajas que el desbloqueo de las partes cifradas del disco ya no puede ocurrir durante o después del inicio de sesión del usuario, sino que ahora debe suceder al momento del arranque, esto complejiza mucho el proceso de arranque.

### ¿Cómo funciona?
Todos los métodos de cifrado de disco funcionan de tal manera que, aunque el disco contiene datos encriptados, el sistema operativo y las aplicaciones "lo ven" como los datos legibles normales correspondientes, siempre que el contenedor criptográfico (es decir, la parte lógica del disco que contiene los datos encriptados) han sido "desbloqueados" y montados. Para que esto suceda, el usuario debe proporcionar cierta "información secreta" (generalmente en forma de un archivo de clave y / o frase de [[Passwords|contraseña]]), de la cual se puede derivar la clave de cifrado real (y almacenarla en el llavero del núcleo durante el tiempo de la sesión).