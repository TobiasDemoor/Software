#### ALOHA puro
La idea básica de un sistema ALOHA es sencilla: permitir que los usuarios transmitan cuando tengan datos por enviar. Por supuesto, habrá oclisiones y las tramas en colisión se dañarán. Los emisores necesitan alguna forma de saber si éste es el caso. En el sistema ALOHA después de que cada estación envía su trama a la computadora central, ésta vuelve a difundir la trama a todas las estaciones. Así una estación emisora puede escuchar la difusión de la estación terrena maestra (hub) para ver si pasó su trama o no. En otros sistemas, como las [[Wireless LAN|LAN alámbricas]], el emisor podría ser capaz de escuchar si hay colisiones mientras transmite.

Si la trama fue destruida, el emisor simplemente espera un tiempo aleatorio y la envía de nuevo. El tiempo de espera debe ser aleatorio o las mismas tramas chocarán una y otra vez, en sincronía. Los sistemas en los cuales varios usuarios comparten un canal común de modo tal que puede dar pie a conflictos se conocen como sistemas de **contención**. A esta versión del algoritmo se la denomina **ALOHA puro** al ser un algorítmo tan simple es ineficiente, ronda en un 18% de uso del canal.

![[RRCC_aloha_puro.png]]

#### ALOHA ranurado
Si se definen [[Problema de acceso al medio|ranuras]] donde se pueden enviar tramas la eficiencia mejora mucho (se duplica), ya que sin esto basta con que se solapen ligeramente dos tramas para que ambas se pierdan. A este algorítmo se lo llama **ALOHA ranurado**.

![[RRCC_aloha_ranurado.png]]