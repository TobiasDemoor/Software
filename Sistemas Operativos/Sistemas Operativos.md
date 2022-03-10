---
aliases: [sistema operativo]
---
Es la interfaz entre el usuario y el hardware. Es una máquina extendida virtual que ofrece un conjunto de funciones e [[Interfaz|interfaces]] para utilizar los recursos del hardware. Es un manejador de eventos, gestiona la ejecución de [[Proceso|procesos]] (avance de las instrucciones de los [[Programa|programas]]). Es por ello que el SO es el responsable de la [[Seguridad]] del [[Sistemas de Computación|sistema de computación]] (SC) y la [[protección]] de sus recursos.

 El SO ofrece una transparencia al usuario, es decir, crea una “ilusión” de invisibilidad del hardware al usuario.

 Su tarea principal es llevar un registro de qué [[Proceso|proceso]] está utilizando qué recursos, de otorgar las peticiones de recursos, de contabilizar su uso y de mediar las peticiones en conflicto provenientes de distintos [[Programa|programas]] y usuarios.
 
 ## Objetivos
- **Eficiencia**: Permitir que los recursos de un sistema informático se aprovechen de la mejor manera posible.
- **Usabilidad**: Pretende que el computador sea más fácil de utilizar por el usuario.
- **Capacidad de evolución** (dinamismo)
	- Permite la introducción de nuevos dispositivos (hardware) y programas en el [[Sistemas de Computación|sistema de computación]] y nuevos servicios en el SO sin interferir en el funcionamiento.
	- Evolución permanente y con aportes de terceras partes.

## Servicios que ofrece
- **Eficiencia**: Soporte para creación de [[Programa|programas]] (editores de código fuente y depuradores).
- **Ejecución de programas** (procesamiento).
- **Acceso a los dispositivos de E/S**.
- **Acceso controlado a los [[Archivo|archivos]]**.
- **Acceso al sistema**.
- **Detección y respuesta a errores**.
	- Errores internos y externos del hardware.
		- Error de memoria
		- Fallo de dispositivos.
	- Errores de software
		- Desbordamiento aritmético
		- Acceso a una posición prohibida de memoria.
	- Incapacidad del SO para satisfacer la solicitud de un proceso.
- **Contabilidad (indicadores)**.
	- Recoger estadísticas.
	- Supervisar [[Performance|rendimiento]].
	- Utilizado para anticiparse a las mejoras futuras
	- Utilizado para los [[Usuario|usuarios]] de cuotas.

### Tipos de servicios
- **Llamadas al sistema**. Las llamadas al sistema son una [[Interfaz|interfaz]] provista por el sistema operativo para que los [[Proceso|procesos]] puedan solicitar la ejecución de los servicios que provee el mismo. Son servicios atómicos, describen qué puede hacer el sistema operativo en cuestión (read, write, open, close, etc.).
	- Solicitudes de un proceso -> instrucciones. Por ejemplo, E/S en un proceso o abrir un archivo.
	- Menos granularidad al ser una instrucción (unidad mínima de procesamiento).
- **Programas del sistema**. Son facilidades para el [[Usuario|usuario]] que vienen incluidas en el sistema operativo (format, copy-paste, cambiar la hora, etc.). Usualmente son interfaces para acceder a system calls más atómicas.
	- Programas -> Comandos.
	- Mayor granularidad.
	- *Un programa del sistema es un conjunto de llamadas al sistema*.

## Ejecución del sistema operativo
Funciona de la misma manera que el software normal de una computadora, dado que es un programa ejecutado por el procesador. El sistema operativo abandona el control del procesador para que ejecute otros procesos. El SO se carga en la memoria al encender el equipo (Boot).

## El SO como administrador de recursos
El trabajo del sistema operativo es proporcionar una asignación ordenada y controlada de los procesadores, memorias y dispositivos de E/S, entre los diversos programas que compiten por estos recursos.

La administración de recursos incluye el multiplexaje (compartir) de recursos en dos formas distintas:

