Una **blockchain** o cadena de bloques es una lista creciente de registros, llamados bloques, que están vinculados entre sí mediante criptografía. Las blockchain suelen ser administradas por una red [[P2P|peer-to-peer]] para su uso como un “libro contable distribuido públicamente”, donde los nodos se adhieren colectivamente a un protocolo para comunicarse y validar nuevos bloques.

Al ser peer-to-peer no se deposita la confianza sobre un único nodo. Las reglas son convenidas entre los nodos, no son impuestas por ninguna autoridad central.

![[SSDD_blockchain_1.png]]

## Bitcoin
La primer y más popular implementación de blockchain es Bitcoin. Bitcoin es una forma de registrar transacciones, especificamente transferencias de valor. Los bloques son los responsables de agrupar transacciones.

![[SSDD_bitcoin_1.png]]

### Árboles Merkle
![[Árboles Merkle]]

En Bitcoin las transacciones son las hojas del árbol Merkle.

### Bloque Bitcoin
El bloque Bitcoin contiene una lista de transacciones verificadas y previo a estas una cabecera. Esta cabecera contiene varios campos importantes.

![[SSDD_bitcoin_bloque_1.png]]

El primer campo relevante es el *Previous Block Hash*, el cual es la referencia al bloque anterior. Luego se tiene *Merkle Root* que es justamente la raíz del árbol Merkle que verifica todas las transacciones.

El *Difficulty Target* establece cuantos 0s deben preceder al hash del bloque, este se calcula según el hashrate total de la red. Asociado a este anterior es el campo *Nonce* este campo es el que debe ser calculado como **proof of work**.

![[SSDD_bitcoin_bloque_2.png]]

### Bloque Génesis
Como todo bloque debe hacer referencia a su predecesor mediante un hash de este, es necesario tener un punto inicial que no haga referencia a nada, esto es el **bloque Génesis**. Este está hardcodeado en el código de Bitcoin y tiene la tapa del times para mostrar que no puede ser anterior a la fecha (además porque Satoshi es medio sínico).

### Proof of work
> "La proof-of-work consiste en escanear en busca de un valor que cuando fue hasheado, al igual que con SHA-256, el hash comience con un número de cero bits. El trabajo medio que hace falta es exponencial en el número de cero bits requeridos y puede verificarse ejecutando un único hash.” -- Satoshi Nakamoto

$$H(nonce||prev\_hash||tx||tx||\cdots||tx) < target$$

> “Si la mayoría de la potencia de CPU está controlada por nodos honestos, la cadena honesta crecerá más rápido y dejará atrás cualquier cadena que compita. Para modificar un bloque pasado, un atacante tendría que rehacer la proof-of-work del bloque y de todos los bloques posteriores, y entonces alcanzar el trabajo de los nodos honestos.” -- Satoshi Nakamoto

### Manejo de transacciones nuevas
1. Las transacciones nuevas se transmiten a todos los nodos 
2. Cada nodo recoge todas las transacciones en un bloque. 
3. Cada nodo trabaja en resolver una proof-of-work compleja para su bloque. 
4. Cuando un nodo resuelve una proof-of-work, transmite el bloque a todos los nodos. 
5. Los nodos aceptan el bloque si todas las transacciones en él son válidas y no se han gastado con anterioridad. 
6. Los nodos expresan su aceptación del bloque al trabajar en crear el siguiente bloque en la cadena, usando el hash del bloque aceptado como hash previo.

### Fuente
https://nakamotoinstitute.org/static/docs/bitcoin-es.pdf