Genmsi es un sistema que permite desarrollar un modelo gráficamente y generar código
[[GPSS]].

## Diagrama de Flujo de Transacciones (DFT)
El DFT especifica el comportamiento de las transacciones en el modelo. Está compuesto por **módulos enlazados** donde cada módulo representa “una acción” o comportamiento específico. 

Los **módulos son de una clase**, dicha clase representa un comportamiento genérico. Algunos módulos se utilizan para declarar entidades, como por ejemplo los storage. Pero algunas entidades se “instancian” automáticamente con el primer uso, como por ejemplo los facility. Durante la ejecución de la simulación las transacciones se “mueven” por el diagrama en forma concurrente.

![[MyS_DFT_ejemplo.png]]

## Módulos
Representan el comportamiento o acción de una transacción. 
- Pertenecen a una clase que define el comportamiento genérico. 
	- Demora de tiempo 
	- Tomar un recurso 
	- Liberar un recurso 
	- Tomar una decisión 
	- Ingresar al sistema 
	- Salir del sistema 
- El comportamiento específico lo definen las propiedades del módulo 
	- ¿Cuánto tiempo está demorado? 
	- ¿Qué recurso toma? 
	- ¿Qué recurso libera? 
	- ¿Qué condición se debe cumplir para tomar una decisión? 
	- ¿Con qué frecuencia ingresa al sistema una transacción? 
- Tienen entradas y salidas para definir el flujo de las transacciones. 
	- De donde vienen y a dónde van las transacciones.

### Propiedades de un módulo
Las propiedades "son los parámetros" de un módulo, definen valores que son utilizados en su interior. En los módulos compuestos se pueden crear **propiedades sintetizadas** que son propiedades definidas por los módulos en su interior que pasan a ser del módulo compuesto. Se puede definir una propiedad sintetizada en varios módulos siempre que las propiedades originales sean del mismo tipo y clase.

La sintaxis para definirlas es ``[nombrePropiedad:'hint']`` o ``[nombrePropiedad]``.

### Módulos atómicos
- **Assign:** Permite asignar un valor a un parámetro de transacción.
- **InitialSV:** es un módulo no ejecutable que setea el valor de un [[SaveValue]] al inicio de la simulación.
- **VariableA:** es un módulo no ejecutable que utiliza una variable para devolver un número aleatorio en un rango especificado.
- **Variable:** es un módulo que permite utilizar libremente una variable para implementar cualquier cálculo.
- **Loop:** es un módulo ejecutable con 2 salidas, donde el destino de la transacción que ingresa depende del valor del parámetro de la transacción utilizado en la propiedad “Parámetro” del módulo. Funcionamiento: 
	- Resta 1 al valor del parámetro de la transacción 
	- Si el resultado es mayor a cero, la transacción itera por la salida “loop” 
	- Si el resultado es igual a cero, la transacción continúa por la salida 1
- **Table - Tabulate**
	- **Tabulate:** es un módulo ejecutable. Lo inserto en el lugar a contabilizar o tabular.
	- **Table:** es un módulo descriptivo. Indica de qué forma quiero mostrar los resultados y qué [[SNA]] se tabula.