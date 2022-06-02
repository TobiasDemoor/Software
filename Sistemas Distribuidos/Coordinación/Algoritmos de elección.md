---
aliases: ["coordinador"]
---

En muchos [[sistemas distribuidos]] se requiere que un proceso actúe como **coordinador**, iniciador o que cumpla un rol especial. En general no importa cuál proceso tiene esta responsabilidad, pero uno debe hacerlo y el resto debe estar de acuerdo en quien lo hace.

Si todos los procesos son exactamente idénticos es indistinto cuál es elegido. Podemos suponer que cada proceso P tiene un identificador único $id(P)$. En general, los algorítmos de elección intentan localizar el proceso con el mayor id y designarlo como coordinador. Los algorítmos difieren en cómo localizan al coordinador.

También suponemos que cada proceso conoce los identificadores de todos los otros procesos. Lo que desconocen es el estado de los procesos. El objetivo es que cuando se inicia la elección esta concluya con todos los procesos de acuerdo en quién es el nuevo coordinador.

### Bully algorithm
Se consideran N procesos $\set{P_0,\cdots,P_{N-1}}$ siendo $id(P_k)=k$. Cuando algún proceso nota que el coordinador ya no reacciona da inicio a una elección. Un proceso $P_k$ lleva a cabo una elección de la siguiente manera:
1. $P_k$ envia un mensaje ELECTION a todos los proceso con ids mayores a el ($P_{k+1},P_{k+2},\cdots,P_{N-1}$).
2. Si ninguno responde, $P_k$ gana la elección y se convierte en el coordinador.
3. Si uno responde toma el control y el trabajo de $P_k$ finaliza.

En cualquier momento un proceso puede recibir un mensaje ELECTION de uno de sus colegas inferiores. Cuando recibe este mensaje, el receptor envía un OK al remitente para indicar que está vivo y puede hacerse cargo. El receptor entonces lleva a cabo una elección (a menos que ya esté llevando una a cabo). Eventualmente, todos los procesos excepto uno se rinden, y entonces ese es el nuevo coordinador. Luego anuncia su victoria enviando un mensaje a todos los procesos comunicando que con efecto inmediato el es el nuevo coordinador.

Si un proceso que no estaba activo pasa a estarlo entonces lleva cabo una elección. Si ocurre que el es el de mayor id entonces gana la elección. Por lo tanto siempre gana el mayor (por esto el nombre).

### Ring algorithm
Un posible algorítmo basado en el uso de un anillo lógico sería el siguiente. Cuando un proceso nota que el coordinador no está funcionando, construye un mensaje ELECTION conteniendo su propia id y se lo pasa a su sucesor. Si el sucesor se encuentra caido se lo envía al siguiente miembro (y así hasta que pueda enviarlo). En cada paso el remitente añade su propio id a la lista.

Eventualmente el mensaje es recibido por el remitente original (lo reconoce al tener ya su id en la lista). En este punto el mensaje es cambiado a tipo COORDINATOR y es circulado una vez más, esta vez para informar a todos el nuevo coordinador (el proceso con mayor id) y los miembros del nuevo anillo.

### Elections in large-scale systems
Hay situaciones en donde varios nodos deberían ser selecionados, este es el caso de los **super peers** en [[Sistemas P2P|sistemas P2P]]. Los siguientes requerimientos deben cumplirse para la elección de un super peer:
1. Los nodos normales deberían tener acceso de baja latencia a los super peers.
2. Los super peers deberían estar distribuidos uniformemente sobre la [[Overlay Network|red superpuesta]].
3. Debería haber una proción predefinida de super peers relativo al número total de nodos en la red superpuesta.
4. Cada super peer no debería servir a más de un número fijo de nodos normales.

Afortunadamente estos requerimientos se relativamente sencillos de cumplir en la mayoría de los sistemas P2P.

En el caso de los sistemas basados en [[DHT]], la idea básica es reservar una fracción del estaco de identificación para los super peers. En estos sistemas cada nodo recibe un identificador de m bits aleatorio. Se podrían reservar los primeros k bits para identificar a los super peers.

Una solución completamente distinta se basa en posicionar los nodos en un espacio geométrico m-dimensional. En este daso asumimos que necesitamos posicionar N super nodos *uniformemente* a través de la red superpuesta. El concepto básico consiste de un total de N tokens distribuidos en N nodos elegidos aleatoriamente. Ningún nodo puede retener más de un token. Cada token representa una fuerza de repulsión mediante la cual otro token se aleja. El efecto neto (siempre que todos los tokens ejerzan la misma fuerza) es que estos tokens quedan distribuidos uniformemente en el espacio.

Esta solución requiere que los nodos que tienen token conozcan su posición relativa. Para esto se puede utilizar un protocolo de gossiping mediante el cual la fuerza del token se disemina a través de la red. Si un nodo descubre que la fuerza total actuando sobre el supera un límite traslada el token en la dirección de la fuerza resultante.