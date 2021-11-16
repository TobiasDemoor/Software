Una característica de los [[sistemas distribuidos]] que los distingue de los sistemas tradicionales es el concepto de una **falla parcial**. Una falla parcial ocurre cuando una parte del sistema está fallando mientras que el resto sigue operando correctamente. Un objetivo importante de un sistema distribuido es construir el sistema de manera que pueda recuperarse automáticamente de fallas parciales sin afectar significativamente la performance.

El que un sistema sea tolerante a fallas está muy relacionado a los sistemas fiables. La [[Reliability|fiabilidad]] es un concepto que cubre un número de requerimientos útiles para sistemas distribuidos, incluyendo los siguientes:
- Disponibilidad: se define como la propiedad de que un sistema está listo para ser utilizado de inmediato.
- Confiabilidad: se refiere a la propiedad de que un sistema sea capaz de funcionar de manera continua sin fallar (a diferencia de la disponibilidad se define para unintervalo de tiempo en lugar de para un instante).
- Seguridad: se refiere a la situación en que no acontece nada catastrófico cuando un sistema deja de funcionar correctamente durante un tiempo.
- [[Mantainability|Mantenibilidad]]: qué tan facil puede ser reparado.

Es importante diferenciar [[Fault, Failure|falla de error]]. Se dice que un sistema falla cuando no puede cumplir sus promesas. Un error en cambio es una parte del estado de un sistema que puede conducir a una falla.

La construcción de sistemas fiables tiene mucho que ver con el control de fallas. Se puede hacer una distinción entre evitar, eliminar, y pronosticar fallas. Para nuestros propósitos, el tema más importante es la **tolerancia a las fallas** lo que significa que un sistema puede proveer sus servicios incluso en presencia de fallas. En otros términos, el sistema puede tolerarlas y continuar operando con normalidad.

Las fallas se suelen clasificar como transitorias, intermitentes o permantentes:
- **Fallas transitorias:** Son aquellas que ocurren una vez y luego desaparecen 
- **Fallas intermitentes:** ocurren esporádicamente. Aparecen y desaparecen solas, para luego volver a aperecer. 
- **Fallas permanentes:** Aparecen y solo son resueltas cuando el componente defectuoso se reemplaza

### Modelos de fallas
Si se considera un sistema distribuido como un conjunto de servidores que se comunican entre sí y con sus clientes ([[Client-Server]]), no proporcionar adecuadamente los servicios significa que los servidores, los canales de comunicación, o posiblemente ambos, no están haciendo lo que se supone deben hacer. Las relaciones de dependencia aparecen en alta medida en los sistemas distribuidos.

![[tolerancia_a_fallas_modelos_de_fallas.png]]

Un **crash failure** ocurre cuando un servidor termina prematuramente, pero estaba funcionando correctamente hasta ese momento.

Una **falla de omisión** ocurre cuando el servidor falla en responder a una solicitud. Muchas cosas pueden haber salido mal. En el caso de **fallas de omisión de recepción** el servidor posiblemente no recibió la solicitud en primer lugar. De manera similar las **fallas de omisión de respuesta** ocurren cuando el servidor ha realizado su trabajo pero de alguna manera falla en enviar la respuesta. En este último contrario al primero hay un posible cambio de estado por parte del servidor.

Las **fallas de timing** ocurren cuando la respuesta cae fuera de un intervalo de tiempo especificado.

Un tipo serio de falla es la **falla de respuesta** en la cual la respuesta del servidor es simplemente incorrecta. Hay dos tipos posibles, en el caso del **fallo de valor**, el servidor provee una respuesta erronea a una solicitud. En el caso de **fallo de transición de estado** el servidor reacciona de manera inesperada a una solicitud entrante.

El tipo más serio son las **fallas arbitrarias** o **fallas Bizantinas**. En realidad, cuando ocurren fallas arbitrarias, los clientes deberían estar preparados para lo peor. En particular puede ocurrir que el servidor está produciendo salidas que nunca debería haber producido, pero las cuales no pueden ser detectadas como incorrectas. 

> Si un servidor exhibe fallas arbitrarias, pero de manera benigna. Estas fallas también se conocen como **fallas seguras**.

### Enmascaramiento de fallas mediante redundancia
Una técnica clave para ocultar fallas es el uso de [[Replicación|redundancia]]. Hay tres tipos posibles: redundancia de información, redundancia de tiempo y redundancia física.

Con la **redundancia de información**, se añaden bits extra para permitir la recuperación de bits corrompidos. Un ejemplo de esto sería utilizar los [[códigos de Hamming]].

Con la **redundancia de tiempo**, una acción es realizada, y luego, si es necesario es realizada nuevamente. Las [[transacciones]] utilizan esta táctica. Si una transacción aborta, puede ser realizada nuevamente sin problema. La redundancia temporal es particularmente útil cuando las fallas con transitorias o intermitentes.

Con la **redundancia física** se añaden equipos o procesos adicionales para permitir que el sistema como un todo tolere la pérdida o malfuncionamiento de alguno de sus componentes. La redunancia física puede ser realizada por hardware o software.

Un ejemplo de redundancia física para fallas de valor. proveniente del área de la electrónica es la redundancia modular triple o **Triple Modular Redundancy (TMR)**. Donde se tienen todos los componentes replicados para tener un total de tres instancias de cada uno y el output de estas tres instancias es agregado en un valor concreto mediante una "votación" donde gana la mayoría. Entonces para que el sistema falle deben fallar dos componentes en simultáneo y de la misma manera.

![[tolerancia_a_fallos_tmr.png]]

### Resiliencia de procesos mediante grupos
La protección a fallas en los procesos se logra replicando los procesos (idénticos) en grupos. Una propiedad fundamental es que tienen todos los grupos de procesos es que cuando un mensaje es enviado al grupo, todos los miembros lo reciben. Si en un grupo falla un proceso, alguno de sus compañeros puede hacerse cargo.

Los grupos de procesos pueden ser dinámicos. Nuevos grupos pueden ser creados y grupos viejos pueden ser destruidos. Un proceso se puede unir a un grupo o irse durante la operación del sistema.

#### Organización de grupo
Una diferencia importante entre grupos tiene que ver con su estructura interna. En algunos grupos todos los procesos son iguales. No hay un lider distinguido y todas las decisiones son tomadas colectivamente. En otros grupos, existe algún tipo de jerarquía. Por ejemplo un proceso es el [[Algoritmos de elección|coordinador]] y los otros son los workers.

Cada una de estas organizaciones tiene sus ventajas y desventajas. Un grupo plano es simétrico y no tiene ningún single point of failure. Pero el proceso de toma de decisiones es más complicado. Mientras tanto en los grupos jerárquicos la toma de decisiones es más sencilla pero hay un single point of failure.

![[tolerancia_a_fallas_organizacion_de_grupos.png]]

#### Manejo de membresía
Cuando en un grupo existe comunicación, se requiere de algún método para crear y eliminar grupos, así como también para permitir que los procesos se unan a los grupos o los abandonen. Un método es tener un **servidor de grupo** al cual todas estas solicitudes pueden ser enviadas. La táctica opuesta es manejar la membresía en forma distribuida.