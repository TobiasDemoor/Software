La criptología estudia los problemas teóricos en la [[Seguridad|seguridad]] en el intercambio de mensajes. Tiene dos ramas, la [[Criptografía|criptografía]] (el arte de escribir mensajes secretos) y el [[Criptoanálisis|criptoanálisis]] (el arte de descifrar mensajes secretos).

## Criptosistemas
![[Criptosistemas]]

## Esteganografía
![[Esteganografía]]

## Criptoanálisis
![[Criptoanálisis]]

## Criptosistemas específicos
### El cuadrado de Polibio
Es un algoritmo trivial donde cada letra del alfabeto es reemplazada por las coordenadas de su posición en un cuadrado. El cuadrado básico es de 5x5 (agrupando i y j) y se puede extender a 6x6 para agregar cifras y signos de puntuación.

### Método de los confederados
Es un tipo de sustitución poli alfabética. Básicamente, se escoge una clave, que se va “sumando” al texto llano para dar lugar al texto cifrado. Para sumar se suman los índices de las letras (A=1, B=1, etc.). Los espacios se pueden ignorar.

### Cifrados mono-alfabéticos
Sin desordenar los símbolos dentro de un mensaje, establecen una correspondencia única para todos ellos en todo el texto.

#### *Cifrado de cesar*	
Se establece una correspondencia de una letra a la otra según un salto fijo.

#### *Cifrado de cesar con salto y palabra*
Consiste en utilizar un salto y una palabra clave. Para escribir el diccionario de destino primero se coloca una palabra elegida, sin repetir caracteres, y luego se completa el abecedario. Después de esto se efectúa un cifrado de Cesar común con el alfabeto de destino modificado.

### Cifrados poli-alfabéticos
La sustitución aplicada a cada carácter varía en función de la posición que ocupe éste dentro del texto plano. 

#### *Sistema Vigénere*
Matriz de 26x26 (a..z) desplazada de a 1 por fila. La clave es una palabra de K letras. Teniendo una frase a encriptar y la clave se toman los primeros caracteres de ambas palabras colocando la letra de la palabra para determinar la fila y la de la clave la columna. El carácter resultante va al criptograma, se avanza en ambas palabras. Al terminar la palabra clave se vuelve a su inicio.

Esto es equivalente a sumar los índices letra por letra con los índices comenzando en 0.

### Cifrado de trasposición
La idea es no sustituir unos símbolos por otros, sino que cambia su orden dentro del texto.

## Algoritmos simétricos de cifrado (criptografía moderna)
La gran mayoría de los algoritmos de cifrado simétricos se apoyan en los conceptos de confusión y difusión inicialmente propuestos por Shannon. Para conseguir algoritmos fuertes sin necesidad de almacenar tablas enormes es intercalar confusión (sustituciones simples, con tablas pequeñas) y difusión (permutaciones). En muchos casos el criptosistema no es más que un paso simple de sustitución-permutación repetido n veces, como ocurre con [[DES]] (Data Encryption Standard).

### Fesitel
![[Feistel]]

### DES
![[DES]]

### IDEA
![[IDEA]]

## Algoritmos asimétricos de cifrado
Constan de dos claves diferentes denominadas clave privada y clave pública. Una de ellas se emplea para codificar, mientras que la otra se usa para decodificar. Dependiendo de la aplicación que le demos al algoritmo la clave pública será la de cifrado o viceversa. En el caso de comunicación privada se cifra con la clave pública y en caso de autenticación se cifra con la clave privada.

### Autenticación
La segunda aplicación de los algoritmos asimétricos es la autentificación de mensajes con ayuda de funciones resumen. Las funciones resumen permiten obtener una firma a partir de un mensaje.

### RSA
![[RSA]]

### La propagación de la confianza
- Infraestructura de clave pública o PKI.
	- Entidades emisoras de certificados (Autoridades de certificación o CA del inglés Certification Authority)
- Establecimiento de una red de confianza.
	- No hay nodos aparte de los usuarios.
	- Los usuarios recogen claves públicas de otros usuarios y aseguran su autenticidad.
- Criptografía basada en identidad.
	- PKG (Private Key Generator)
	- Hay un Generador que reparte las Caves Publicas y privada a quien corresponda.
- Criptografía basada en certificados.
	- En este modelo el usuario posee una clave privada y otra pública.
	- La clave pública la envía a una Autoridad de certificación que basándose en criptografía basada en identidad genera un certificado que asegura la validez de los datos.
- Criptografía sin certificados.
	- KGC (Key Generator Center) es una clave parcial.
	- La clave privada completa se genera a partir de la clave privada parcial y un valor generado aleatoriamente por el usuario

## Firma Digital
![[Firma digital]]