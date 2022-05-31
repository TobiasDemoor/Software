---
aliases: ["proxys", "proxy", "server proxy"]
---
Un proxy es un intermediaro entre el host local y otra red, normalmente la web. La máquina local no sale a la red externa sino que le hace la petición al proxy. Hay varios tipos de proxy, entre ellos:
- Proxy [[HTTP]] (puerto 80)
- Proxy [[HTTPS]] (puerto 443)
- Proxy cache:  este tipo de proxy almacena respuestas previas aumentando la velocidad aparente de la red.
- Proxy FTP (puertos 20,21)

Ventajas de usar proxys:
- **Control**: sólo el proxy hace el trabajo real. Puede limitar y restringir.
- **Ahorro Trafico**: Solo el proxy navega o sale a [[Internet]] (se ahorra ancho de banda).
- **Velocidad Tiempo Respuesta**: Si varios clientes van a pedir el mismo recurso, el uso del cache disminuye el tiempo de respuesta aparente.
- **Filtrado de contenidos**: El proxy aplica politicas de permitir o no una petición.
- **Modificación**: Puede modificar la información.
- **Anonimato**: Oculta los usuarios detras del proxy.

Desventajas de usar proxys:
- **Abuso**: Al recibir peticiones de muchos usuarios y responderlas. Es dificil de controlar la cantidad de trabajo.
- **Carga**: Un proxy ha de hacer el trabajo de muchos usuarios.
- **Intromisión**: Es un paso más entre origen y destino, hay usuarios que no quieren pasar por el proxy.
- **Incoherencia**: Si hace de caché y este falla.
- **Irregularidad**: No siempre es bueno ocultar usuarios. Hay sitios que restringen su uso.

Algunos proxys:
Basados en hardware propietario: CISCO, Enterasys, MikroTic, etc.
Basados en software: [[Apache HTTP Server|Apache]], SQUID, Microsoft Proxy Server, etc.