- *En el tiempo.* Cuando un recurso es multiplexado en el tiempo, los distintos programas o usuarios toman turnos para utilizarlo: uno de ellos obtiene acceso al recurso, después otro, y así en lo sucesivo. 
- *En el espacio.* En vez de que los clientes tomen turnos, cada uno obtiene una parte del recurso. Por ejemplo, asignar espacio en disco y llevar el registro de quién está utilizando cuáles bloques de disco es una tarea típica de administración de recursos común del sistema operativo.

## Arquitectura del SO (Núcleo)
Parte del sistema operativo se encuentra en la memoria principal, incluyendo las funciones utilizadas con más frecuencia. Esta parte imprescindible se denomina kernel. Los demás programas tales como drivers y otras funciones del SO no se cargan en memoria, no son procesos residentes en la misma.

Se puede contemplar el sistema como una serie de niveles, donde cada uno de ellos lleva a cabo un determinado subconjunto de funciones. Cada nivel se basa en el nivel inferior para llevar a cabo funciones más primitivas. De este modo, se descompone un problema en un número de subproblemas más manejables. A medida que descendemos de nivel, el nivel de [[abstracción]] disminuye, hasta llegar a los circuitos electrónicos.

- *Driver.* Software dentro del so que permite la operación lógica de un dispositivo.
- *Controlador.* Hardware que permite manipular mecánicamente un dispositivo.

### Tipos de sistemas operativos (por arquitectura - capacidades)
#### Monolítico
Sistema operativo con núcleo muy grande que es cargado completamente en memoria. No deja mucho espacio para la ejecución de procesos del usuario. Ineficiente en el manejo de memoria principal. El proceso de boot es muy largo y los tiempos de respuesta son rápidos, pero ocupan mucho espacio en memoria.

En este diseño, que hasta ahora se considera como la organización más común, todo el sistema operativo se ejecuta como un solo programa en modo kernel. El sistema operativo se escribe como una colección de procedimientos, enlazados entre sí en un solo programa binario ejecutable extenso.

#### Sistemas de capas
Sistema operativo organizado como una jerarquía de capas, cada una construida encima de la que tiene abajo. 

- En el *nivel 0* se suele manejar la asignación del procesador, cambiar entre un proceso y otro en caso de interrupciones, etc. 
- En el *nivel 1* se suele manejar la administración de la memoria. 
- En el *nivel 2* la comunicación entre procesos y operadores. 
- En el *nivel 3* se administra la E/S.
- En el *nivel 4* suelen encontrarse los programas de usuario y, finalmente. 
- En el *nivel 5* se encuentra el operador del sistema. 

A medida que se desciende de nivel, se tiene mayor privilegio. Cuando un procedimiento de un cierto nivel quiere llamar a otro de un nivel inferior, debe realizar el equivalente a una llamada al sistema; es decir, una instrucción TRAP.

#### Micro-Kernel
Con el diseño de capas, los diseñadores podían elegir en dónde dibujar el límite entre kernel y usuario. Tradicionalmente todas las capas iban al kernel, pero eso no es necesario. De hecho, puede tener mucho sentido poner lo menos que sea posible en modo kernel, debido a que los errores en el kernel pueden paralizar el sistema de inmediato. En contraste, los procesos de usuario se pueden configurar para que tengan menos poder, por lo que un error en ellos tal vez no sería fatal.

La idea básica detrás del diseño de microkernel es lograr una alta confiabilidad al dividir el sistema operativo en módulos pequeños y bien definidos, sólo uno de los cuales (el microkernel) se ejecuta en modo kernel y el resto se ejecuta como procesos de usuario ordinarios, sin poder relativamente, por lo cual se asignan solamente unas pocas funciones esenciales al núcleo. Se cargan en memoria los servicios que se solicitan y SOLO cuando son solicitados. Se asignan unas pocas funciones esenciales al núcleo, tales como el manejo de espacios de direcciones, comunicación de procesos (IPC) y servicios de planificación básica.

