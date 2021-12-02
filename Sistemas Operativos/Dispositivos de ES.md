## **¿Qué es un dispositivo de entrada/salida?**
Un dispositivo de E/S es todo aquel dispositivo que sea externo al entorno de ejecución puro (Procesador + memoria, es lo mínimo que necesita un proceso para ejecutarse). Es utilizado por el procesador y los procesos para comunicar información al entorno.
### Ejemplos
Teclado, mouse, pantalla. Clásicos.

Discos de almacenamiento, tarjetas de red, placas de video también lo son.

## **Clasificación de Tanenbaum**
### Dispositivos de bloques
- Todos aquellos cuya mínima unidad de tratamiento de datos es un bloque de tamaño fijo. Por ejemplo, discos rígidos, pendrives, etc.
- Bloques referenciados y direccionados unívocamente.
- Cada operación es independiente de las demás.

### Dispositivos de carácter
- Mínima unidad de tratamiento de datos: carácter (byte).
- No hay forma de referenciarlos ni son direccionables.
- Operan con flujos de caracteres sin importar la estructura.
- Por ejemplo, teclado envía caracteres y ni a él ni al sistema le interesan referenciarlos como tal. Otros ejemplos son el mouse, la impresora, la placa de red.

## **Clasificación de Stallings**
### Legibles por humanos
Adecuados para dialogar con las personas (teclados, mouse, monitor, impresora).

### Legibles por máquina
Adecuados para dialogar con máquinas electrónicas, pero no con humanos (disco rígido, pendrive). El SO abstrae el disco rígido y uno llega a pensar que se comunica con el mismo, pero no.

### Comunicación
Adecuados para dialogar con otros dispositivos que están a largas distancias (placa de red, módem).

## **Diferencias según su naturaleza – Stallings**
### Velocidad de transferencia de datos
Los dispositivos que dialogan con el ser humano suelen ser más lentos, dado que se debe limitar a la percepción de los sentidos humanos. Un claro ejemplo es la pantalla, que debe mostrar figuras que sean distinguibles por el humano, el humano no puede diferenciar 30 cuadros en un mismo segundo, por lo que hay mucha redundancia. Además, el ser humano hace foco en una cierta parte de la pantalla.

### Aplicación
Según el uso que se le dé a cada dispositivo será el software necesario para operar en él. Un disco puede ser utilizado para almacenar archivos en un file-system o actuar como espacio para memoria virtual (configuración totalmente distinta). Distinto software estará asociado, pero el hardware es el mismo.

### Conjunto de operaciones
#### *Solo lectura*
Mouse, teclados.
#### *Solo escritura*
Impresora.
#### *Lectura/escritura*
Discos rígidos, pendrives.

### Unidad de transferencia
Los datos pueden ser transferidos mediante un stream de bytes o caracteres (teclado, ratón) o en bloques (discos de E/S).

### Complejidad de control
- Cuantas más operaciones pueda desempeñar, mayor es el control. 
- Los dispositivos de lecto-escritura suelen tener más complejidad de control. 
- Ejemplo: La impresora posee una interfaz de control más sencilla que el disco rígido.

### Representación de los datos
- Diferentes esquemas de codificación son usados por cada dispositivo.
- Diferente manejo de los datos entre los dispositivos. Cada dispositivo almacena a su manera.

### Condiciones de error
#### *Críticos*
Ejemplo: lectura de un bloque defectuoso. Pérdida de información en un disco. No hay solución sin backup.
#### *No críticos*
Ejemplo: no tiene papel la impresora. Puede continuarse con la impresión solucionando el problema.


## **Objetivos del SO frente a los dispositivos de E/S**
### Rendimiento (Maximizar la eficiencia)
Debido a la notable diferencia de velocidad entre el procesador y los dispositivos de I/O.
### Independencia del dispositivo (abstracción del hardware)
Capacidad del sistema operativo de brindar una visión lógica simplificada de los dispositivos de E/S hacia los usuarios, procesos y otros componentes el sistema.
## **Capas del esquema de Entrada/Salida**
### Proceso de usuario
Se realiza una llamada al sistema a través de una interrupción de E/S. Por ejemplo, guardar un documento.

### Scheduler de I/O
Se encarga del manejo de la cola y el control de las operaciones de E/S. Además, maneja las interrupciones recolectando el estado de los dispositivos y reportando el mismo. Interactúa con el módulo de E/S.

### Módulo de E/S del SO
Es un software independiente del dispositivo.  Trata con dispositivos lógicos, sin conocer los detalles para controlar realmente el dispositivo. Maneja operaciones básicas de E/S requeridas por los procesos de usuario, tales como open, close, read y write.
#### *Funciones*
- *Nombramiento de los dispositivos.* Utilizar cadenas de caracteres amigables asociando los nombres lógicos a los físicos (por medio de tablas).
- *Resolver errores.* Los que no se resolvieron hasta ese nivel (ejemplo bloque defectuoso). Debe traducir los códigos de error del controlador del dispositivo.
- *Control de concurrencia.* Asignar y liberar los dispositivos de uso exclusivo o dedicado. Ejemplo: dos procesos quieren transmitir por la placa de red al mismo tiempo.
- *Protección.* Evita que procesos utilicen dispositivos indiscriminadamente. 
- *Seguridad.* Controles de acceso.
- *Control de flujo de operaciones.* Buffering y spooling.

