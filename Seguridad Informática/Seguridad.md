---
aliases: ["seguridad"]
---
 La **seguridad** es un concepto muy amplio, que va más allá de la informática, es un concepto instalado en la sociedad y está íntimamente relacionado con los **riesgos**. 
 
La seguridad es una medida de [[Reliability|fiabilidad]] del [[Sistemas de Computación|sistema de computación]] relacionada, fundamentalmente a la garantía de la **[[Integridad|integridad]]** del propio SC y de la capacidad de discriminar el acceso al mismo. Es una característica que implica que un sistema está libre de peligro, daño o riesgo.

> La seguridad es una **tendecia**, algo a buscar.

Fundamentalmente queremos proteger el hardware, el software, los datos y principalmente **la información**.

Hay cuatro tipos de ataques generales, no solo en el contexto de [[Sistema de Información|sistemas de información]] sino también cuando se habla de seguridad en general:
1. **Interrupción**: consiste en que un objeto del sistema se pierda, quede inutilizable o no disponible. Ejemplos de estos ataques son desde desconectar físicamente un equipo hasta un DOS.
2. **Interceptación**: acceso no autorizado a un objeto del sistema. Un ejemplo claro de esto es el **snooping** donde un actor malicioso intercepta paquetes mandados a través de una red (por ejemplo si se usa un medio inalámbrico o una conexión cableada no conmutada). Este tipo de ataque **no agrega latencia** por lo tanto es muy difícil de detectar.
3. **Modificación**: consiste en interceptar y modificar un mensaje. Esto podría ocurrir con un [[Proxys|server proxy]] que recibe y reenvia mensajes, posiblemente modificandolos. Una característica de este tipo de ataque es que **agrega latencia** ya que hay un proceso intermedio en al comunicación, y gracias a esto se puede detectar con relativa facilidad.
4. **Fabricación**: directamente se fabrica un nuevo objeto.

Nos queremos proteger de 3 agentes:
1. **Personas**
	1. Personal (accidentes por error o desconocimiento)
	2. Ex-empleados
	3. Curiosos (atacantes no destructivos)
	4. Crackers (scanners, expoits)
	5. Terroristas (ataques a DB, WEBS, etc.)
	6. Intrusos remunerados (pagos por otras empresas)
2. **Amenazas lógicas**
	1. Software incorrecto (bugs, etc.)
	2. Herramientas de seguridad (las mísmas herramientas que permiten detectar intrusos se pueden utilizar para atacar)
	3. Backdoors
	4. Bombas lógicas (activadas ante un evento)
	5. Canales cubiertos
	6. Virus
	7. Gusanos (se propagan a través de una red, son los "portadores" de un virus)
	8. Caballos de troya
	9. Programas conejo o bacteria
	10. Técnicas  Salami
3. **Catastrofes**
	1. Naturales
	2. Artificiales

Y para protegernos hay 4 mecanísmos de seguridad generales:
1. **Prevención**
2. **Detección**
3. **Recuperación**
4. **Análisis forense**

## Seguridad de la Información
![[Seguridad de la Información]]

%%
## Resumen Polo
- Cuando decimos que una ciudad es segura o insegura, estamos hablando de una “medida” o “grado” de la ciudad en relación a los riesgos a los que uno se expone viviendo en ella. Riesgo, por ejemplo, de que te maten o te roben en la ciudad. 
- La seguridad es una medida de confiabilidad del sistema (en general, en sentido amplio).
  - Incluso el sistema “ciudad”, “casa”, “persona” tiene su medida en términos de seguridad. 
  - Así, podemos pensar en los riesgos en una casa e implementar mecanismos para mitigarlos. Por ejemplo: puerta con llave, alarma, rejas, un vigilante en la puerta, etc.
  - **Todos estos mecanismos intentan que nadie no autorizado entre a la casa.**
- Cuantos más mecanismos de seguridad tengamos, “más seguridad” tendremos menos riesgo.
- Los mecanismos de seguridad suman su efecto más que linealmente.
- La seguridad es una medida de confiabilidad que está dada por la suma de los efectos potenciales de los mecanismos de seguridad implementados (dado por el “eslabón más débil de la cadena”).
  - **Cualquier “amenaza” u oportunidad que no consideremos o no abordemos con nuestros mecanismos de seguridad constituye una “vulnerabilidad” para el objeto en cuestión.**
- El humano es el responsable de la seguridad. Decide qué riesgos quiere correr y cuánta seguridad quiere.
- La seguridad es una inversión.

## **Mecanismos a priori y a posteriori**
Hay mecanismos de seguridad que actúan a **priori** (alarma, puerta con llave, sistema antimisiles, etc.) que tratan de evitar el incidente de inseguridad.

Hay otros mecanismos que actúan a **posteriori** (seguro contra incendios), tratando de reparar el efecto ocasionado por el incidente.

Con todos ellos llegamos a cierto punto o nivel, **la garantía o “seguridad total” no existe. El riesgo siempre está. Tratamos de minimizarlo.**

### Control de acceso
Cuando hablamos del **Control de Acceso**, nos referimos a la capacidad de verificar que solamente acceda al sistema quien está autorizado para ello.

