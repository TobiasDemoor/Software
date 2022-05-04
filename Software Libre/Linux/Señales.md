Los [[Sistemas Operativos/Conceptos/Proceso|procesos]] en [[Linux]] pueden recibir señales de otros procesos. Las señales se usan para notificar a otros procesos y "avisarles" cosas, como por ejemplo que un hijo suyo ha ejecutado exit (SIGCHLD) o que debe finalizar su ejecución (SIGKILL, SIGTERM).

|  Señal  |  Valor   | Acción | Comentario                                                                       |
|:-------:|:--------:| ------ | -------------------------------------------------------------------------------- |
| SIGHUP  |    1     | Term   | Cuelgue detectado en la terminal de <br> control o muerte del proceso de control |
| SIGINT  |    2     | Term   | Interrupción procedente del teclado                                              |
| SIGQUIT |    3     | Term   | Terminación procedente del teclado                                               |
| SIGILL  |    4     | Term   | Instrucción ilegal                                                               |
| SIGABRT |    6     | Term   | Señal de aborto procedente de abort(3)                                           |
| SIGFPE  |    8     | Term   | Excepción de coma flotante                                                       |
| SIGKILL |    9     | Term   | Señal de matar (no puede ser capturada <br> por el proceso)                      |
| SIGSEGV |    11    | Core   | Referencia inválida a memoria                                                    |
| SIGPIPE |    13    | Term   | Tubería rota: escritura sin lectores                                             |
| SIGALRM |    14    | Term   | Señal de alarma de alarm(2)                                                      |
| SIGTERM |    15    | Term   | Señal de terminación (enviada por Ctrl+C)                                        |
| SIGUSR1 | 30,10,16 | Term   | Señal definida por usuario 1                                                     |
| SIGUSR2 | 31,12,17 | Term   | Señal definida por usuario 2                                                     |
| SIGCHLD | 20,17,18 | Ign    | Proceso hijo terminado o parado                                                  |
| SIGCONT | 19,18,25 |        | Continuar si estaba parado                                                       |
| SIGSTOP | 17,19,23 | Stop   | Parar proceso  (no puede ser capturada <br> por el proceso)                      |
| SIGTSTP | 18,20,25 | Stop   | Parada escrita en la tty                                                         |
| SIGTTIN | 21,21,26 | Stop   | Entrada de la tty para un proceso de fondo                                       |
| SIGTTOU | 22,22,27 | Stop   | Salida a la tty para un proceso de fondo                                         |
