La escalabilidad es la capacidad de crecer a un costo razonable.

#### Dimensiones de la escalabilidad
La escalabilidad de un sistema puede medirse sobre tres dimensiones distintas:

* **Escalabilidad respecto del tamaño.** Poder añadir usuarios al sistema sin tener una pérdida de performance. Si tenemos un solo servidor centralizado corriendo en una sola computadora, muy posiblemente tenga problemas ante múltiples request. Utilizar un grupo de servidores que colaboran entre sí es una mejor opción.
* **Escalabilidad geográfica.** La escalabilidad geográfica tiene que ver con los inconvenientes que surgen al distribuirse el sistema en distancias grandes, empieza a haber [[Latencia|latencia]] considerable. Una solución a esto es al comunicación asíncrona.
* **Escalabilidad administrativa.** Puede cambiar el sistema dependiendo de las cuestiones legales de los países donde se esté ejecutando. Se deben tener en cuenta posibles ataques provenientes de los nuevos dominios (Ejemplo, República Popular China, personal).

#### Técnicas de escalabilidad
En la mayoría de los casos, los problemas de escalabilidad aparecen como problemas causados por límites de capacidad de los servers y la red, por lo que incrementar la memoria RAM, los CPUs o reemplazar módulos de red deberían ayudar a ampliar la red. Cuando se trata de escalar la red, existen tres principales técnicas:

* **Ocultar latencia de comunicación.** Es aplicable en el caso de **escalabilidad geográfica**, cuando los límites físicos son quienes causan la latencia y no tenemos muchas soluciones para solventarlo. Consta de construir la aplicación de modo que solo se comunique de manera asíncrona. De esta manera, no generamos una espera activa del lado del cliente. En algunos casos, el usuario no tiene nada mejor que hacer que esperar la respuesta, por lo que dicha solución no es conveniente y es preferible reducir las comunicaciones en general, moviendo parte de la funcionalidad a la aplicación del cliente.
* **Particionar y distribuir.** Consiste en tomar un [[Componente|componente]], dividirlo en varias partes más pequeñas y repartir esas partes a lo largo del sistema. Por ejemplo, [[DNS]] procesa las url mediante un árbol que divide las partes genéricas (dominio, por ejemplo) y las extensiones que refieren a las regiones.
* **Replicación.** Replicar componentes a lo largo del sistema distribuido, incrementando la disponibilidad y la performance del mismo. Además, puede solventar problemas de la escalabilidad geográfica al poder replicar nodos en distintas regiones. La replicación llevan a problemas de consistencia entre las copias. Actualizar cada replica es muy costoso ([[Transparencia de distribución#Transparencia de replicación|Transparencia de replicación]]).
	* **Caching.** Es una forma especial de replicación. Se almacena la copia de un recurso, generalmente en un lugar de más rápido acceso para el usuario.