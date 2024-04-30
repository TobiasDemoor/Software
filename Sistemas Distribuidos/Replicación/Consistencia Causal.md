---
aliases: ["consistencia causal"]
---
El modelo de **consistencia causal** representa una flexibilización de la [[Consistencia Secuencial|consistencia secuencial]] en que hace la distinción entre eventos que son potencialmente relacionados causalmente y los que no (la causalidad se puede representar mediante un [[Relojes Lógicos#Relojes Vectoriales|reloj vectorial]]).

Considerando una interacción simple donde un proceso P1 escribe el valor de datos $x$. Y luego P2 lee $x$ y escribe $y$. Aquí la lectura de $x$ y la escritura de $y$ son potencialmente causalmente relacionados, dado que el cálculo de $y$ puee haber dependido del valor de $x$ leido por P2.

Por otro lado si dos procesos espontáneamente y simultáneamente escriben dos items de datos distinto, no están relacionados causalmente. A las operaciones que no están relacionadas causalmente se las llama **concurrentes**.

Para que un almacen de datos se considere causalmente consistente, es necesario que cumpla la siguiente condición:

> Escrituras que potencialmente están relacionadas por la causalidad, deben ser vistas por todos los procesos en el mismo orden. Las escrituras concurrentes pueden verse en un orden diferente en diferentes máquinas.

![[SSDD_consistencia_causal.png]]
