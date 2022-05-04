- Cuando hablamos de *[[Seguridad]]*, hablamos de una medida de confiabilidad del Sistema de Computación (SC) relacionada, fundamentalmente a la garantía de la integridad del propio SC y de la capacidad de discriminar el acceso al mismo.
- Una vez que el usuario ingresó al SC (incluso habiendo cumplido adecuadamente la identificación y autenticación) tiene acceso a los recursos (e instancias de recursos) del SC para realizar sus operaciones, por medio de procesos. No todos los usuarios tienen los mismos permisos de acceso a los diferentes recursos. Aquí interviene la **PROTECCIÓN.**
- El rol de la protección es el de proveer un mecanismo para reforzar las políticas que gobiernan un recurso.

Cuando hablamos de **PROTECCIÓN**, nos referimos a un problema interno del SC, y tiene que ver con la capacidad de administrar los permisos de acceso y de uso de los recursos del SC por parte de los procesos.

- *Garantizar la Protección de un SC es administrar, conforme la política establecida, los privilegios que los procesos tienen sobre los recursos (e instancias) del SC.*
- Un sistema es una colección de procesos y recursos (hardware o software).
- Los recursos básicos (4) tienen una granularidad muy grande para ser susceptibles de asignar privilegios. Incluso si hablamos de instancias.
- Un [[Sistemas Operativos/Conceptos/Proceso]] no puede tener tal o cual privilegio sobre “la información” como recurso, dado que es un recurso muy amplio y es conveniente asignar privilegios según una unidad menor (carpeta o [[archivo]] o celda de un archivo, por ejemplo). Si un proceso tuviese privilegios sobre un dispositivo de E/S por ejemplo, podría manipular TODA la información que maneje dicho dispositivo.
- Si la granularidad la hacemos muy fina, nos quedamos con una unidad de asignación de privilegios muy pequeña y, entonces, la asignación de privilegios es interminable.

## **Principio del mínimo privilegio**
A cada programa, usuario o sistema se le otorga los privilegios justos y necesarios para realizar sus tareas. Por ejemplo, si a un guardia se le asigna una llave para abrir solamente la habitación que debe cuidar, si pierde la llave entonces el daño es pequeño.
## **Objeto**
Un **Objeto** es cualquier componente del SC (hardware o software) que pueda ser identificado unívocamente (puede ser tanto un dispositivo, un directorio, un archivo, un archivo de datos, una fila dentro del archivo de datos, una columna o una celda, según convenga). Se le puede aplicar privilegios de acceso a un objeto.
### Cada Objeto tiene: 
- Un nombre único que lo identifica (Object Id.)
- Un conjunto de operaciones que puede realizar un proceso sobre él. Este conjunto está limitado por el objeto. Por ejemplo, una impresora se limita a imprimir.
- Si el administrador del SC puede definir los Objetos del mismo, tiene la flexibilidad necesaria para manejar la protección y definir las operaciones permitidas. 
### Derecho de acceso (Access Right, AR)
Es el permiso o privilegio que tiene un proceso para realizar una operación sobre un objeto.

### Estructura de un Dominio
- Un **Dominio** es un conjunto de procesos con iguales privilegios (derechos de acceso) sobre los mismos objetos.
- Decimos que el proceso opera en un dominio.
- Asociación *proceso-dominio*
  - *Estática.* El conjunto de objetos disponibles para un proceso es fijo durante la vida del proceso.
  - *Dinámica.* El proceso puede cambiar de dominio durante la ejecución
#### *Formas de definir un dominio*
- *Por usuario.* Cada usuario podría es un dominio. El cambio de dominio implica un cambio de usuario.
- *Por proceso.* Cada proceso es un dominio. El cambio de dominio ocurre cuando un proceso envía un mensaje a otro y espera una respuesta.
- *Por función-método.* El conjunto de objetos que pueden ser accedidos corresponde a las variables locales definidas en el procedimiento. El cambio de dominio ocurre cuando se invoca una función.* 

### Perfiles de usuario
- Los usuarios que comparten privilegios sobre determinados recursos se definen persistentemente en grupos denominados Perfiles.
- Procesos de usuarios que comparten un Perfil conforman, por defecto, un Dominio.
- Un Dominio de protección define un conjunto de objetos junto con sus derechos de acceso.




## **Matriz de protección de acceso**
Es un modelo o mecanismo que permite especificar distintas políticas, y definir e implementar un control estricto (tanto para asociación estática como dinámica) de los privilegios de acceso. 

Usualmente, es el usuario quien define los AR para un objeto. Por ejemplo, cuando un usuario crea un archivo, puede definir los accesos de R/W para los distintos dominios.
### Elementos de la matriz de acceso:
- Filas (Dominios).
- Columnas (Objetos).
- Celdas (AR que los procesos del dominio tienen sobre el objeto).
- Es 3D, dado que cada celda puede contener más de un AR (read/write/execute, etc.).

