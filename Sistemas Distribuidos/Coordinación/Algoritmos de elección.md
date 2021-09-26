En muchos [[Sistemas Distribuidos]] se requiere que un proceso actúe como coordinador, iniciador o que cumpla un rol especial. En general no importa cuál proceso tiene esta responsabilidad, pero uno debe hacerlo y el resto debe estar de acuerdo en quien lo hace.

Si todos los procesos son exactamente idénticos es indistinto cuál es elegido. Podemos suponer que cada proceso P tiene un identificador único $id(P)$. En general, los algorítmos de elección intentan localizar el proceso con el mayor id y designarlo como coordinador. Los algorítmos difieren en cómo localizan al coordinador.

También suponemos que cada proceso conoce los identificadores de todos los otros procesos. Lo que desconocen es el estado de los procesos. El objetivo es que cuando se inicia la elección esta concluya con todos los procesos de acuerdo en quién es el nuevo coordinador.

### Bully algorithm
Se consideran N procesos $\{P_0,\cdots,P_{N-1}\}$ siendo $id(P_k)=k$. Cuando algún proceso nota que el coordinador ya no reacciona da inicio a una elección. Un proceso $P_k$ lleva a cabo una elección de la siguiente manera:
1. $P_k$ envia un mensaje ELECTION a todos los proceso con ids mayores a el ($P_{k+1},P_{k+2},\cdots,P_{N-1}$).
2. Si ninguno responde, $P_k$ gana la elección y se convierte en el coordinador.
3. Si uno responde toma el control y el trabajo de $P_k$ finaliza.

En cualquier momento un proceso puede recibir un mensaje ELECTION de uno de sus colegas inferiores. Cuando recibe este mensaje, el receptor envía un OK al remitente para indicar que está vivo y puede hacerse cargo. El receptor entonces lleva a cabo una elección (a menos que ya esté llevando una a cabo). Eventualmente, todos los procesos excepto uno se rinden, y entonces ese es el nuevo coordinador. Luego anuncia su victoria enviando un mensaje a todos los procesos comunicando que con efecto inmediato el es el nuevo coordinador.

Si un proceso que no estaba activo pasa a estarlo entonces lleva cabo una elección. Si ocurre que el es el de mayor id entonces gana la elección. Por lo tanto siempre gana el mayor (por esto el nombre).