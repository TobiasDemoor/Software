La síntesis relacional es un algorítmo para obtener una descomposición en 3FN ([[Formas Normales|formas normales]]) SPI y SPDF ([[Propiedades de las descomposiciones relacionales|propiedades de descomposiciones]]):

1. Hallar la cobertura minimal $F_min$ para $F$ ([[Dependencia Funcional#Conjunto minimal de DF's|Fmin]]).
2. Cada DF de $F_min$ se convierte en un subesquema, juntando las que tienen igual lado izquierdo.
3. Si ninguno de los esquemas resultantes contiene una clave, se agrega un subesquema con los atributos de alguna clave.
4. Si alguno de los subesquemas está contenido totalmente en otro, se elimina (eliminar subesquemas redundantes).
5. Si hay atributos de R que no aparecen en ninguna relación, agregar un nuevo subesquema con los mismos ([[Propiedades de las descomposiciones relacionales#Preservación de atributos|propiedad de preservación de atributos]]).