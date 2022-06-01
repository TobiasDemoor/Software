---
aliases: ["syslog"]
---
Syslog es un framework simple para generar entradas de log, almacenarlas y transferirlas. Está diseñado para cualquier sistema operativo prácticamente y es parte de [[Linux]]. Es el más utilizado.
- Monitorea todos los estados de todas las fuentes de logs. 
- Monitorean las rotaciones de los logs, su proceso de archivo y disposición.
- Chequear todas las actualizaciones tanto de los software de logueo como los software que loguea.
- Asegurarse que los sistemas que tienen un registro tienen sincronizados los relojes!! 
- Reconfigurar los sistemas de logueo basados en cambio de políticas, tecnologías y otros factores. 
- Documentar anomalías, configuraciones y procesos 
- Dos atributos importantes: 
	- Tipo: kernel, mail, autorización o auditoría. 
	- Security: nivel de importancia desde 0 (emergencia) hasta 7 (debug)

### ¿Qué se debería registrar?
- Procesos del sistema.
	- Eventos significativos. 
	- Errores en los eventos. 
	- Eventos que fueran anómalos 
- Auditoría de registros (seguridad) 
	- Registros de acceso. 
	- Registros de intentos fallidos. 
	- Cambios dentro del sistema que se requieran privilegios. 
	- Borrados o modificaciones de información crítica.
- En aplicaciones 
	- Solicitudes y pedidos a sistemas externos. 
	- Accounting information. Intentos de logueos tanto exitosos como fallidos. Cambios de perfil. En lo posible, cierres de sesión también. 
	- Datos de utilización. Cantidad de transacciones ocurridas en un período.
	- Acciones significativas. Errores de sistemas, arranques y apagados, borrado o modificaciones de registros importantes. 
- ```<timestamp> <equipo> <servicio> <[etiqueta]: registro>```
	- (se debe informar el equipo dado que se puede centralizar los logs)

### Arquitectura de syslog
- Equipos que generan logs. Generan los eventos de logs. 
- Equipos que almacenan. 
- Equipos que procesan. Procesamiento intermedio, chequeos de integridad, análisis para enviar información a otros equipos. 
- Equipos de monitoreo. Monitorean el flujo de información y generan reportes, buscan anomalías, etc.

### Políticas
- ¿Qué equipos deberían logear? 
- ¿Qué tipos de eventos deben ser registrados? 
- ¿Qué atributos guardar de cada evento? Usuario, dir, ip, etc. 
- ¿Con qué frecuencia? Todas las ocurrencias, cada n ocurrencias, cada una cantidad de tiempo, etc.