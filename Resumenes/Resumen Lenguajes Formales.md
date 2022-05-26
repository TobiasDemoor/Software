# **Definiciones básicas**
## **Alfabeto**
Conjunto no vacío y finito de símbolos. A estos símbolos también se les suele llamar letras del alfabeto.

El conjunto de palabras que se pueden formar con los símbolos de un alfabeto recibe el nombre de “lenguaje universal” sobre ese alfabeto.

## **Palabra – Cadena**
Se denomina palabra, cadena, sarta o hilera (formada con los símbolos de un alfabeto) a toda secuencia finita de símbolos de ese alfabeto.

La longitud de una palabra se determina por el número de símbolos que la componen.

Se define la palabra vacía como aquella cuya longitud es cero. Se representa mediante la letra l (lambda). Cualquiera que sea el alfabeto considerado, siempre puede formarse con sus símbolos la palabra vacía (bastaría formar una palabra sin seleccionar a ninguno de ellos).

***CONVENCION*** → Se usarán letras minúsculas para representar las palabras de un alfabeto.

***CONVENCION*** →  l no será parte de ningún alfabeto.

### ***Operaciones con cadenas***
#### *Concatenación de cadenas*
Se llama concatenación de las palabras x y w (y se representa por xw o x.w) a otra palabra (z) obtenida poniendo los símbolos de w a continuación de las de x.

Propiedades:

1. *Operación cerrada*. Es decir, la concatenación de dos palabras de A\* es otra palabra de A\*. Si x *Î* A\*    e    y *Î* A\*, entonces xy *Î* A\* 
1. *Propiedad asociativa.* *"* x,  y,  z    se cumple que   x(yz) = (xy)z 
1. *Existencia de elemento neutro*. El elemento neutro es la cadena nula l, tanto por la derecha como por la izquierda. *"*x x*l* = *l*x = x 
1. *No cumple la propiedad conmutativa*. Esto se observa mediante cualquier contraejemplo. Sean las palabras x= ABC e y = CDE. Tenemos que xy = ABCCDE mientras que yx = CDEABC.
1. La función longitud de una palabra tiene, respecto a la concatenación, propiedades semejantes a las de la función logaritmo respecto de la multiplicación: | xy | = | x | + | y |

#### *Potencia de una cadena*
Se denomina potencia i-ésima de una palabra a la concatenación consigo misma i veces.

#### *Trasposición de cadenas*
Sea x = A1A2A3 .... An, se denomina palabra traspuesta o inversa de x, representado por x-1 o xt o x~ o xR a AnAn-1  ....  A3A2A1.

## **Lenguaje**
Se llama lenguaje a un conjunto de cadenas.

***CONVENCION*** → Se usarán letras mayúsculas para representar los lenguajes.

Se denomina lenguaje sobre el alfabeto A a cualquier subconjunto del lenguaje universal A\* →L *Ì* A\*. 

El conjunto vacío, *f*, es un subconjunto de A\*, no debe confundirse con aquel que contiene únicamente a la palabra vacía.  *f* = 0  y  | { *l* } | = 1

***CONVENCION*** →   *l* = *L*


### ***Operaciones con lenguajes***
#### *Unión*
Sean dos lenguajes diferentes definidos sobre el mismo alfabeto L1 *Ì* A\* y L2 *Ì* A\*. Se denomina unión de ambos lenguajes, L1 *È* L2, al lenguaje definido así:  { x / x *Î* L1 ó x *Î* L2}.

Propiedades

1. *Operación cerrada.* La unión de dos lenguajes definidos sobre el mismo alfabeto será otro lenguaje definido sobre ese alfabeto. 
1. *Propiedad asociativa.* (L1 *È* L2) *È* L3 = L1 *È* (L2 *È* L3) 
1. *Existencia de elemento neutro.* *"*L, se cumple que L *È* *f* = *f* *È* L = L 
1. *Propiedad conmutativa.* *"*L1 , L2, se verifica que L1 *È* L2 = L2 *È* L1 
1. *Propiedad de idempotencia.* *"*L, se verifica que L *È* L = L

#### *Concatenación de lenguajes*
Consideremos dos lenguajes definidos sobre el mismo alfabeto, L1 y L2. Se denomina concatenación de estos lenguajes al lenguaje definido así: { xy / x *Î* L1 e y *Î* L2} (todas las palabras de este lenguaje estarán formadas al concatenar cada una palabra del primero de los lenguajes con otra del segundo).

Propiedades

1. *f*L = L*f* = *f*
1. *Operación cerrada*. La concatenación de lenguajes sobre el mismo alfabeto es otro lenguaje sobre ese alfabeto.
1. *Propiedad asociativa*. (L1 L2) L3 = L1 (L2 L3).
1. *Elemento neutro (L).* *"* L, se cumple que *L*L = L*L* = L

#### *Potencia de un lenguaje*
Se define la potencia i-ésima de un lenguaje a la operación de concatenarlo consigo mismo i veces

L0 = {*l*} = *L*

#### *Clausura positiva de un lenguaje*
L+= 1∞Li

Análogo para cadenas
#### *Clausura cierre o iteración de un lenguaje*
L\*= 0∞Li

Análogo para cadenas

#### *Trasposición de lenguajes*
Sea L un lenguaje cualquiera. Se llama lenguaje traspuesto o inverso de L, representándose por L-1 o LT a { x-1 / x *Î* L }. Es decir, se trata de un lenguaje que contiene las palabras inversas a las palabras de L.

