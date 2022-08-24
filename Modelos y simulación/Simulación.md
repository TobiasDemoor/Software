![[Simular]]

## Etapas de la simulación
### Construcción del modelo
- **Definición del sistema con el máximo de detalle:** evaluar sus características, definir límites del mismo, analizar condiciones iniciales, régimen transitorio y permanente, qué resultados se desean obtener, evitar construir el modelo inmediatamente.
- **Elección del método para realizar el estudio:** buscar una solución analítica al problema, si no se encuentra entonces usar simulación.
- **Variables a incluir en el modelo:** cuáles variables / parámetros son importantes y debo incluir en mi estudio. Cuáles son internas y controladas por mi sistema y cuales son externas y fuera de control.
- **Recolección y análisis de los datos del sistema:** qué valores toman las variables, varían con el tiempo u otro factor, siguen alguna distribución de probabilidad: [[Distribución normal|normal]], [[Distribución de Poisson|poisson]], [[Distribución uniforme|equiprobables]].
- **Definición de la estructura del modelo:** identificar y definir los atributos de las entidades permanentes y las transitorias, que eventos producen cambios de estado en mi sistema.
- **Creación del modelo:** crear un programa que represente el modelo

### Ensayo de alternativas
- **Validación del modelo:** hay que verificar algunas situaciones conocidas y analizar sus resultados para ver si se corresponden con el sistema real.
- **Análisis y crítica de los resultados:** verificar que con los resultados obtenidos se puedan tomar decisiones, evitar información superflua, compactar la información representándola en cuadros, tablas o gráficos para simplificar su análisis y estudio por parte del usuario final. Si es posible, proponer alguna alternativa que mejore el rendimiento del sistema.

## Preguntas frecuentes
- **¿Puede fallar una simulación?** SI, puede fallar porque el modelo no es válido (no representa fielmente al sistema real) y/o porque las alternativas simuladas no son buenas alternativas y al recomendar la mejor se recomendará "la menos mala" de las ensayadas (la cual no dejaría de ser mala).
- **¿Se puede demostrar que un modelo es válido?** NO, ya que para esto habría que probar todos los casos posibles, ensayarlos tanto en el sistema real como en el modelo y verificar su concordancia (imposible en la práctica).
- **¿Se puede demostrar que un modelo es inválido?** SI, basta un caso en que los resultados obtenidos en el modelo y los obtenidos en el sistema real no se correspondan para demostrar que el modelo es inválido.
- **¿Se puede simular un sistema continuo usando un modelo discreto?** SI, el estudio del movimiento del fluido por una cañería (Fluidodinámica) corresponde a sistemas continuos. Sin embargo si el fluido se lo discretiza dividiéndolo en gotas y se construye un modelo discreto por el cual circulan gotas de agua (una, dos, diez, cien, mil) podemos simularlo correctamente.
- **¿Se puede simular un sistema determinístico usando un modelo estocástico?** SI, supongan que se desea calcular la superficie comprendida entre el eje X y una curva Y=f(X) en el intervalo 0 -1, aplicando integrales obtenemos el resultado (problema determinístico). Sin embargo, si generamos una cantidad muy grande de puntos al azar con coordenadas (X,Y) donde 0<=X<=1 y 0<=Y<=1, entonces podemos calcular la superficie utilizando el método de Monte Carlo, donde: $Area = n / N$

## Herramientas
Lenguaje de programación:
- **[[GPSS]]**: General Purpose Simulation System (GPSS, en español: Simulación de Sistemas de Propósito General) es un lenguaje de programación de propósito general de simulación a tiempo discreto. Desarrollado por Geoffrey Gordon (1960 - Bell Telephone Laboratories/IBM).

Software
- **VisualSis**: Es un sistema que implementa GPSS y permite realizar simulaciones. Desarrollado por Eduardo Garrido y Estanislao Mileta (2001 - Universidad FASTA).
- **Genmsi**: Es un sistema que permite desarrollar un modelo gráficamente y generar código GPSS. Desarrollado por Eduardo Barrena y Juan Ignacio Iturriaga (2008 - Universidad FASTA). En el 2014 se amplió para realizar y monitorear simulaciones.