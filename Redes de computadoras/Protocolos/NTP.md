**Network Time Protocol** es un [[Protocolo|protocolo]] de la [[Capa de aplicación|capa de aplicación]] del modelo OSI y pertenece a la pila de protocolos del [[Modelo TCP IP|modelo TCP/IP]].

El funcionamiento es bastante simple. Primero El cliente envia una solicitud con timestamp T₁ al servidor que al recibir coloca el timestamp T₂ (según su reloj local) y antes de enviar coloca el timestamp T₃, luego al regresar al cliente este almacena el timestamp T₄ de llegada. Ahora suponiendo que el delay de propagación de A a B es aproximadamente igual al delay de B a A se puede calcular el offset necesario $\theta$ mediante la siguiente formula:

$$\theta = T_3 + \frac {(T_2 - T_1)+(T_4-T_3)} 2 - T_4 = \frac {(T_2 - T_1)+(T_3-T_4)} 2$$

Se tienen estratos según la distancia lógica a un servidor que tiene un [[Reloj físico|reloj]] atómico, siendo estos los llamados servidor de estrato 1. Se dice que el propio reloj opera en el estrato 0.