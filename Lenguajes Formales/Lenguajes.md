Se llama lenguaje a un conjunto de cadenas y se denomina lenguaje sobre el alfabeto $A$ a cualquier subconjunto $L$ del lenguaje universal $A^* \rightarrow L \subset A^*$. 

El conjunto vacío, $\emptyset$, es un subconjunto de $A^*$, no debe confundirse con aquel que contiene únicamente a la palabra vacía $|\emptyset|=0$ y $|\set{\lambda}| = 1$.

> **CONVENCIONES**  
> - Se usarán letras mayúsculas para representar los lenguajes.
> - $\set{ \lambda } = \Lambda$

| Lenguajes                                 | Máquina                        |
| ----------------------------------------- | ------------------------------ |
| Lenguajes Tipo 0                          | [[Máquinas de Turing]]         | 
| Lenguajes Tipo 1                          | Autómatas linealmente acotados |
| [[Lenguajes libres de contexto]] (Tipo 2) | [[Autómatas de pila]]              |
| [[Lenguajes regulares]] (Tipo 3)          | [[Autómatas finitos]]              |

## Operaciones con lenguajes
#### Unión
Sean dos lenguajes diferentes definidos sobre el mismo alfabeto $L1 \subset A^*$ y $L2 \subset A^*$. Se denomina unión de ambos lenguajes, $L1 \cup L2$, al lenguaje definido así: $\set{x / x \in L1 \vee x \in L2}$.

Propiedades:
1. Operación cerrada: La unión de dos lenguajes definidos sobre el mismo alfabeto será otro lenguaje definido sobre ese alfabeto. 
2. Propiedad asociativa: $(L1 \cup L2) \cup L3 = L1 \cup (L2 \cup L3)$
3. Existencia de elemento neutro: $\forall L \text{ se verifica } L \cup \emptyset = \emptyset \cup L = L$
4. Propiedad conmutativa: $\forall L1, L2 \text{ se verifica } L1 \cup L2 = L2 \cup L1$
5. Propiedad de idempotencia: $\forall L, \text{ se verifica } L \cup L = L$

#### Concatenación de lenguajes
Consideremos dos lenguajes definidos sobre el mismo alfabeto, $L1$ y $L2$. Se denomina concatenación de estos lenguajes al lenguaje definido así: $\set { xy / x \in L1 \wedge y \in L2 }$ (todas las palabras de este lenguaje estarán formadas al concatenar cada una palabra del primero de los lenguajes con otra del segundo).

Propiedades
1. Existencia del elemento nulo: $\emptyset L = L \emptyset = \emptyset$
2. Operación cerrada: La concatenación de lenguajes sobre el mismo alfabeto es otro lenguaje sobre ese alfabeto.
3. Propiedad asociativa: $(L1 L2) L3 = L1 (L2 L3)$
4. Elemento neutro:  $\forall L, \text{ se verifica } \Lambda L = L \Lambda = L$

#### Potencia de un lenguaje
Se define la potencia i-ésima de un lenguaje a la operación de concatenarlo consigo mismo i veces.

$$L^0 = \set{\lambda} = \Lambda$$
$$L^i = LL...L$$

#### Clausura positiva de un lenguaje
$$L^+ = \bigcup ^\infty _1  L^i$$
> Análogo para cadenas

#### Clausura cierre o iteración de un lenguaje
$$L^+ = \bigcup ^\infty _0  L^i$$
> Análogo para cadenas

#### Trasposición de lenguajes
Sea L un lenguaje cualquiera. Se llama lenguaje traspuesto o inverso de L, representándose por $L^{-1} \text{ o } L^T \text{ a } \set{ x^{-1} / x \in L }$. Es decir, se trata de un lenguaje que contiene las palabras inversas a las palabras de L.

## Lenguajes de programación 
![[Lenguajes de programación]]

## Lenguajes naturales
Son muy expresivos pero requieren de representaciones porque son poco concisos.

## Lenguaje ideal
El lenguaje ideal es muy expresivo y conciso.

## Sintaxis y Semántica
![[Sintaxis]]![[Semántica]]