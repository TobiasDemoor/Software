---
aliases: ["GnuPG"]
---
GnuPG es una aplicación (parte de [[Proyecto GNU|GNU]]) que sirve para [[Criptografía|encriptar]] y/o [[Firma digital|firmar]] mensajes y documentos. GnuPG usa un sistema de claves públicas donde cada usuario tiene una clave privada y una clave pública.

```sh
# para encriptar se utiliza la opción --armor
$ gpg --armor --recipient <destinatario> -encrypt <mensaje>
# para desencriptar se utiliza la opción --decrypt
$ gpg --decrypt <archivo>

# para firmar
$ gpg --clearsign <archivo> # genera un archivo .asc no encriptado
$ gpg --sign <archivo> # genera un archivo .gpg encriptado que se puede desencriptar con --decrypt
$ gpg --verify <archivo .asc> # verifica la firma
```

Los usuarios pueden firmar las claves públicas de otros para establecer una cadena de confianza de claves públicas, donde cada usuario firmate asegura que la clave pública es de quién dice ser.