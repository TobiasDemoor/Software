%%Fuente: [Medium | Backend for frontend](https://medium.com/mobilepeople/backend-for-frontend-pattern-why-you-need-to-know-it-46f94ce420b0)%%
El patrón BFF es una variante del patrón [[API Gateway]], pero también provee una capa adicional entre microservicios y cada tipo de cliente por separado. Debido a eso es posible tener una API a medida para las necesidades de cada cliente y remover el volúmen que causado por tener todo en un mismo lugar.
![[AyD_BFF.webp]]
Algunas recomendaciones del autor
- Poner el foco en UI/UX y la información requerida por ellos.
- Evitar hacer todo genérico desde el principio, esto puede causar que el componente sea utilizado más ampliamente (?).
- Usar *feature particular* sobre *uso genérico*. Este aproach es el mejor para lograr mantener una API limpia dedicada a un cliente.
- Usar la [[Rule of Three|regla de tres]]

## ¿Por qué usar BFF?
Decoupling of Backend and Frontend for sure gives us faster time to market as frontend teams can have dedicated backend teams serving their unique needs. The release of new features of one frontend does not affect the other.

We can much easier maintain and modify APIs and even provide API versioning dedicated for specific frontend, which is a big plus from a mobile app perspective as many users do not update the app immediately.

Simplify the system from Frontend and Backend perspectives as we don’t need any compromise.

The BFF can benefit from hiding unnecessary or sensitive data before transferring it to the frontend application interface, so keys and tokens for 3rd party services can be stored and used from BFF.

Allows to send formatted data to frontend and because of that can minimalize logic on it.

Additionally, give us possibilities for performance improvements and good optimization for mobile.

## ¿Cuándo usar BFF?
Cuando una aplicación provee un solo front, probablemente BFF solo tendrá sentido cuando se tiene una agregación alta del lado del servidor. De igual manera, se puede usar el concepto de API Gateway. BFF se puede considerar cuando se planea extender a varios tipos de frontend.

Si tu aplicación necesita desarrollar un backend optimizado para una interfaz de front específica o tus clientes necesitan consumir información que requiere agregación en el backend, BFF es una opción adecuada. Por supuesto, se debe considerar el costo de deployar servicios BFF adicionales.