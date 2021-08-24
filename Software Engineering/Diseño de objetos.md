The design of objects can be broadly divided into two groups:
1. Those chosen by **representational decomposition**.
2. Those chosen by **behavioral decomposition**.

For example, the cration of a software class such as *Sale* is by representational decomposition; the software class is related to or represents a thing in a [[Software Engineering/Fundamentals/Dominio|domain]]. Representational decomposition is a common strategy in object design and supports the goal of reduced representational gap. But sometimes, we desire to assign responsibilities by grouping behaviors or by algorithm, without any concern for creating a class with a name or purpose that is related to a real-world domain concept.

A good example is an "algorithm" object such as a *TableOfContentsGenerator*, whose purpose is to generate a table of contents and was created as a helper or convenience class by a developer, without any concern for chosing a name from the [[Software Engineering/Fundamentals/Dominio|domain]] vocabulary of books and documents. It exists as a convenience class conceived by the developer to group together some related behavior or methods, and is thus motivated by *behavioral decomposition*.

To contrast, a software class named *TableOfContents* is inspired by *representational decomposition*, and should contain information consistent with our concept of the real [[Software Engineering/Fundamentals/Dominio|domain]].

- (Larman, Applying UML and patterns)

# Diseño detallado
Luego de identificar los [[Requerimientos|requerimientos]] y crear un [[Domain Model|modelo de dominio]], se añaden métodos a las clases de software y se definen los mensajes entre los objetos para completar los requerimientos. El definir qué métodos pertenecen a qué objetos y cómo los objetos deberían interactuar es una tarea crucial.