1. Buscar una [[Dependencia Funcional|DF]] $X \rightarrow Y$ que viole la [[Formas Normales#Forma Normal de Boyce-Codd FNBC|FNBC]]. Partir $R$ en $R_1$ y $R_2$ tal que:
	1. $R_1 = XY$
	2. $R_2 = R-Y$
> $\rho = (R_1, R_2)$ es SPI porque aplica la [[Propiedades de las descomposiciones relacionales#Propiedad de descomposición binaria|regla de descomposición binaria]].
2. Seguir descomponiendo cada subesquema hasta que todas las hojas del árbol de descomposición estén en FNBC. Las hojas formarán la descomposición en FNBC SPI.