- La Matriz de acceso es un mecanismo flexible y autoprotegido. La misma matriz y los mismos dominios pueden ser objetos.
- Puede expandir la protección dinámicamente: Permite que determinados dominios agreguen o eliminen AR, es decir, existen dominios que tienen privilegios sobre otros dominios. 
- Al permitir cambios controlados de los valores de la matriz, se requieren operaciones especiales: 
  - *Owner de un objeto.* Cuando un dominio tiene el acceso de owner sobre un objeto, un proceso que se ejecute en ese dominio puede modificar los accesos que los demás dominios u objetos posean sobre ese objeto.
  - *Copy AR de un objeto a otro*. Por ejemplo, si D1 tiene un AR de read\* (el asterisco indica que puede copiarse) sobre el archivo F2, un proceso ejecutándose en el dominio D1 puede copiar ese AR a cualquier otra entrada referida a F2. Puede suceder que, si se copia el AR a otra entrada de F2, no se transfiera la copiabilidad, es decir, se copia AR y no AR\*. Existe la variante de cortar y pegar.




- *Control.* Si un dominio Di tiene control sobre otro dominio Dj, entonces Di puede modificar los accesos del dominio Dj (usualmente solo eliminar, no agregar).
 
- Transferencia de AR de un dominio a otro.
- Cuando un proceso quiere cambiar de un dominio a otro, se debe tratar a los dominios como un objeto. Un proceso del dominio D1 puede cambiar al dominio D2 si (D1, D2) contiene switch.


- Establecida la política de protección, el Administrador del SC debe configurar la Matriz (Mecanismo) para llevar adelante la política.
- La matriz, como objeto, debe ser protegida y debe asegurarse el uso correcto de la misma.
- El SO debe proveer los medios para implementar la matriz como mecanismo general de administración de la protección. 
- Hay diversas formas de implementar esta matriz, dependiendo del SO.
## **Implementaciones de la matriz de acceso**
### Tabla global
- La matriz se implementa como una tabla global en memoria.
- Es dinámica, muy grande y 3D (cada celda posee varios AR).
- Muy cara y difícil de administrar.
- Es rala (baja densidad de datos).
- Cada ocasión en la que un proceso quiere realizar una acción sobre un objeto, el SO debe acceder a la tabla para verificar si la operación requerida está permitida en su dominio.

### Listas de control de acceso (ACL)
- La matriz se puede descomponer en columnas. Tantas listas como objetos haya en el SC.
- Para cada objeto, una lista de control de acceso enumera los usuarios y sus derechos de acceso permitidos.
- Cada lista de objeto (ACL) tiene elementos del tipo dupla: **(*Dominio, AR).
- No se utiliza espacios muertos para guardar valores nulos de la matriz.
- Si quiero filtrar los AR de un dominio, tengo que recorrer las listas de todos los objetos (costoso). Es sencillo desde la perspectiva del objeto, no así del dominio.

### Listas de capacidades (CL)
- Descomposición por filas de la matriz de acceso. Tantas listas como dominios haya en el SC.
- Especifica los objetos y las operaciones autorizadas para un proceso que opera en ese dominio.
- Cada lista de capacidades (CL) tiene elementos del tipo dupla: (Objeto, AR).
- Cada elemento de la lista se llama “capacidad”.
- Las CL son mantenidas y protegidas por el sistema operativo. Si todas las capacidades de un objeto están protegidas, entonces el objeto también lo está.

### Bits de protección - Unix
- Es una implementación para Archivos, generalizable a otros objetos.
- Consiste en agregar un atributo de 9 bits por archivo, que indican si el Dueño, Grupo u otros usuarios pueden Leer, Escribir o Ejecutar el archivo ([[UNIX]]).

### ACL vs CL
- La ACL se corresponde con necesidades del usuario. Se carga cuando un proceso de un dominio solicita una operación sobre el objeto. Muchas listas cortas.
- La CL se utiliza para localizar información del proceso. Se carga cuando nace un proceso del dominio y quiere acceder a un objeto (debe tener la capacidad para realizar la acción). Pocas listas largas.
- La mayoría de los SSOO utilizan una combinación de ACL y CL. Cuando un proceso intenta a acceder por primera vez a un objeto, se busca en la lista de acceso. Si el acceso es denegado, ocurre una interrupción. Si el acceso es concedido, se crea y se asigna una capacidad al proceso para futuros accesos más rápidos. Luego del último acceso, se destruye la capacidad. Esta estrategia se utiliza en los sistemas MULTICS.

## **Seguridad y protección**
- La [[Seguridad]] y la Protección son dos aspectos complementarios en un SC que el ser humano debe administrar.
- En ambos casos, las definiciones en términos de política y administración son cuestiones propias de un profesional de la informática.
- El SO solo brinda herramientas para facilitar la administración.
- Se deben definir políticas que garanticen un equilibrio entre Seguridad y Protección en base al fin pretendido.