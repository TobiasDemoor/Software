BIND 9 es uno de los servidores [[DNS]] más utilizados.

En linux se instala como el paquete bind9 y bind9utils con su directorio de configuración en /etc/bind. Si se desea agregar una zona se debe referenciar a nuestro archivo de configuración para esta en `named.conf.default-zones`, se agregan de la siguiente forma:

``` conf
zone "gidi.edu.ar" {
	type master;
	file "/etc/bind/db.gidi.edu.ar";
}
```

### Ejemplos
``` conf
; BIND data file for Ejemplo
;
$TTL 60800
@    IN  SOA gidi.edu.ar. root.gidi.edu.net. (
		2022052600    ; Serial:  siempre incremental
		    604800    ; Refresh: tiempo de espera para el secundario
		     86400    ; Retry:   tiempo de espera si falla
		   2419200    ; Expire:  máxima espera para expirar en el secundario
		    604800 )  ; Negative Cache TTL: tiempo de vida
;
@        IN    NS        gidi.edu.ar.
@        IN    A         10.0.1.1     ; <- gidi.edu.ar
www      IN    A         10.0.1.10    ; <- www.gidi.edu.ar
mail     IN    A         10.0.2.100   ; <- mail.gidi.edu.ar
server2  IN    A         10.0.2.101   ; <- server2.gidi.edu.ar
mail2    IN    CNAME     server2      ; mail2.gidi.edu.ar == server2.gidi.edu.ar
dns1     IN    CNAME     gidi.edu.ar. ; dns1.gidi.edu.ar == gidi.edu.ar
@        IN    MX    5   mail.gidi.edu.ar.
@        IN    MX    10  mail2.gidi.edu.ar.
```

``` conf
; BIND reversa data file
;
$TTL 60800
@    IN  SOA gidi.edu.ar. root.gidi.edu.net. (
		2022052600    ; Serial:  siempre incremental
		    604800    ; Refresh: tiempo de espera para el secundario
		     86400    ; Retry:   tiempo de espera si falla
		   2419200    ; Expire:  máxima espera para expirar en el secundario
		    604800 )  ; Negative Cache TTL: tiempo de vida
;
@        IN    NS    gidi.edu.ar.
1.1      IN    PTR   gidi.edu.ar.
10.1     IN    PTR   www.gidi.edu.ar.
100.1    IN    PTR   mail.gidi.edu.ar.
101.1    IN    PTR   server2.gidi.edu.ar.
```