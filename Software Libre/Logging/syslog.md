syslog es un framework simple para generar entradas de log, almacenarlas y transferirlas. Está diseñado para cualquier sistema (desde un sistema operativo a una aplicación). Es el más utilizado. Se encuentra formalizado en la [[RFC]] 5424 y cada registro tiene sos atributos importantes: 
- Tipo: si es de kernel, mail, autorización o auditoría entre otros. 
- Security: nivel de importancia desde 0 (emergencia) hasta 7 (debug)

Dentro de las funciones de syslog se encuentra:
- Monitorear todos los estados de todas las fuentes de logs. 
- Monitorear las rotaciones de los logs, su proceso de archivo y disposición (logrotate).
- Chequear todas las actualizaciones tanto de los software de logueo como los software que loguea.
- Asegurarse que los sistemas que tienen un registro tienen sincronizados los relojes!! 
- Reconfigurar los sistemas de logueo basados en cambio de políticas, tecnologías y otros factores. 
- Documentar anomalías, configuraciones y procesos 

### ¿Qué se debería registrar?
- Procesos del sistema.
	- Eventos significativos. 
	- Errores en los eventos. 
	- Eventos que fueran anómalos 
- Auditoría de registros ([[Seguridad]]) 
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
	- (se debe informar el nombre del equipo dado que se puede centralizar los logs)

### Arquitectura de syslog
- Equipos que generan logs. Generan los eventos de logs. 
- Equipos que los almacenan. 
- Equipos que los procesan. Procesamiento intermedio, chequeos de integridad, análisis para enviar información a otros equipos. 
- Equipos de monitoreo. Monitorean el flujo de información y generan reportes, buscan anomalías, etc.

### Preguntas
#### Generación de registros
- ¿Qué equipos deben o deberían realizar el registro centralizado?
- ¿Qué componentes de software del equipo deben realizar el registro centralizados?
- ¿Qué tipos de eventos deben ser registrados? (Eventos de seguridad, conexiones, intentos de autenticación, errores de aplicación)
- ¿Qué atributos debe guardar de cada evento? (ejemplo: usuario, dir. ip de conexión, etc ) 
- ¿Con qué frecuencia? (Ejemplo todas las ocurrencias, cada n ocurrencias dentro de un tiempo, toda ocurrencia después de n instancias, etc.)

#### Transmisión de eventos
- ¿Qué máquinas deben o deberían transferir sus logs a un sistema centralizado?
- ¿Qué entradas y características deben o deberían ser transferidas al sistema centralizador?
- ¿Con qué frecuencia debe ser transferido (Ej. en tiempo real, cada 5 minutos o cada hora)?
- ¿Que tipo de confidencialidad, integridad y disponibilidad debe tener cada entrada de evento?
- ¿Que nivel de confiabilidad y seguridad debe tener la transmisión (que protocolo y que cifrado)?

#### Guardado y disposición
- ¿Cada cuanto los log deben ser rotados?
- ¿Qué nivel de confidencialidad, integridad y disponibilidad debe tener cada registro de evento? Esto permite saber que tipo/s de dispositivos o esquemas de almacenamiento vamos a usar para proteger y preservar los datos. Define la infraestructura de almacenamiento
- ¿Cuándo se define que una información es innecesaria? ¿Cuánto tiempo se va a guarda la misma? ¿Cómo va a ser el procedimiento de borrado?
- ¿Cuanto del espacio de almacenamiento voy a usar?
- ¿Hay requerimientos legales de los eventos almacenar?

### Recomendaciones básicas
- Armar un sistema centralizado de eventos.
- Limitar el acceso a los registros de eventos.
- Los sistemas de registro deben garantizar solo “append” de eventos.
- Evitar almacenar información sensible (passwords,etc).
- Proteger los archivos de registro. Al menos generar algún sistema de firmas para garantizar la integridad.
- Securizar el sistema de reloj del sistema de bitácoras. No dejar que sistemas no autorizados procesen entradas de log. Preferentemente generar una copia que no acceda ningún sistema.
- Los sistemas de transporte del registro de evento deberían ser implementados en su máximo nivel de seguridad. De mínima no debe permitir el “man in the middle” o inyección no autorizada.

### journald
![[journald]]

### rsyslog
![[rsyslog]]

### Comandos
```sh
# para monitorear
$ tail -f /var/log/syslog

# comando logger
$ logger "Message"                     # añade el texto al system log
$ logger -n 127.0.0.1 -P 514 "Message" # añade el texto a un servidor externo
```