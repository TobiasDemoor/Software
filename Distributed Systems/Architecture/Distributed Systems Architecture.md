# Distributed Systems Architecture
Los [[Distributed Systems|sistemas distribuidos]] (DS) suelen ser piezas complejas de software en las cuales por definición sus [[Component|componentes]] están distribuidos a través de multiples equipos. Para dominar esta complejidad es necesario que estos sistemas estén correctamente organizados. Se puede realizar una división entre la organización lógica de la colección de componentes de software, y la organización física.

La organización de DS es principalmente acerca de los componentes de software que componen el sistema. Estas [[Software Architecture|arquitecturas de software]] nos dicen cómo los varios componentes van a estar organizados y como deberían interactuar.

Un objetivo importante de los DS es separar las aplicaciones de las plataformas subyacentes mediante la capa de [[Middleware|middleware]]. El adoptar esta capa es una desición arquitectónica importante, y su propósito principal es el proveer [[Distribution Transparency|transparencia de distribución]]. Se debe notar que hay trade-offs necesarios para lograr la transparencia, eso ha llevado a varias técnicas para ajustar el middleware a las necesidades de las aplicaciones que lo utilizan.

La realización contreta del DS requiere que instanciemos y coloquemos software en hardware real. Hay varias decisiones que se deben tomar para hacer esto. La instanciación final de la arquitectura de software suele ser nombrada como la arquitectura de sistema o [[System architecture|system architecture]].
