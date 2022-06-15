---
aliases: ["httpd", "Apache server"]
---
[[Servidor]] [[World Wide Web|WEB]] [[Software libre|software libre]] que corre en sistemas [[Linux]] como el [[Deamon|deamon]] httpd. El usuario con el cual se ejecuta dicho deamon es **www-data**.

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
<!-- file 001-www.dominio.com.conf -->
<VirtualHost *:80>
	ServerName www.dominio.com
	ServerAlias dominio.com
	
	ServerAdmin webmaster@dominio.com
	DocumentRoot /home/usuario/public_html
	
	ErrorLog ${APACHE_LOG_DIR}/usuario_error.log
	CustomLog ${APACHE_LOG_DIR}/usuario.log combined
	
	<Directory /home/usuario/public_html>
		 AllowOverride none
		 Require all granted
	</Directory>
</VirtualHost>
```

### Modelos de multiprocesamiento (MPM)
%%Copiado de Daily/20220603%%
[[kqueue]] y [[epoll]] son llamadas a la api de [[linux]] que se incluyeron hace 12 años masomenos que permiten que los procesos queden escuchando eventos del so. Estos se usan para ser eficiente al reaccionar ante llamadas de la red y quedan escuchando los eventos de creación de sockets.
con estas funciones el servidor no tiene la necesidad de trabajar con hilos, y simplemente reaccionar a los eventos

a2enmod mpm_prefork
a2enmod mpm_worker
a2enmod mpm_event ([[Threads#Máquina de estado finito event-loop|Máquina de estados]])

Prefork: solo con procesos, sin hilos (se usa cuando lo que corre no es thread safe)
Worker: puede atender por hilos pero tiene que tener un proceso de control
Event: como el event-loop de node

se mapea a lo que está en [[Threads]]

el mpm event intenta solucionar el problema "Keep Alive" de [[HTTP]] que causa un gran desperdicio de recursos en el servidor. Ya que por cada conexión Keep Alive en modo worker o prefork se tiene un hilo o proceso en espera.

#ApacheFoundation 