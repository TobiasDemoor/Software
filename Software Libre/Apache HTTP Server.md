---
aliases: ["httpd", "Apache server"]
---

[[Servidor]] [[World Wide Web|WEB]] [[Software Libre|software libre]] que corre en sistemas [[Linux]] como el [[Deamon|deamon]] httpd. El usuario con el cual se ejecuta dicho deamon es **www-data**.

### Configuración
Directorio raíz:
- /etc/apache2

Configuración general:
- /etc/apache2/conf-available/
- /etc/apache2/conf-enabled/

Módulos:
- /etc/apache2/mods-available/
- /etc/apache2/mods-enabled/

Sitios:
- /etc/apache2/sites-avaiable/ (aquí van las configuraciones de los sitios disponibles)
- /etc/apache2/sites-enabled/ (aquí van links simbólicos a archvios de sites-avaiable, se crean y eliminan con los comandos `ad2ensite` y `ad2dissite`)

Para crear una configuración nueva debemos definir el `ServerName` para que apache sepa cuál es el nombre de dominio que debe asociar con dicho sitio y `ServerAlias` si los hubiera. Se debe establecer el `DocumentRoot` que será de donde se toman los archivos estáticos para el servidor y se deben modificar las rutas de logs para loguear en archivos especiales.

Si el directorio en `DocumentRoot` no se encuentra permitido para que el servidor acceda se debe agregar el siguiente elemento dentro del elemento `VirtualHost`
```XML
<Directory {ruta_en_DocumentRoot}>
	 AllowOverride none
	 Require all granted
</Directory>
```

#ApacheFoundation
