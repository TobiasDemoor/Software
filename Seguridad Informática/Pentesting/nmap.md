nmap → Herramienta de reconocimiento por defecto.
zenmap → GUI de nmap.

```sh
$ nmap [tipo(s)_de_escaneo] [opciones] {red|host_objetivo}
```
Opciones comunes: 
- -sn : ping scan 
- -sS : syn/half scan 
- -sT : tcp/connect scan 
- -sA : ack scan 
- -sN : null scan 
- -sU : udp scan 
- -sF : fin scan 
- -sX : xmas scan 
- -sV : detección de versión de servicios 
- -O : detección de sistema operativo 
- -T<0-5>: temporizador, el valor más alto es más rápido 
- -v : salida detallada 
- -A : Enable OS detection, version detection, script scanning, and traceroute 
- -Pn: Tratar los host como online -- Evitar la descubrimiento con el ping.
