Es el [[Protocolo|protocolo]] que utilizan los navegadores web para intercambiar información con los sitios web. Se encuentra en la [[Capa de aplicación|capa de aplicación]].

| Version | Descripción                                                  | [[RFC]] |
| ------- | ------------------------------------------------------------ | ------- |
| 1.0     | Versión pública inicial, solo tiene GET                      | 1945    |
| 1.1     |                                                              | 2616    |
| 1.2     |                                                              | 2774    |
| 2.0     | Protocolo binario en vez de texto; multiplexado; server push | 7540    |
| 3.0     | Adios TCP, hola [[QUIC]]                                         | 9000    |

> Un método no seguro es aquel que modifica el estado interno del servidor.

En HTTP/3 se pasa de TCP a QUIC por las ineficiencias de TCP frente a las pérdidas de paquetes y al inicio de la conexión.

> TCP slow start se usa porque la ventana TCP arranca chica y se va agrandando. Empieza chica para evitar las retransmisiones. La pérdida de paquetes en TCP genera que se reduzca abruptamente la ventana.
