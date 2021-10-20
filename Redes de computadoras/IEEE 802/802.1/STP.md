Cuando un [[Switch|switch]] con **Spanning Tree (STP, IEEE 802.1D)** se enciende no arranca inmediatamente, tiene un tiempo de convergencia. Primero tiene que armar el árbol, para esto intercambian paquetes de STP. Una vez establecida la topología periódicamente se mandan mensajes para comunicar que siguen en pie. Los enlaces extra quedan en stand-by y si se llega a perder uno en uso se reforma la topología.

**Rapid Spaning Tree (IEEE 802.1w)** es un desarrollo sobre STP para reducir el tiempo de convergencia del protocolo, ya que en el STP básico es muy elevado (en el orden del minuto).