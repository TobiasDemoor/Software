El patrón BFF es una variante del patrón API Gateway, pero también provee una capa adicional entre microservicios y cada tipo de cliente por separado. Debido a eso es posible tener una API a medida para las necesidades de cada cliente y remover el volúmen que causado por tener todo en un mismo lugar.
![[AyD_BFF.webp]]
Algunas recomendaciones del autor
- Poner el foco en UI/UX y la información requerida por ellos.
- Evitar hacer todo genérico desde el principio, esto puede causar que el componente sea utilizado más ampliamente (?).
- Usar *feature particular* sobre *uso genérico*. Este aproach es el mejor para lograr mantener una API limpia dedicada a un cliente.
- Usar la [[Rule of Three|regla de tres]]