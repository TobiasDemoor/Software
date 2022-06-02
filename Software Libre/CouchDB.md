CouchDB es una [[Bases de Datos|base de datos]] [[Software Libre|software libre]] de la fundación Apache. Un servidor CouchDB aloja bases de datos nombradas, que almacenan documentos. Cada documento tiene un nombre único en la base de datos a la que pertenece.

Los documentos son la unidad principal de datos en CouchDB y constan de cualquier número de campos y archivos adjuntos, en formato [[JSON]] (schemaless). Los documentos también incluyen metadatos que mantiene el sistema de base de datos. Los campos del documento tienen un nombre único y contienen valores de diferentes tipos (texto, número, booleano, listas, etc.), y no hay un límite establecido para el tamaño del texto o el recuento de elementos. 

Características:
- [[Transacciones|Transacciones ACID]]
- Administrador visual "Fauxton"
- Basada en documentos
- API [[REST]]
- Consultas
- [[Índice|Índices]]
- Schemaless
- Vistas
- Búsqueda
- [[Decentralized organizations|Arquitectura distribuida]] mediante replicación
- Suscripción a cambios

### Fauxton
Fauxton es una interfaz web nativa integrada en CouchDB. Proporciona una interfaz básica para la mayoría de las funciones. Proporciona acceso a los parámetros de configuración y una interfaz para iniciar la replicación.

Una vez instalado CouchDB se puede acceder al panel en el puerto 5984 y el path /\_utils. Por ejemplo: http://127.0.0.1:5984/_utils

### Documentos
El modelo de actualización de documentos de CouchDB es optimista y sin bloqueo. Las ediciones de documentos se realizan mediante aplicaciones cliente que cargan documentos, aplican cambios y los guardan en la base de datos. Si otro cliente que edita el mismo documento guarda sus cambios primero, el cliente obtiene un error de conflicto de edición al guardar. Para resolver el conflicto de actualización, se puede abrir la última versión del documento, volver a aplicar las ediciones y volver a intentar la actualización.

Las actualizaciones de un solo documento (agregar, editar, eliminar) son todo o nada, ya sea exitosamente o fallando completamente (ACID). La base de datos nunca contiene documentos parcialmente guardados o editados.

### Índices
Los índices se almacenan como filas que se mantienen ordenadas por los campos que se especifiquen, utilizando una estructura de datos de [[B Tree|árbol B]]. Esto hace que la recuperación de datos de un rango de claves sea eficiente incluso cuando hay miles o millones de filas.

Por defecto, todos los campos se indexan utilizando el campo \_id de la metadata de cada documento, pero se pueden crear nuevos índices simples o compuestos.

Si cuando se ejecuta una consulta con un filtro en algún campo y existen índices para dicho campo, CouchDB lo utilizará para filtrar (debe utilizarse el comando atributo “use_index”); de lo contrario deberá cargar cada documento y evaluarlo en el momento de la consulta.

### Vistas
Al ser schemaless, se dificulta el poder filtrar, organizar y reportar datos de varios documentos, ya que cada uno puede tener su propia estructura.

Las vistas son una forma de combinar/modificar/filtrar datos de los documentos. Cada vista es una representación de los contenidos de los documentos en una base de datos, y al generarse de manera dinámica de manera independiente a los documentos, se pueden tener tantas vistas (representaciones) de un documento como se quiera.

Las vistas de CouchDB se definen dentro de documentos de diseño especiales y pueden replicarse en instancias de bases de datos como documentos normales, de modo que no solo los datos se replican en CouchDB, sino que también se replican diseños de aplicaciones completos.

Las vistas se definen mediante **funciones de JavaScript** que actúan como parte del mapa en un sistema de reducción de mapas. Una función de vista toma un documento CouchDB como argumento y luego realiza los cálculos necesarios para determinar los datos que estarán disponibles a través de la vista, si los hubiera.

Cuando se consulta una vista, CouchDB toma el código fuente de la función y lo ejecuta en cada documento de la base de datos. Si hay muchos documentos, eso lleva bastante tiempo y se volvería ineficiente.

