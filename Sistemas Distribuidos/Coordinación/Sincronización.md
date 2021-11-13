Sincronización y coordinación son 2 fenómenos relacionados.
- En **sincronización de [[Proceso|procesos]]**, nos queremos asegurar que un proceso espera a otro para completar su operación.
- Cuando hablamos de **sincronización de datos**, el problema es asegurar que 2 conjuntos de datos son los mismos (consistencia de datos).
- En **coordinación**, el objetivo es manejar las interacciones y dependencias entre actividades en un [[Sistemas Distribuidos|sistema distribuido]].
Desde esta perspectiva, podemos afirmar que **la coordinación encapsula la sincronización**.

## Sincronización del reloj
Cuando cada máquina tiene su propio [[Reloj físico|reloj]], es posible que a un evento que ocurrió después de otro se le asigne una hora anterior aunque se los haya sincronizado tiempo atrás. Esto es así ya que cada reloj tiene una tendencia diferente y se retrasa o adelanta a lo largo del tiempo.

### ¿Qué hora es?
#### Referencia astronómica
- **Referencia al sol.** Todos los días, el sol asciende por el este, se posiciona en un punto máximo en el cielo (mediodía), y luego vuelve a descender por el oeste (desde nuestro sistema de referencias, claro). Como se define que un día tiene 24 horas y cada hora contiene 3600 segundos, el **segundo solar** se define como 1/86400 partes de día solar. Se define al **segundo medio solar** tomando la duración media de un día. Un problema que se presenta es que la tierra gira cada vez más lento, el período orbital no es constante. 
- **Referencia a una estrella más lejana**

#### Reloj atómico
En 1948, se comienza a utilizar el conteo de las transiciones del átomo de cesio 133 (definido como Tiempo Atómico Internacional). Se define a 1 segundo como el tiempo que le toma a un átomo de cesio 133 en realizar 9.192.631.770 transiciones.

Como la tierra gira cada vez más lento, el segundo medio solar es cada vez más largo, por lo que, si no se ajusta el TAI, el mediodía será cada vez más temprano respecto al verdadero punto máximo del sol. Para esto se aplican correcciones cada vez que el TAI difiere en 800𝑚𝑠 del segundo solar medio.

#### UTC
Para acordar qué hora es hoy en día se utiliza el tiempo coordinado universal (UTC). Existen 40 estaciones de radio de onda corta emiten un pulso por cada segundo UTC con una precisión de 1ms (el error de recepción en la práctica es de ~10ms), a su vez algunos satélites terrestres ofrecen servicio UTC. Combinando la recepción de múltiples satélites se puede lograr una precisión de 50ns.

### Algorítmos de sincronización
Si una máquina tiene un receptor de UTC, el objetivo es mantener todas las otras máquinas sincronizadas a esta. Si ninguna tiene un receptor de UTC, cada máquina lleva cuenta de su propio tiempo y el objetivo es mantenerlas a todas tan juntas como sea posible.

Siendo el tiempo UTC t. El objetivo de los algoritmos de sincronización es mantener la desviación entre los relojes de dos máquinas pertenecientes a un sistema distribuido dentro de un margen especifico conocido como **precisión** $\pi$ (**sincronización externa**): 
$$\forall t, \forall p, q : |C_p(t)-C_q(t)| \le \pi $$

Notesé que la presición se refiere a la desviación *entre máquinas del sistema distribuido*. Si se considera una referencia externa se habla de **exactitud** ($\alpha$). Un conjunto de relojes exactos dentro de un margen $\alpha$ es preciso dentro de un margen $\pi = 2\alpha$.

$$\forall t, \forall p : |C_p(t)-t| \le \alpha $$

En las especificaciones de un [[Reloj físico|reloj físico]] se incluye su **maximum clock drift rate** $\rho$. Si dos relojes se están desviando de UTC en direcciones opuestas en un tiempo $\Delta t$ luego de que fueron sincronizados, pueden estar a lo sumo a $2\rho * \Delta t*$. Si se quiere garantizar una precisión $\pi$, los relojes deben ser resincronizados (por software) al menos cada $\pi/(2\rho)$ segundos.

#### NTP
![[NTP]]

#### Berkeley algorithm
En Berkeley Unix hay un time server (en realidad es un time daemon) activo que consulta periodicamente al resto de los equipos sus tiempos. En base a esas respuestas, calcula un tiempo promedio y le comunica a las otras máquinas que avancen  o retrasen sus relojes al tiempo nuevo. Este método es adecuado para un sistema en el que ninguna máquina tiene un receptor de UTC. El tiempo del time daemon debe ser seteado periódicamente por un operador.

## Relojes Lógicos
![[Relojes Lógicos]]