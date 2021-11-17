---
aliases: [e-mail]
---

La arquitectura del sistema, que consiste en dos tipos de subsistemas: los **agentes de usuario (UA)**, que permiten a la gente leer y enviar correo electrónico, y los **agentes de transferencia de mensajes (MTA)**, que mueven los mensajes del origen al destino. También nos referiremos a los agentes de transferencia de mensajes de una manera informal como **servidores de correo**.

![[RRCC_correo_electronico_arquitectura.png]]

El agente de usuario es un programa que proporciona una interfaz gráfica, o algunas veces una interfaz basada en texto y comandos, que permite interactuar con el sistema de correo electrónico. Incluye un medio para redactar mensajes y respuestas a éstos, desplegar los mensajes entrantes y organizarlos al archivarlos, realizar búsquedas y eliminarlos. El acto de enviar nuevos mensajes al sistema de correo para su entrega se conoce como **envío de correo**.

Los agentes de transferencia de mensajes son en general procesos del sistema. Se ejecutan en segundo plano en equipos servidores de correo con la intención de estar siempre disponibles. Su tarea es mover de manera automática el correo electrónico a través del sistema, desde el que lo originó hasta el receptor mediante el **SMTP (Simple Mail Transfer Protocol)**. Éste es el paso de transferencia del mensaje.

El SMTP se especificó originalmente como el [[RFC]] 821 y se revisó para convertirse en el RFC 5321 actual. Envía el correo electrónico sobre las conexiones y devuelve el estado de entrega, junto con los errores.

Los agentes de transferencia de mensajes también implementan las **listas de correo**, en donde se entrega una copia idéntica de un mensaje a cualquiera de los miembros en una lista de direcciones de correo electrónico. Otras características avanzadas son las copias al carbón, copias al carbón ocultas, correo electrónico de alta prioridad, correo electrónico secreto (es decir, cifrado), destinatarios alternativos si el primario no está disponible en ese momento, y la habilidad de que los asistentes lean y respondan el correo electrónico de sus jefes.

Vincular los agentes de usuario y los agentes de transferencia de mensajes son los conceptos de los buzones de correo y un formato estándar de mensajes de correo electrónico. Los buzones de correo almacenan el correo electrónico que recibe un usuario. Los servidores de correo se encargan de su mantenimiento. Para ello, los agentes de usuario envían comandos a los servidores de correo para manipular los buzones de correo, inspeccionar su contenido, eliminar mensajes, etc. Con esta arquitectura, un usuario puede usar distintos agentes de usuario en varias computadoras para acceder a un buzón de correo. 

El correo se envía entre un agente de transferencia de mensajes y otro en un formato estándar conocido como MIME, el mismo que es usado en [[HTTP]].

Una idea clave en el formato de los mensajes es la distinción entre el **envelope** (envoltura) y su contenido. La primera encapsula el mensaje y contiene toda la información necesaria para transportarlo, como la dirección de destino, la prioridad y el nivel de seguridad, todo lo cual es distinto del mensaje en sí. Los agentes de transporte de mensajes usan el envelope para el enrutamiento, al igual que la oficina postal con el correo convencional.

El mensaje dentro de la envoltura consiste en dos partes separadas: el **encabezado** y el **cuerpo**. El primero contiene la información de control para los agentes de usuario. El cuerpo es exclusivo para el destinatario humano; a ninguno de los agentes le importa mucho.

![[RRCC_correo_electronico_disposicion.png]]

### Formatos de mensaje
Los mensajes consisten en una envoltura primitiva (descrita como parte del [[SMTP]] en el [[RFC]] 5321), cierto número de campos de encabezado, una línea en blanco y después el cuerpo del mensaje. Cada campo de encabezado consiste (lógicamente) en una sola línea de texto ASCII que contiene el nombre del campo, un signo de dos puntos y para la mayoría de los campos un valor.

En la siguiente tabla se listan los principales campos de encabezado.

| Encabezado   | Significado                                                                |
| ------------ | -------------------------------------------------------------------------- |
| To:          | Dirección(es) de correo electrónico del (los) recipiente(s) primario(s).   |
| Cc:          | Dirección(es) de correo electrónico del (los) recipiente(s) secundario(s). |
| Bcc:         | Dirección(es) de correo electrónico para las copias al carbón ocultas.     |
| From:        | Persona o personas que crearon el mensaje.                                 |
| Sender:      | Dirección de correo electrónico del emisor actual.                         |
| Received:    | Línea que agrega cada agente de transferencia a lo largo de la ruta.       |
| Return-path: | Se puede usar para identificar una ruta de vuelta al emisor.               |

*To:* proporciona la dirección DNS del destinatario principal. También se permite tener varios destinatarios.

*Cc:* proporciona las direcciones de los destinatarios secundarios. En términos de entrega, no hay distinción entre los destinatarios primarios y los secundarios. Es una diferencia totalmente psicológica que podría ser importante para las personas involucradas, pero para el sistema de correo no lo es. El término *Cc:* (Copia al carbón) es un poco obsoleto, ya que las computadoras no usan papel de carbón, pero está bien establecido.

