## Propósito
Definir el esqueleto del algorítmo de un método, delegando tareas a las subclases para que redefinan o completen la funcionalidad pendiente.

## Motivación
Se pueden implementar partes invariables de un algorítmo, dejando a las subclases que definan el comportamiento que puede variar.

## Usos
Hay dos formas principales de implementarlo:
1. El templateMethod() establece **métodos hook** para que sean implementados en subclases y templateMethod() {leaf} (final en Java), para que no sea redefinida la lógica y se puedan alterar solo los hook.
2. El templateMethod() establece **métodos hook** para que sean implementados en subclases y el mismo templateMethod() también puede ser redefinido.