Así, un error en el driver del dispositivo de audio hará que el sonido sea confuso o se detenga, pero la computadora no fallará. En contraste, en un sistema monolítico con todos los drivers en el kernel, un driver de audio con errores puede hacer fácilmente referencia a una dirección de memoria inválida y llevar a todo el sistema a un alto rotundo en un instante.

Posee un booteo mucho más rápido y ocupan menor espacio en memoria, pero el tiempo de respuesta a las solicitudes de servicios es más lento dado que se deben cargar en memoria en el momento que se requiere dicho servicio.


### Evolución de los SSOO
#### *Primera generación (1945 a 1955): Procesamiento en serie*
No había un sistema operativo como tal, las operaciones con estas máquinas se realizaban desde una consola que constaban de unos indicadores luminosos, unos conmutadores (0 o 1), un dispositivo de entrada y una impresora. Eran operados únicamente por los Switcher Masters (programador + administrador + usuario).

La preparación incluía cargar un compilador, un programa fuente, salvar el programa compilado y, por último, cargar, ejecutar y descargar. La planificación de tareas era manual. Procesos rutinarios que podían automatizarse.

Toda la programación se realizaba exclusivamente en lenguaje máquina o, peor aún, creando circuitos eléctricos mediante la conexión de miles de cables a tableros de conexiones (plugboards) para controlar las funciones básicas de la máquina. Los lenguajes de programación eran desconocidos (incluso se desconocía el lenguaje ensamblador). Los sistemas operativos también se desconocían.
#### *Segunda generación (1955 a 1965). Sistemas sencillos de procesamiento por lotes: transistores y mainframes*
La introducción del transistor a mediados de la década de 1950 cambió radicalmente el panorama. Las computadoras se volvieron lo bastante confiables como para poder fabricarlas y venderlas a clientes dispuestos a pagar por ellas, con la expectativa de que seguirían funcionando el tiempo suficiente como para poder llevar a cabo una cantidad útil de trabajo.

Estas máquinas, ahora conocidas como mainframes, constaban en un monitor residente: un software que controla los programas que están en la cola (lotes) y el que se está ejecutando. Los trabajos se agrupaban por lotes. El proceso volvía al monitor al terminar su procesamiento. El monitor residente está siempre en la memoria principal y disponible para su ejecución. Primer intento de sistema operativo.

##### SO Mono Programado
Capacidad de mantener un solo programa en memoria (código en memoria). Carga P1, ejecuta P1, descarga P1… carga P2, ejecuta P2, descarga P2… etc.

#### *Tercera generación (1965 a 1980). Circuitos integrados y multiprogramación*
Se adoptaron nuevas técnicas referidas a la multiprogramación, por lo cual el SO tiene la capacidad de mantener varios programas en memoria a la vez. Se aprovechan los tiempos muertos de carga y descarga de código. Siempre hay un solo proceso en ejecución. Se populariza la técnica de spooling.

La aparición de los circuitos integrados permitió ofrecer una mayor ventaja precio/rendimiento en comparación a las máquinas de segunda generación.

Aparecen las primeras implementaciones de timesharing (tiempo compartido), una variante de la multiprogramación donde cada usuario tenía una terminal en línea para operar el computador.
##### Mono Tarea
El SO tiene la capacidad de ejecutar solo una tarea por vez.
##### Multi Tarea
El SO tiene la capacidad de ejecutar varias tareas a la vez. El tiempo de procesador se comparte entre los diversos usuarios (tiempo compartido). Se aprovechan las llamadas al sistema de los procesos (E/S) para ejecutar otra tarea. Esto genera una ilusión de “cuasi concurrencia”.

##### Mono usuario
El SO tiene la capacidad de atender un solo usuario a la vez
##### Multi Usuario
El SO tiene la capacidad de atender varios usuarios de manera concurrente. Por ello requiere un registro de usuario con identificación y autenticación de identidad.

