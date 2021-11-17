En la práctica las operaciones sobre una base de datos son efectuadas en forma de [[Transacciones|transacción]]. Para esto se requieren primitivas especiales que deben ser provistas o por el [[Sistemas Distribuidos|sistema distribuido]] (DS) subyacente o por el language system runtime. En particular, las llamadas a procedimientos remotos ([[RPC|Remote Procedure Calls, RPC]]), suelen estar encapsuladas en transacciones, llevando a lo que se llama **transactional RPC**.

En los DS las transacciones suelen estar construidas por un número de subtransacciones, que juntas forman una transacción anidada o **nested transaction**. La transacción de alto nivel puede ramificar hijos que corran en paralelo entre ellos, en máquinas distintas, para mejorar la [[Performance|performance]]. Cada uno de estos hijos puede a su vez ejecutar una o más subtransacciones propias. Siendo este el caso surge el inconveniente de que la transacción debe ser atómica, osea que si la última subtransacción en ejecutarse falla, todo el resto de los cambios deben revertirse.

En principio una solución a esto es agregar un [[Componente|componente]] intermediario ([[Middleware|middleware]]) llamado **transaction processing monitor** o **TP monitor**. Su tarea principar es permitir a una aplicación acceder a múltiples servidores/bases de datos ofreciendo un modelo de programación transaccional. Escencialmente este coordina las subtransacciones siguiendo un [[Protocolo|protocolo]] estandar llamado **distributed commit**.

![[SSDD_distributed_transactions_tp_monitor.png]]

### Commit distribuido
El problema de los commit distribuidos implica lograr que una operación sea realizada por cada miembro de un grupo o por ninguno en absoluto. Con transacciones distribuidas, la operación puede ser la realización de una transacción en un solo sitio que interviene en la transacción.

#### One-phase commit protocol
Los commits distribuidos frecuentemente se suelen establecer mediante un [[Algoritmos de elección|coordinador]], este comunica a todos los demás procesos involucrados, llamados participantes, si deben realizar o no (localmente) la operación de que se trate. El problema es que los procesos no pueden informar al coordinador.

#### Two-phase commit protocol (2PC)
Suponemos varios procesos. Cada uno se ejecuta en una máquina diferente. El protocolo se compone de dos fases,cada fase comprende dos pasos:
1. El coordinador envía un mensaje VOTE_REQUEST a todos los participantes. 
2. Cuando un participante recibe un mensaje VOTE_REQUEST, regresa el mensaje VOTE_COMMIT al coordinador para decirle que se prepare para realizar localmente su parte de la transacción, o de lo contrario envía un mensaje VOTE_ABORT. 
3. El coordinador reúne todos los votos de los participantes. Si todos los participantes votaron para realizar la transacción, entonces también lo hará el coordinador. En ese caso envía un mensaje GLOBAL_COMMIT a todos los participantes. Sin embargo, si un participante ha votado abortar la transacción, el coordinador también decidirá abortar la transacción y multitransmitir el mensaje GLOBAL_ABORT. 
4. Cada participante que votó por la realización espera la reacción final del coordinador. Si un participante recibe un mensaje GLOBAL_COMMIT, entonces realiza localmente la transacción. De lo contrario, cuando se recibe un mensaje GLOBAL_ABORT, la transacción también es abortada localmente.

La primer fase es la de votación que consiste de los pasos 1 y 2. La segunda es la fase de decisión, y consiste de los pasos 3 y 4.

![[SSDD_transacciones_distribuidas_two-phase_commit.png]]

Las acciones tomadas por un participante P cuando está en el estado READY y habiendo contactado otro participante Q.

| Estado de Q | Acción de P                   |
| ----------- | ----------------------------- |
| COMMIT      | Realizar transición a COMMIT  |
| ABORT       | Realizar transición a ABORT   |
| INIT        | Realizar transición a ABORT   |
| READY       | Contactar a otro participante | 


#### Three-phase commit protocol (3PC)
Un problema con 2PC es que cuando el coordinador falla, los participantes pueden no ser capaces de llegar a una decisión final. Consecuentemente los participantes pueden necesitar permanecer bloqueados hasta que el coordinador se recupere.

Los estados del coordinador y de cada participante satisfacen las dos condiciones siguientes: 
1. No existe un estado único a partir del cual sea posible realizar una transición directamente ante un estado COMMIT o un estado ABORT.
 2. No existe ningún estado en el cual no sea posible elaborar una conclusión final, y a partir de la cual se pueda realizar una transición ante un estado COMMIT.

![[SSDD_transacciones_distribuidas_three-phase_commit.png]]

A diferencia de 2PC cuando el coordinador determina que es posible realizar el commit, no envía la instrucción de hacerlo inmediatamente, sino que primero envía un mensaje PREPARE-COMMIT. Solamente después que cada participante haya respondido que está preparado el coordinador envía el GLOBAL-COMMIT final.

Aunque 3PC es muy referido en la literatura no suele ser utilizado en sistemas reales ya que las condiciones en las que falla 2PC rara vez ocurren.