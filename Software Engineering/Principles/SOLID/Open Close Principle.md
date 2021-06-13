"A module should be open for extension but closed for modification." ([[Software Engineering/Patrones/GRASP/Polimorfismo]])

The Open-Closed Principle (OCP), described by Bertrand Meyer in \[MeyerSS\] is essentially equivalent to the [[Variaciones protegidas|PV pattern]] and to [[Ocultamiento de la información|information hiding]]. A definition of OCP is:
>Modules should be both open (for extension; adaptable) and closed (the module is closed to modification in ways that affect clients).

OCP and [[Variaciones protegidas|PV]] are essentially two expressions of the same principle, with different emphasis: protection at variation and evolution points. In OCP, "module" includes all discrete software elements, including methods, classes, subsystems, applications, and so forth. In the context of OCP, the phrase "closed with respect to X" means that clients are not affected if X changes. For example, "the class is closed with respect to instance field definitions" through the mechanism of data encapsulation with private fields and public accessing methods. At the same time, they are open to modifying the definitions of the private data, because outside clients are not directly coupled to the private data.