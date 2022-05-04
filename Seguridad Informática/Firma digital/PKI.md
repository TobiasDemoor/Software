Una **infraestructura de clave pública** (PKI) es una combinación de hardware, software y políticas y procedimientos de seguridad que permiten la ejecución con garantías de [[Criptografía|operaciones criptográficas]], como el cifrado, la [[Firma digital|firma digital]] y el no repudio de las transacciones electrónicas.

Usos de PKI:
- Identificación de usuarios y sistemas (''login'')
- Identificación del interlocutor
- Cifrado de datos digitales
- Firma Digital de datos (documentos, software, etc.)
- Asegurar las comunicaciones
- Garantía de no repudio (negar que cierta transacción tuvo lugar)

#### Tipos de certificados
- **Certificado personal**, que acredita la identidad del titular. 
- **Certificado de pertenencia a empresa**, que además de la identidad del titular acredita su vinculación con la entidad para la que trabaja. 
- **Certificado de representante**, que además de la pertenencia a empresa acredita también los poderes de representación que el titular tiene sobre la misma.
- **Certificado de persona jurídica**, que identifica una empresa o sociedad como tal a la hora de realizar trámites ante las administraciones o instituciones (en la PKI de [[Firma digital Argentina|firma digital Argentina]] estos ya no existen).
- **Certificado de atributo**, permite identificar una cualidad, estado o situación. Este va asociado al certificado personal. (p.ej. Informatico, Director, Soltero, Apoderado de..., etc.).
- **Certificado de servidor seguro**, utilizado en los servidores web que quieren proteger ante terceros el intercambio de información con los usuarios.
- **Certificado de firma de código**, para garantizar la autoría y la no modificación del código de aplicaciones informáticas.

#### Componentes de una PKI
- **Autoridad de certificación CA**: es la encargada de emitir y revocar certificados. Es la entidad de confianza que da legitimidad a la relación de una clave pública con la identidad de un usuario o servicio. 
- **Autoridad de registro RA**: es la responsable de verificar el enlace entre los certificados (concretamente, entre la clave pública del certificado) y la identidad de sus titulares.
- **Los repositorios**: son las estructuras encargadas de almacenar la información relativa a la PKI. Los dos repositorios más importantes son el repositorio de certificados y el repositorio de lista de revocación de certificados.
- **Lista de revocación**: En una lista de revocación de certificados (CRL, Certificate Revocation List) se incluyen todos aquellos certificados que por algún motivo han dejado de ser válidos antes de la fecha establecida dentro del mismo certificado.
- **Autoridad de validación VA**: es la encargada de comprobar la validez de los certificados digitales.
- **Autoridad de sellado de tiempo TSA**: es la encargada de firmar documentos con la finalidad de probar que existían antes de un determinado instante de tiempo.
- **Los usuarios y entidades finales** son aquellos que poseen un par de claves (pública y privada) y un certificado asociado a su clave pública. Utilizan un conjunto de aplicaciones que hacen uso de la tecnología PKI (para validar firmas digitales, cifrar documentos para otros usuarios, etc.)