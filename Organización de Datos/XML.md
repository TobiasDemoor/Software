**XML (eXtensible Markup Language)** es un subconjunto de SGML (Standard Generalised Mark-up Language), simplificado y adaptado a [[internet]]. XML es un meta-lenguaje que nos permite definir lenguajes de marcado adecuados a usos determinados. XML es el lenguaje sobre el cual está construido HTML. XML no es un lenguaje para hacer páginas web.

XML sirve para representar información estructurada en la web (todos documentos), de modo que esta información pueda ser almacenada, transmitida, procesada, visualizada e impresa, por diversos tipos de aplicaciones y dispositivos.
## Características
- XML es un subconjunto de SGML que incorpora las tres características más importantes de este:
  - Extensibilidad
  - Estructura
  - Validación
- Basado en texto.
- Orientado a los contenidos no a la presentación.
- Las etiquetas se definen para crear los documentos, no tienen un significado preestablecido.
## Ventajas del XML
1. Es fácilmente procesable.
1. Separa radicalmente el contenido y el formato de presentación.
1. Diseñado para cualquier lenguaje y alfabeto.
## Estructura de un documento XML
Un documento está formado por datos y marcas. Las marcas son las etiquetas. Dentro del documentos existen dos partes:

- Prólogo: indica los datos de la versión y encoding del documento junto con datos otros datos generales.
- Cuerpo: contiene la información a transmitir.

En un documento XML existen los siguientes componentes:

1. Elementos: pieza lógica del marcado, se representa con una cadena de texto (dato) encerrada entre etiquetas. Pueden existir elementos vacíos (`<br/>`). Los elementos pueden contener atributos.
1. Instrucciones: ordenes especiales para ser utilizadas por la aplicación que procesa: 		`<?xml-stylesheet type=”text/css” href =” estilo.css” >`
1. Las instrucciones XML: comienzan por `<?` y terminan por `?>`.
1. Comentarios: información que no forma parte del documento. Comienzan por `<!--` y terminan por `-->`.
1. Declaraciones de tipo: especifican información acerca del documento:	 
`<!DOCTYPE persona SYSTEM “persona.dtd”>`
1. Secciones CDATA: se trata de un conjunto de caracteres que no deben ser interpretados por el procesador:
`<![CDATA[ aquí se puede meter cualquier carácter, como <, &, >, sin que sean interpretados como marcación]]>`
## Árbol de análisis
Estructura que muestra los objetos que forman el documento y las relaciones entre ellos. A los componentes de un documento se les llama “objetos” (elementos, comentarios y cadenas de texto). El propio documento es un objeto. A cada objeto del árbol se le denomina “nodo”. Al nodo principal que contiene a los demás se le llama nodo “raíz”. Cuando un nodo contiene a otro se le denomina “rama”. Los nodos finales, que no contienen a otros nodos, se llaman “hojas”.
## Sobre el diseño
A la hora de diseñar se nos plantean dudas entre escoger atributo o elemento. Hay que tener en cuenta lo siguiente:

1. Los atributos no pueden contener subelementos ni subatributos.
1. Los atributos no se organizan en ninguna jerarquía por lo que la representación es mucho más reducida que los elementos.
1. La utilización de los atributos será una mera modificación de los elementos a los que se aplica, la información que deben de contener debe ser de poca entidad, sencilla y sin estructura.

Aun así, muchas veces llegamos a la misma conclusión utilizando atributos y elemento.
## Definición de reglas de construcción de XML
Para definir y validar un XML se puede utilizar las DTD y/o los esquemas XML (XML Schema Definition o XSD).
### DTD (Document type data)
Define los elementos, atributos, entidades y notaciones que pueden utilizarse para construir un tipo de documentos, así como las reglas para su utilización:

- Mediante ellas se comprueba la validez de un documento.
- Tienen su origen en SGML.
- Posee una sintaxis especializada.

Al definir el lenguaje XML ya nos referimos a la definición del tipo de documento que, en resumen, cumple con las siguientes funciones:

- Una DTD especifica la clase de documento
  - Describe un formato de datos.
  - Usa un formato común de datos entre aplicaciones.
  - Verifica los datos al intercambiarlos.
  - Verifica un mismo conjunto de datos.
- Una DTD describe
  - Elementos: cuáles son las etiquetas permitidas y cuál es el contenido de cada etiqueta.
  - Estructura: en qué orden van las etiquetas en el documento.
  - Anidamiento: qué etiquetas van dentro de cuáles.

Los elementos en una DTD son los siguientes:

- Elementos con “contenido ELEMENT”: Un elemento tiene contenido ELEMENT, si solo puede contener a otros elementos, opcionalmente separados por espacios en blanco.
- Elementos con “contenido TEXT”: Un elemento tiene contenido TEXT, si solo puede contener texto (PCDATA = printable character data).
- Elementos con “contenido MIXED”: Un elemento tiene contenido MIXED, si puede contener texto u otros elementos.
- Elementos con “contenido EMPTY”: Un elemento tiene contenido EMPTY, si no puede contener otros elementos.

