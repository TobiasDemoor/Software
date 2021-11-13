> El **ruido** son las señales adicionales insertadas entre el transmisor y el receptor.

Para cualquier dato transmitido, la señal recibida consistirá en la señal transmitida modificada por las distorsiones introducidas en la transmisión, además de señales no deseadas que se insertarán en algún punto entre el emisor y el receptor. A estas últimas señales no deseadas se les denomina **ruido**. El ruido es el factor de mayor importancia de entre los que limitan las prestaciones de un sistema de comunicación.

La señal de ruido se puede clasificar en cuatro categorías:
- **Ruido térmico.** Se debe a la agitación térmica de los electrones. Está presente en **todos** los dispositivos electrónicos y medios de transmisión; como su nombre indica es función de la temperatura. El ruido térmico está uniformemente distribuido en el espectro de frecuencias, por esto a veces se denomina ruido blanco. 
	> N = kTB \[W]
	> donde
	> k = constante de Boltzmann,
	> T = temperatura \[K],
	> B = Ancho de banda \[Hz]

- **Ruido de itermodulación.** Puede producirse cuando señales de distintas frecuencias comparten el mismo medio de transmisión. El efecto del ruido de intermodulación es la aparición de señales a frecuencias que sean suma o diferencia de las dos frecuencias originales o múltiplos de éstas.

- **Diafonía.** Se trata de un acoplamiento no deseado entre las líneas que transportan las señales, es decir a señal de un cable "se pasa al otro". Esto puede ocurrir por el acoplamiento eléctrico entre cables de pares cercanos o, en raras ocasiones, en líneas de cable coaxial que transporten varias señales. La diafonía también puede aparecer cuando las señales no deseadas se captan en las antenas de microondas; aunque éstas se caracterizan por ser altamente direccionales, la energía de las microondas se dispersa durante la transmisión. Generalmente, la diafonía es del mismo orden de magnitud (o inferior) que el ruido térmico.

- **Ruido impulsivo.** A comparación de los anteriores es no continuo y está constituido por pulsos o picos irregulares de corta duración y de amplitud relativamente grande. Se generan por una gran diversidad de causas, por ejemplo, por perturbaciones electromagnéticas exteriores producidas por tormentas atmosféricas o por fallos y defectos en los sistemas de comunicación o por aparatos electrónicos cercanos (ej: motores eléctricos, tubos fluorecentes, transformadores, *"mientras más watts más interferencia"*).