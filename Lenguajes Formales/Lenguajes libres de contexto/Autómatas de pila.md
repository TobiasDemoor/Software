Es como un autómata finito, pero con memoria, capaz de reconocer [[Lenguajes libres de contexto|CFL]].  Es decir, recuerda cuáles símbolos puso antes, por lo que el autómata va cambiando de estado no solo en función de la entrada, sino también de los datos en la pila.

Dependiendo del estado actual del Autómata, del símbolo que hay en la cima de la pila y del que hay en la cadena de entrada, habrá que elegir entre un conjunto de posibles transiciones. Cada transición está formada por un posible cambio de estado y por una cadena (puede ser λ) que reemplazará al símbolo que ocupa la cima de la pila. Después de realizar un movimiento se avanza en el análisis de la cinta de entrada.

Un **AP es** <AE, Ap, z0, Q, q0, F, δ>

- AE: alfabeto de Entrada. Puede estar incluido en el alfabeto de pila. 
- AP: alfabeto de Pila. 
- Z0 ε AP: Simbolo de Pila Vacia.
- Q: conjunto finito de estados. 
- q0 ε Q: estado inicial. 
- F ⊂ Q: conjunto de estados finales. 
- δ: Q x AE’ x AP’ → Q x AP    \*

No para todo APND existe un APD equivalente. 

No hay estado trampa, no muestro lo que no acepto.

En general, lo que meto en la pila es la cadena resultante de analizar la cadena de entrada y termina cuando vuelve a ingresar Z0 a la misma.

f(q, a, z) = {(p1, ψ1),(p2, ψ2),...,(pn, ψn)} 

Estas transiciones indican que, si el Autómata de Pila se encuentra en el estado q, recibe como entrada el símbolo a y z es el símbolo que se encuentra en la cima de la pila, el Autómata puede pasar al estado p1 y reemplazar en la pila el carácter z por la cadena** ψ1, o bien elegir cualquiera de las otras posibilidades.

## **Descripción Instantánea** 
Permite definir un lenguaje aceptado por un AP. Es el autómata en un momento determinado.

q,w, γ

Donde q es el estado actual del Autómata, w es la cadena de símbolos de entrada que aún queda por procesar, y γ es la cadena de los símbolos almacenados en la pila (el caracter más a la izquierda de γ será la cima de la pila).

Si tengo una transición a, x / yz →  si viene una a y en el tope de la pila hay una x, desapilo x , apilo z y luego y y consumo a .

## **Movimiento Atómico** 
Es el pasaje de una descripción instantánea a otra.

## **Lenguaje aceptado por un AP**
- *Por estados de aceptación (modo T)*. De forma análoga a los Autómatas Finitos, es decir, el lenguaje aceptado es el conjunto de entradas que hacen que el Autómata llegue a un estado final.
  - LM = α ε AE   \* /q0, α, Z0→\*q,  λ,  γ,  q ε F 

- *Por Pila Vacía (modo N)*. El lenguaje está formado por el conjunto de entradas que vacían la pila.
  - LM = α ε AE   \*/q0, α, Z0 →\* q’,  λ,  Z0  

## **AP a gramática libre de contexto**
1. Para cada X ::= W →    bucle con λ, x/w
1. ∀a ∈AE→ bucle con a, a/λ
1. Ingreso al AP con λ,  λ/Z0
1. Salida del AP con λ,  Z0/λ

## **Propiedades de lenguajes libres de contexto**
Sean L1,  L2 dos lenguajes libres de contexto tal que L1:G1<VN1 ,  VT1 ,  S1 ,  P1> y L2:G2= <VN2 ,  VT2 ,  S2 ,  P2 >   y     VN1 ∩VN2= ∅

1. *Unión.* 

VN=VN1 ∪ VN2 ∪{S0} 

VT=VT1 ∪  VT2

PL1 ∪  L2=P1 ∪ P2 ∪  S0∷=S1  S2} 

1. *Concatenación.*

VN=VN1 ∪ VN2 ∪{S0} 

VT=VT1 ∪  VT2

PL1 ∪  L2=P1 ∪ P2 ∪{S0∷=S1S2}

1. *Clausura.*
   1. *Positiva*

VL1 +=VN1 ∪{S0} 

VL1   +=VT1

PL1   +=P1 ∪S0∷=S0S1  S1}

1. *Asterisco.*

VL1 \*=VN1 ∪{S0} 

VL1    \*=VT1

PL1   \*=P1 ∪S0∷=S0S1  λ}

*Los CFL NO SON cerrados respecto de la intersección, ni del complemento ni de la diferencia.* 
\*