Así pues, la DTD especifica la clase de documento XML. Una DTD indica sólo qué elementos, atributos, etc. tiene un documento y cómo se anidan, pero no dice nada acerca de tipos de dato. El único tipo de dato que conoce es PCDATA (texto plano), por tanto, las DTDs se quedan algo cortas y cuando se necesita algo más potente y rígido, se usa XSD.
### XML Schema Definition
Tiene la misma finalidad que las DTDs, de hecho, es la evolución de la DTD descripta por la W3C. Describen los elementos y atributos que se pueden utilizar para construir documentos CML y las reglas de utilización. Permiten asociar tipos de datos con los elementos. Se crean utilizando la sintaxis XML.

Surgen para dar respuesta a las limitaciones de las DTDs. Se basa en el vocabulario XML-Data que se utiliza para describir la estructura de los documentos. A la tecnología para la creación de esquemas se le conoce como XML Schema. IE 5.0 no realiza validación del documento a través del esquema.

Elementos:

- Schema: es el elemento raíz del documento, actúa como contenedor para el resto de los elementos. Contiene los atributos:
  - name: nombre del esquema
  - xmlns: espacio de nombres del esquema. Hace referencia a la DTD donde se definen los elementos del esquema. Su valor se establece a 		urn:schemas-microsoft-com:xml-data
- ElementType: define los tipos de elementos que se utilizarán para la elaboración de documentos que sigan el esquema. Contiene los atributos:
  - name: nombre del elemento
  - content: contenido del elemento:
    - eltOnly: solo puede contener elementos secundarios.
    - textOnly solo puede contener texto.
    - mixed: puede contener texto y elementos secundarios.
    - Empy: sin contenido.
  - order: orden y frecuencia del grupo de elementos secundarios del elemento:
    - one: solo se permite una serie de elementos.
    - seq: los elementos deben producirse en la secuencia especificada.
    - many: los elementos pueden aparecer las veces que sea en cualquier orden.
  - dt:type: establece el tipo de contenido del elemento.
- element: declara el modelo de contenido para un elemento. Dispone de los atributos:
  - type: tipo de elemento. Es el nombre con el que ha sido declarado ElementType.
  - minOcurrs: mínimo número de veces que el elemento puede aparecer. Su valor es 0 o 1.
  - maxOcurrs: máximo número de veces que el elemento puede aparecer. Puede ser 1 o \*.
- AttributeType: se utiliza para definir los tipos de atributos que van a ser utilizados en los elementos. Los atributos son:
  - name: nombre del atributo.
  - dt:types: tipo de datos del atributo.
  - dt:values: lista posible de valores de un atributo enumerado. Aplica dt:type a enumeration.
  - default: valor predeterminado.
  - required: indica si el atributo es o no obligatorio. Su valor es yes o no.
  - type: nombre del atributo.
  - default: valorpredeterminado.
  - required: si es o no obligatorio.
- attribute:se utiliza para declarar el modelo de contenido de un elemento. Sus atributos son:
  - type: nombre del atributo.
  - default: valor predeterminado.
  - required: si es o no obligatorio.

Los tipos de datos de XSD están definidos en el espacio de nombres urn:schema-microsoft-com:datatypes. Entre los tipos de datos más importantes están:

- char: carácter.
- string: cadena de caracteres.
- boolean: booleano 0 o 1.
- int: número entero.
- float: número real.
- date: fecha.
- time: hora.
- [[URI]]: identificador uniforme de recursos.
- enumeration: tipo enumerado, sólo válido para atributos.
- ID: atributo de tipo identificador.

Ejemplo:
```XML
<Schema
	xmlns="urn:schemas-microsoft-com:xml-data"
	xmlns:dt="urn:schemas-microsoft-com:datatypes"
>
	<AttributeType name='id' dt:type='string' required='yes'/>
	<ElementType name='nombre' content='textOnly'/>
	<ElementType name='persona' content='mixed'>
		<attribute type='id'/>
		<element type='nombre'/>
	</ElementType>
	<ElementType name='documento' content='eltOnly'>
		<element type='persona'/>
	</ElementType>
</Schema>
```

Estándares relacionados con XML:

- [XPath](https://www.w3.org/TR/xpath20/): es un lenguaje de expresión que permite procesar valores conforme a los modelos de datos XML.
- [XPointer](https://www.w3.org/TR/xptr/) (the XML pointer language): permite armar hipervinculos que apuntan a partes específicas de fragmentos de documents XML.
- [XLink](https://www.w3.org/TR/xlink11/) (the XML linking language): define el método para crear links dentro de los documentos XML.
- [XSLT](https://www.w3.org/TR/xslt20/): permite las transformaciones de documentos CML a otros formatos como por ejemplo XHTML.
- [DOM](https://www.w3.org/TR/dom41/): define el estándar para acceder y manipular los documentos CML. El DOM presenta un documento XML como una estructura de árbol. El DOM es separado por la W3C en tres diferentes partes:
  - CORE DOM: define el modelo estándar para cualquier documento estructurado.
  - XML DOM: el modelo estándar para documentos XML.
  - HTML DOM: el modelo estándar para documentos HTML.