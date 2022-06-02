Es un sistema que construye un [[Índice]] a partir de texto y responde a consultas utilizando este índice. Utilizan índices invertidos. El archivo invertido se crea siguiendo cuatro pasos principales: parseo, ordenamiento, agrupamiento, y generación del diccionario y posting.

1. Parseo: a cada documento se le extrae los términos y un id documento.
1. Ordenamiento: se ordena al archivo creado por términos manteniendo los duplicados.
1. Agrupamiento: corte de control por término y documento.
1. Diccionario y posting: generación de ambos archivos. El diccionario (archivo inverso con índice no denso) agrupa por término, informa frecuencia total y direcciona al posting. El posting (archivo con lista inversa) direcciona a los documentos, informa la frecuencia y contiene listas enlazadas.

Existen distintas variantes de búsqueda:

- Modelo booleano: indica si un documento dado contiene o no a un término.
- Modelo vectorial: relaciona un conjunto dado de documentos (D) con el conjunto de todos los términos relevantes del conjunto D (T). A diferencia del modelo booleano este si informa la frecuencia.
- Frases y términos: para cada término se debe tener la lista de posiciones donde aparece en el documento.

## Consulta con patrones
Hay varias alternativas:

- Fuerza bruta: recorrido secuencial del léxico.
- Índice secundario de n-gramas: por cada término que se agrega al índice invertido, se indexan en el secundario todos sus n-gramas.
- Índice secundario de léxico rotado: por cada término que se agrega al índice invertido, se agregan al secundario todas sus rotaciones.

Los índices secundarios permiten buscar en el invertido todos los términos que cumplan con el patrón de búsqueda.

*Distancia de edición de Levenshtein:* Número mínimo de operaciones requeridas para transformar una cadena de caracteres en otra.