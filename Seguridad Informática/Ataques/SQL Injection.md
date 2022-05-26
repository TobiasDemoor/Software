Uno de los posibles tipos de ataque es una "Inyección de [[SQL]]", para que exista este ataque primero debe existir un error de software (programación insegura). Ese defecto da como resultado una [[Vulnerabilidad|vulnerabilidad]]. Una causa que hacen más común este tipo de ataque es el desacople entre front y back ([[Client-Server]]), con esta arquitectura un equipo inexperto podría estar permitiendo entrada de datos inseguros al backend sin validación.

Una inyección de SQL es un tipo de [[Arbitrary Code Excecution|arbitrary code excecution]] donde se permite al atacante ejecutar código arbitrario en el servidor. Permiten al atacante modificar la lógica original de la consulta SQL y la creación de queries dinámicas.

### ¿Cómo prevenir las inyecciones?
1. Uso de declaraciones ya preparadas (con consultas parametrizadas). 
2. Uso de stored procedures.
3. [[Validación de entradas]] con lista de datos permitidos (“sanitizar”). 
4. Escapar todas las entradas proporcionadas por el usuario.