#### *Buffering*
Técnica que permite superponer la carga de datos a memoria con la ejecución del proceso. Podemos hacer algo con el proceso mientras voy cargando a memoria la información que necesito para este u otro proceso.

Dispone de un espacio de memoria principal para regular el intercambio de datos entre los procesos y los dispositivos de E/S, impidiendo pérdidas de información por desbordes o bajas de performance por insuficiencia de datos.

Por ejemplo, antes era más notoria la espera de carga del video. 


#### *Spooling*
Técnica que permite superponer la descarga de datos de memoria con la ejecución del proceso. 

Dispone de un espacio en memoria secundaria como un buffer de almacenamiento persistente para reducir la espera cuando los procesos transfieren datos a dispositivos periféricos.

Por ejemplo, cuando enviamos a imprimir un documento, Word envía este archivo a una zona de spooling en la memoria secundaria, de la cual otro proceso (el de la impresora en este caso) levantará el archivo para imprimirlo. Mientras tanto, el usuario puede seguir utilizando Word.


### Driver
Transforman las operaciones genéricas que le pasa el SO en comandos específicos que el controlador interpreta. Es software específico del dispositivo, pero posee la capacidad de hablar de manera genérica con el SO.

### Controlador - Adapter
Transforman los comandos a flujos de bits y los entregan al dispositivo y al bus del sistema. Es hardware que se comunica directamente con los buses de datos del dispositivo. 

### Dispositivo
Ejecuta físicamente la operación que el controlador le solicitó.


## **Evolución de las técnicas de E/S**
### E/S programada
El procesador envía un mandato de E/S, a petición de un proceso, a un dispositivo de E/S; a continuación, ese proceso realiza una espera activa hasta que se complete la operación antes de continuar.  El procesador pregunta periódicamente si la E/S finalizó, ocupando tiempo de procesador. Usualmente los bloques no podían viajar todos juntos por el bus de datos, por lo que una vez cargados en el buffer del disco de E/S, debían ser solicitados de a un fragmento de datos a la vez.


### E/S dirigida por interrupciones
El procesador emite un mandato de E/S a petición de un proceso. Si la solicitud de E/S requiere suspender el proceso, este se suspende y se carga otro proceso en el procesador para ser ejecutado. Luego, el proceso actual es interrumpido por el mismo módulo de E/S cuando la solicitud haya sido satisfecha. En esta técnica, todavía se debía recuperar la información bloque a bloque, por lo que se debía interrumpir cada vez que se requiera transferir un fragmento, por lo que el procesador está altamente implicado en el control de la operación de E/S.

### Entrada Salida por Acceso Directo a Memoria (DMA)
Un módulo de DMA controla el intercambio de datos entre la memoria principal y el dispositivo de E/S. El procesador manda una petición de transferencia de un bloque de datos al módulo de DMA y resulta interrumpido sólo cuando se haya transferido el bloque completo. De esta manera, las operaciones de E/S son resueltas por el DMA y no por el procesador. Se optimiza el tiempo ocioso.

#### *Módulos de E/S*
Los módulos de E/S se convierten en un procesador independiente con un set de instrucciones específicamente pensadas para operaciones de E/S. De esta manera, el procesador central le indica al módulos o canal de E/S que ejecute un programa de I/O en memoria principal, de modo que el CPU ya no tiene que intervenir ni ocupar tiempo en estas operaciones. 

Más adelante, se incorporaron a estos módulos de E/S una memoria local propia, de form a que se pueda controlar una gran cantidad de dispositivos de E/S de manera independiente, con mínima intervención del CPU.



#### *Funcionamiento de la técnica*
Cuando el procesador desea leer o escribir un bloque de datos, emite un comando al módulo de DMA con la siguiente información:

- Tipo de operación (R/W).
- Dirección del dispositivo de E/S involucrado.
- Dirección inicial de memoria a leer o escribir.
- La cantidad de palabras a leer o escribir.

Luego, el procesador continúa con otro proceso. El DMA se encarga de transferir el bloque directamente de la memoria palabra por palabra sin necesidad de utilizar el procesador. Cuando la transferencia se completa, el DMA envía una señal de interrupción al procesador. De esta manera, el procesador solo está involucrado en el inicio y el fin de las operaciones de E/S



Por otra parte, el DMA utiliza el bus de datos del sistema para comunicarse con los dispositivos de I/O, y lo realiza mediante una E/S programada para cada palabra que transfiere. Esto implica dos ciclos de bus por cada palabra del bloque que se lea o escriba. Para solucionar este problema, varios sistemas implementan un bus de E/S que conecta los dispositivos directamente con el DMA, de modo que éste no interfiere en el bus del sistema para transferir palabras, sino únicamente para recibir comandos para iniciar una operación de E/S y para enviar la interrupción que indique el fin de la misma.


