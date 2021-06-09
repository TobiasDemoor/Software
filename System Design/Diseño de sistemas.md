"El diseño es la actividad del ciclo de desarrollo del software donde se unen la creatividad, los [[Requerimientos]] de los participantes, las necesidades del negocio y las consideraciones técnicas para formular un sistema o producto" -(Pressman, 2010)

El diseño es la actividad que tiene que ver con la toma de decisiones importantes, toma las decisiones más generals que afectan fuertemente a todo el producto. Esta es la etapa en la cuál se genera la [[Deuda técnica|deuda técnica]].

# Características
- El entregable principal es el modelo de diseño que incluye las representaciones a nivel sistema y a nivel aplicación.
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
- **Diseño arquitectónico** (llamado diseño de alto nivel) que implica la organización y esctructura del sistema e identifica los diferentes componentes. Se diseña la [[Arquitectura de software|arquitectura de software]].
- **Diseño detallado**, especificar cada componente con el suficiente detalle para facilitar su construcción.
Se tiene un buen diseño cuando:
- Se contemplan todos los [[Requerimientos|requerimientos]] explícitos en el modelo de análisis y los implícitos que implica el producto en sí.
- Es legible y comprensible para todos los stakeholders relacionados.
- Debe ser completo y dar un panorama completo del software.

# Principios
- Abstracción
- [[Acoplamiento]] y [[Cohesión]]
- Descomposición y modularización
- Encapsulamiento
- [[Ocultamiento de la información]]
- Interfaz e implementación
- Sufficency, completness and primitiveness
- [[Separación de concerns]]

# Aplicaciones OO
La [[Object oriented programming|OO]] representa hoy el mejor framework metodológico para la ingeniería de software gracias al pragmatismo del paradigma y la sitematisación de procesos que permite. Brinda homogeneidad a través del análisis, diseño e implementación (siempre trabajamos con entidades). Pone el énfasis en el estado, comportamiento e interacción de objetos. Trae consigo las ventajas de la maduración y los patrones de prácticas. Se tienen variedad de técnicas, métodos, procesos, estándares, modelos, notaciones, herramientas, componentes, lenguajes, ambientes, ejemplos, comunidad, práctica y experiencia.

# Diseño de [[Requerimientos#Atributos de Calidad|QA]]
Primero se deben identificar los [[Requerimientos#Requerimientos no funcionales|requerimientos no funcionales]] y priorizar por su impacto en la arquitectura (poniendo el foco en [[FURPS+]]). Luego debemos seleccionar uno y buscar alternativas de implementación para crear la solucion elegida. Estas actividades son iterativas hasta el nivel de detallee que se desee o atributos de calidad a atender.

# Diseñando la persistencia
Propiedades que se deben tener en cuenta:
- ¿Qué se almacenará? (esto determina la tecnología que debemos usar, SQL vs NoSQL).
- Manejo de metadata (DDL y DML).
- Integridad de datos.
- Licencia y costos.
- Gobernabilidad.
- Tiempo de vida de los datos.
- Formato de almacenamiento (datos, imágenes y documentos).
- Objetos o datos. Serialización, ODBMS o RDBMS.
- Transacciones.
- Backup y restore.
- Seguridad.
- [[FURPS+#Reliability|Disponibilidad]] (centralizada vs distribuida).
- Escalabilidad.
- [[FURPS+#Performance]]

Depende el nivel que estemos analizando tenemos distintos elementos a los cuales estudiar.

## Realidad
En el nivel de la realidad hablamos de entidades que tienen atributos, esto lo representamos en el modelo de dominio.

## Datos
En el nivel de los datos tenemos ocurrencias de registros que tienen ocurrenciasd de elementos de datos, esto lo vemos en las tablas de datos.

## Metadatos
En el nivel de los metadatos tenemos las definiciones de registros y las definiciones de los elementos de datos que contienen, esto se describe con un DDL.