##### Mono Procesador
El SO tiene la capacidad de trabajar con un solo procesador.
##### Multi Procesador
El SO tiene la capacidad de trabajar con varios procesadores a la vez. Los procesos comparten la misma memoria principal y secundaria, periféricos y demás, pero pueden ejecutarse en simultáneo.
####
#### *Cuarta generación (1980 - actualidad). GUI’S y computadoras personales.*	
Con el desarrollo de los circuitos LSI (Large Scale Integration, Integración a gran escala), que contienen miles de transistores en un centímetro cuadrado de silicio (chip), nació la era de la computadora personal.

Junto a las computadoras de uso personal, comenzaron a aparecer las primeras interfaces gráficas de usuario, con el fin de que cualquier persona ajena al mundo de la informática pudiera operar una computadora.

### Sistemas operativos de mainframe
Las mainframes son computadoras del tamaño de un cuarto completo que aún se encuentran en los principales centros de datos corporativos. Las mainframes también están volviendo a figurar en el ámbito computacional como servidores Web de alto rendimiento, servidores para sitios de comercio electrónico a gran escala y servidores para transacciones de negocio a negocio. 

Los sistemas operativos para las mainframes están profundamente orientados hacia el procesamiento de muchos trabajos a la vez, de los cuales la mayor parte requiere muchas operaciones de E/S. Por lo general ofrecen tres tipos de servicios: procesamiento por lotes, procesamiento de transacciones y tiempo compartido

### Sistemas operativos de servidores
Se ejecutan en servidores, que son computadoras personales muy grandes, estaciones de trabajo o incluso mainframes. Dan servicio a varios usuarios a la vez a través de una red y les permiten compartir los recursos de hardware y de software.


### SSOO Distribuidos
- Proporciona la ilusión de un único espacio de memoria principal y un único espacio de memoria secundaria (virtuales).
- Utilizado para el [[sistemas de archivos distribuidos]].
- Un sistema operativo distribuido se presenta a sus usuarios en forma de un sistema tradicional con un procesador, aun cuando en realidad está compuesto de varios procesadores.
- Los sistemas distribuidos permiten con frecuencia que las aplicaciones se ejecuten en varios procesadores al mismo tiempo.


### Tipos de SSOO (por interacción)
#### *Batch (por lotes)*
No hay dialogo Usuario-Proceso. Por ejemplo, un programa para calcular la cantidad de días de vacaciones, no permite consultar por un solo empleado, sino que requiere todos los datos cargados en un archivo y cuando se ejecuta, por ejemplo, calcula las vacaciones para todos los empleados y los imprime en pantalla.
#### *Interactivo*
Hay diálogo Usuario-Proceso, iniciado por el proceso. Por ejemplo, ejecutar un sistema que solicita un dato al usuario necesario para realizar una tarea. El proceso espera a que el usuario responda para poder seguir ejecutándose. El tiempo de respuesta depende del usuario.
#### *Tiempo Real (RTOS)*
Hay un diálogo Usuario-Proceso, iniciado por el usuario, el cual es el que le pregunta y es el proceso quien le responde. Por ejemplo, una aplicación que conste en que se le ingrese una temperatura y que ésta indique si está por prenderse fuego algo o no.

## Interrupciones
Es el mecanismo mediante el cual el SO se entera que ha ocurrido un evento que es de su interés y que debe ser atendido.

Es la interrupción de un proceso debida a un factor externo al mismo y que se lleva a cabo de tal modo que el procesador pueda atender la demanda y reanudar luego la ejecución de dicho proceso.

### Interrupciones de hardware
#### *Sincrónicas*
Se producen con una determinada frecuencia. Por ejemplo, el reloj interrumpe a cada segundo para que el SO lo plasme en la pantalla.
#### *Asincrónicas*
Provocadas por dispositivos o fallas de hardware.

### Interrupciones de software
#### *Explícitas*
Llamadas al sistema. Un proceso solicita la utilización del hardware.
#### *Implícitas*
Desbordamiento aritmético, división por cero, intento de ejecutar una instrucción ilegal, referencia a una zona de memoria fuera del espacio de direcciones permitido al usuario.

### Tratamiento de la interrupción
Cuando el SO identifica una interrupción pendiente, se detiene la ejecución del proceso de usuario y se transfiere el control al SO.

