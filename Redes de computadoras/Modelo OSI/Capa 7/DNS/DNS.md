El DNS (Domain Name System) es una [[Bases de Datos|base de datos]] distribudida y jerárquica. En ella se almacena información que mapea nombres de host a [[direcciones IP]] y visceversa.

Las solicitudes se envían utilizando [[UDP]] (a través del puerto bien conocido UDP/53). Los nombres de dominio de nivel superior son controlados por la ICANN.

En lo que respecta al modelo OSI, DNS es una aplicación y por lo tanto recide lógicamente en la [[capa de aplicación]]. Sin embargo es claro que ofrece un servicio de uso general independiente de la aplicación, por esto se podría argumentar que forma parte del [[middleware]].

Existen 13 servidores raíz (root servers) en toda [[Internet]], cuyos nombres son de la forma \<letra>.root-servers.net, aunque siete de ellos no son realmente servidores úncios, sino que representan múltiples servidores distribuidos a lo largo del globo terráqueo. En argenina existen nodos de f.root-servers.net (ns.isc.org) y f.root-servers.net (ICANN).

El comité asesor del sistema de servidores DNS raíz (en inglés DNS Root Server System Advisory Committee) es un comité de la ICANN, que por estatutos tienen autoridad sobre la operación del sistema Sin embargo, la zona raíz es controlada por el Departamento de Comercio de Estados Unidos, que debe aprobar todos los cambios en el archivo de zona raíz solicitados por la ICANN.

NIC Argentina (Network Information Center Argentina) administra el Registro de nombres de dominio y asegura el funcionamiento del DNS para el Dominio de Nivel Superior Geográfico (Country Code Top Level Domain, ccTLD) .ar.

### Espacio de nombres de DNS
El [[espacio de nombres]] del DNS se encuentra organizado jerárquicamente como un árbol con raíz. Una etiqueta es un string (case-insensitive) conformado por caracteres alfanuméricos y con una longitúd máxima de 63 caracteres. La longitud de una ruta completa está restringida a 255 caracteres. La representación de la ruta consiste de una lista de sus labels, empezando por la derecha, y separandolas con un punto ("."). La raíz es representada con un punto aunque generalmente se omite.

Porque cada nodo en DNS tiene exactamente una sola arista entrante (exceptuando al raíz), la etiqueta adherida a la arista también es usada como el nombre para dicho nodo. Un subárbol es llamado **dominio** o **domain** y una ruta de el nodo raíz es llamada **nombre de dominio** o **domain name**.

![[dns_1.png]]

### Registros de recursos de dominio
Cada dominio, sea un host individual o un dominio de nivel superior, puede tener un grupo de **registros de recursos** asociados a él. Estos registros son la base de datos del DNS. En un host individual, el registro de recursos más común es simplemente su dirección IP, pero también existen muchos otros tipos de registros de recursos. Cuando un resolvedor asigna un nombre de dominio al DNS, lo que recibe son los registros de recursos asociados a ese nombre. Por lo tanto, **la función principal del DNS es relacionar los nombres de dominios con los registros de recursos.**

Un registro de recursos es una 5-tupla. Aunque éstas se codifican en binario por cuestión de eficiencia, en la mayoría de las presentaciones, los registros de recursos se presentan como texto ASCII, una línea por registro de recursos. El formato que siguen aproximadamente es el siguiente:
< Nombre_dominio, Tiempo_de_vida, Clase, Tipo, Valor >

El *Nombre_dominio* indica el dominio al que pertenece este registro. Por lo general, existen muchos registros por dominio y cada copia de la base de datos contiene información sobre múltiples dominios. Por lo tanto, este campo es la clave primaria de búsqueda que se utiliza para atender las consultas. El orden de los registros de la base de datos no es importante.

El campo de *Tiempo_de_vida* es una indicación de la estabilidad del registro. La información altamente estable recibe un valor grande, como 86400 (la cantidad de segundos en 1 día). A la información que es altamente volátil se le asigna un valor pequeño, como 60 (1 minuto).

El tercer campo de cada registro de recursos es la *Clase*. Para información de Internet, siempre es IN. Para información que no es de Internet se pueden utilizar otros códigos, pero en la práctica, éstos raras veces se ven.

El campo *Tipo* indica el tipo de registro del que se trata. Hay muchos tipos de registros de DNS.

