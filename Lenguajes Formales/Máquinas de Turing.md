Consiste en un control finito que puede estar en cualquier estado de un conjunto finito de estados. Se tiene una cinta dividida en celdas, cada celda con un símbolo. Inicialmente, la entrada (cadena finita de símbolos del alfabeto) se coloca en la cinta, el resto de las celdas tienen el símbolo especial vacío.

La cabeza de la cinta está siempre sobre una celda y al principio está sobre la celda más a la izquierda con el primer símbolo de la cadena de entrada (a menos que se indique otra cosa). Un movimiento o transición puede cambiar de estado (o quedarse en el actual), escribir un símbolo (reemplazando el símbolo que existía o dejando el mismo) y mover la cabeza la izquierda o derecha o no moverla (**R L H** (Halt, fin)) .

Todas las celdas tienen un símbolo que indica que están en blanco. En algún lugar de la cinta, está la sarta con la que queremos trabajar.

Una MT es $<Q, A, \phi, q_0, \delta>$ 

- $Q$  Conjunto finito de estados
- $A$  Alfabeto de entrada
- $\phi$  Alfabeto de cinta, $A \subseteq \phi$ $(B \in \phi, B \notin A)$
- $q_0 \in Q$ Estado inicial.
- $F \subseteq Q$ Conjunto de estados de aceptación.
- $\delta:Q \times \phi \times \{R, L, H\}$ Función de transición.

Las transiciones son $\alpha, \beta / M$
- $\alpha$ Es el símbolo de entrada
- $\beta$ Es el símbolo que reemplazará a α en la cinta
- $M$ Es el movimiento del cabezal de lectura (R, L, H)

### Descripción instantánea
$$(\alpha, q, \beta) \text{ con } \alpha \in \phi^*, q \in Q, \beta \in \phi^* $$
### Movimiento atómico
L: Si $(\alpha b, q, \bf{c} \mu) \vdash (\alpha, q', \bf{b} h\mu)$ entonces $\exists \ \delta (q,c) = (q', h, L)$
R: Si $(\alpha b, q, \bf{c} \mu) \vdash (\alpha bh, q', \bf{\mu})$ 
R: Si $(\alpha b, q, \bf{c} \mu) \vdash (\alpha b, q', \bf{h}\mu)$ entonces $\exists \ \delta (q,c) = (q', h, R)$entonces $\exists \ \delta (q,c) = (q', h, H)$
