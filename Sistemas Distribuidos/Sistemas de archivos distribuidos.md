Si consideramos que el compartir datos es fundamental en los [[sistemas distribuidos]], no sorprende que los [[sistemas de archivo]] compartidos constituyan el fundamento de muchas aplicaciones. Los sistemas de archivo distribuidos permiten que múltiples procesos compartan datos durante largos periodos en forma segura y confiable.

## Arquitectura
La mayoría se construye siguiendo una [[Client-Server|arquitectura cliente-servidor]] tradicional, aunque también existen soluciones [[Decentralized organizations|descentralizadas]].

### Arquitecturas cliente-servidor
Muchos sistemas de archivo distribuidos se organizan a lo largo de las líneas de arquitecturas clienteservidor, siendo el **sistema de archivo de red ([[NFS]])** de Sun Microsystem una de las más ampliamente utilizadas en los sistemas basados en UNIX.

El modelo que sirve de fundamento al NFS y a sistemas similares es de un **servicio de archivos remoto**. Este modelo ofrece a los clientes un acceso transparente a un sistema de archivo gestionado por un servidor remoto. Sin embargo, los clientes normalmente desconocen la ubicación de los archivos. En cambio, disponen de una interfaz para que interactúen con el sistema de archivo similar a la interfaz ofrecida por un sistema de archivo convencional. En particular, al cliente sólo se le ofrece una interfaz que contiene varias operaciones de archivo, pero el servidor es responsable de implementarlas. Por consiguiente, a este modelo también se le denomina **modelo de acceso remoto**.

![[fs_distribuido_modelo_de_acceso_remoto.png]]

Por contraste, en el **modelo de carga y descarga** un cliente accede a un archivo localmente después de haberlo descargado del servidor. Cuando el cliente termina con el archivo, lo carga otra vez en el servidor para que pueda ser utilizado por otro cliente. El servicio FTP de internet se utiliza de esta manera cuando un cliente descarga un archivo completo, lo modifica y luego lo repone.

#### NFS
![[NFS]]

### Sistemas basados en cluster
Si consideramos que los grupos de servidores a menudo se utilizan en aplicaciones en paralelo, no sorprende que sus sistemas de archivo asociados se ajusten como corresponde. Una técnica muy conocida es desplegar **técnicas de distribución de archivos**, mediante las cuales un archivo se distribuye a través de múltiples servidores. La idea básica es simple: distribuyendo un archivo grande entre múltiples servidores, es posible buscar sus diferentes partes en paralelo. Desde luego, semejante organización funciona bien sólo si la aplicación se organiza de tal forma que el acceso a los datos en paralelo tenga sentido. Esto requiere generalmente que los datos, tal como se guardan en el archivo, tengan una estructura muy regular, por ejemplo, una matriz (densa).

![[fs_distribuido_distribucion_de_archivos.png]]

### Arquitecturas simétricas
Desde luego, también existen organizaciones totalmente simétricas basadas en técnicas punto a punto. Todas las propuestas actuales utilizan un sistema basado en [[DHT]] de distribución de datos, combinado con un mecanismo de búsqueda basado en una clave. Una importante diferencia es decidir si construyen un sistema de archivos sobre una capa de almacenamiento distribuido, o si archivos completos deben guardarse en los nodos participantes.

## Procesos
