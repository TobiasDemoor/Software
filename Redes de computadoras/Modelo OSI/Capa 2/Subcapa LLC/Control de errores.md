Se tienen dos estrategias básicas para manejar errores. Una es incluir suficiente información redundante para que el receptor pueda deducir cuáles debieron ser los datos transmitidos. La otra estrategia es incluir sólo suficiente redundancia para permitir que el receptor sepa que ha ocurrido un error (pero no qué error) y entonces solicite una retransmisión. La primera estrategia utiliza **códigos de corrección de errores**; la segunda usa **códigos de detección de errores**. El uso de códigos de corrección de errores por lo regular se conoce como **FEC (Forward Error Correction)**.

Cada una de estas técnicas tiene sus nichos. En los canales que son altamente confiables por ejemplo es más económoco utilizar un código de detección de errores y sólo retransmitir los bloques defectuosos que surgen ocasionalmente. En cambio en los canales con muchos errores, como los enlaces inalámbricos, es mejor agregar la redundancia suficiente a cada bloque para que el receptor pueda descubrir cuál era el bloque original que se transmitió.

#### Códigos de corrección de errores
Códigos de Hamming
Códigos de Reed-Solomon
Etc.

Todos estos códigos agregan redundancia a la información que se envía. Una trama consiste en m bits de datos y r bits redundantes.

#### Códigos de detección de errores
Paridad
Checksums
[[CRC]]

