La virtualización permite a una aplicación, y posiblemente su entorno completo incluyendo el [[Sistemas Operativos|sistema operativo]], correr concurrentemente con otras aplicaciones pero de una manera altamente independiente del hardware subyacente, llevando esto a un alto nivel de portabilidad.

En esencia la virtualización trata con extender o reemplazar una [[Interfaz|interfaz]] existente con el fin de imitar el comportamiento de otro sistema.

### Tipos de virtualización
Para entender los tipos de virtualización primero se debe entender que los [[Sistemas de Computación|sistemas de computación]] generalmente ofrecen cuatro tipos de [[Interfaz|interfaces]] en tres niveles distintos:
1. Una interfaz entre el hardware y el software, referida como **instruction set architecture (ISA)**, formando el conjunto de intrucciones de máquina. Este conjunto se divide en dos grupos:
	* Instrucciones privilegiadas, las cuales solo pueden ser ejecutadas por el [[Sistemas Operativos|sistema operativo]].
	* Instrucciones generales, las cuales pueden ser ejecutadas por cualquier programa.
2. Una interfaz que consiste de la **llamadas al sistema** ofrecidas por el [[Sistemas Operativos|sistema operativo]].
3. Una interfaz consistente de llamadas a librerías, que generalmente forman lo que es conocido como **application programming interfaze ([[API]])**. En muchos casos, las llamadas al sistema antes mencionadas están [[Encapsulamiento|encapsuladas]] mediante una API.

La virtualización puede tomar lugar de dos formas distintas. Primero podemos construir un sistema de runtime que provee un conjunto de instrucciones abstracto que puede ser usado por las aplicaciones en ejecución. Las instrucciones pueden ser interpretadas (como en la JVM) o pueden ser emuladas (como con las aplicaciones de Windows corriendo en plataformas UNIX). Este tipo de virtualización es llamada **process virtual machine**, remarcando que la virtualización es para un solo proceso.

Una alternativa es proveer un sistema que es implementado como una capa que encapsula el hardware subyacente, pero ofreciendo simultaneamente un conjunto completo de instrucciones como [[Interfaz|interfaz]]. A esto se le llama **native [[Hipervisor|virtual machine monitor]]**. Es llamado nativo ya que se encuentra  implementado directamente sobre el harware. Notesé que esta interfaz es ofrecida a varios procesos en simultaneo. como resultado es posible tener múltiples y diferentes **guest operating systems** corriendo independiente y concurrentemente en la misma plataforma.

Una monitor de máquina virtual nativa debe proveer y regular acceso a varios recursos, como almacenamiento externo y redes. Como cualquier sistema operativo, esto implica que debe implementar drivers de dispositivo para estos recursos. En vez de rehacer todo esto, un **hosted virtual machine monitor** corre arriba de un **host operating system** de confianza. En este caso el monitor de máquina virtual puede hacer uso de las facilidades provistas por el sistema operativo anfitrión.

![[tipos_de_virtualizacion_1.png]]

### Razones
* Consolidación de servidores. Puedo tener un solo servidor físico y los demás virtualizados.
* Eficiencia energética. Puedo virtualizar varios servidores en una misma máquina.
* Administración centralizada
* Relocación. Si tengo el servidor en una MV, puedo levantar la MV en otro hardware totalmente distinto, puedo portear el servidor.
* [[Reliability|Confiabilidad]]
* [[Abstracción|Abstracción]]
