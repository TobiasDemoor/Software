*Aquellos sistemas que tienen componentes que están en distinto hardware conectados por una red.*

>**“Colección de elementos autónomos de computación que se presentan a los usuarios como un sistema único y coherente”.** - (Tanenbaum, Van Steen)

>“Sistema en el cual tenemos componentes comunicados por una red de computadoras coordinando sus acciones mediante el intercambio de mensajes” - (Coulouris et al)

## Consecuencias de la definición
- Elementos autonomos de computacion (nodos). Pueden ser dispositivos de hardware o software. Aparecen:
	- Paso de mensajes
	- Sincronización y coordinación (no hay un reloj global)
	- Manejo de grupos y seguridad
	- Organización : redes sobrepuestas
- Sistema único y coherente: los usuarios o aplicaciones lo perciben como un sistema único (es [[Transparencia|transparente]]), por lo tanto los nodos necesitan colaborar.


## ¿Qué queremos obtener?
### Soportar compartir recursos
Ejemplos canonicos
- Almacenamiento basado “en la nube” 
- Streaming multimedia asistido por redes P2P 
- Servicios de email compartido 
- Web hosting compartido (content distribution networks)

### [[Tipos de Transparencia#Transparencia de distribución]]

### Apertura 
Ser capaces de interactuar con servicios de otros sistemas abiertos, independientemente del sistema subyacente
- Los sistemas deben utilizar interfaces bien definidas 
- Deberían interoperar fácilmente 
- Portabilidad de aplicaciones 
- Fácilmente extensibles

### Escalabilidad
“capacidad de crecer a un costo razonable” 
- ¿Que es ser escalable? 
- ¿Cuanto? ¿Cómo?
Características de los algoritmos descentralizados
- Ninguna máquina tiene información completa del estado del sistema
- Las distintas máquinas toman decisiones basadas solo en información local 
- La falla de un equipo no arruina todo el algoritmo 
- No se asume que existe un reloj global

Tipos de escalabilidad
**Escalabilidad respecto del tamaño**
	¿Cúantos usuarios pueden usar mi sistema?
	Se puede solucionar en un principio con mejoras en el hardware.
**Escalabilidad geográfica**
	¿Dónde pueden estar los usuarios que utilizan mi sistema?
	La escalabilidad geográfica tiene que ver con los inconvenientes que surgen al distribuirse el sistema en distancias grandes, empieza a haber latencia considerable. Una solución a esto es al comunicación asíncrona.
**Escalabilidad administrativa**
	¿Cómo se administra mi sistema a medida que crece? (Ejemplo, República Popular China, personal)

## Políticas vs Mecanismos
### Políticas
- ¿Qué tipo de consistencia requerimos para los datos en el cache de cliente? 
- ¿Que operaciones permitimos realizar a código descargado? 
- ¿Como podemos acomdar el tipo de requerimientos cuando el ancho de banda varía? 
- ¿Qué grado de secreto necesitamos para la comunicación?

### Mecanismos 
- Permitir la modificación dinamica de las politicas de caching 
- Soportar diferentes niveles de confianza para código movil 
- Proveer parámetros ajustables de calidad de servicio por stream de datos 
- Ofrecer la posibilidad de distintos algoritmos de cifrado

## Errores frecuentes
Cuando se viene de diseñar sistemas centralizados a diseñar sistemas distribuidos hay una serie de suposiciones que son erroneas:
- La red es confiable
- La red es segura
- La red es homogénea
- La topología no cambia
- La latencia es cero
- El ancho de banda es infinito
- El costo del transporte es cero
- Existe un administrador

## Tipos de sistemas distribuidos
