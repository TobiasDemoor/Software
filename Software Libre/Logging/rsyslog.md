Sistema de [[syslog]] estándar en varios sistemas operativos de [[Linux]]. Cumple con el estandar syslog. Permite compatibilidad para tener instalado el [[journald]]. Permite encriptación, envío de registros a bases de datos y RELP (Reliable Event Logging Protocol).

![[SL_rsyslog.png]]

### Archivos importantes
- boot -> logueo de arranque 
- kern.log -> logueo de módulos de kernel 
- auth.log -> autentificación de usuarios 
- dpkg.log -> programas instalados, borrados o actualizados 
- syslog.log -> archivo principal de registro 
- user.log -> "registro de aplicación"
- wtmp/btmp -> registro de acceso al sistema