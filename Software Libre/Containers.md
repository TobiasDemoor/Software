---
aliases: ["containers", "container"]
---
Un container es una entidad que me brinda abstracción del entorno de donde se está ejecutando pero a nivel SO es un proceso más. Es [[Virtualización|virtualización]] a nivel SO.

Los containers o contenedores son posibles gracias al aislamiento y la virtualización de procesos del sistema operativo, que permiten que varios componentes de la aplicación compartan los recursos de una sola instancia de un kernel de la misma manera que la virtualización de máquinas permite que varias máquinas virtuales (VM) compartan el recursos del hardware de un servidor físico.

![[SL_Containers.png]]

> La virtualización a nivel SO no es única de los containers sino que también se utiliza en:
> - zones (Solaris containers)
> - virtual private servers (OpenVZ)
> - virtual kernels (DragonFly BSD)
> - jails (FreeBSD, IOS)
> - etc.

### Ventajas
Los containers traen los mismos beneficios que las [[Virtualización#Razones|máquinas virtuales]] (VMs), incluido el aislamiento de aplicaciones, la [[Escalabilidad|escalabilidad]] y la [[Reliability|disponibilidad]]. Además tienen ventajas respecto a las VMs.

**Peso más ligero**: a diferencia de las máquinas virtuales, los contenedores no llevan la carga útil de una instancia completa del sistema operativo.

**Eficiencia de los recursos**: Se pueden ejecutar varias veces más copias de una aplicación en el mismo hardware que con las máquinas virtuales.

**Productividad mejorada para los desarrolladores**: en comparación con las máquinas virtuales, los contenedores son más rápidos y fáciles de implementar, aprovisionar y reiniciar. Esto los hace ideales para su uso en integración continua para un mejor ajuste para los equipos de desarrollo y DevOps.

> Es importante notar que no nos brindan seguridad de la misma manera que las VMs, ya que las llamadas al sistema siguen pasando al SO subyacente.
