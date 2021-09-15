
## Sincronización
Sincronización y coordinación son 2 fenómenos relacionados.
* En sincronización de [[Proceso|procesos]], nos queremos asegurar que un proceso espera a otro para completar su operación.
* Cuando hablamos de sincronización de datos, el problema es asegurar que 2 conjunto dse datos son los mismos.
* En coordinación, el objetivo es manejar las interacciones y dependencias entre actividades en un [[Sistemas Distribuidos|sistema distribuido]].
Desde esta perspectiva, podemos afirmar que **la coordinación encapsula la sincronización**.

### Sincronización del reloj
Cuando cada máquina tiene su propio [[Reloj|reloj]], es posible que a un evento que ocurrió después de otro se le asigne una hora anterior.
