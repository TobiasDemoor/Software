Cuando tratamos con [[Sistemas Distribuidos|sistemas distribuidos]] muy grandes que se encuentran dispersos a través de una WAN, suele ser necesario tener en cuenta la proximidad. Si dos procesos se comunican con frecuencia puede ser conveniente asegurarse de que se encuentren cercanos físicamente.

### GPS
El problema del posicionamiento es resuelto, por un sistema distribuido dedicado especifico denominado GPS (sistema de posicionamiento global), el cual es un sistema distribuido basado en satélites. El sistema utiliza 24 [[Satélites de comunicación|satélites]] que orbitan a ~20.200 Km (MEO). Cada satélite tiene hasta cuatro relojes atómicos que son regularmente calibrados. 

Cada satélite difunde continuamente su posición, añadiendo un Timestamp del tiempo local. Esto permite a cada receptor en la tierra calcular su propia posición usando, en principio, solamente 4 satélites.

La forma de calcular un punto en el espacio se hace mediante intersección de 4 casquetes esféricos de radio conocido. El radio del casquete se conoce ya que se conoce el tiempo que demoró la señal en llegar.

El sistema GPS también se utiliza para sincronizar relojes