[[systemd]] tiene un sistema de registro ("log") propio llamado journal. Intenta reemplazar al los esquemas de [[syslog]] y logra en desktop que no sea necesario un demonio syslog. mantiene compatibilidad con otros sistemas de syslog para poder coexistir. Journal tiene su propia herramienta para filtrado de mensajes. Esto se debe a que el almacenamiento es en binario. En un sistema tradicional de log la herramienta estándar de búsqueda es el comando grep.

Cuenta con la posibilidad de enviar a los datos a otros sistemas journal mediante HTTP o HTTPS.

### journald vs otros syslog
journald fue diseñado para manejar eficientemente los logs locales en desktop . Por el otro lado syslog-ng y rsyslogd fueron diseñados para alta perfomance de sistemas centralizados de recolección de logs.

Los otros syslog permite recolección por varios métodos. journald fue diseñado para registrar los eventos de los procesos que controla el systemd. Está diseñado para aislar el registro de eventos mediante namespace.

Journal tiene un solo sistema sistema de almacenamiento (en forma binario) por defecto en /var/log/journal. En cambio otros sistemas de syslog permite almacenar en distintos formatos (por default guarda en texto) como por ejemplo base de datos, sistemas encriptados, o reenvío por varios protocolos syslog, http, etc.

### Uso
```sh
$ journalctl -b # Ver los mensajes de arranque 
$ journalctl --since="2012-10-30 18:17:16" # Ver los mensajes desde.. 
$ journalctl --since "20 min ago" # Ver los mensajes de hace 20 minutos 
$ journalctl -f # Seguir los últimos mensajes 
$ journalctl /usr/lib/systemd/systemd # Mostrar los log de un binario 
$ journalctl _PID=1 # Ver los mensajes de un pid especial 
$ journalctl -u man-db.service # De una unidad de systemd 
$ journalctl -k # Mostrar el búfer del kernel 
$ journalctl -p err..alert # Mostrar solo los de un tipo de criticidad 
$ journalctl -D /mnt/var/log/journal -xe # Mostrar otros archivos de log.
```