---
aliases: ["gramáticas libres de contexto", "gramáticas independientes del contexto"]
---
En las gramáticas independientes del contexto las producciones son menos restrictivas que en las [[Gramáticas regulares|gramáticas regulares]]. En este caso, la parte izquierda de la producción también está formada por un único símbolo no terminal, pero no hay restricciones respecto a la parte derecha de la producción. Por lo tanto, **las producciones pueden derivar en cualquier combinación de símbolos terminales y no terminales y lambda.** Estas gramáticas son capaces de reconocer [[Lenguajes libres de contexto|CFL]].

### Derivación más a izquierda
Siempre se reemplaza el VN más a la izquierda por uno de los cuerpos de sus producciones. Por lo que a la izquierda del VN elegido solamente hay símbolos terminales.

### Derivación más a la derecha
Siempre se reemplaza el VN más a la derecha por uno de los cuerpos de sus producciones. Por lo que a la derecha del VN elegido solamente hay símbolos terminales.
