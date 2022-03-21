Si consideramos que el compartir datos es fundamental en los [[sistemas distribuidos]], no sorprende que los [[Sistemas de archivos]] compartidos constituyan el fundamento de muchas aplicaciones. Los sistemas de archivo distribuidos permiten que múltiples procesos compartan datos durante largos periodos en forma segura y confiable.

### Arquitectura
La mayoría se construye siguiendo una [[Client-Server|arquitectura cliente-servidor]] tradicional, aunque también existen soluciones [[Decentralized organizations|descentralizadas]].

#### Arquitecturas cliente-servidor
Muchos sistemas de archivo distribuidos se organizan a lo largo de las líneas de arquitecturas clienteservidor, siendo el **sistema de archivo de red ([[NFS]])** de Sun Microsystem una de las más ampliamente utilizadas en los sistemas basados en [[UNIX]].

El modelo que sirve de fundamento al NFS y a sistemas similares es de un **servicio de archivos remoto**. Este modelo ofrece a los clientes un acceso transparente a un sistema de archivo gestionado por un servidor remoto. Sin embargo, los clientes normalmente desconocen la ubicación de los archivos. En cambio, disponen de una interfaz para que interactúen con el sistema de archivo similar a la interfaz ofrecida por un sistema de archivo convencional. En particular, al cliente sólo se le ofrece una interfaz que contiene varias operaciones de archivo, pero el servidor es responsable de implementarlas. Por consiguiente, a este modelo también se le denomina **modelo de acceso remoto**.

![[SSDD_fs_distribuido_modelo_de_acceso_remoto.png]]

Por contraste, en el **modelo de carga y descarga** un cliente accede a un archivo localmente después de haberlo descargado del servidor. Cuando el cliente termina con el archivo, lo carga otra vez en el servidor para que pueda ser utilizado por otro cliente. El servicio FTP de internet se utiliza de esta manera cuando un cliente descarga un archivo completo, lo modifica y luego lo repone.

#### Sistemas basados en cluster
Si consideramos que los grupos de servidores a menudo se utilizan en aplicaciones en paralelo, no sorprende que sus sistemas de archivo asociados se ajusten como corresponde. Una técnica muy conocida es desplegar **técnicas de distribución de archivos**, mediante las cuales un archivo se distribuye a través de múltiples servidores. La idea básica es simple: distribuyendo un archivo grande entre múltiples servidores, es posible buscar sus diferentes partes en paralelo. Desde luego, semejante organización funciona bien sólo si la aplicación se organiza de tal forma que el acceso a los datos en paralelo tenga sentido. Esto requiere generalmente que los datos, tal como se guardan en el archivo, tengan una estructura muy regular, por ejemplo, una matriz (densa).

![[SSDD_fs_distribuido_distribucion_de_archivos.png]]

#### Arquitecturas simétricas
Desde luego, también existen organizaciones totalmente simétricas basadas en técnicas punto a punto. Todas las propuestas actuales utilizan un sistema basado en [[DHT]] de distribución de datos, combinado con un mecanismo de búsqueda basado en una clave. Una importante diferencia es decidir si construyen un sistema de archivos sobre una capa de almacenamiento distribuido, o si archivos completos deben guardarse en los nodos participantes.

### Procesos
El aspecto más interesante con respecto a procesos de sistemas de archivo es si deberán o no ser sin estado. El [[NFS]] es un buen ejemplo que ilustra los compromisos. Una de sus características distintivas de larga duración (comparada con otros sistemas de archivo distribuidos) fue el hecho de que los servidores eran sin estado. En otros términos, el protocolo NFS no requería que los servidores mantuvieran cualquier estado de cliente. Este método se siguió en las versiones 2 y 3, pero fue abandonado en la versión 4.

La ventaja principal del método sin estado es la simplicidad. Por ejemplo, cuando un servidor sin estado se congela, esencialmente no hay necesidad de entrar a una fase de recuperación para llevarlo a un estado previo.

### Sincronización
Existen varios aspectos que requieren atención. En primer lugar, implementar la sincronización en los sistemas de archivo no sería un problema si los archivos no fueran compartidos. Sin embargo, en un sistema distribuido, la semántica de archivos compartidos se vuelve un poco engañosa cuando el desempeño está en peligro. Con esta finalidad, se han propuesto diferentes soluciones.

#### Semántica de archivos compartidos
Cuando dos o más usuarios comparten el mismo archivo al mismo tiempo, es necesario definir con precisión la **semántica de lectura y escritura** para evitar problemas. En sistemas de un solo procesador que permiten a los procesos compartir archivos, tal como [[UNIX]], la semántica establece normalmente que una operación read sigue a una operación write, la operación read regresa el valor que se acaba de escribir. Asimismo, ocurren dos operaciones write en rápida sucesión, seguidas por una operación read, el valor leído es el valor guardado por la última operación de escritura. A este modelo se lo denomina **semántica [[UNIX]]**.