*Bcc:* (Copia al carbón oculta) es como el campo *Cc:*, sólo que esta línea se elimina de todas las copias que se envían a los destinatarios primarios y secundarios. Esta característica permite a las personas enviar copias a terceros sin que los destinatarios primarios y secundarios se enteren de ello.

Los siguientes dos campos, *From:* y *Sender:*, indican quién escribió y envió el mensaje, respectivamente. No necesitan ser iguales. Por ejemplo, un ejecutivo de negocios puede escribir un mensaje, pero su secretaria podría ser la que lo transmita. En este caso, el ejecutivo estaría listado en el campo *From:* y la secretaria en *Sender:*. *From:* es necesario, pero el campo *Sender:* se puede omitir si es igual a *From:*. Estos campos son necesarios en caso de que el mensaje no se pueda entregar y deba devolverse al remitente

Se agrega una línea que contiene *Received:* por cada agente de transferencia de mensajes a lo largo de la trayectoria. La línea contiene la identidad del agente, la fecha y hora de recepción del mensaje, e información adicional que puede servir para depurar el sistema de enrutamiento.

El campo *Return-Path:* lo agrega el agente de transferencia de mensajes final y estaba destinado para indicar la manera de regresar al emisor. En teoría, esta información puede tomarse de todos los encabezados *Received:* (con excepción del nombre del buzón del emisor), pero pocas veces se llena de esta manera y por lo general contiene sólo la dirección del remitente.

Además de los campos anteriores, los mensajes del RFC 5322 también pueden contener una variedad de campos de encabezado usados por los agentes de usuario o los destinatarios. A continuación se listan los más comunes.

| Encabezado   | Significado                                                              |
| ------------ | ------------------------------------------------------------------------ |
| Date:        | Fecha y hora de envío del mensaje.                                       |
| Reply-To:    | Dirección de correo electrónico a la que se deben enviar las respuestas. |
| Message-Id:  | Número único para hacer referencia a este mensaje después.               |
| In-Reply-To: | Identificador del mensaje al que éste responde.                          |
| References:  | Otros identificadores de mensaje relevantes.                             |
| Keywords:    | Palabras clave seleccionadas por el usuario.                             |
| Subject:     | Resumen corto del mensaje para desplegar en una línea.                   |

El campo *Reply-To:* a veces se usa cuando ni la persona que redactó el mensaje ni la que lo envió quieren ver la respuesta. Por ejemplo, suponga que un gerente de marketing escribe un mensaje de correo electrónico para informar a los clientes sobre un nuevo producto. El mensaje lo envía una secretaria, pero *Reply-To:* indica el jefe del Departamento de Ventas, quien puede contestar preguntas y surtir pedidos. Este campo también es útil cuando el emisor tiene dos cuentas de correo electrónico y desea que la respuesta llegue a su otra cuenta.

El campo *Message-Id:* es un número que se genera de manera automática y se utiliza para enlazar mensajes (por ejemplo, cuando se usa en *In-Reply-To:*), además de evitar la entrega de duplicados.

El documento RFC 5322 indica explícitamente que los usuarios pueden inventar encabezados opcionales para su propio uso privado. Por convención desde el RFC 822, estos encabezados empiezan con la cadena *X-*. Se garantiza que no habrá encabezados futuros que usen nombres que comiencen con *X-*, con el fin de evitar conflictos entre los encabezados oficiales y los privados.

### SMTP
![[SMTP]]

### Transferencia de mensajes
Una vez que el agente de transferencia de mensajes recibe un mensaje del agente de usuario, lo entrega al agente de transferencia de correo receptor mediante SMTP. Para ello, el emisor usa la dirección de destino.

Para determinar el correo servidor de correcto que se debe contactar, es necesario consultar al [[DNS]]. En este caso se realiza una consulta DNS sobre los registros MX del dominio correspondiente. Esta consulta devuelve una lista ordenada de los nombres y direcciones IP de uno o más servidores de correo.

A continuación, el agente de transferencia de correo emisor realiza una conexión TCP en el puerto 25 a la dirección IP del servidor de correo para comunicarse con el agente de transferencia de correo receptor, y usa SMTP para transmitir el mensaje. A su vez, el agente de transferencia de correo receptor colocará el correo para el usuario en el buzón correcto para que lo lea después. Tal vez en este paso de entrega local sea necesario mover el mensaje entre computadoras, si hay una gran infraestructura de correo.

Con este proceso de entrega, el correo viaja del agente de transferencia de correo inicial al agente final en un solo salto. No hay servidores intermedios en la etapa de transferencia del mensaje. Sin embargo, es posible que este proceso de entrega ocurra varias veces.

### Entrega final
En la actualidad es probable que el agente de usuario en una PC, laptop o equipo móvil se encuentre en una máquina distinta al servidor de correo del ISP o de la empresa. Los usuarios desean acceder a su correo en forma remota, desde cualquier lugar en donde se encuentren. En esta configuración, la tarea del agente de usuario es presentar una vista del contenido del buzón de correo y permitir que éste se manipule en forma remota. Se pueden usar varios protocolos distintos para este fin, pero SMTP no es uno de ellos.

![[IMAP]]

