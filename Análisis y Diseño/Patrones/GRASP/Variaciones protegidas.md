## Problema
¿Cómo diseñar [[Componente|componentes]] de manera que futuras variaciones e inestabilidades no tengan impacto en el funcionamiento de otros?

## Solución
Identificar potenciales puntos de variación o inestabilidades y asignar responsabilidades para crear una [[Interfaz|Interfaz]] (contrato) estable alrededor de ellos.

Este es un patrón general que implica la motivación de aplicar principios de diseño, [[Patrones|patrones]] y [[Tácticas|tácticas]] de programación para proporcionar flexibilidad.
Hay que prestar atención, especular y elegir batallas. Porque hay:
- **Puntos de variación:** cambios en los requerimientos actuales.
- **[[Puntos de evolución]]:** potenciales cambios que podrían aparecer pero no están presentes en los requerimientos actuales.

## Ventajas
- Se añaden fácilmente las extenciones ([[Open Close Principle]]).
- Se pueden introducir variaciones sin afectar clientes ([[Liskov Substitution Principle]]).
- Se reduce el [[Acoplamiento|acoplamiento]].
- Menor costo de cambios.

## Mecanismos
### Core protected variations mechanisms 
Data encapsulation, interfaces, [[Polimorfismo|polymorphism]], [[Indirección|indirection]], and standards.

### Data-driven designs
Data-driven designs cover a broad family of techniques include reading codes, values, class file paths, class names, and so forth, from an external source in order to change the behavior of, or "parameterize" a system in some way at runtime.

### Service lookup
Service lookup includes techniques such as using naming services or traders to obtain a service. Clients are protected from variations in the location of services, using the stable interface of the lookup service. It is a special case of **data-driven desings**.

### Interpreter-driven desings
Interpreter-driven desings include rule interpreters that execute rules read from an external source, script or language interpreters that read and run programs, virtual machines, neural network engines that execute nets, constraint logic engines that read and reason with contraint sets, and so forth.this approach allows changing or parametrizing the behavior of a system via external logic expressiones. The system is protected from the impact of logic variations by externalizing the logic, reading it in, and using an iterpreter.

### Reflective desings
An example of this approach is using the java.beansJntropsector to obtain a BeanInfo object, asking for the getter Method object for a bean property X, and calling Methos, invoke (Dependency injection). The system is protected from the impact of logic or external code variations by reflective algorithms that use introspectionand meta-language services. It may be considered a special case of **data-driven designs**.

### Uniform access
Some languages support a syntactic construct so that both a method and field acces are expressed the same way. For example, adrcle.radius may invoke a radiusQ:float method or directly refer to a public field, depending on the definition of the class. We can change from public fields to access methods, without changing the client code.

### [[Liskov Substitution Principle ]]
LSP formalizes the principle of protection agains variations in diferent implementations of an interface, or subclass extensions of a superclass.

### Structure-hiding desings
**Don't talk to strangers** or the **Law of Demeter**. Briefly it means to avoid creating designs that traverse long object structure paths and send messages (or talk) to distant, indirect objects (strangers). Such desings are fragile with respect to changes in the object structures (a common point of instability).
It places constraints on what objects you should send messages to within a method. It states that within a method, messages should only be sent to the following objects:
1. The *this* object (or *self*).
2. A parameter of the method.
3. An attribute of *this*.
4. An element of a collection which is an attribute of *this*.
5. An object created within the method.
The intent is to avoid coupling a client to knowledge of indirect objects and the object connections between objects. 
```Java
class Register {
	private Sale sale;

	public void slightlyFragileMethod() {
		// sale.getPayment() sends a message to a "familiar"
		
		// but in sale.getPayment().getTenderedAmount()
		// the .getTenderedAmount() message is to a "stranger" Payment
		
		Money amount = sale.getPayment().getTenderedAmount();
		//...
	}
	//...
}
```

## Notas
Este GRASP es muy similar tanto a el [[Ocultamiento de la información]] como al [[Open Close Principle]].