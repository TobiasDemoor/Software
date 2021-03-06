Se puede observar que lo que suele importar en materias de [[Sincronización|sincronización]] no es estar de acuerdo en el tiempo sino estar de acuerdo en *el orden en que ocurren los eventos*. Cuando es este el caso se suele hablar de los relojes como **relojes lógicos**.

### Relojes lógicos de Lamport
Para sincronizar relojes lógicos, Lamport define una relación llamada **happens-before** (ocurre-antes). La expresión $a \rightarrow b$ se lee como "el evento $a$ ocurre antes que el evento $b$". La relación happens-before puede observarse directamente en dos situaciones:
1. Si los eventos $a$ y $b$ son eventos en el mismo proceso, y $a$ ocurre antes que $b$, entonces $a \rightarrow b$ es verdadero.
2. Si $a$ es el evento de un mensaje siendo enviado por un proceso, y $b$ es el evento de un mensaje siendo recibido por otro proceso,  entonces $a \rightarrow b$ es verdadero. Un mensaje no puede ser recibido antes de ser enviado, o incluso al mismo tiempo, ya que toma un tiempo finito, no nulo para llegar.

Esta relación es transitiva, por lo tanto si  entonces $a \rightarrow b$ y $b \rightarrow c$ entonces $a \rightarrow c$. Si dos eventos $x$ e $y$ ocurren en procesos distintos que no intercambian mensajes (ni siquiera indirectamente), entonces $x \rightarrow y$ no es verdadero, pero tampoco lo es $y \rightarrow x$. Se dice que estos eventos son **concurrentes**, que significa que no se puede decir nada respecto su orden.

La solución de Lamport para implementar esto es tener en cada proceso un **contador de eventos** y al recibir un proceso un mensaje, verifica que el contador de este mensaje sea menor que el contador actual del proceso, si lo es continua ejecutando, si no lo es settea el contador acual del proceso al valor siguiente del contador del mensaje recibido, para así mantener la consistencia.

Los relojes de Lamport esán ubicados a nivel lógico en la capa de [[Middleware|middleware]].

### Relojes Vectoriales
Los relojes de Lamport llevan a una situación donde todos los eventos en un sistema distribuido están totalmente ordenados. Lo que no brindan es información acerca de la relación de dos eventos a y b mediante una simple comparación de valores de tiempo.

El problema yace en que los relojes de Lamport no capturan la **causalidad**. En la práctica la causalidad es capturada mediante **vector clocks**. El llevar cuenta de la causalidad es simple si se asigna a cada evento un nombre único (por ejemplo la combinación del pid con un contador interno). El problema entonces se destila a llevar cuenta de **causal histories**.

Supongamos que se tiene un proceso P que envia un mensaje a un proceso Q, y que al momento de arrivo, la historia causal más reciente de Q es {q₁}. Para llevar cuenta de la causalidad P envía su historia causal más reciente (siendo esta {p₁, p₂} extendida con p₃ que  representa el envío del mensaje). Al llegar, Q graba el evento (q₂), y une las dos historias en una nueva: {p₁, p₂, p₃, q₁, q₂}.

Para ver si un evento p precede causalmente a un evento q se puede ver si $H(p) \subset H(q)$. De hecho con la notación presentada basta que $p \in H(q)$, suponiendo que q es siempre el último evento local en H(q).

El problema con las historias causales es que su representación no es muy eficiente. Sin embargo no es necesario recordar todos los eventos sucesivos sino que basta con el último. Si asignamos subsequentemente un índice a cada proceso, pordemos representar la historia causal como un vector en el cual el elemento i-ésimo representa el número de eventos que ocurrieron en el proceso $P_j$. La cuasalidad entonces puede ser almacenada mediante **vector clocks** (relojes vector), los cuales son construidos permitiendo que cada proceso $P_i$ mantenga un vector $VC_i$ con las siguientes propiedades:
1. $VC_i [i]$ es el número de eventos que ocurrieron hasta este instante en $P_i$. En otras palabras $VC_i [i]$ es el reloj lógico del proceso $P_i$.
2. Si $VC_i [j] = k$ entonces $P_i$ sabe que han ocurrido $k$ eventos en $P_j$. Osea, este es el conocimiento de $P_i$ acerca del tiempo local de $P_j$.

La primer propiedad se mantiene incrementando $VC_i [i]$ por cada evento nuevo que ocurre en $P_i$. La segunda propiedad es mantenida enviando vectores junto con mensajes enviados. En particular se llevan a cabo los siguientes pasos:
1. Antes de ejeuctar un evento, $P_i$ incrementa $VC_i [i]$.
2. Cuando un proceso $P_i$ envia un mensaje m a $P_j$, establece el timestamp de m (ts(m)) como $VC_i$ luego de haber ejecutado el último paso (osea incluye el envío del mensaje).
3. Al recibir un mensaje, el proceso $P_j$  ajusta su vector modificando $VC_j \leftarrow max(VC_j [k],\ ts(m)[k])$ para cada k (lo que es equivalente a unir las historias causales).