## **Discos Rígidos**
### ¿Por qué optimizar su rendimiento?
- La capacidad de proceso ha aumentado un 40% cada año, mientras que el rendimiento de los discos rígidos solo ha mejorado un 50% durante la última década. 
- Los discos RIGIDOS llegaron a un límite mecánico.
- En todo sistema la velocidad más lenta es la más determinante. 
- Son un cuello de botella.

### Estructura de un disco
A nivel lógico, es un arreglo de bloques consecutivos.

- *Pistas.* Círculos concéntricos sobre el plato donde se sitúa la cabeza lectora.
- *Cilindro.* Conjunto de pistas alineadas verticalmente en los distintos platos. Proyección en vertical de las pistas entre todos los platos.
- *Sector.* Subdivisión dentro de las pistas.
- *Bloque.* Mínima unidad de almacenamiento utilizada por el disco. Intersección pista/sector.
- *Cabezal.* Dispositivo que efectúa la lectoescritura.
- *Brazo.* Extensión mecánica que ubica el cabezal.

### Tiempo de lecto escritura (tiempo de acceso a datos)
Tacceso=Tbusqueda+Tlatencia+Ttransferencia

#### *Tiempo de búsqueda*
Tiempo de seek. Tiempo que tarda el cabezal lector en desplazarse desde la pista en la que está a la que corresponde leer.

Tbúsqueda=Tarranque+Tdesplazamiento

- El *tiempo de arranque* es el tiempo que tarda el cabezal en acelerar hasta llegar a una velocidad constante.
- Tdesplazamiento=Tcilindro\*Ncilindros El único tiempo mejorable por el sistema operativo. Es el tiempo que tarda en recorrer las pistas.

#### *Tiempo de latencia*
Tiempo que tarda el plato en girar para colocar el inicio del sector correspondiente debajo de la cabeza lectora.

Se estima como un promedio entre el mejor tiempo (cuando el cabezal se encuentra justo arriba del sector) y el peor tiempo (cuando el cabezal tiene que esperar toda una vuelta del plato para estar arriba del sector).

Tlatencia=Trotación2
#### *Tiempo de transferencia*
Tiempo que se tarda en leer el sector. 

Ttransferencia=Nbloques\*TrotacionMbloquescilindro= TrotacionSectores por pista

### **Algoritmos de scheduling de disco**
### FCFS
Primera solicitud en llegar, primera en ser satisfecha.

- *Ventaja.* El más justo desde el punto de vista del orden de llegada. Simple de implementar.
- *Desventaja.* Al no poder atender desordenadamente, una secuencia intercalada sobre anillo y orilla puede ocasionar demasiado movimiento en el brazo (que se pidan leer secuencialmente sectores muy lejanos).



### Shortest Service Time First puro
Primero la lectura más cercana, aquella que requiera el menor movimiento del brazo del disco desde su posición actual.

- *Ventaja.* Elimina el problema de exceso de desplazamientos del brazo, disminuye el tiempo de búsqueda. 
- *Desventaja.* Posibles solicitudes sin atender durante largos períodos de tiempo.

### SCAN
El brazo barre de anillo a orilla y satisface todas las peticiones que se encuentren en la ruta hasta que llega a la pista final del plato y realiza el recorrido en sentido contrario.

- *Ventaja:* No tiene las desventajas ni de FCFS ni de SSTF. Movimiento simple del brazo. 
- *Desventajas.* Una solicitud que cae por detrás del lector debe esperar 2 recorridos de la superficie atendiendo solicitudes (ida y vuelta). Cuando no hay más solicitudes hasta llegar a la orilla igual el brazo recorre los cilindros restantes.

### C-SCAN
Ídem SCAN, pero solo lee en un sentido y vuelve sin leer.

- *Ventaja sobre SCAN.* Como máximo se espera 1 recorrido de superficie leyendo.

### C-LOOK
Misma lógica que C-SCAN, pero no llega a la orilla sino a solicitud más cercana a ella, y luego vuelve.

### N-step-SCAN and FSCAN
Con las técnicas de SSTF, SCAN, C-SCAN y C-LOOK, si un proceso realiza continuamente en una pista, pueden monopolizar el dispositivo entero repitiendo peticiones en esa misma pista. 

N-step-SCAN segmenta la cola de peticiones de disco en sub colas de longitud N. Estas sub colas son procesadas una a la vez, usando SCAN. Mientras una cola está siendo procesada, las peticiones nuevas deben ser añadidas a otra subcola. 

Si existen menos de N peticiones al finalizar el SCAN, entonces todas son procesadas con el siguiente SCAN. 

Si N es muy grande, se asimila a SCAN.

Si N=1, se a simila a FIFO.

FSCAN es una política que utiliza dos sub colas. Cuando empieza el SCAN, todas las peticiones se encuentran en una sola cola, mientras la otra se encuentra vacía. Durante el SCAN, todas las nuevas peticiones son almacenadas en la otra cola.

## RAID
![[RAID]]