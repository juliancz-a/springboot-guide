**`xmlns`** es un atributo en XML que se utiliza para declarar un **espacio de nombres (namespace)**. Los espacios de nombres ayudan a evitar conflictos de nombres en documentos XML/HTML cuando se combinan diferentes vocabularios, como cuando un documento contiene elementos o atributos de varios estándares.

### **¿Por qué usar `xmlns`?**

El uso de espacios de nombres es fundamental cuando se combinan datos de diferentes fuentes o cuando se usan tecnologías que definen sus propios elementos y atributos. Sin un espacio de nombres, los elementos de diferentes fuentes podrían entrar en conflicto si tienen el mismo nombre pero significados diferentes.

Sintaxis
`<book xmlns="http://example.com/books"> <title>Introducción a XML</title> <author>Juan Pérez</author> </book>`