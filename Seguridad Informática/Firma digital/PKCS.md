**Public-Key Cryptography Standars** se refiere a un grupo de estándares de criptografía de clave pública concebidos y publicados por los laboratorios de [[RSA]].

PKCS#7 es un estándar para firmar o cifrar datos (ellos lo llaman "sobreado"). Dado que el certificado es necesario para verificar datos firmados, es posible incluirlos en la estructura SignedData. Un archivo .P7C es simplemente una estructura SignedData, sin datos para firmar.

PKCS#12 evolucionó del estándar PFX (Personal inFormation eXchange) y se usa para intercambiar objetos públicos y privados dentro de un archivo.