El SO identifica la interrupción por un número que usa como subíndice en el vector de interrupciones para obtener la dirección del código de la interrupción y lo ejecuta.

El SO devuelve el control al proceso de usuario que reanuda su ejecución.

1. Un proceso o dispositivo causa una interrupción.
1. El procesador verifica si hay un pedido de interrupción pendiente y atiende la que corresponda.
1. Se almacenan los datos necesarios para continuar posteriormente la ejecución del proceso (registros de datos del procesador, PC, PSW, etc.).
1. El procesador carga el PC con la ubicación de entrada de la rutina de tratamiento de la interrupción correspondiente y comienza su ejecución. 
1. Cuando el proceso de interrupción se completa, se restauran los datos necesarios para retomar la ejecución del proceso que causó la ejecución y se continúa con la misma.
### Interrupciones múltiples
#### *Secuenciales*
Termina la ejecución de la rutina de atención una interrupción para luego atender la siguiente.
#### *Anidadas*
Interrumpe (dada las prioridades) una rutina de atención de una interrupción para atender la nueva interrupción.
### Prioridad de las interrupciones
Las interrupciones de prioridad más alta pueden hacer que las de prioridad más bajas tengan que esperar (No desalojo).

Hace que se interrumpa la rutina de tratamiento de prioridad más baja (desalojo – Tiempo Real)

Por ejemplo, cuando llega una interrupción desde la línea de comunicaciones, se necesita atender ésta rápidamente para hacer lugar a nuevas entradas.

## Modo dual de protección
Es un mecanismo de protección de los recursos del SC que implementa el sistema operativo (información, procesador, memoria y dispositivos de E/S) y debe tener soporte de hardware (bit de modo en el procesador).

- El *modo Kernel* es el estado del sistema operativo en el cual tiene acceso completo a todo el hardware y puede ejecutar cualquier instrucción. Aquí se van a incluir los servicios de uso más frecuentes.
- El *modo usuario* es el estado del sistema operativo en el cual solo un subconjunto de instrucciones es permitido, aquellas que no requieren acceso al hardware. Se recurre a llamadas al sistema para E/S.

### Instrucciones privilegiadas
Comprenden las llamadas al sistema. Son aquellas que requieren la manipulación del hardware.

### Instrucciones no privilegiadas
No requieren la manipulación del hardware, pueden ser ejecutadas por el proceso. Comprenden las instrucciones lógicas tales como “a+b”.

El sistema operativo debe resolver las instrucciones privilegiadas, mientras que debe solicitar a un tercero que resuelva las no privilegiadas.

Para que el procesador conozca el tipo de instrucción que se está ejecutando, existe el *Bit de Modo* para indicar que el proceso cargado en memoria es un proceso del sistema operativo (1), que por sí solo podrá resolver la instrucción, o bien es un proceso del usuario que requerirá una llamada al sistema para resolver ciertas instrucciones (0).

## **Ejecución del sistema operativo**
Dado que el sistema operativo es un conjunto de programas y es ejecutado por el procesador como cualquier otro programa, ¿Es el SO un proceso? ¿Quién y cómo lo controla?

La ejecución del SO puede darse por procesos que se encuentran dentro de:

1. *Núcleo (fuera de todo proceso de usuario).* Ejecuta el kernel del SO fuera de cualquier proceso. El SO tiene su propia región de memoria para utilizar, así como su propia pila del sistema para controlar llamados a procedimientos y retornos de los mismos. A su vez, el mismo se encarga de completar la función de guardar el entorno del procesador y proceder a cambiar a otro proceso. Es por ello que el concepto de proceso sólo se utiliza para programas de usuario. El código del SO se ejecuta como una entidad separada que opera en modo privilegiado.
2. *Ejecución dentro de los procesos de usuario.* Software del SO en el contexto de un proceso de usuario. Un proceso se ejecuta en modo privilegiado SÓLO cuando se ejecuta el código del SO. Cuando se produce una interrupción en el programa de usuario, el procesador realiza un Mode Switch al modo kernel y le pasa el control al SO, pero sin realizar un Process Switch.