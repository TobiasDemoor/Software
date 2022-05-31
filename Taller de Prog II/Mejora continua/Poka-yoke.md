Es un mecanismo de control de calidad que se encuentra dentro de un proceso que evita que el operario cometa errores, es una restricción que fue diseñada para forzar la correcta operación. Un ejemplo de esto es un USB que solo permite ser conectado de certa forma.

Dos tipos:
1. El error humano se vuelve imposible -> Funciones de **control**
2. Se resalata el error para que sea obvio para quien lo cometió -> Funciones de **advertencia**

Caracterísitcas:
- Es sencillo
- Es parte del proceso
- Está puesto en el lugar donde ocurre el error

### Implementación
Pasos:
- Describir el defecto
- Identificar lugares
- Detallar procedimientos
- Identificar errores
- Identificar condiciones
- Identificación del dispositivo.

Métodos:
- Método de contacto: se basa en los atributos físicos de nuestro producto (método pasa no pasa).
- Método del valor fijo: aplicado para tareas repetitivas, se le suele alertar al operario en caso que no se hayan cumplido todas las repeticiones.
- Método de secuencia: se tienen pasos distintos, se busca determinar si se cumplieron todos los pasos en el orden establecido.

### Beneficios
- Menos tiempo de capacitación
- Eliminación de operaciones de control de calidad
- Quitarle un pepso de encima a operadores con tareas repetitivas
- Prevenir que malos productos lleguen al consumidor
- Detección de errores a medida que ocurran
- Suele ser una técnica muy barata de implementar

### En el desarrollo de software
1. Listar todos los casos de uso para la aplicación.
2. Analizar los casos de uso preguntándose los 5 por qué (se va preguntando sobre la pregunta anterior hasta llegar al núcleo del problema).
3. aplicarse la técnica poka-yoke para evitar problemas.
4. Asegurarse de que la técnica diseñada para evitar el defecto funciona de manera correcta.
5. Añadir esta técnica a la lista de poka-yokes que deben realizarse antes de una nueva release.
6. Medir el éxito.

Se suele presentar como distintos tipos de pruebas o advertencias al usuario.
