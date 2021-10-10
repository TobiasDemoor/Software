Cuando tratamos con [[Sistemas Distribuidos|sistemas distribuidos]] muy grandes que se encuentran dispersos a través de una WAN, suele ser necesario tener en cuenta la proximidad. Si dos procesos se comunican con frecuencia puede ser conveniente asegurarse de que se encuentren cercanos físicamente.

### GPS
![[GPS]]

### Posicionamiento lógico
![[Geometric Overlay Networks]]

### Posicionamiento centralizado
Para posicionar un nodo en un espacio geométrico m-dimensional requiere m+1 medidas de distancia a nodos con posiciones conocidas. Surgen inconvenientes por el hecho de que las medidas no son constantes en el tiempo y que por ejemplo en [[Internet]] las mediciones de latencia pueden romper con la [[Desigualdad Triangular]].

Una solución a estos problemas es medir distancias contra nodos que son puntos de referencia (**landmarks**). Los landmarks miden sus latencias par a par y subsecuentemente informan al nodo central de computo las coordenadas para cada landmark. Un parámetro extra para minimizar el error acumulado es la dimensión m.
