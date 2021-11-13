Los **unique resource identifier** o **URI**  son una forma genérica y uniforme de identificar recursos definida en el [[RFC]] 3986.
Tienen el formato: scheme:\[//authority]path\[?query]\[#fragment].
Donde authority = \[userinfo@]host\[:port]

- **schema**: El formato es cualquier carácter de letra y digito, mas signo más (+) y menos(-) y el punto (.). Implica el esquema del servicio o recurso a utilizar. Existen esquemas registrados como no registrados. El ente de registro de esquemas es el Internet Assigned Number Autority (IANA). Ejemplo de schemas: coap, cvs,chrome, [[HTTP|http]], imap, ftp, tel, tftp, ws, xmpp, etc.
- **authority**: Muchos esquemas de URI incluyen un elemento jerárquico de autoridad de gobierna el nombre de espacios. Este elemento se lo suele denominar **host**. También se puede encontrar información del usuario (nombre de usuario : clave) y el puerto de servicio que atiende. 
- **path**: Es el componente de la URI que contiene la ruta al dato o recurso, se puede usar en conjunto con la consulta/query que es la parte no jerarquica. 
- **query** (optional): Es el que maneja las consultas en forma no jerarquica. Utiliza como separador entre el Path y la query el signo de interrogación (?). Para separar consultas se utiliza el ampersant (&) o el punto y coma (;). En todos los casos 
- **fragment** (optional) :Fragmento de la información consultada. Tambien denominado ancla.