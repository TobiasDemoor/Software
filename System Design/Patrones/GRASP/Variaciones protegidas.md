## Problema
¿Cómo diseñar componentes de manera que futuras variaciones e inestabilidades no tengan impacto en el funcionamiento de otros?

## Solución
Identificar potenciales puntos de variación o inestabilidades y asignar responsabilidades para crear una interfaz (contrato) estable alrededor de ellos.

Este es un patrón general que implica la motivación de aplicar principios de diseño, [[Patrones|patrones]] y [[Tácticas|tácticas]] de programación para proporcionar flexibilidad.
Hay que prestar atención, especular y elegir batallas. Porque hay:
- **Puntos de variación:** cambios en los requerimientos actuales.
- **Puntos de evolución:** potenciales cambios que podrían aparecer pero no están presentes en los requerimientos actuales.

## Ventajas
- Se añaden fácilmente las extenciones ([[SOLID Principles#Open Close Principle OCP|OCP]]).
- Se pueden introducir variaciones sin afectar clientes ([[SOLID Principles#Liskov Substitution Principle LSP|Liskov]]).
- Se reduce el [[Acoplamiento|acoplamiento]].
- Menor costo de cambios.

## Mecanismos
- Data-driven designs.
- Service lookup.
- Interpreter-driven desings.
- Reflective desings.
- Uniform access.
- [[SOLID Principles#Liskov Substitution Principle LSP|Liskov Substitution Principle]].
- Structure-hiding desings ("No hables con extraños")
```
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