---
aliases: ["Google hack"]
---
Google dorking describe la aplicación de cadenas de búsqueda que utilizan operadores de búsqueda innovadores para encontrar información que no se puede obtener rápidamente en la red. Tales detalles podrían ser en tipo de texto, imágenes, información clasificada, direcciones de correo electrónico, contraseñas, etc. Con frecuencia, la información se ha dejado expuesta en la web por error.

Se usan los filtros de google como: 
- cache: Busqueda en el Cache de google 
- allintext: Busqueda en todos los texto 
- filetype: Buscar solo los tipos de archivos. 
- site: Filtrar el archivo 
- inurl: en la url 
Ejemplo:
- site:mdp.edu.ar filetype:log -> Buscar todos los archivos tipos log
- inurl:top.htm inurl:currenttime -> busqueda de camaras live (suelen tener estos datos las webcam)
- robots.txt -> buscar en archivo robots a ver qué páginas no se quiere que se entere.
- site:mdp.edu.ar filetype:xls -> Buscar los xls del sitio