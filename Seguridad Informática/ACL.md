Las **listas de control de acceso** (ACL, access control list) son listas de filtrado de [[Capa de red|capa 3]] y [[Capa de transporte|capa 4]] que se aplican en los [[Router|routers]] o [[Switch|switches]] (aunque por lo general no es conveniente usarlo en switches).
- Son listas de condiciones para acceder a una red o dispositivo
- Son una herramienta muy poderosa para controlar el acceso en ambos sentidos: tanto de entrada a la red como de salida de la misma.
- Pueden filtrar tráfico no deseado y son utilizadas para implementar [[Políticas de Seguridad de la Información|políticas de seguridad]].
- Al aplicar una AL, se obliga al router a analizar cada paquete que atraviesa una interface en un sentido específico (IN/OUT). Por lo que reduce la [[Performance|performance]] del dispositivo.

Las listas de acceso se pueden aplicar sea en el ingreso (IN) o en la salida (OUT) del paquete de una interfaz. En el caso de ingreso el paquete es procesado por la lista de acceso antes de ser enrutado al puerto de salida. Y en el de salida el paquete es conmutado hacia el puerto de salida y allí es procesado por la lista de acceso.

### Funcionamiento
- Cada paquete es comparado con cada línea de la lista de acceso en orden secuencial según han sido ingresadas. 
- La comparación se realiza hasta que se encuentra una coincidencia. 
- El final implícito de toda lista de acceso es una denegación de todo tráfico: deny all.

### Standard access-list
Son más performantes dado que no se meten en la capa de transporte. 
- En CISCO, son las AL que tienen un numero <= 100
- Filtran paquetes IP considerando únicamente la dirección origen. 
- IPX. Filtran teniendo en cuenta tanto la dirección IPX de origen como la de destino

### Extended access-list
- Filtran paquetes IP según IP origen y destino, y los números de puerto del encabezado de la capa de transporte.
- Filtran teniendo en cuenta tanto la IPX de origen como la de destino, además del número de socket del encabezado de la capa de transporte.
- Se indica el host, protocolo y puerto/s.

### Máscaras de wildcard
El uso de máscaras de wildcard permite especificar tanto un host individual como un grupo de hosts, subred o red de origen. La máscara de wildcard debe acompañar la dirección de la red, subred o host que se desea filtrar. En esta máscara, el dígito binario en 0 indica que los mismos dígitos de la dirección IP deben coincidir exactamente. son distintas a las máscaras de red en varios sentidos

### Sugerencias para su aplicación
- Solo se puede asignar una lista de acceso por interface
- Organice su lista de acceso de modo que los criterios más específicos estén al inicio.
- Si en algún momento agrega una nueva línea a la lista, esta se ubicará al final de la misma. 
- No se puede remover una línea de una lista de acceso. 
- Al menos que su lista termine con un comando permit, todo los paquetes que no coincidan con alguno de los criterios serán descartados.
- Toda lista de acceso debe tener al menos un comando permit. 
- Primero cree la lista de acceso, y luego aplíquela a la interface. 
- Las listas de acceso están diseñadas para filtrar el tráfico que atraviesa el router. No filtran el tráfico originado en el router. 
- Ubique las listas de acceso estándar lo más cerca posible del destino. 
- Ubique las listas de acceso extendidas lo más cerca posible del origen.