Pero CouchDB está diseñado para evitar costos adicionales: solo se ejecuta a través de todos los documentos una vez, cuando se consulta la vista por primera vez. Si se cambia un documento, la función de mapa solo se ejecuta una vez, para volver a calcular las claves y los valores de ese único documento.

### Búsqueda
Los índices de búsqueda permiten consultar una base de datos utilizando la sintaxis del analizador de consultas de Lucene (Apache Lucene). Un índice de búsqueda utiliza uno o varios campos de los documentos. Se puede utilizar un índice de búsqueda para ejecutar consultas, buscar documentos según el contenido que contienen o trabajar con grupos, facetas o búsquedas geográficas.

### Arquitectura distribuida mediante replicación
CouchDB es un [[DDBMS|sistema de base de datos distribuido]] basado en pares. Permite a los usuarios y servidores acceder y actualizar los mismos datos compartidos mientras están desconectados. Cada uno tiene una instancia de base de datos local. Posteriormente, esos cambios se pueden replicar bidireccionalmente.

Utiliza un modelo de replicación llamado [[Consistencia eventual|consistencia eventual]]. En este sistema, los clientes pueden escribir datos en un nodo de la base de datos sin esperar a que otros nodos se pongan de acuerdo (inclusive puede estar offline). El sistema copia incrementalmente los cambios de documentos entre los nodos, lo que significa que eventualmente estarán sincronizados (si lo vemos a través del [[CAP Theorem]] CouchDB cumpliría con Availability y Partitioning).

Si una instancia de CouchDB recibe dos actualizaciones distintas de una misma versión de documento, esta decide de manera determinista que actualización es la "ganadora" y cuáles son los conflictos. No realiza fusión de los datos, por lo que esto queda como tarea de la aplicación. Solo el documento ganador puede aparecer en las vistas, mientras que los conflictos "perdedores" aún son accesibles y permanecen en la base de datos hasta que se eliminan o purgan durante la compactación de la base de datos.

#### Suscripción a cambios
Se pueden obtener los últimos cambios de un documento, utilizando HTTP, de 3 maneras:
- Polling: se consulta periódicamente. 
- Long polling: se consulta y se mantiene abierta la conexión hasta que ocurra un cambio el cual es comunicado. 
- Continuos: nunca se cierra la conexión.

De esta forma, si se quiere mantener sincronizadas varias bases de datos, simplemente se pueden replicar los documentos que cambien

### Práctica
```html
<!-- PouchDB es una base de datos “inspirada” en CouchDB, implementada en JavaScript y optimizada para ejecutarse en navegadores. Su principal objetivo es ayudar en el desarrollo de aplicaciones offline. Al tener una API compatible con CouchDB, la aplicación puede tener una base de datos local PouchDB y sincronizarse mediante mecanismos de replicación con una base de datos remota CouchDB. -->
<script src="//cdn.jsdelivr.net/npm/pouchdb@7.2.1/dist/pouchdb.min.js"></script>
<script type="text/javascript">
	const db = new PouchDB('mibaseLocal');
	db.post({ 'name': 'pedro' });
	db.put({ '_id': '123', 'name': 'mariano' });
	db.get('123').then((doc) => { console.log(doc) });
	db.get('docId').then((doc) => { doc.name: 'maria'; return db.put(doc) });
	db.allDocs({ include_docs: true }).then((docs) => { console.log(docs) });
	
	const remote = new PouchDB(<urlRemota>)
	db.sync(remote, {
		live: true, // mantiene conexión abierta
		retry: true // si se cae la conexión vuelve a intentar conectarse
	}).on('change', function (change) {
		console.log('data change', change)
	}).on('error', function (err) {
		console.log('sync error', err)
	});
</script>
```

### PouchDB
PouchDB es una base de datos “inspirada” en CouchDB, implementada en JavaScript y optimizada para ejecutarse en navegadores. Su principal objetivo es ayudar en el desarrollo de aplicaciones offline. Al tener una API compatible con CouchDB, la aplicación puede tener una base de datos local PouchDB y sincronizarse mediante mecanismos de replicación con una base de datos remota CouchDB

#ApacheFoundation