| Tipo  | Significado                             | Valor                                                         |
| ----- | --------------------------------------- | ------------------------------------------------------------- |
| SOA   | Inicio de autoridad                     | Parámetros para esta zona                                     |
| A     | Dirección IPv4 de un host               | Entero de 32 bits.                                            |
| AAAA  | Dirección IPv6 de un host               | Entero de 128 bits                                            |
| MX    | Intercambio de correo                   | Prioridad, dominio dispuesto a aceptar [[correo electrónico]] |
| NS    | Servidor de nombres                     | Nombre de un servidor para este dominio                       |
| CNAME | Nombre canónico                         | Nombre de dominio                                             |
| PTR   | Apuntador                               | Alias de una dirección IP                                     | 
| SPF   | Marco de trabajo de política del emisor | Codificación de texto de la política de envío de correo       |
| SRV   | Servicio                                | Host que lo provee                                            |
| TXT   | Texto                                   | Texto ASCII descriptivo                                       |
| HINFO | Información del host                    | Información del hardware del host                             |

Un nodo en el espacio de nombres de DNS usualmente representará varias entidades al mismo tiempo. Por ejemplo un nombre de dominio es usuado para representar un dominio y una zona. En este caso el dominio es implementado por medio de varias zonas sin overlap.

Un registro SOA proporciona el nombre de la fuente primaria de información sobre la zona del servidor de nombres (que describiremos más adelante), la dirección de correo electrónico de su administrador, un número de serie único, varias banderas y temporizadores.

El tipo de registro más importante es el registro A (dirección), el cual contiene una dirección IPv4 de 32 bits de una interfaz para algún host. El registro AAAA correspondiente, o “quad-A”, contiene una dirección IPv6 de 128 bits. Cada host de Internet debe tener cuando menos una dirección IP, para que otras máquinas se puedan comunicar con él. Algunos hosts tienen dos o más interfaces de red, en cuyo caso tendrán dos o más registros de recursos tipo A o AAAA. En consecuencia, DNS puede regresar varias direcciones para un solo nombre

Otro tipo de registro es el MX (mail exchange), el cual es como un link simbólico a un nodo que representa el servidor de mail.

NS es otro tipo de registro importante, ya que especifica un servidor de nombres para el dominio o subdominio. Es un host que tiene una copia de la base de datos para un dominio. Se utiliza como parte del proceso para buscar nombres.

El DNS distingue los alias de lo que se le llama **nombres canónicos** o **cannonical names**. Se supone que cada host tiene un nombre canónico o primario. Un alias es implementado por medio de almacenar n registro CNAME conteniendo el nombre canónico de un host. Este registro que contiene el nombre funciona de la misma manera que un symbolic link.

Al igual que CNAME, PTR apunta a otro nombre. Sin embargo, a diferencia de CNAME, que en realidad es sólo una definición macro (es decir, un mecanismo para reemplazar una cadena por otra), PTR es un tipo de datos DNS normal, cuya interpretación depende del contexto en el que se encuentre. En la práctica, casi siempre se usa para asociar un nombre a una dirección IP con el fin de permitir búsquedas de la dirección IP y devolver el nombre de la máquina correspondiente. Éstas se llaman **búsquedas inversas**. Para permitir las búsquedas de nombres de host al tener solo una dirección IP, DNS mantiene un dominio llamado *in-addr.arpa*, que contiene nodos que representan hosts de [[Internet]] que son nombrados por la dirección IP del host representado. Por ejemplo el host *www.cs.vu.nl* tiene la dirección IP 130.37.20.20 DNS crea un nodo llamado *20.20.37.130.in-addr.arpa*, la cual almacena el nombre canónico del host.

SRV es un tipo reciente de registro, el cual permite identificar a un host para un servicio dado en un dominio. Por ejemplo, el servidor web para cs.washington.edu se podría identificar como cockatoo. cs.washington.edu. Este registro generaliza el registro MX que realiza la misma tarea, pero que es sólo para servidores de correo. El servicio en sí mismo es identificado por medio de un nombre junto con el nombre del protocolo.

SPF es otro tipo reciente de registro, el cual permite a un dominio codificar información sobre qué máquinas en el dominio enviarán correo al resto de Internet. Esto ayuda a las máquinas receptoras a verificar que el correo sea válido.

Luego están los registros TXT, cuyo objetivo original era permitir que los dominios se identificaran a sí mismos en formas arbitrarias. En la actualidad usualmente codifican información legible por máquina, por lo general la información SPF.

Finalmente, un registro HINFO (host info) es utilizado para almacenar información adicional del host, tal como su típo de máquina y sistema operativo (está cayendo en desuso por problemas de seguridad). De manera similar los registros TXT son usados para otro tipo de datos que el usuario encuentra útiles de almacenar sobre la entidad representada por el nodo.

### Resolución de nombres
![[Resolución de nombres DNS]]