En un sistema distribuido, la semántica [[UNIX]] es fácil de lograr en tanto exista sólo un servidor y los clientes no guarden los archivos en la memoria caché. Todas las operaciones read y write se van directamente al servidor de archivos, el cual las procesa estrictamente en secuencia.

En la práctica, sin embargo, el desempeño de un sistema distribuido en el cual todas las solicitudes de archivo deben dirigirse a un solo servidor con frecuencia es deficiente. Este problema a menudo se resuelve permitiendo que los clientes mantengan copias locales de archivos muy utilizados en sus cachés privados ([[replicación]] local). Con este esquema, si un cliente modifica localmente un archivo guardado en la memoria caché y poco después otro cliente lo lee desde el servidor, el segundo cliente obtendrá un archivo obsoleto.

![[SSDD_fs_distribuido_semantica_de_lectura_y_escritura.png]]

Una forma de superar esta dificultad es regresar al servidor todos los cambios a archivos guardados en la memoria caché de inmediato. Aunque este método es conceptualmente simple, en la práctica resulta ineficiente. Una solución alternativa es hacer más flexible la semántica del compartimiento de archivos. En lugar de requerir que una operación read vea los efectos de todas las operaciones previas write, se puede establecer una regla que diga: “Los cambios a un archivo abierto inicialmente son visibles sólo para el proceso (o la máquina) que lo modificó. Solamente cuando se cierre el archivo los cambios serán visibles para otros procesos (u otras máquinas).”

Esta regla es ampliamente implementada y se conoce como **semántica de sesión**. La mayoría de los sistemas distribuidos implementan semántica de sesión. Esto significa que, aunque en teoría siguen el modelo de acceso remoto, la mayoría de las implementaciones utilizan cachés locales, que efectivamente implementan el modelo de carga y descarga.

Con la semántica de sesión surge la pregunta acerca de qué sucede si dos o más clientes, al mismo tiempo, están guardando en el caché y modificando el mismo archivo. Una solución es decir que puesto que cada archivo se cierra en su oportunidad, su valor es regresado al servidor, por ello el resultado final depende de qué solicitud de cierre es la más recientemente procesada por el servidor. Una solución menos agradable, aunque más fácil de implementar, es decir que el resultado final es uno de los candidatos, pero dejar la alternativa de cuál sin especificar.

Un método completamente diferente para la semántica de compartimiento de archivos en un sistema distribuido es hacer que todos los **archivos sean inmutables**. No existe, por tanto, ninguna forma de abrir un archivo para escribir. En realidad, las únicas operaciones en archivos son create y read.

Lo que sí es posible es crear un archivo enteramente nuevo e ingresarlo al sistema de directorio con el nombre de un archivo previo existente, que entonces se vuelve inaccesible (por lo menos con ese nombre). Por tanto, aunque llega a ser imposible modificar el archivo x, sigue siendo posible reemplazar atómicamente x con uno nuevo. En otros términos, aunque los archivos no pueden ser actualizados, los directorios sí. Una vez decidido que los archivos no pueden ser cambiados en absoluto, el problema de cómo manejar dos procesos, uno de los cuales está escribiendo en un archivo y el otro está leyéndolo, simplemente desaparece y el diseño se simplifica en gran medida

Lo que queda es el problema de qué sucede cuando dos procesos tratan de reemplazar el mismo archivo al mismo tiempo. Igual que con la semántica de sesión, la mejor solución parece ser permitir que uno de los archivos nuevos reemplace al viejo, o al último o no determinísticamente.

Una cuarta forma de ocuparse de los archivos compartidos en un sistema distribuido es utilizar **[[Transacciones]] atómicas**. Resumiendo brevemente, para acceder a un archivo o grupo de archivos, un proceso ejecuta primero algún tipo de primitivo BEGIN_TRANSACTION para señalizar que lo que sigue debe ser ejecutado indivisiblemente. Entonces el sistema llama para leer y escribir uno o más archivos. Cuando el trabajo solicitado ha sido completado, se ejecuta un primitivo END_TRANSACTION. La propiedad fundamental de este método es que el sistema garantiza que todas las llamadas contenidas dentro de la transacción serán realizadas en orden, sin ninguna interferencia de otras transacciones concurrentes. Si dos o más transacciones se inician al mismo tiempo, el sistema garantiza que el resultado final será el mismo como si se estuvieran ejecutando en algún orden secuencial (no definido).

| Método              | Comentario                                                                            |
| ------------------- | ------------------------------------------------------------------------------------- |
| Semántica UNIX      | Toda operación realizada en un archivo es visible al instante para todos los procesos |
| Semántica de sesión | Ningún cambio es visible para otros procesos hasta que el archivo se cierra           |
| Archivos inmutables | No son posibles actualizaciones; simplifica el compartimentar y la replicación        |
| Transacciones       | Todos los cambios ocurren atómicamente                                                | 

### NFS
![[NFS]]