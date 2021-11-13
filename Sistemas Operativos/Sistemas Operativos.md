Es la interfaz entre el usuario y el hardware. Es una máquina extendida virtual que ofrece un conjunto de funciones e [[Interfaz|interfaces]] para utilizar los recursos del hardware. Es un manejador de eventos, gestiona la ejecución de [[Proceso|procesos]] (avance de las instrucciones de los [[Programa|programas]]). Es por ello que el SO es el responsable de la seguridad del [[Sistemas de Computación|sistema de computación]] (SC) y la protección de sus recursos.

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
	- Supervisar rendimiento.
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
