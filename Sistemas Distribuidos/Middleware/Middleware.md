# Middleware
Para asistir en el desarrollo de aplicaciones distribuidas los [[Sistemas Distribuidos|sistemas distribuidos]] (DS) suelen estar organizados para tener una capa de software separada que se encuentra lógicamente posicionada sobre el [[Sistemas Operativos|sistema operativo]] de las computadoras que son parte del sistema.
El middleware es a un DS, lo que un [[Sistemas Operativos|sistema operativo]] es a una computadora individual: un administrador de recursos ofreciendo sus aplicaciones para compartir y deployar eficientemente esos recursos a través de la red. Junto con la administración de recursos brinda otros servicios que también se suelen encontrar en la mayoría de los [[Sistemas Operativos|sistemas operativos]], incluyendo:
- Facilidades para la comunicación entre aplicaciones
- Servicios de seguridad 
- Administración de uso de recursos (Accounting services)
- Enmascaramiento y recuperación de errores

La principal diferencia que tienen con los [[Sistemas Operativos|sistemas operativos]] es que los servicios del middleware se ofrecen en un entorno conectado.

## Middleware organization
%%En el contexto de la [[Distributed Systems Architecture|arquitectura de sistemas distribuidos]].%%
En general hay dos [[Patrones|patrones de diseño]] que son aplicados usualmente a la organización del middleware, wrappers e interceptors. Cada uno apunta a diferentes problemas, pero ambos apuntan al mismo objetivo del middleware, lograr [[Sistemas Distribuidos#Apertura|apertura]].

### Wrappers
Cuando se construye un DS a partir de [[Componente|componentes]] existentes, inmediatamente nos topamos con un problema fundamental: las [[Interfaz|interfaces]] ofrecidas por el componente legacy muy probablemente no son aptas para todas las aplicaciones.

Un **wrapper** o [[Adapter|adapter]] es un componente especial que ofrece una interfaz aceptable a una aplicación cliente, de la cual las funciones son transformadas en las disponibles en el componente.

Aunque originalmente fueron definidos en el contexto de [[OOP|OOP]], en el contexto de los sistemas distribuidos los wrappers son mucho más que un simple transformador de interfaces. Por ejemplo, un **object adapter** es un componente que permite a las aplicaciones invocar objetos remotos, aunque esos objetos puedan haber sido implementados como una combinación de funciones de librería operando sobre tablas de una base de datos relacional.

Una tarea del middleware es minimizar la cantidad de estos wrappers, ya que si cada aplicación se conectara con todas las otras mediante un adapter distinto habría un número inmanejable. Una forma de lograr esto es implementando un **broker**, que es un componente centralizado que administra los accesos entre aplicaciones.
![[wrappers_1.png]]

### Interceptors
Conceptualmente un **interceptor** es nada más que una construcción de software que va a interrumpir el flujo de control usual y permitir que se ejecute otro código. Los interceptors son el medio principal para adaptar middleware a las necesidades específicas de una aplicación.

Para llevarlo a un ejemplo concreto, supongamos tener un objeto A que puede invocar un método que pertenece al objeto B que recide en una máquina diferente a la de A. Esta invocación remota se lleva a cabo en 3 pasos:
1. El objeto A tiene disponible una interfaz local idéntica a la ofrecida por el objeto B. A llama al método disponible en dicha interfaz.
2. La llamada de A es transformada en una invocación genérica a objeto, gracias a una interfaz general de invocación de objetos ofrecida por el middleware.
3. La invocación genérica a objeto es transformada en un mensaje que es enviado a través de la red de [[Capa de transporte|capa de transporte]].
![[interceptors_1.png]]

Supongamos que en el ejemplo anterior ahora B se encuentra replicado. En este casa cada réplica debería ser invocada ([[Tácticas para disponibilidad#Recuperación de fallas|redundancia activa]]). Este es un punto claramente definido donde la intercepción puede ayudar. Lo que realizara el **request-level interceptor** es simplemente realizar la invocación genérica para cada una de las réplicas. Esto es ideal ya que ni el objeto A ni el middleware tienen que estar al tanto de que B está replicado.

Luego podríamos requeriri que el mensaje enviado sea dividido en bloques más pequeños debido a que es muy grande. En este caso el **message-level interceptor** puede asistir realizando esto, sin que el middleware se vea involucrado.