##
## **Gramáticas**
Una gramática describe la estructura de las frases y palabras de un lenguaje a través del uso de reglas definidas.

Una gramática G = <VN,  VT,  S,  P>  consta de 4 elementos ordenados dónde: 

- VN={A,B,C...}  es un conjunto finito de símbolos no terminales (variables). 
- VT= {a, b, c...} es un conjunto finito de símbolos terminales. 
- S *Î*  VN  es el símbolo inicial de la gramática. 
- P es un conjunto finito de reglas de derivación o reglas de reescritura o producciones (indican cómo sustituir variables) de la forma x ::= y con x, y *Î* V\* 
- Se cumple que VN *Ç* VT = *f* 
- Se define V = VN *È*  VT 

Dos gramáticas G y G' se dicen equivalentes (G ≡ G') si generan el mismo lenguaje, es decir, si L(G) = L(G').
### ***Derivación***
*Si* α, β *Î* V\*,* 

*se dice que* α → β (“β deriva de α”) 

*si existe alguna regla* γ :≔δ  *Î* P  *tal que* α = α1 *γ* α2   *y*    β = α1 δ α2* 

*con* α1,  α2 *Î*  V\** 

Se indica con ∗→ la aplicación de una o más operaciones de derivación. 

Se dice que una palabra α es una forma sentencial si S ∗→ α con α *Î* V\*
### ***Árboles de derivación***
A toda secuencia de derivación de una gramática le corresponde un árbol de derivación, que se construye así: 

- La raíz del árbol corresponde al símbolo no terminal inicial 
- Una derivación directa se representa por un conjunto de ramas que salen de un nodo determinado. Al aplicar una regla, uno de los símbolos de la parte izquierda de la producción queda sustituido por la parte derecha. Por cada uno de los símbolos de se dibuja una rama, que parte del nodo correspondiente al símbolo sustituido.

A lo largo del proceso de construcción del árbol, los nodos finales de cada paso, leídos de izquierda a derecha, forman la forma sentencial obtenida por la derivación representada por el árbol.

### ***Ambigüedad***
En algunas gramáticas, una misma cadena/sentencia puede obtenerse como resultado de varias derivaciones diferentes, pero a las que les corresponde un único árbol de derivación. *Pero hay otros casos en que para una misma cadena/sentencia podemos tener varios árboles de derivación diferentes. En este caso, se dice que la gramática es ambigua*. Hay lenguajes para los cuales es imposible encontrar gramáticas no ambiguas. Estos lenguajes se denominan inherentemente ambiguos.

Si un lenguaje puede ser representado mediante una [[Expresiones regulares|expresión regular]], entonces es un lenguaje regular.

# **Lenguajes regulares**
## Expresiones regulares
![[Expresiones regulares]]

## **Gramáticas regulares**




# **Autómatas**
Representa un cambio de estado en un grafo. Debe haber una única situación inicial, pero puede haber múltiples estados finales. 

## **Autómata parcialmente especificado**
Solo muestra los caminos hacia el estado de aceptación. Cuando armo la matriz, me quedan espacios en blanco. Puedo solucionarlo poniendo un estado terminal que no sea aceptable y que no tenga flechas salientes a él.

## **Autómatas finitos**
Un autómata finito tiene una cantidad finita de estados. Todo autómata finito acepta un lenguaje regular.

Los autómatas finitos sirven para describir lenguajes regulares. 

Dos AF M y M' se dicen equivalentes (M ≡ M') si reconocen el mismo lenguaje, es decir, si L(M) = L(M')

### ***AF determinísticos***
Es aquel que para cualquier estado se cumple que no posee más de un resultado para una misma transición.

Formalmente, un Autómata Finito Determinista (AFD) se define como una tupla 

AFD = A, Q, δ, q0, F ,  δ : Q × Σ→ Q

- A es el alfabeto de entrada 
- Q es el conjunto finito y no vacío de los estados del Autómata 
- q0 ∈ Q es el estado inicial 
- F ⊂ Q es el conjunto de estados finales de aceptación F ≠ Æ

Lenguaje aceptado por un AFD L(M) = { ω *Î* A\* / δ\* (q0, ω) *Î* F }

### ***AF No determinísticos***
Es aquel que para alguno de sus estados posee más de un resultado para una misma transición.

Formalmente, un Autómata Finito No Determinista (AFND) se define como una tupla 

AFND = A, Q, δ, q0, F ,  δ : Q × Σ→P{Q} 

- PQ Es el conjunto de partes de los estados, el cual es conjunto de todos los subconjuntos posibles de Q.

Lenguaje aceptado por un AFND L(M) = { ω *Î* A\* / δ\* (q0, ω) ∩ F ≠ Æ }


### ***AFND – λ***
AFND que admite transiciones lambda.

## **AFND a AFD**
Hacer la tabla de transición de estados y definir estados que son conjuntos de otros estados a partir de las transiciones posibles. Los estados de aceptación serán aquellos conjuntos que posean un estado de aceptación del AFND.




## **AFND – λ a AFD**
Todo AFND-λ puede convertirse en un AFD equivalente. Se realiza de forma similar a AFND a AFD pero en vez de analizar los conjuntos de estados, se analizan las clausuras lambda de los estados, que indican el conjunto de nodos a los cuales se pueden llegar a partir de una o más transiciones lambda. 



### ***λ-clausura***
Sea q ∈ Q, se llama λ-clausura(q) al conjunto de estados de Q que son accesibles desde q mediante una o más λ-transiciones.

Se define V Ì Q x Q (pares de estados con transiciones lambda).

- q, q’*Î* V si *d*(q, *l*) = q’ 
- Si q,q’*Î* V     y     (q’,q”) *Î* V       entonces       (q,q”) *Î*   V2 *Ì* V\* 
- (q,q) *Î* V , *"* q *Î* Q

## **Minimización de un AFD**
El objetivo es, dado un AFD, construir otro que reconoce el mismo lenguaje con un número mínimo de estados. La idea básica que permite reducir el número de estados de un AFD consiste en eliminar un estado siempre que ya exista otro que realiza la misma función.

Dos estados realizan la misma función cuando cualquier palabra de entrada da el mismo resultado tanto si se parte de uno como de otro estado. Se dice que los dos estados son, en este caso, indistinguibles.

Procedimiento:

1. Dividir el conjunto de estados en dos subconjuntos iniciales:
   1. *Terminales.* 
   1. *No terminales.*
1. Llamar a todos con el mismo nombre que el representante (Q0 por ej).
1. Armar la tabla de transición de estados usando la nomenclatura.
1. Verificar si hay símbolos cuyas transiciones son equivalentes y subdividir los subconjuntos.
1. Repetir hasta tener dos iteraciones seguidas iguales.


## **Tipos de Reglas**
- **Lexicográficas:**  VN  :: = VT
- **Borradoras:** VN  ::= λ
- **Recursivas:** A ::= aA
### ***Eliminación de borradoras***
Para cada producción N::=λ (excepto S::=λ) eliminarla.

Por cada producción M::=aN, agregar M::=a. N, M ε VN
### ***Eliminación de Lexicográficas*** 
Sea Z ε VN U VT y VN’= VN U{Z}

Cada producción N :: = a, la reemplazo por N::=aZ y agrego Z ::=λ 

***No se puede dar un lenguaje sin lexicográficas o borradoras.***

### ***Eliminación de Símbolos Inútiles***

Sea X ε VN, se dice **útil** si es alcanzable y generador.

- **Generador:** Э α ε VT\* / X →\* α
- **Alcanzable:** Э α ε VT\* / S →\*Xα y S →\* αX

## **Equivalencia Entre Formalismos**
- **ER→AF:** dada una ER siempre es posible encontrar un AF equivalente.
- **AF→GR:** para todo AF existe una GR equivalente, pero el AF no debe tener transiciones λ.
  - VN = Q
  - VT = A 
  - S = q0
  - Producciones
    - Si qi  ε F → qi  ::= λ ε P
    - Si (qi, a, qj) ε δ → qi ::=a  qj ε P

- **GR→AF:** la gramática no debe tener lexicográficas.
  - Q = VN
  - A = VT
  - q0 = S
  - F = {X ε VN / X ::= λ ε P}
  - δ = si  N ::= aM ε P → (N, a, M) ε δ

- **GR→ER:** igualación.
# **Lenguajes regulares**
Un lenguaje regular es todo aquel que es generado por una gramática regular y puede ser definido mediante una [[Expresiones regulares|expresión regular]].
## **Operaciones entre lenguajes regulares**
Algunas operaciones sobre lenguajes regulares garantizan producir lenguajes regulares: 

- *Unión:* L ∪ M (lenguajes con cadenas de L, M o ambos).
- *Intersección:* L ∩ M  (lenguajes con cadenas de ambos). 
- *Complemento:* L (cadenas que no están en L).
- *Diferencia:* L – M (cadenas de L que no están en M). 
- *Trasposición:* LT = {wT / w ∈ L} 
- *Clausura:* L\* 
- *Concatenación:* LM 
- *Homomorfismo (sustitución):* Sea w = a1a2 . . . an ∈ Σ. Entonces                             h(w) = h(a1)h(a2). . . h(an) y* h(L) = hw∈ L *s*iendo h un homomorfismo. 
- *Homomorfismo inverso (sustitución inversa):*  h-1 (L) = {w ∈ Σ : h(w) ∈ L,  h : Σ →} es un homomorfismo.

## **No todo subconjunto de un lenguaje regular es regular**
Si tenemos a\*b\* que es un lenguaje regular, y tomo las cadenas tales que anbn con    n≥0, no obtengo un lenguaje regular.

## **Lema de Pumping (PL)**
Si L es un lenguaje regular, entonces existe una constante n tal que cada cadena w ∈ L, de longitud n o más, puede ser escrita como w=xyz, donde:

1. y ≠λ 
1. |xy| ≤ n 
1. Para todo     i ≥ 0,    wyiz     también está en L. 

El Lema de Pumping se utiliza para mostrar que un lenguaje L no es regular. 

1. Se inicia asumiendo que L es regular. 
1. Luego, debe haber alguna n que sirva como la constante de PL. Puede que no sepamos el valor de n, pero podemos seguir con el resto del “juego” con n como un parámetro. 
1. Escogemos una w que sabemos que está en L. Típicamente, w depende de n. 
1. Aplicando el PL, sabemos que w puede descomponerse en xyz, satisfaciendo las propiedades del PL. De nuevo, puede que no sepamos como descomponer w, así que utilizaremos x, y, z como parámetros. 
1. Derivamos una contradicción escogiendo i (la cual puede depender de n, x, y, y/o z) tal que   xyiz   no está en L.


### ***Ejemplo*** 
Considere el lenguaje de cadenas con el mismo número de 0’s y 1’s. Por el pumping lemma, w = xyz , |xy| ≤ n ,  y≠λ y xy^k z ∈ L.


En particular, xz ∈ L, pero xz tiene menos 0’s que 1’s.

# **Gramáticas libres del contexto (CFG)**
En las Gramáticas Independientes del Contexto las producciones son menos restrictivas que en las gramáticas regulares. En este caso, la parte izquierda de la producción también está formada por un único símbolo no terminal, pero no hay restricciones respecto a la parte derecha de la producción. Por lo tanto, **las producciones pueden derivar en cualquier combinación de símbolos terminales y no terminales y lambda.**

### ***Derivación más a izquierda***
Siempre se reemplaza el VN más a la izquierda por uno de los cuerpos de sus producciones. Por lo que a la izquierda del VN elegido solamente hay símbolos terminales.

### ***Derivación más a la derecha***
Siempre se reemplaza el VN más a la derecha por uno de los cuerpos de sus producciones. Por lo que a la derecha del VN elegido solamente hay símbolos terminales.


# **Autómatas de pila**
Es como un autómata finito, pero con memoria, capaz de reconocer CFL.  Es decir, recuerda cuáles símbolos puso antes, por lo que el autómata va cambiando de estado no solo en función de la entrada, sino también de los datos en la pila.

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


Segundo Parcial
# **Lenguajes Linealmente Acotados (Tipo 1)**
También llamados lenguajes sensibles al contexto. Las gramáticas pueden tener más de un símbolo a la izquierda ya sea terminal o no terminal.

α M β :≔α γ β

α, β∈VN ∪VT\* 

M∈VN

γ∈VN ∪VT+

# **Análisis sintáctico**
## **Etapas básicas de un compilador**
### ***Fase de análisis***
#### *Análisis lexicográfico*
- Tokens o palabras bien escritas de acuerdo a las reglas del lenguaje. Ejemplo: escribir un nombre de una variable en C que inicie con un número es un error de léxico.
- ER
- AF

#### *Análisis sintáctico*
- Que los tokens pertenezcan a frases gramaticales válidas. 
- Tabla de símbolos 
- Arboles de Análisis Sintáctico

#### *Análisis semántico*
- Comprobación de la consistencia semántica.
- Verificación estática de tipos.
- Verifica que tengan sentido las frases.

### ***Análisis léxico***
- El compilador revisa y controla que las palabras estén bien escritas y pertenezcan a algún tipo de token (lexema o cadena) definido dentro del lenguaje (palabra reservada, id escrito de acuerdo a las pautas de definición del lenguaje).
- Se crea la tabla de símbolos: contiene las variables y el tipo de dato al que pertenece, las constantes literales, el nombre de funciones y los argumentos que reciben.
- Este análisis se organiza de acuerdo a la sintaxis del lenguaje que se va a compilar (CFG).
- La tarea que realiza el analizador Lexicográfico es un caso especial de coincidencia de patrones, por lo que principalmente se utilizan las [[Expresiones regulares|expresiones regulares]] y los autómatas finitos.
- Ejemplo: escribir un nombre de una variable en C que inicie con un número es un error de léxico.

### ***Análisis sintáctico***
- Se revisa que los tokens estén ubicados y agrupados de acuerdo a la definición del lenguaje. O sea, que los tokens pertenezcan a frases gramaticales válidas que por lo general son representadas por medio de árboles de análisis sintáctico. 
- En esta etapa se completa la tabla de símbolos con la dimensión de los identificadores y los atributos necesarios.

### ***Análisis Semántico***
- Utiliza el árbol sintáctico y la tabla de símbolos para comprobar la consistencia semántica del programa fuente.
- Se reúne la información sobre los tipos para la fase posterior.
- Se hace la verificación estática de tipos.
- *La semántica de un programa determina su comportamiento durante el tiempo de ejecución.*
#### *Tabla de símbolos*
- No es una etapa del proceso de compilación, sino que una tarea, una función que debe realizar el proceso de compilación.
- Almacena los identificadores que aparecen en el código fuente puro, como así también los atributos de los mismos, su tipo, su ámbito y en el caso de los subprogramas el número y tipo de argumentos.
- Es accedida tanto para escritura como para lectura por todas las etapas.


### ***Fase de síntesis***
- Generación de código intermedio.
- Optimización de código.
- Generación de código.

### ***Detector de errores o manejador de errores***
- Tampoco es una etapa del proceso de compilación, sino que es una función.
- Al ocurrir un error esta función debe tratar de alguna forma el error para seguir con el proceso de compilación (la mayoría de errores son detectados en las etapas de análisis léxico, análisis sintáctico, análisis semántico).
- Los errores estáticos (tiempo de compilación) deben ser notificados por un compilador, y el compilador debería ser capaz de generar mensajes de error significativos y reanudar la compilación después de cada error.
- Una definición de lenguaje por lo general requerirá no solamente que los errores estáticos sean detectados por un compilador, sino también ciertos errores de ejecución.
- Esto requiere que un compilador genere código extra (realizará pruebas de ejecución apropiadas para garantizar que todos esos errores provocarán un evento apropiado durante la ejecución). El evento más simple: detener la ejecución del programa.
- Más complejos: requerir la presencia de mecanismos para el manejo de excepciones.


#### *Pasadas*
- Es el procesamiento de todo el programa fuente antes de generar el código.
- Después del paso inicial, dónde se construye un árbol sintáctico o un código intermedio a partir de la fuente, una pasada consiste en procesar la representación intermedia agregando información a ella, alterando su estructura o produciendo una representación diferente.
- Un compilador puede ser de una pasada, en el que todas las fases se presentan durante un paso único. Esto resulta en una compilación eficaz pero también en (por lo regular) un código objeto menos eficiente. Tanto Pascal como C son lenguajes que permiten la compilación de una pasada.
- Compiladores con optimizaciones utilizan más de una pasada. Una pasada para análisis léxico y sintáctico, otra pasada para análisis semántico y optimización a nivel del fuente, y una tercera pasada para generación de código y optimización a nivel del objeto.

## **Análisis sintáctico**
### ***Funciones del análisis sintáctico***
- Comprobar que la secuencia de componentes léxicos cumple las reglas de la gramática 
- Generar el árbol sintáctico

### ***Tipos de analizadores sintáctico***
- Descendentes (top-down)
- Ascendentes (bottom-up)
  - Construyen el árbol de análisis sintáctico desde abajo hacia arriba.
  - Analizadores de Precedencia de Operador.
  - Analizadores LR(k) (L: se analiza desde la izquierda, R: RM, k 0 o 1).

### ***Definiciones***
- *Reducción:* inverso de un paso en una derivación.
- *Árbol de Derivación:* representación que describe el proceso de derivación.
- *Forma Sentencial:* secuencia de terminales y no terminales obtenida mediante derivaciones a partir del no terminal inicial.
- *Derivación por la derecha (rm):* derivación dónde el no terminal más a la derecha se sustituye a cada paso.
- *Pivote:* es un substring que concuerda con un lado derecho de alguna producción y que representa un paso reverso de la derivación más a la derecha. No todo substring es un pivote. Si la gramática fuera ambigua el pivote no es único. El pivote puede ser reemplazado por un lado izquierdo de una gramática.

### ***Análisis sintáctico ascendente***
- Corresponde a la construcción de un árbol de análisis sintáctico para una cadena de entrada que empieza en las hojas y avanza hacia la raíz. 
- Un tipo general de análisis sintáctico es el que se conoce como de desplazamiento-reducción (shift-reduce). La clase de gramáticas para las cuales pueden construirse estos analizadores se denominan LR. 
- En cada paso de una reducción un substring que concuerde con el lado derecho de alguna producción, se reemplaza por el lado izquierdo de la misma.
### ***Shift/Reduce***
- Este algoritmo se basa en una pila de estados y una tabla de análisis. Existen diferentes métodos para generar la tabla de análisis (LR(0), SLR, LALR, LR(1)).
  - El método LR(1) genera la tabla para cualquier gramática LR(1), pero genera tablas muy grandes.
  - El método SLR genera tablas muy compactas pero no puede aplicarse a todas las gramáticas LR(1)
  - El método LALR genera tablas compactas y puede aplicarse a la mayoría de gramáticas LR(1)
- Los métodos LR(k), consideran k símbolos antes de decidir por una acción.



#### *Prefijo viable*
Es un prefijo sentencial derecha que puede aparecer en la pila de un analizador sintáctico shift-reduce.

A *®* *b*1 *b*2  es válido para un prefijo viable α*b*1 si hay una derivación

S *Þ* rm \*   αA*w*   *Þ* rm   α*b*1 *b*2 *w*


#### *Conflictos*
Hay gramáticas para las cuales este análisis no se puede realizar pues, dado el estado de la pila y el siguiente símbolo de entrada no es posible determinar si se debe desplazar o reducir (1) (conflicto shift/reduce), o no se puede decidir qué reducción realizar (conflicto reduce/reduce).


## **Analizador Sintáctico LR**
- Los analizadores sintácticos LR son controlados por tablas.
- Para que una gramática sea LR basta con que un analizador sintáctico S/R de izquierda a derecha, pueda reconocer los pivotes cuando éstos aparecen en la parte superior de la pila.
- La construcción de este tipo de analizadores es ardua, pero puede hacerse mediante algún generador automático, por ejemplo, YACC (recibe una CFG y retorna un analizador sintáctico para ella, si la misma tuviera ambigüedades, el programa puede detectarlas).
- Funcionalmente hablando, un analizador LR consta de dos partes diferenciadas, un programa de proceso y una tabla del análisis.
- El programa de proceso posee un funcionamiento muy simple y permanece invariable de analizador a analizador. Según sea la gramática a procesar deberá variarse el contenido de la tabla de análisis que es la que identifica plenamente al analizador.

## **Tabla de análisis sintáctico**
- Dos partes
  - *Acciones.* Para cada símbolo terminal y $ (delimitador)
  - *Ir-a (GOTO).* Para cada símbolo no terminal.
- Las filas corresponden a los estados
- Cuatro acciones
  - *Desplazar.* Consumir un símbolo de la cadena de entrada.
  - *Reducir.* Sustituir en la pila los símbolos de una parte derecha de una regla por su parte izquierda. Reducir por sobre desplazar.
  - *Aceptar.* Terminar el análisis aceptando la cadena.
  - *Error.* Todo lo demás. Cuando no se puede efectuar ninguna de las anteriores acciones.

## **LR(0)**
Un elemento LR(0) (item) de una gramática G es una producción de G con un punto en cualquier posición de la parte derecha. Significa que los símbolos a la izquierda del punto ya han sido reconocidos.

- A → XYZ produce los siguientes cuatro ítems:
  - A ® .XYZ; A ® X.YZ; A ® XY.Z; A ® XYZ.
- A ® .XYZ significa que se espera una cadena que pueda derivarse de XYZ
- A ® X.YZ significa que se espera una cadena que pueda derivarse de YZ y que ya se analizado una entrada que puede derivarse de X.

- El conjunto de ítems LR(0) canónico es un AFD. Cada estado es un conjunto de ítems. Para definir ese AFD se necesitan 3 cosas:
  - Una gramática aumentada: P ∪ { S´ *®* S }. Esta nueva producción sirve para que el analizador sintáctico sepa cuando debe aceptar la entrada y dejar de analizar. **Aumentamos la gramática agregando la producción** S´ ***®*** S **y sólo se acepta cuando la reducción que corresponde es** S´ ***®*** S**.**
  - La función ***CLAUSURA.***
  - La función ***GOTO***

### ***Clausura LR(0)***
Si I es un conjunto de ítems, la **CLAUSURA(I)** se construye así:

- Todos los elementos de **I** pertenecen a la **CLAUSURA(I)** 
- Si A ***®*** α.Bβ está en la CLAUSURA(I) y B ***®***  γ  (B es no terminal) es una producción, entonces agregar B ***®*** .γ si no pertenece ya al conjunto. Aplicar esta regla hasta que no haya más elementos para agregar.
- Se clausura siempre que se tenga una producción con un punto a la izquierda de un no terminal.

### ***Función GOTO***
Sea I un conjunto de elementos y X un símbolo de la gramática (terminal o no terminal), la operación Ir\_A(I, X) da como resultado otro conjunto de ítems. Se utiliza para definir la transiciones en el autómata LR(0).

- Para cada ítem de I de la forma A ***®*** α.Xβ se agrega a Ir\_A(I,X) los elementos del conjunto clausura (A ***®*** αX.β)
- Si se representan los conjuntos de la colección como estados y las operaciones Ir\_A() como transiciones, se obtiene un autómata reconocedor de prefijos viables.




### ***Uso del autómata***
El estado inicial del autómata LR(0) es CLAUSURA([S’ ® .S]), dónde S’ es el símbolo inicial de la gramática aumentada. Cuando se llega a un estado se elige: 

- un desplazamiento por el siguiente símbolo de entrada si el estado tiene una transición por él, o 
- se elige reducir, los ítems en el estado indicarán qué regla utilizar.


### ***Estructura de la tabla de ANÁLISIS SINTÁCTICO***
- La tabla de análisis sintáctico consta de dos partes: ACCION e Ir\_A. El estado inicial del autómata LR(0) es CLAUSURA([S’ ® S]), dónde S’ es el símbolo inicial de la gramática aumentada. Cuando se llega a un estado si es posible reducir, se reduce; sino, se elige un desplazamiento por el siguiente símbolo de entrada.
- La tabla tiene tantas filas como estados en el autómata y tantas columnas como símbolos en la gramática. 
- Los símbolos terminales determinan la acción que realiza el analizador en cada situación y los símbolos no terminales determina la función Ir\_a.

#### *Construcción de la tabla de ANÁLISIS SINTÁCTICO*
Contenido de la sección Ir\_a de la tabla de análisis: 

- Cada transición Ir\_a(Ii , X) = Ij , siendo X un símbolo no terminal de la gramática, significa colocar el valor j en la celda Ir\_a(i, X)

Contenido de la sección Acción de la tabla de análisis 

- Cada transición Ir\_a(Ii , x) = Ij , siendo x un símbolo terminal, significa colocar el Sj (Shift al estado j) en la celda Acción(i, x)
- Para los estados i que contengan un elemento con el punto al final de la regla k-ésima [X ® Yβ.] colocar Rk (Reducir por k) en todas las celdas del estado.
- Para cada estado i que contenga el elemento [X *®*S.$] se coloca Aceptar en la celda Acción(i, $).

Las celdas que queden vacías representan errores sintácticos.

### ***Análisis LR0***
El algoritmo LR(0) no requiere de la consideración de ningún símbolo de preanálisis. Cuando se alcanza un estado que sólo tiene acciones de reducción, se aplican éstas sin necesidad de estudiar el siguiente símbolo de la cadena de entrada. Cuando se alcanza un estado que no es de reducción, se lee el símbolo de la cadena de entrada y se ejecuta la acción de desplazar correspondiente (o Aceptar o Error).

1. Inicializar la pila al estado 0. 
1. Mientras no esté vacía la cadena de entrada comprobar para el estado y símbolo actual, la acción a realizar en “Acción”. 
   1. Si es un desplazamiento: guardar en la pila, el símbolo y el número del estado destino. Y desplazar un símbolo en la cadena. 
   1. Si es una reducción: eliminar de la pila los símbolos que hay en la parte derecha de la regla. Guardar en la pila la parte izquierda de la regla, y el número del estado que le corresponda según “Ir\_a”. 
1. Cuando se llegue a “Aceptar”, cadena aceptada. En caso contrario, error



### ***Conflictos***
Se dice que una gramática es LR(0) si las reglas anteriores son no ambiguas. Esto significa que si un estado contiene un elemento completo [A *®* α.] no puede contener otros.

- Si un estado así también contiene un elemento “desplazado” [A *®* α.X*b*] (donde X es un terminal), entonces surge una ambigüedad (conflicto shift/reduce).
- De manera similar, si un estado de esta clase contiene otro item completo [B *®* *b*.], surge una ambigüedad pues no se puede decidir por qué producción realizar la reducción.

Los conflictos aparecen cuando una determinada celda de la sección Acción de la tabla puede rellenarse con varios valores. Estos conflictos significan que la gramática no es LR(0).

## **SLR**
Para evitar estos conflictos es necesario considerar los conjuntos SIGUIENTE de cada símbolo no terminal y tener en cuenta un token de preanálisis. Esto es la base del algoritmo SLR.

Este algoritmo es idéntico al algoritmo LR(0) salvo en la forma de rellenar las acciones de reducción:

- Para los estados i que contengan un elemento con el punto al final de la regla k-ésima [X → b.] colocar Rk en todas las celdas de los tokens pertenecientes a SIGUIENTE(X).

### ***Cálculo del PRIMERO***
PRIMERO(α) es el “conjunto de terminales que inician las cadenas derivadas de α” y, en el caso de que desde α se pueda derivar la cadena vacía (λ), entonces λ también pertenecerá a PRIMERO(α).

- *P1.* Si X es terminal, entonces PRIMERO(X) es {X} 
- *P2.* Si X ® l es una producción, entonces añadir l a PRIMERO(X). 
- *P3.* Si X es no terminal y X*®* Y1 Y2 ...  Yk es una producción, entonces poner a en PRIMERO(X) si, para alguna i, a está en PRIMERO(Yi) y l está en todos los PRIMERO(Y1)


### ***Cálculo del SIGUIENTE***
Si X es un símbolo no terminal, SIGUIENTE(X) es el “conjunto de terminales que pueden aparecer inmediatamente a la derecha de X en alguna forma sentencial”. Si X puede ser el símbolo situado más a la derecha de una forma sentencial, entonces $ pertenecerá a SIGUIENTE(X).

- *S1.* Poner $ en SIGUIENTE(S), con S símbolo inicial y $ delimitador derecho de la entrada. 
- *S2.* Si hay una producción A ® aBb, entonces todo lo que está en PRIMERO(b) excepto l se pone en SIGUIENTE(B).
- *S3.* Si hay una producción A ® aB o una producción A ® aBb, donde PRIMERO(b) contenga l, entonces todo lo que esté en SIGUIENTE(A) se pone en SIGUIENTE(B).


# **Análisis semántico**
## **Gramáticas de atributos**
Un ***atributo*** es cualquier propiedad de una construcción del lenguaje de programación. Los atributos pueden variar ampliamente en cuanto a la información que contienen y su complejidad. 

- Ejemplos típicos de atributos son: el tipo de datos de una variable, el valor de una expresión

- *Fijación del atributo:* proceso de calcular un atributo y asociar su valor calculado con la construcción del lenguaje en cuestión.
- *Tiempo de fijación:* momento (compilación/ejecución) en el que se da la fijación del atributo.
  - Los atributos que pueden fijarse antes de la ejecución se denominan *estáticos*, mientras que los atributos que sólo se pueden fijar durante la ejecución son *dinámicos*. (un escritor de compiladores está interesado en aquellos atributos que se fijan durante el tiempo de traducción).

### ***Atributos y reglas semánticas***
- *Atributos:* Se asocian a los símbolos no terminales.
- *Reglas:* Se asocian a las producciones. 

Si X es un símbolo y a un atributo X.a denota el valor de a en el nodo del árbol de análisis sintáctico etiquetado con X.

### ***Tipos de atributos estáticos***
- *Sintetizados:* un atributo sintetizado en el nodo N define su valor en términos de los valores de los atributos en el hijo de N. (de abajo hacia arriba).
- *Heredados:* un atributo heredado en el nodo N define su valor en términos de los valores de los atributos en el padre de N y es posible utilizar los hermanos de N. (de arriba hacia abajo).
  - Los terminales pueden tener atributos sintetizados, pero no atributos heredados.
  - Los atributos para los terminales tienen valores léxicos que suministra el analizador léxico.

## **Comprobación de tipos**
Los atributos pueden utilizarse para la comprobación de tipos. 

- Para realizarla, un compilador debe asignar una expresión de tipos a cada componente del programa fuente y luego debe determinar que estas expresiones sean conforme a una colección de reglas lógicas conocidas como el sistema de tipos para el lenguaje fuente. 
- El compilador debe calcular y mantener la información de tipos de datos (inferencia de tipos), y usarla para asegurar que cada parte de un programa tenga sentido bajo las reglas de tipo del lenguaje (verificación de tipo).
- La información del tipo de datos puede ser **estática o dinámica**, o una combinación de las dos.
- La información de tipo estático también se emplea para determinar el tamaño de memoria necesario para la asignación de cada variable y la manera en que se puede tener acceso a la memoria, y esto puede utilizarse para simplificar el ambiente en tiempo de ejecución.
- La comprobación de tipos tiene el potencial de atrapar errores en los programas.
- Una implementación de un lenguaje es fuertemente tipeada si el compilador garantiza que los programas que acepta se ejecutarán sin errores de tipos.

- Un *tipo de datos* es un conjunto de valores con ciertas operaciones sobre ellos. 
  - El tipo de datos "entero” en un lenguaje de programación hace referencia a un subconjunto de los enteros matemáticos, junto con las operaciones aritméticas, tales como + y \*, que son proporcionadas por la definición del lenguaje.
- Un lenguaje de programación siempre contiene un número de tipos ya incluidos, con nombres tales como int y double. Estos tipos predefinidos corresponden, ya sea a tipos de datos numéricos que son provistos internamente mediante diversas arquitecturas de máquina y cuyas operaciones ya existen como instrucciones de máquina, o a tipos elementales como boolean y char, cuyo comportamiento es fácil de implementar. 
  - Tales tipos de datos son **tipos simples**, ya que sus valores no exhiben estructura interna explícita.
- Dado un conjunto de tipos predefinidos, se pueden crear nuevos tipos de datos utilizando **constructores de tipo**, tales como array o record o struct. Tales constructores se pueden ver como funciones que toman tipos existentes como sus parámetros y devuelven nuevos tipos con una estructura que depende del constructor. 
  - Tales tipos con frecuencia son denominados **tipos estructurados**.
- Los lenguajes que tienen un rico conjunto de constructores de tipo por lo regular también tienen un mecanismo para que un programador asigne nombres a expresiones de tipo (**definiciones de tipo**).

### ` `***Equivalencia de tipos***
Dadas las posibles expresiones de tipo de un lenguaje, un verificador de tipo con frecuencia debe responder la cuestión de cuándo dos expresiones de tipo representan al mismo tipo: **equivalencia de tipos.** 

- *Equivalencia estructural:* dos expresiones son o bien del mismo tipo básico o están formadas aplicando el mismo constructor (C).
- *Equivalencia por nombre:* esto puede darse cuando las expresiones de tipos pueden tener nombre. Esta equivalencia es más restrictiva. Dos expresiones son el mismo tipo simple o tienen el mismo nombre de tipo (Pascal y C). 
  - Dos expresiones pueden tener la misma estructura, pero distinto nombre y, por ejemplo, pascal no las considera equivalentes.

### ***Conversiones de TIPOS***
#### *Sobrecarga*
Un operador está sobrecargado si se utiliza el mismo nombre de operador para dos operaciones diferentes.

- Operadores aritméticos. Por ejemplo, 2+3 representa la suma entera, mientras que 2.1+3 representa la de punto flotante, que debe ser implementada de manera interna mediante una instrucción o conjunto de instrucciones diferente.
- Se puede extender a procedimientos y funciones definidos por el usuario, donde se puede emplear el mismo nombre para operaciones relacionadas, pero definido para parámetros de tipos diferentes.
#### *Coerción y conversión de tipos*
Una extensión común de las reglas de tipo de un lenguaje es permitir expresiones aritméticas de tipo mezclado tal como 2.1 + 3, donde se suma un número real y un número entero. Debe hallarse un tipo común que sea compatible con todos los tipos de las subexpresiones, y deben aplicarse operaciones para convertir los valores en el tiempo de ejecución a las representaciones apropiadas antes de aplicar el operador.

- En la expresión 2.1 + 3, el valor entero 3 se debe convertir a punto flotante antes de la suma, y la expresión resultante tendrá el tipo de punto flotante.

Existen dos métodos que un lenguaje puede tomar para tales conversiones:

- Que el programador realice conversiones explícitas
- Que el verificador de tipo suministre la operación de conversión de manera automática, basándose en los tipos de las subexpresiones.

Una conversión automática se conoce como **coerción**.


**Una implementación de un lenguaje (compiladores o intérpretes) no puede romper las reglas del lenguaje.**



# **Lenguajes sin restricciones (T0)**
## **Máquinas de Turing**
Consiste en un control finito que puede estar en cualquier estado de un conjunto finito de estados. Se tiene una cinta dividida en celdas, cada celda con un símbolo. Inicialmente, la entrada (cadena finita de símbolos del alfabeto) se coloca en la cinta, el resto de las celdas tienen el símbolo especial vacío.

La cabeza de la cinta está siempre sobre una celda y al principio está sobre la celda más a la izquierda con el primer símbolo de la cadena de entrada (a menos que se indique otra cosa). Un movimiento o transición puede cambiar de estado (o quedarse en el actual), escribir un símbolo (reemplazando el símbolo que existía o dejando el mismo) y mover la cabeza la izquierda o derecha o no moverla (**R L H** (Halt, fin)) .

Todas las celdas tienen un símbolo que indica que están en blanco. En algún lugar de la cinta, está la sarta con la que queremos trabajar.


Una MT es <Q,  A,  φ,  q0,  δ>

- Q   Conjunto finito de estados
- A    Alfabeto de entrada
- φ    Alfabeto de cinta, A ⊆ φ   (B∈ φ,  B ∉A)  
- q0∈Q   Estado inicial.
- F ⊆Q   Conjunto de estados de aceptación.
- δ:Q × φ ×{R, L, H} Función de transición.

Las transiciones son  α, β/M

- α  Es el símbolo de entrada
- β  Es el símbolo que reemplazará a α en la cinta
- M Es el movimiento del cabezal de lectura (R, L, H)

### ***Descripción instantánea***
α, q,β con α∈ φ\*,  q ∈Q,  β ∈ φ\* 
###
### ***Movimiento atómico***

