## Contexto - Problema
Mantener separadas del resto del sistema las modificaciones en la interfaz de usuario de modo que la vista únicamente tenga la [[Responsabilidad|responsabilidad]] de actuar como medio de entrada/salida del sistema. 

## Solución
Separar la aplicación en tres componentes principales:
- **Model**: contiene los datos de la aplicación referidos al modelo de negocios.
- **View**: muestra una determinada porción de los datos e interactúa con el usuario.
- **Controller**: se encarga de mediar la interacción entre el modelo y la vista y maneja las notificacions de cambio de estado.
Es una aplicación del principio de [[Model-View Separation]].

## Debilidades
La complejidad de implementación puede no valer la pena dependiendo de la simplicidad de la interfaz de usuario. Puede suceder que la división no encaje perfectamente para algunas librerías de componentes visuales.