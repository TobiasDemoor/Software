---
aliases: ["consistencia eventual"]
---
La **consistencia eventual** es un modelo de consistencia donde se tienen pocos procesos que escriben (o usualmente uno solo), por lo que se evitan los conflictos write-write. Entonces lo único que se debe gestionar en este modelo son los conflictos read-write y que las copias se actualicen. La forma de tratar con esto es tratar las operaciones de escritura como lazy, por lo tanto tomarán lugar cuando puedan, así el almacen llegando a un estado consistente eventualmente.
