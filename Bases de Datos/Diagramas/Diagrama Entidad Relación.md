# Diagrama Entidad Relación (DER)
## Elementos de un DER
### Conjunto de Entidades
Todos los conceptos, cosas u objetos del mundo real que queremos modelar constituyen las entidades de nuestro modelo. *Las entidades se denotan con un rectángulo, con el nombre dentro de él.*
El nombre de la entidad lo escribimos en singular. Debe ser claro y explícito de la información contenida en la entidad, ya que nos da la semántica de la entidad.
Las entidades pueden ser **fuertes** o **débiles**. Las entidades fuertes son aquellas que tienen una existencia independiente de cualquier otra entidad, se identifican sólo por atributos propios. Las entidades débiles son aquellas que derivan su existencia de otra entidad y necesitan la identificación de dicha entidad para distinguirse de otras.
Las entidades fuertes se denotan con un rectángulo con línea simple. *Las entidades débiles se denotan con un rectángulo con línea doble.*
![[der_entidades_fuertes_1.png]]
![[der_entidades_debiles_1.png]]

### Atributos
Los atributos describen a las entidades. Son la información concreta que queremos mantener para una entidad. *Se denotan con una elipse vinculada a una entidad, con el nombre dentro de la elipse.*
![[der_atributos_1.png]]

#### Atributos identificatorios
Los elementos de cualquier entidad se distinguen por el valor de algún atributo identificatorio (o de varios atributos en conjunto). A este atributo (o conjunto de atributos) se lo denomina **clave primaria** (PK – Primary Key).
La clave primaria es un **conjunto minimal** (que no tiene elementos redundantes) de atributos identificatorios y *se denota subrayando a los mismos con una línea continua*. **Toda** entidad debe tener indefectivlemente una clave primaria.
Hay ocasiones donde hay más de un atributo que distingue unívocamente a los elementos de una entidad, en forma independiente uno de otro (por ejemplo, un empleado que se distinga por su número de legajo o por su CUIL). Todos ellos son **claves candidatas**, y se deberá elegir uno de ellos como clave primaria. Las claves candidatas no se modelan en el [[Modelo Entidad Relación|MER]], recién lo veremos al trabajar con el [[Modelo Relacional|Modelo Relacional]].
Se llama **discriminante** o **clave parcial** al conjunto de atributos que se usa para distinguir una entidad débil de las otras con la misma relación. Se *identifican mediante un subrayado discontinuo*.
![[der_atributos_identificatorios_1.png]]

#### Atributo cálculado
Si un atributo de una entidad se obtiene a partir de una operación con los otros atributos se dice que es una atributo cálculado. *Un atributo cálculado se denota con una elipse de trazo discontinuo vinculada a la entidad.*

### Interrelaciones
Una interrelación es una asociación entre entidades. Formalmente una interrelación es una relación matemática sobre n>=2 entidades (no necesariamente distintas). *Las interrelaciones se representan con un rombo que vincula las distintas entidades participantes de la misma*.
Cada interrelación tiene un nombre, que debe ser lo más representativo posible, ya que ese nombre nos va a indicar la semántica de la interrelación. El nombre de la interrelación en lo posible debe estar expresado como un predicado.
Cuando se trata de interrelaciones, hay 3 características a considerar: el **grado**, la **cardinalidad** y la **participación** de las entidades.
![[der_interrelaciones_1.png]]

#### Grado
El grado de una interrelación se refiere a la cantidad de entidades que intervienen en ella.

#### Cardinalidad
La cardinalidad de una interrelación se refiere a la cantidad de elementos de un rol de la interrelación que puede estar vinculado a un elemento de otro rol de la interrelación. Se pueden tener interrelaciones 1:1, 1:N o N:M, y se debe escribir junto al vínculo en el diagrama.
*Una interrelación muchos a muchos puede ser representada por un conjunto de entidades fuertes con dos interrelaciones uno a muchos.*

