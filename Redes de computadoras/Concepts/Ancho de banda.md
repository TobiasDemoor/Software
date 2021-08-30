Se denomina **ancho de banda** al rango de frecuencia que se transmite a través de un medio sin una atenuación considerable. En la práctica se mide desde 0 hasta la frecuencia donde disminuye la potencia a la mitad.

El ancho de banda es una propiedad física del medio de transmisión que depende; por ejemplo, de la construcción, el grosor y la longitud de un cable o fibra óptica. A menudo se utilizan filtros para limitar el ancho de banda de una señal. Por ejemplo, los canales inalámbricos [[WiFi|802.11]] pueden utilizar aproximadamente 20MHz, por lo que los radios 802.11 filtran el ancho de banda de la señal con base a este tamaño. Este filtrado permite que más señales compartan una región dada en un espectro, lo cual mejora la eficiencia del sistema en general. Lo que significa que el rango de frecuencia para ciertas señales no empezará en cero, pero no importa. El ancho de banda sigue siendo el rango de la banda de frecuencias que se transmiten, y la información que se puede transportar depende sólo de este ancho de banda, no de su frecuencia inicial ni final. Las señales que van desde cero hasta una frecuencia máxima se llaman señales de **banda base**. Las que se desplazan para ocupar un rango de frecuencias más altas, como es el caso de todas las transmisiones inalámbricas, se llaman señales de **pasa-banda**.

Es importante notar que al limitar el ancho de banda se limita la tasa de datos, incluso en canales perfecto. En la siguiente tabla se muestra que ocurre al aumentar la tasa de datos con un ancho de banda base fijo en 3000 Hz.

![[ancho_de_banda_tasa_de_datos.png]]

Lo definido anterior mente es el **ancho de banda analógico**, como se define en electrónica. Para el area de ciencias de la computación se suele hablar del **ancho de banda digital** que es la tasa de datos máxima de un canal (medido en bps). Esa tasa de datos es el resultado final de usar el ancho de banda analógico de un canal físico para transmisión digital, ambos están relacionados.

## La tasa de datos máxima de un canal
Henry Nyquist (1924) demostró que si se pasa una señal cualquiera a través de un filtro low-pass con un ancho de banda *B*, la señal filtrada se puede reconstruir por completo tomando sólo *2B* muestras (exactas) por segundo. No tiene caso muestrear la línea más de *2B* veces por segundo, ya que los componentes de mayor frecuencia que dicho muestreo pudiera recuperar ya se han filtrado. Si la señal consiste en *V* niveles discretos, el teorema de Nyquist establece lo siguiente:

Tasa de datos máxima = 2*B* log<sub>2</sub>(*V*) bits/seg

Por ejemplo, un canal sin ruido de 3kHz no puede transmitir señales binarias (de dos niveles) a una velocidad mayor de 6000 bps.

Hasta ahora hemos considerado sólo los canales sin ruido. Si hay ruido aleatorio presente, la situación se deteriora con rapidez. Y siempre hay ruido aleatorio (térmico) presente debido al movimiento de las moléculas en el sistema. La cantidad de ruido térmico presente se mide con base en la relación entre la potencia de la señal y la potencia del ruido; llamada **SNR (Signal-to-Noise Ratio)**. Si denotamos la potencia de la señal mediante S y la potencia del ruido mediante N, la SNR es S/N. Por lo general la relación se expresa en decibeles (*10 log<sub>10</sub>(S/N \[bps]) \[dB]*).

El principal resultado de Shannon es que la tasa de datos máxima (o **capacidad**) de un canal ruidoso, cuyo ancho de banda es *B* Hz y cuya relación señal a ruido es S/N, está dada por:

Capacidad = *B log<sub>2</sub> (1 + S/N)*

Esto nos indica las mejores capacidades que pueden tener los canales reales. Por ejemplo, la **ADSL (Línea Asimétrica de Suscriptor Digital)** que provee acceso a Internet a través de líneas telefónicas comunes, utiliza un ancho de banda de aproximadamente 1 MHz. La SNR depende en gran parte de la distancia entre el hogar y la central telefónica; una SNR de alrededor de 40 dB para líneas cortas de 1 a 2 km es algo muy bueno. Con estas características, el canal nunca podrá transmitir a más de 13 Mbps, sin importar cuántos niveles de señal se utilicen ni con qué frecuencia se tomen las muestras. En la práctica, el servicio ADSL se especifica hasta 12 Mbps, aunque es frecuente que los usuarios vean tasas más bajas. En realidad esta tasa de datos es muy buena, con más de 60 años de técnicas de comunicaciones que han reducido la brecha entre la capacidad de Shannon y la capacidad de los sistemas reales.

El resultado de Shannon se derivó de los argumentos de la teoría de la información y se aplica a cualquier canal sujeto a ruido térmico. Los ejemplos contrarios se deben clasificar en la misma categoría que las máquinas de movimiento perpetuo. Para que el servicio ADSL sobrepase los 13 Mbps, debe mejorar la SNR (por ejemplo, insertando repetidores digitales en las líneas más cercanas a los clientes) o usar más ancho de banda, como se está haciendo con la evolución al servicio ADSL2+.