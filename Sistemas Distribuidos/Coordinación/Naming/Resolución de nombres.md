Los espacios de nombre ofrecen un mecanismo conveniente para almacenar y recuperar información acerca de entidades por medio de nombres. Más generalmente, dada una ruta, debería ser posible buscar cualquier información almacenada en el nodo referido por ese nombre. El proceso de buscar un nombre se llama **resolución de nombres** o **name resolution**.

#### Mecanismo de clausura
La resolución de nombres solo puede ocurrir si conocemos cómo y dónde empezar. Conocer cómo y dónde comenzar la resolución de nombres es conocido, por lo general, como el **mecanismo de clausura**.

> Esencialmente, un mecanismo de clausura se encarga de seleccionar el nodo inicial en un espacio de nombres del cuál la resolución de nombres debe comenzar - Radia, 1989

#### Linking
Fuertemente relacionado a la resolución de nombres es el uso de **alias**. Un alias es otro nombre para la misma entidad. Una variable de entorno es un ejemplo de un alias. En términos de grafos de nombres, hay básicamente dos formas diferentes de implementar un alias. La primera es simplemente permitir múltiples rutas absolutas para referirse al mismo nodo (**hard link**). La segunda es representar una entidad con un nodo hoja pero en vez de almacenar la dirección o estado de dicha entidad, el nodo almacena una ruta absoluta (**symbolic link**).

#### Mounting
La resolución de nombres descripta hasta ahora toma lugar dentro de un solo espacio de nombres. Sin embargo, esta puede ser usada para combinar distintos espacios de nombres de una manera transparente (**mounting**).