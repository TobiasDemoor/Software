Es un estándar [[UIT-T]] para infraestructuras de claves públicas ([[PKI]]). X.509 especifica, entre otras cosas, formatos estándar para certificados de claves públicas y un algoritmo de validación de la ruta de certificación. Su sintaxis, se define empleando el lenguaje ASN.1 (Abstract Syntax Notation One), y los formatos de codificación más comunes son DER (Distinguish Encoding Rules) o PEM (Privacy Enhanced Mail). En el sistema X.509, la autoridad certificadora (AC) emite un certificado asociando una clave pública a un Nombre Distinguido particular en la tradición de X.500 o a un Nombre Alternativo tal como una dirección de correo electrónico o una entrada de DNS.

La estructura de un certificado digital X.509 v3 es la siguiente:
- Certificado
    - Versión
    - Número de serie del certificado
    - ID del algoritmo utilizado por el CA para firmar (típicamente RSA o DSA)
    - Emisor (CA)
    - Validez
        - No antes de
        - No después de
    - Sujeto, (sujeto titular) expresado en notación DN (Distinguished Name), compuesto por CN (Common Name), OU (Organizational Unit), O (Organization) y C (Country). El sujeto puede ser una persona, un servidor o un servicio.
    - Información de clave pública del sujeto
        - Algoritmo de clave pública
        - Clave pública del sujeto
    - Identificador único de emisor (opcional)
    - Identificador único de sujeto (opcional)
    - Extensiones (opcional)
        - ...
- Algoritmo usado para firmar el certificado
- Firma digital del certificado


Las extensiones de archivo de certificados X.509 son:
- .CER - Certificado codificado en CER (Canonical Encoding Rules), algunas veces es una secuencia de certificados
- .DER - Certificado codificado en DER (Distinguished Encoding Rules)
- .PEM - Certificado codificado en Base64, encerrado entre "-----BEGIN CERTIFICATE-----" y "-----END CERTIFICATE-----"
- .P7B - Ver .p7c
- .P7C - Estructura [[PKCS]]#7 SignedData sin datos, solo certificado(s) o CRL(s)
- .PFX - Ver .p12
- .P12 - [[PKCS]]#12, puede contener certificado(s) (público) y claves privadas (protegido con clave)
