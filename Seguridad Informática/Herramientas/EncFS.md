EncFS es un [[Sistemas de archivos|sistema de archivos]] basado en FUSE. Transfiere archivos de forma transparente, utilizando un directorio arbitrario como almacenamiento para los [[Cifrado de archivos|archivos cifrados]]. Es un ejemplo de cifrado de archivos de usuario.

Hay dos directorios involucrados en el montaje de un sistema de archivos EncFS: el directorio de origen y el punto de montaje. Cada archivo en el punto de montaje tiene un archivo específico en el directorio de origen que le corresponde. El archivo en el punto de montaje proporciona la vista sin cifrar del que está en el directorio de origen. Los nombres de archivo se cifran en el directorio de origen

Los archivos se cifran utilizando una clave de volumen, que se almacena dentro o fuera del directorio de código cifrado. Otra contraseña se usa para descifrar esta clave.

Ejemplo:
```sh
~$ mkdir textoPlano
~$ mkdir cifrado
# monto directorios
~$ encfs ~/cifrado/ ~/textoPlano/
# desmonto directorios
~$ fusermount -u ~/textoPlano
~$ encfsctl info ~/cifrado
```