### Dimensión ambiental.
- Tanto la integridad como el control de acceso a un Sistema de Computación van más allá del sistema propiamente dicho. Tienen que ver, antes que nada, con aspectos ambientales. Por ejemplo, si instalamos el pc del servidor en la vereda.
- Esta dimensión tiene que ver con el acceso y cuidado de la integridad del sistema en su conjunto desde el punto de vista físico.
- En esta dimensión se incluyen inundaciones, problemas eléctricos, robos, etc.
- La seguridad es relativa al contexto. El contexto supone ciertos riesgos.
- La seguridad en general y, muy particularmente, en la dimensión ambiental *es un problema y responsabilidad estrictamente humana. El SO no es responsable del ambiente.*

### Dimensión de las aplicaciones
- Las aplicaciones, en tiempo de ejecución, pueden causar problemas de seguridad, atentando contra la integridad del sistema (caballos de troya, virus, gusanos, malware, por ejemplo).
- El SO debe, por sí o por terceros, implementar mecanismos de seguridad que mantengan la integridad del SC ante el potencial accionar de las aplicaciones (antivirus, firewalls, etc.).

### Dimensión del control de acceso de usuarios
- El SO debe brindar mecanismos efectivos que garanticen el acceso al Sistema de Computación exclusivamente de los usuarios habilitados al efecto.
- Dimensión más relevante.
- La responsabilidad por la seguridad, aún en estos aspectos, es siempre de gerenciamiento; siempre humana.
- **La administración de la seguridad NO ES responsabilidad del SISTEMA OPERATIVO (que solo debe proveer los medios o mecanismos),** sino que** es el administrador el que instala y actualiza antivirus (o no) y define el uso contraseñas de acceso (o no) u otros mecanismos brindados por el SO.
- **El nivel de seguridad de un sistema siempre es producto de una decisión humana.**

## **Gestión de la seguridad**
### Plano político
En el **plano político** se definen los grandes objetivos de la gestión (igual que en los ministerios gubernamentales).

- El plano político tiene que ver con el **qué** queremos lograr:
  - Reducir la desnutrición infantil.
  - Garantizar el acceso físico al sistema exclusivamente al personal habilitado.
  - Evitar incidentes que atenten contra la integridad del Sistema.
  - Disponer de los resguardos actualizados cada 24 horas.
  - Recuperar el sistema en menos de 24 horas ante un incidente.
- Decidimos dónde queremos pararnos en términos de seguridad. 
- Qué riesgo estamos dispuestos a correr y qué riesgos no. 
- Se definen los costos.
- El nivel de seguridad se define en la política en base a:
  - El efecto del riesgo (en caso de ocurrir). Cuánto prestigio se pierde si no se tiene en cuenta, pérdida de confiabilidad, etc.
  - Probabilidad de ocurrencia del riesgo.
  - El valor de la información en juego.
  - Costo de la política (no solo en $, sino también en usabilidad del sistema, etc.). Suele ser determinante.
- La Gerencia General decide la política dependiendo del análisis conjunto de estos factores y de la relación inversión vs. riesgo final. Luego, le ordena a la Gerencia de Sistemas que diseñe e implemente los mecanismos necesarios para garantizarla.
- Siempre en el plano de los mecanismos se deben prever algunos que actúen a priori (preventivos) y otros que actúen a posteriori (remediales), de forma tal de garantizar que ante un error en la prevención (todo puede fallar), el sistema se pueda recuperar

### Plano de los mecanismos
En el **plano de los mecanismos** se definen los instrumentos o medios que contribuirán a cumplir con la política definida.

- El plano de los mecanismos tiene que ver con el **cómo** vamos a lograr la política definida.
- Se pueden definir varios mecanismos que actúan concurrentemente y contribuyen a una política. 
- Es una relación N a 1. (N mecanismos – 1 Política).

### Plano de implementación
En el **plano de la implementación** se concretan los instrumentos o mecanismos definidos, por medio de una serie de decisiones y acciones concretas.

- Se llevan los mecanismos a la realidad.
- Puede haber cientos de alternativas para implementar un mismo mecanismo (deben cumplir el mismo objetivo).

## **Autenticación de acceso**
Para el **Control de Acceso** implementa la identificación y autenticación, que permite definir usuarios (en tiempo de registro de los mismos) e identificarlos y autenticarlos (en tiempo de acceso de los mismos al SC).

### Registro de usuarios
- Dar de alta usuarios y contraseñas en la tabla de usuarios (enrolamientos).
- La contraseña (como mecanismo de autenticación) que el usuario elige a la hora de su registro es encriptada por el sistema para su almacenamiento.

fk=kregistrada

- Se pueden registrar varios medios de autenticación (huella dactilar, iris del ojo, ADN, etc.). Mientras más mecanismos o medios de autentificación tengamos, la certeza que tenemos de que el usuario que pretende ingresar es quien dice ser es mucho mayor. 
- Se recomienda usar funciones unidireccionales (hash). No es conveniente que exista una función inversa a la función que encripta los medios de autenticación.

### Identificación de usuarios
Poder saber cuál es el usuario registrado que pretende ingresar al SC.

### Autenticación
Poder verificar si realmente el usuario que pretende ingresar al SC es quien dice ser (contraseña).

### Integridad
- El SO debe proveer mecanismos para garantizar la integridad del SC (firewalls) y delega a terceros la administración de la seguridad.
- Queda en manos del administrador de la seguridad, la incorporación de otros instrumentos preventivos al efecto que sean compatibles con el SC y no disminuyan el rendimiento notablemente.
- Como dijimos, no hay conjunto de mecanismos capaz de GARANTIZAR la seguridad total. 
- **El único mecanismo que puede brindar garantías de recuperación del SC cuando todos los mecanismos preventivos fallan, es el BACK UP.**
- El resguardo de la información del SC es clave a la hora de definir una política.
%%