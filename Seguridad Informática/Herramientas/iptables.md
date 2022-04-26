iptables es una utilidad del kernel de [[Linux]] que permite definir reglas de [[Firewall|firewall]]

Ejemplo 
```sh
# setup
iptables -I INPUT 1 -p tcp --dport 80 -j DROP
iptables -I INPUT 1 -s 181.31.236.50 -p tcp --dport 80 -j ACCEPT
iptables -I INPUT 1 -s 159.223.155.189 -p tcp --dport 80 -j ACCEPT
iptables -I INPUT 1 -s 140.93.240.242 -p tcp --dport 80 -j ACCEPT
iptables -I INPUT 1 -s 5.189.164.172 -p tcp --dport 80 -j ACCEPT
iptables -I INPUT 1 -s 165.232.141.187 -p tcp --dport 80 -j ACCEPT
iptables -I INPUT 1 -s 104.248.93.232 -p tcp --dport 80 -j ACCEPT
iptables -I INPUT 1 -s 54.232.107.172 -p tcp --dport 80 -j ACCEPT
iptables -I INPUT 1 -s 144.126.212.95 -p tcp --dport 80 -j ACCEPT
iptables -I INPUT 1 -s 66.70.255.144 -p tcp --dport 80 -j ACCEPT

# agregar
sudo iptables -I INPUT 1 -s <IP> -p tcp --destination-port 80 -j ACCEPT
sudo iptables-save > /etc/iptables/rules.v4 # persiste los cambios

# borrar
iptables -L INPUT --line-numbers # para ver numeros por regla
sudo iptables -D INPUT <numero de regla>
sudo iptables-save > /etc/iptables/rules.v4 # persiste los cambios
```