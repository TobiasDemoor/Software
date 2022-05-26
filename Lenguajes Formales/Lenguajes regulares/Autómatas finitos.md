---
aliases: ["autómatas finitos", "autómata finito"]
---
%%chequear símbolos%%
Un autómata finito tiene una cantidad finita de estados. Todo autómata finito acepta un lenguaje regular.

Los autómatas finitos sirven para describir [[lenguajes regulares]]. 

Dos AF M y M' se dicen equivalentes (M ≡ M') si reconocen el mismo lenguaje, es decir, si L(M) = L(M')

### AF determinísticos
Es aquel que para cualquier estado se cumple que no posee más de un resultado para una misma transición.

Formalmente, un Autómata Finito Determinista (AFD) se define como una tupla 

AFD = A, Q, δ, q0, F ,  δ : Q × Σ→ Q

- A es el alfabeto de entrada 
- Q es el conjunto finito y no vacío de los estados del Autómata 
- q0 ∈ Q es el estado inicial 
- F ⊂ Q es el conjunto de estados finales de aceptación F ≠ Æ

Lenguaje aceptado por un AFD L(M) = { ω *Î* A\* / δ\* (q0, ω) *Î* F }

### AF No determinísticos
Es aquel que para alguno de sus estados posee más de un resultado para una misma transición.

Formalmente, un Autómata Finito No Determinista (AFND) se define como una tupla 

AFND = A, Q, δ, q0, F ,  δ : Q × Σ→P{Q} 

- PQ Es el conjunto de partes de los estados, el cual es conjunto de todos los subconjuntos posibles de Q.

Lenguaje aceptado por un AFND L(M) = { ω *Î* A\* / δ\* (q0, ω) ∩ F ≠ Æ }


### AFND – λ
AFND que admite transiciones lambda.

### **AFND a AFD**
Hacer la tabla de transición de estados y definir estados que son conjuntos de otros estados a partir de las transiciones posibles. Los estados de aceptación serán aquellos conjuntos que posean un estado de aceptación del AFND.

### AFND – λ a AFD
Todo AFND-λ puede convertirse en un AFD equivalente. Se realiza de forma similar a AFND a AFD pero en vez de analizar los conjuntos de estados, se analizan las clausuras lambda de los estados, que indican el conjunto de nodos a los cuales se pueden llegar a partir de una o más transiciones lambda. 

#### λ-clausura
Sea q ∈ Q, se llama λ-clausura(q) al conjunto de estados de Q que son accesibles desde q mediante una o más λ-transiciones.

Se define V Ì Q x Q (pares de estados con transiciones lambda).

- q, q’*Î* V si *d*(q, *l*) = q’ 
- Si q,q’*Î* V     y     (q’,q”) *Î* V       entonces       (q,q”) *Î*   V2 *Ì* V\* 
- (q,q) *Î* V , *"* q *Î* Q

### Minimización de un AFD
El objetivo es, dado un AFD, construir otro que reconoce el mismo lenguaje con un número mínimo de estados. La idea básica que permite reducir el número de estados de un AFD consiste en eliminar un estado siempre que ya exista otro que realiza la misma función.

Dos estados realizan la misma función cuando cualquier palabra de entrada da el mismo resultado tanto si se parte de uno como de otro estado. Se dice que los dos estados son, en este caso, indistinguibles.

Procedimiento:

1. Dividir el conjunto de estados en dos subconjuntos iniciales:
   1. *Terminales.* 
   2. *No terminales.*
2. Llamar a todos con el mismo nombre que el representante (Q0 por ej).
3. Armar la tabla de transición de estados usando la nomenclatura.
4. Verificar si hay símbolos cuyas transiciones son equivalentes y subdividir los subconjuntos.
5. Repetir hasta tener dos iteraciones seguidas iguales.

### Tipos de Reglas
- **Lexicográficas:**  VN  :: = VT
- **Borradoras:** VN  ::= λ
- **Recursivas:** A ::= aA

### Eliminación de borradoras
Para cada producción N::=λ (excepto S::=λ) eliminarla.

Por cada producción M::=aN, agregar M::=a. N, M ε VN

### Eliminación de Lexicográficas 
Sea Z ε VN U VT y VN’= VN U{Z}

Cada producción N :: = a, la reemplazo por N::=aZ y agrego Z ::=λ 

No se puede dar un lenguaje sin lexicográficas o borradoras.

### Eliminación de Símbolos Inútiles
Sea X ε VN, se dice **útil** si es alcanzable y generador.

- **Generador:** Э α ε VT\* / X →\* α
- **Alcanzable:** Э α ε VT\* / S →\*Xα y S →\* αX