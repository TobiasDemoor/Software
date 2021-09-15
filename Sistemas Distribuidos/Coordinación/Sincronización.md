Sincronización y coordinación son 2 fenómenos relacionados.
* En **sincronización de [[Proceso|procesos]]**, nos queremos asegurar que un proceso espera a otro para completar su operación.
* Cuando hablamos de **sincronización de datos**, el problema es asegurar que 2 conjunto dse datos son los mismos.
* En **coordinación**, el objetivo es manejar las interacciones y dependencias entre actividades en un [[Sistemas Distribuidos|sistema distribuido]].
Desde esta perspectiva, podemos afirmar que **la coordinación encapsula la sincronización**.

## Sincronización del reloj
Cuando cada máquina tiene su propio [[Reloj físico|reloj]], es posible que a un evento que ocurrió después de otro se le asigne una hora anterior.

### Algorítmos
Si una máquina tiene un receptor de UTC, el objetivo es mantener todas las otras máquinas sincronizadas a esta. Si ninguna tiene un receptor de UTC, cada máquina lleva cuenta de su propio tiempo y el objetivo es mantenerlas a todas tan juntas como sea posible.

Siendo el tiempo UTC t. El objetivo de los algoritmos de sincronización es mantener la desviación entre los relojes de dos máquinas pertenecientes a un sistema distribuido dentro de un margen especifico conocido como **precisión** $\pi$: 
$$\forall t, \forall p, q : |C_p(t)-C_q(t)| \le \pi $$

Notesé que la presición se refiere a la desviación *entre máquinas del sistema distribuido*. Si se considera una referencia externa se habla de **exactitud** ($\alpha$). Un conjunto de relojes exactos dentro de un margen $\alpha$ es preciso dentro de un margen $\pi = 2\alpha$.

En las especificaciones de un [[Reloj físico|reloj físico]] se incluye su **maximum clock drift rate** $\rho$. Si dos relojes se están desviando de UTC en direcciones opuestas en un tiempo $\Delta t$ luego de que fueron sincronizados, pueden estar a lo sumo a $2\rho * \Delta t*$. Si se quiere garantizar una precisión $\pi$, los relojes deben ser resincronizados (por software) al menos cada $\pi/(2\rho)$ segundos.

#### NTP
![[NTP]]

#### Berkeley algorithm
En Berkeley Unix hay un time server (en realidad es un time daemon) activo que consulta periodicamente al resto de los equipos sus tiempos. En base a esas respuestas, calcula un tiempo promedio y le comunica a las otras máquinas que avancen  o retrasen sus relojes al tiempo nuevo. Este método es adecuado para un sistema en el que ninguna máquina tiene un receptor de UTC. El tiempo del time daemon debe ser seteado periódicamente por un operador.
