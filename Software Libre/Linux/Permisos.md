### Permisos sobre archivos
Al ser [[UNIX]] un sistema operativo multiusuario por diseño los archivos deben ser tratados como [[Archivos compartidos|archivos compartidos]] y por ende deben explicitar los permisos según usuario. En UNIX se utiliza un esquema donde se explicitan los permisos para el dueño, los usuarios que pertenezcan al grupo del dueño y para el resto. Para cada uno de estos se tienen 3 bits que indican el permiso de lectura, escritura y ejecución (para los directorios ejecución=apertura).

![[SL_UNIX_Permisos_archivos.png]]

Dado que son 3 bits los permisos se suelen representar en octal, siendo por ejemplo `rwx = 4+2+1 = 7` o `r-x = 4+0+1 = 5`.

#### Comandos útiles
```sh
# cambiar dueño
$ chown usuario:grupo archivo
$ chown -R usuario:grupo directorio
# cambiar permisos
$ chmod    644 archivo    # dueño rw-, grupo y el resto r--
$ chmod    640 archivo    # dueño rw-, grupo r-- y para el resto ---
$ chmod -R 755 directorio # dueño rwx, grupo y el resto r-x
$ chmod -R 750 directorio # dueño rwx, grupo r-x y para el resto ---
```

#### Tipos de archivo
- d: directorio
- -: archivo regular
- l: enlace simbólico
- c: dispositivo de caracteres
- b: dispositivo de bloques
- p: pipe con nombre
- s: socket con nombre