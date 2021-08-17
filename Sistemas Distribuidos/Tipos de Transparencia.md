De ISO Reference Model-Open Distributed Processing 1998 ([[Transparencia]])

# Transparencia de acceso
Ocultar las diferencias en representación de datos y la forma en que el usuario accede a los recursos (arquitecturas, OS)

# Transparencia de ubicación 
Ocultar las diferencias donde físicamente se ubican los recursos en un sistema. Utilización de nombres lógicos (ej. http://www.slashdot.org/index.htm)

# Transparencia de migración 
Soportar la movilidad de procesos y recursos iniciados por los usuarios

# Transparencia de reubicación 
El transporte de un recurso de una ubicación a otra no debe ser “notado” mientras lo estamos usando (portátiles en uso de un lugar a otro)

# Transparencia de replicación 
Ocultar que existen diferentes copias del mismo recurso (replicas). (= transp. ubicación)

# Transparencia de concurrencia 
Un usuario no debería notar que otro está haciendo uso del mismo recurso. Al finalizar, el recurso tiene que estar en un estado consistente

# Transparencia de fallas
Un usuario o aplicación no debe notar que alguna parte del sistema falla. Muchas veces es prácticamente imposible.
Incapacidad de distinguir un proceso penosamente lento de uno muerto o una red severamente congestionada.
Tipos de fallas:
- Falla de congelación ("no responde más")
- Falla de omision
	- De recepción ("nunca se recibió el mensaje")
	- De envío ("nunca se envió la respuesta")
- Falla de tiempo (timeout)
- Falla de respuesta ("hay una respuesta pero no es lo esperado")
	- Falla de valor
	- Falla de transición de estado 
- Falla arbitraria . “Bizantina”