El [[espacio de nombres]] del [[DNS]] se encuentra organizado jerárquicamente como un árbol con raíz. Una etiqueta es un string (case-insensitive) conformado por caracteres alfanuméricos y con una longitúd máxima de 63 caracteres. La longitud de una ruta completa está restringida a 255 caracteres. La representación de la ruta consiste de una lista de sus labels, empezando por la derecha, y separandolas con un punto ("."). La raíz es representada con un punto aunque generalmente se omite.

Porque cada nodo en DNS tiene exactamente una sola arista entrante (exceptuando al raíz), la etiqueta adherida a la arista también es usada como el nombre para dicho nodo. Un subárbol es llamado **dominio** o **domain** y una ruta de el nodo raíz es llamada **nombre de dominio** o **domain name**.

Los contenidos de un nodo son una colección de **registros de recursos** o **resource records**. Hay varios típos de registros de recursos.

![[dns_name_space.png]]

Un nodo en el espacio de nombres de DNS usualmente representará varias entidades al mismo tiempo. Por ejemplo un nombre de dominio es usuado para representar un dominio y una zona. En este caso el dominio es implementado por medio de varias zonas sin overlap.

Un registro SOA (start of authority) contiene información como una dirección de email del administrador de sistema responsable por la zona representada, el nombre del host donde los datos de la zona pueden ser recolectados, y así.

Un registro A (adress) representa un host particular en la [[Internet]]. El registro contiene una dirección IP de dicho host para permitir la comunicación. Si un host tiene varias direcciones IP el nodo tendrá un registro A por cada dirección.

Otro tipo de registro es el MX (mail exchange), el cual es como un link simbólico a un nodo que representa el servidor de mail.

Relacionado a los registros MX están los SRV, que contienen el nombre de un servidor para un servicio específico. El servicio en sí mismo es identificado por medio de un nombre junto con el nombre del protocolo.

Los nodos que representan una zona contienen uno o más registros NS (name server). Como los registros MX, un registro NS contiene el nombre de un servidor de nombres que implementa la zona representada por el nodo. En principio, cada nodo en el espacio de nombres puede almacenar un registro NS refiriendosé al servidor de nombres que lo implementa.

El DNS disstingue los alias de lo que se le llama **nombres canónicos** o **cannonical names**. Se supone que cada host tiene un nombre canónico o primario. Un alias es implementado por medio de almacenar n registro CNAME conteniendo el nombre canónico de un host. Este registro que contiene el nombre funciona de la misma manera que un symbolic link.

El DNS mantiene un mapeo inverso de direcciones IP a nombres de host por medio de registros PTR (pointer). Para permitir las búsquedas de nmombres de host al tener solo una dirección IP, DNS mantiene un dominio llamado *in-addr.arpa*, que contiene nodos que representan hosts de [[Internet]] que son nombrados por la dirección IP del host representado. Por ejemplo el host *www.cs.vu.nl* tiene la dirección IP 130.37.20.20 DNS crea un nodo llamado *20.20.37.130.in-addr.arpa*, la cual almacena el nombre canónico del host.

Finalmente, un registro HINFO (host info) es utilizado para almacenar información adicional del host, tal como su típo de máquina y sistema operativo (está cayendo en desuso por problemas de seguridad). De manera similar los registros TXT son usados para otro tipo de datos que el usuario encuentra útiles de almacenar sobre la entidad representada por el nodo.