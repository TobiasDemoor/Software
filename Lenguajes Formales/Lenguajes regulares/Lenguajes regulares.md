---
aliases: ["lenguajes regulares", "lenguaje regular"]
---
%%chequear símbolos%%
Un lenguaje regular es todo aquel que es generado por una gramática regular y puede ser definido mediante una [[Expresiones regulares|expresión regular]], una [[Gramáticas regulares|gramática regular]] y un [[Autómatas finitos|autómata finito]].

## Operaciones entre lenguajes regulares
Algunas operaciones sobre lenguajes regulares garantizan producir lenguajes regulares: 

- *Unión:* L ∪ M (lenguajes con cadenas de L, M o ambos).
- *Intersección:* L ∩ M  (lenguajes con cadenas de ambos). 
- *Complemento:* L (cadenas que no están en L).
- *Diferencia:* L – M (cadenas de L que no están en M). 
- *Trasposición:* LT = {wT / w ∈ L} 
- *Clausura:* L\* 
- *Concatenación:* LM 
- *Homomorfismo (sustitución):* Sea w = a1a2 . . . an ∈ Σ. Entonces h(w) = h(a1)h(a2). . . h(an) y* h(L) = hw∈ L *s*iendo h un homomorfismo. 
- *Homomorfismo inverso (sustitución inversa):*  h-1 (L) = {w ∈ Σ : h(w) ∈ L,  h : Σ →} es un homomorfismo.

## No todo subconjunto de un lenguaje regular es regular
Si tenemos a\*b\* que es un lenguaje regular, y tomo las cadenas tales que anbn con    n≥0, no obtengo un lenguaje regular.

## Lema de Pumping (PL)
Si L es un lenguaje regular, entonces existe una constante n tal que cada cadena w ∈ L, de longitud n o más, puede ser escrita como w=xyz, donde:
1. y ≠λ 
2. |xy| ≤ n 
3. Para todo     i ≥ 0,    wyiz     también está en L. 

> El Lema de Pumping se utiliza para **mostrar que un lenguaje L no es regular**. 

1. Se inicia asumiendo que L es regular. 
2. Luego, debe haber alguna n que sirva como la constante de PL. Puede que no sepamos el valor de n, pero podemos seguir con el resto del “juego” con n como un parámetro. 
3. Escogemos una w que sabemos que está en L. Típicamente, w depende de n. 
4. Aplicando el PL, sabemos que w puede descomponerse en xyz, satisfaciendo las propiedades del PL. De nuevo, puede que no sepamos como descomponer w, así que utilizaremos x, y, z como parámetros. 
5. Derivamos una contradicción escogiendo i (la cual puede depender de n, x, y, y/o z) tal que   xyiz   no está en L.

### Ejemplo 
Considere el lenguaje de cadenas con el mismo número de 0’s y 1’s. Por el pumping lemma, w = xyz , |xy| ≤ n ,  y≠λ y xy^k z ∈ L.

En particular, xz ∈ L, pero xz tiene menos 0’s que 1’s.

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