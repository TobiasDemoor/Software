## Descripción
Se organiza el sisteam en módulos/componentes con funcionalidad relacionada. Cada capa se organiza sobre los servicios de la inmediata inferior.

## Usos
Agregar funcionalidad sobre servicios core, distribución del desarrollo, se requiere seguridad multinivel.

## Ventajas
- Mantenibilidad
- Modularidad
- Testeabilidad

## Desventajas
- Performance (se puede sortear con salteo de capas)

## Cualidades
- Separación e independencia entre capas (modularidad, encapsulamiento, mantenibilidad).
- Cada capa se construye sobre los servicios y recursos de la inmediata inferior (reusabilidad).
- El cambio en una capa afecta solamente a su capa adjunta ([[Acoplamiento]]).