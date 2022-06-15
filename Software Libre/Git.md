Git es un DVCS (distributed version control system) que nace en el 2005 por la necesidad de mantener el desarrollo de kernel de [[Linux]]. Tomando como referencia un DVCS propietario llamado BitKeeper.

Algunos de los objetivos del nuevo sistema fueron los siguientes:
- Compatible con protocolos existentes (Git puede utilizarse con [[HTTP]], [[SSH]], [[FTP]], etc)
- Fuerte orientación al desarrollo no lineal (miles de ramas paralelas)
- “Completamente” [[Sistemas Distribuidos|distribuido]]
- Capaz de manejar grandes proyectos (como el núcleo de Linux) de manera eficiente (velocidad y tamaño de los datos)

#### Commits
Un commit es un conjunto de cambios en 1 o más archivos realizados desde el último commit y agrupados atómicamente que actualiza el repositorio. A cada commit, Git lo identifica con un número hexadecimal de 40 caracteres. El número es un checksum generado mediante el algoritmo SHA-1 que toma como argumento el conjunto de cambios en ese commit, incluyendo la metada del mismo (mensaje de commit, autor y checksum del commit anterior)

#### Puntero HEAD
El puntero HEAD es una variable de referencia que apunta a un commit determinado (por defecto al último). El pointer HEAD puede ser movido a cualquier commit. Si se ubica en un commit previo, una vez en él, cada vez que se haga commit se pisarán los commits posteriores. También define el “working tree”.

Para volver a un commit viejo:
- Con el comando **reset** vuelve a un commit previo, desde donde luego cada commit pisará los que le seguían a ese commit.
- Con el comando **revert** se crea nuevos commit que deshacen los cambios entre el commit actual y el pasado en el argumento
