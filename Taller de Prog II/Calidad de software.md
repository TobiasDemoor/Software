Hay diferentes puntos de vista para definir [[Calidad|calidad]] de software. Desde el punto de vista del cumplimiento de los [[Requerimientos|requerimientos]] se puede definir como:
> El cumplimiento de los [[Requerimientos funcionales|requerimientos funcionales]] y de [[Performance|performance]] explícitamente definidos, de los estándares de desarrollo explícitamente documentados y de las características implícitas esperadas del desarrollo de software profesional. - Pressman

Desde el punto de vista del cliente o usuario:
> La calidad no se trata de tener cero defectos o una mejora medible de la proporción de defectos, no se trata de tener los requerimientos documentados. No es mas ni menos que **satisfacer las necesidades del cliente** (por mas que las necesidades estén o no correctamente documentadas). - Al Davis

Desde el punto de vista de los requerimientos y usuario:
> El grado con el que un sistema, componente o proceso cumple con los **requisitos especificados** y las **necesidades o expectativas** del cliente o usuario.

> Grado con el cual el cliente o usuario percibe que el software satisface sus expectativas. - IEEE 729-83

> Conjunto de propiedades y de características de un producto o servicio, que le confieren aptitud para satisfacer **necesidades explícitas o implícitas**. - ISO 8402:1984

#### Consideraciones
Para poder controlar la calidad del software es necesario, **definir** los parámetros e **indicadores de medición**. La calidad del software es medible y varía de un sistema a otro.
> Tom De Marco: "no se puede controlar lo que no se puede medir"

La calidad del software puede medirse después de elaborado el producto. Esto hace que el costo sea alto, ya que si se requieren modificaciones hay retrabajo necesario. La calidad se puede observar en características o atributos que se decidan (por ejemplo, la velocidad de conexión, navegabilidad, usabilidad, etc.).

Ya que hay tanto costo en corregir la calidad, no hay que solo pensar en calidad al momento de hacer las revisiones y pruebas, sino que debe ser una actividad durante todo el [[Software Development Lifecycle|ciclo de vida del software]].

Robert Glass: "La calidad es importante, pero si el usuario no está satisfecho, nada más importa en realidad." Esta frase nos lleva a diferenciar entre **calidad de producto** y **calidad de servicio**. Uno puede construir un producto de altísima calidad, pero si dicho producto no brinda el servicio que el cliente deseaba de nada vale su calidad.

La calidad de software es globalizada, un producto creado en Argentina para el mercado local será comparado con productos de empresas multinacionales. El estándar de los usuarios es alto.

Los cambios atentan contra la calidad de software.

La calidad no es testing, sino que el testing es una herramienta de la calidad.

### Perspectivas de la calidad
Se puede definir a la **calidad necesaria** como la que está dada por las necesidades del usuario.
A la **calidad programada** como la que está definida por el programador.
Y a la **calidad realizada** a la lograda en la implementación, esto no es solo teniendo en cuenta el software sino también la capacitación y la puesta en marcha en producción.

### Niveles de calidad del software
**Usabilidad**: el software es adecuado y fácil de utilizar para el usuario.
**Funcionalidad**: el sistema hace lo que corresponde.
**Funcionamiento**: que el sistema funcione adecuadamente.

### Costo calidad del software
![[Costos de la calidad]]

### Modelos de calidad del software
- ISO-9126 - Estándar de Evaluación de la Calidad de Software
- CMM - Capability Maturity Model
- Bootstrap 
- SPICE - Software Process Improvement and Capability Determination 
- [[FURPS+]] 
- Moprosoft 
- CMMi

### Factores que afectan la calidad de software
La calidad del producto se ve afectada por varios factores:
- Calidad del proceso
- Calidad del personal
- Tecnología de desarrollo
- Costo y tiempo


### Software Software Quality Assurance (SQA)
![[Software Quality Assurance]]

### Fiabilidad del software
La [[Reliability|fiabilidad]] puede ser medida mediante datos históricos. Es la probabilidad de operación libre de fallas de un programa de computadora en un entorno determinado y durante un tiempo específico.

Medidas de Fiabilidad y de Disponibilidad del Software:
Fiabilidad = Tiempo Medio Entre Fallas ( TMEF )
TMEF = TMDF + TMDR
TMDF = tiempo medio de falla
TMDR = tiempo medio de recuperación. (diferencia a TMDF ??)

Disponibilidad = ( TMDF / (TMDF + TMDR) )/100 %
