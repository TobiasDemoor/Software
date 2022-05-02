> "El diseño es la actividad del ciclo de desarrollo del software donde se unen la creatividad, los [[Requerimientos]] de los participantes, las necesidades del negocio y las consideraciones técnicas para formular un sistema o producto" -(Pressman, 2010)

El diseño es la actividad que tiene que ver con la toma de decisiones importantes, toma las decisiones más generals que afectan fuertemente a todo el producto. Esta es la etapa en la cuál se genera la [[Deuda técnica|deuda técnica]].

# Características
- El entregable principal es el [[Design Model|modelo de diseño]] que incluye las representaciones a nivel sistema y a nivel aplicación.
- El scope del trabajo va de lo general a lo particular.
- El proceso de diseño se caracteriza por aplicar técnicas del proceso creativo. [[Divergencia y convergencia#Divergencia|divergencia]] y [[Divergencia y convergencia#Convergencia|convergencia]].
- En general es un proceso iterativo. No se llega a la solución final en el primer intento.
- Disponer de un modelo de diseño permite asegurar la calidad del proceso y del producto al tener una evidencia concreta para evaluar errores, inconsistencias u omisiones.
- El diseño es una actividad que tiene que ver con la toma de decisiones importantes. Comparte con la [[Programación|programación]] el objetivo de abstraer una representación de la [[Dato, información y conocimiento|información]] y el procesamiento, pero con grados de detalle muy diferentes.
- El diseño de software se ubica en el área técnica de la ingeniería de software.
- Se aplica independientemente del proceso que se use.
- Comienza una vez analizados y modelados los [[Requerimientos]], por ello, es la última acción de modelado y de preparación previa a la construcción.

# Proceso
Es un proceso iterativo por medio del cual se traducen los [[Requerimientos|requerimientos]] para poder construir el software (en cada iteración se profundiza el detalle). Generalmente contiene dos etapas que se ubican entre el análisis de [[Requerimientos]] y la construcción del software.
- **Diseño arquitectónico** (llamado diseño de alto nivel) que implica la organización y esctructura del sistema e identifica los diferentes [[Componente|componentes]]. Se diseña la [[Software Architecture|arquitectura de software]].
- **Diseño detallado**, especificar cada [[Componente|componente]] con el suficiente detalle para facilitar su construcción.
Se tiene un buen diseño cuando:
- Se contemplan todos los [[Requerimientos|requerimientos]] explícitos en el modelo de análisis y los implícitos que implica el producto en sí.
- Es legible y comprensible para todos los stakeholders relacionados.
- Debe ser completo y dar un panorama completo del software.

# Principios
- [[Abstracción]]
- [[Acoplamiento]] y [[Cohesión]]
- Descomposición y modularización
- [[Encapsulamiento]]
- [[Ocultamiento de la información]]
- [[Interfaz]] e implementación
- Sufficency, completness and primitiveness:
	- **Sufficency:** el [[Componente|componente]] considera las características de su [[Abstracción|abstracción]] que son necesarias para proveer una interacción significativa y eficiente.
	- **Completness:** el [[Componente|componente]] debe considerer todas las características relevantes de su [[Abstracción|abstracción]].
	- **Primitiveness:** las operaciones que puede realizar el [[Componente|componente]] pueden ser implementadas fácilmente.
- [[Separación de concerns]]

# Aplicaciones OO
La [[OOP|OO]] representa hoy el mejor framework metodológico para la ingeniería de software gracias al pragmatismo del paradigma y la sitematisación de procesos que permite. Brinda homogeneidad a través del análisis, diseño e implementación (siempre trabajamos con entidades). Pone el énfasis en el estado, comportamiento e interacción de objetos. Trae consigo las ventajas de la maduración y los patrones de prácticas. Se tienen variedad de técnicas, métodos, procesos, estándares, modelos, notaciones, herramientas, componentes, lenguajes, ambientes, ejemplos, comunidad, práctica y experiencia.

# Diseño de QA
Primero se deben identificar los [[Requerimientos no funcionales|RNF]] (dentro de los que se encuentran los QA) y priorizar por su impacto en la arquitectura (poniendo el foco en [[FURPS+]]). Luego debemos seleccionar uno y buscar alternativas de implementación para crear la solucion elegida (las alternativas y las decisiones que se tomen deben ir al [[Software Architecture Document|SAD]]). Estas actividades son iterativas hasta el nivel de detalle que se desee o atributos de calidad a atender.

## Attribute Driven Design
ADD es un enfoque para definir una arquitectura de software que basa el proceso de descomposición en los atributos de calidad que debe cumplir el software. Se aplica luego de tener una división en módulos generales.
- En cada iteración se selecciona un módulo a descomponer y se definen un conjunto de escenarios de calidad y requisitos funcionales en los cuales se va a basar la descomposición del [[Componente|componente]].
- Proceso de descomposición de módulos recursivos donde en cada etapa se eligen [[Tácticas|tácticas]] y [[Patrones arquitectónicos|patrones arquitectónicos]] para satisfacer un conjunto de escenarios de calidad y luego se asigna funcionalidad para instanciar los tipos de módulos proporcionados por el patrón utilizado.
	- Se deben identificar los componentes hijos y se les debe asignar una responsabilidad.
	- Se debe documentar y representar mediante vistas estos cambios en la arquitectura.
- ADD se posiciona en el ciclo de vida después del [[Ingeniería de Requerimientos#Fases del proceso de IR|análisis de requerimientos]] y puede comenzar cuando los [[Architectural factors|drivers de arquitectura]] se conocen con cierta confianza.
- El resultado de ADD son los primeros niveles de una vista de descomposición de módulos de arquitectura y otras vistas, según corresponda.

# Diseñando la persistencia
%%[[Bases de Datos]]%%
Propiedades que se deben tener en cuenta:
- ¿Qué se almacenará? (esto determina la tecnología que debemos usar, [[SQL]] vs [[NOSQL]]).
- Manejo de metadata (DDL y DML).
- Integridad de datos.
- Licencia y costos.
- Gobernabilidad.
- Tiempo de vida de los datos.
- Formato de almacenamiento (datos, imágenes y documentos).
- Objetos o datos. Serialización, [[ODBMS|ODBMS]] o [[RDBMS|RDMBS]].
- [[Transacciones]].
- Backup y restore.
- Seguridad.
- [[Reliability|Disponibilidad]] (centralizada vs distribuida).
- [[Escalabilidad|Escalabilidad]].
- [[Performance]]

Depende el nivel que estemos analizando tenemos distintos elementos a los cuales estudiar.

## Realidad
En el nivel de la realidad hablamos de entidades que tienen atributos, esto lo representamos en el modelo de [[Dominio|dominio]].

## Datos
En el nivel de los datos tenemos ocurrencias de registros que tienen ocurrencias de elementos de datos, esto lo vemos en las tablas de datos.

## Metadatos
En el nivel de los metadatos tenemos las definiciones de registros y las definiciones de los elementos de datos que contienen, esto se describe con un DDL (Data Definition Language).