Podemos aplicar la misma perspectiva que en las subredes: los enrutadores en distintas ubicaciones pueden saber acerca de una dirección IP dada que pertenece a prefijos de distintas zonas. Sin embargo, en vez de dividir un bloque de direcciones en subredes, aquí combinamos varios prefijos pequeños en un solo prefijo más grande. A este proceso se le conoce como **agregación de rutas**. Algunas veces al prefijo más grande resultante se le denomina **superred** para contrastar con las subredes como la división de bloques de direcciones.

Como una sorpresa adicional, es posible traslapar a los prefijos. La regla es que los paquetes se envíen en la dirección de la ruta más específica, o el **prefijo más largo coincidente** que tenga la menor cantidad de direcciones IP.