#### Participación
Decimos que los elementos de una entidad participan de una interrelación. Si todo elemento de la entidad tiene que estar necesariamente en la interrelación (al menos una vez), decimos que la participación es total. Caso contrario (puede haber elementos que no participen) decimos que es parcial u opcional.
*La participación parcial de una entidad en una interrelación se denota poniendo una “O” sobre el vínculo que une el rombo de la relación con la entidad.*
*La participación total se denota por la ausencia de la notación anterior.*

#### Atributos de interrelaciones
Las interrelaciones también pueden tener sus atributos en determinadas circunstancias y estos pueden ser descriptivos o identificatorios. Los atributos de una interrelación se representan igual que los de las entidades, con la diferencia que están vinculados al rombo de la interrelación. Estos atributos son permitidos únicamente en interrelaciones N:M.
Un **atributo descriptivo de una interrelación** permite registrar información adicional a la que aportan de las entidades intervinientes en ella.
Un **atributo identificatorio de una interrelacion** es un poco más complejo que el anterior. Es un atributo que identifica esa relación, por ejemplo si tenemos las entidades Estudiante y Materia relacionadas dicha relación tendrá un atributo identificatorio de fecha_inscripción. Así pueden haber muchar relaciones distintas entre el mismo estudiante y la misma materia pero con fechas de inscripción distintas. Estos *se identifican con un subrayado*.

#### Interrelaciones identificatorias de entidades débiles
Una entidad débil es una entidad que necesita a otra para identificarse. Por lo tanto, tenemos que tener una manera de indicar cuál es la entidad fuerte correspondiente a una entidad débil. Si bien la entidad débil va a estar interrelacionada con su entidad fuerte, también podría estarlo con otras de las cuales no depende su identificación. Para no tener ambigüedades, *a la interrelación que vincula una entidad débil con su entidad fuerte correspondiente (llamada interrelación identificatoria) la denotaremos también con un rombo con línea doble*.

## Elementos de un DER extendido
### Jerarquías
Puede darse que haya entidades que constituyan casos particulares de otras entidades, por ejemplo Materia con Laboratorio podría ser un caso especial de Materia. Esta situación la modelamos de una forma especial, con una jerarquía o especialización. Esta relación nos da una jerarquía, una especie de herencia (no es herencia en el sentido completo de objetos). Con estas relaciones, las propiedades de la entidad padre (la superentidad) son heredadas por las entidades hijas (las subentidades).
La identificación de las entidades hijas también es la misma que la de la entidad padre. No puede existir un elemento en una subentidad que no figure en la superentidad. Cada especialización tiene una semántica y decimos que hay un discriminante que determina la especialización. *La notación está dada por un pequeño círculo vinculado a la superentidad, al cual se vinculan las subentidades, colocando el nombre del discriminante junto al círculo (el discriminante nos indica la semántica de la jerarquía).*

#### Cobertura
La cobertura nos indica si todos los elementos de la superentidad van a tener algún elemento correspondiente en alguna subentidad.
**Cobertura Parcial u Opcional**: En este caso, un elemento de la superentidad no necesariamente está en una subentidad. Se lo denota colocando una “O” en el vínculo entre el círculo y la superentidad.
**Cobertura Total**: En este caso, todo elemento de la superentidad debe estar en al menos una subentidad. Se lo denota con una línea simple uniendo el círculo con la superentidad.

#### Solapamiento
El solapamiento nos indica si los elementos de la superentidad pueden estar en más de una subentidad simultáneamente.
**Jerarquía Disjunta**: Los elementos de la superentidad pueden estar a lo sumo en una subentidad. Se lo denota con una 'd' en el círculo.
**Jerarquía con Solapamiento**: Los elementos de la superentidad pueden estar en más de una subentidad. Se lo denota con una 'o' en el círculo (del inglés overlapping).

### Agregación
En algunas ocasiones, durante el proceso de modelado surge la necesidad de representar interrelaciones donde participan otras interrelaciones.
La agregación es una [[Abstracción|abstracción]] en la cual una interrelación (junto con sus entidades vinculadas) es tratada como una entidad de alto nivel y puede participar de interrelaciones. Por supuesto, las entidades vinculadas a una agregación también pueden tener sus propias interrelaciones individualmente.
*El concepto de agregación se denota con un rectángulo conteniendo a la interrelación y sus entidades vinculadas.*
