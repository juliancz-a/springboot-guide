Una [[API]] **RESTful** es una API que sigue los principios de la arquitectura **REST (Representational State Transfer)**, un estilo de diseño para sistemas distribuidos basado en recursos y en el uso de los protocolos HTTP. RESTful es una implementación común para crear servicios web escalables y flexibles.

#### **Características de una API RESTful:**

1. **Basada en Recursos**: Cada entidad o dato se trata como un recurso identificado por una URI única. Ver: [[Endpoint Mappings]]
2. **Uso de HTTP**: Emplea los métodos estándar del protocolo HTTP:
    - `GET`: Para recuperar datos de un recurso.
    - `POST`: Para crear un nuevo recurso.
    - `PUT` o `PATCH`: Para actualizar un recurso existente.
    - `DELETE`: Para eliminar un recurso.
3. **Stateless (Sin estado)**: Cada solicitud del cliente al servidor debe contener toda la información necesaria para entenderla, sin depender de sesiones mantenidas en el servidor.
4. **Representaciones**: Los recursos pueden representarse en diferentes formatos, como **JSON** o **XML**, aunque JSON es el más común.
5. **Soporte de Caching**: Los datos pueden ser almacenados en caché para mejorar el rendimiento.


Podemos devolver cualquier objeto serializable, tipicamente cualquier [[POJO]] o DTA, Maps, Lists/Collections, Sets, entre otros. Serán serializados en JSON preferentemente.


## Serialización JSON

Spring utiliza **Jackson** como la biblioteca predeterminada para convertir objetos Java en JSON. Cualquier clase que cumpla con los requisitos de un **POJO** (Plain Old Java Object) puede ser convertida automáticamente a formato JSON si:

- Tiene un **constructor por defecto** o accesible.
- Proporciona **métodos getters y setters** públicos.
- No utiliza propiedades cíclicas que no puedan resolverse.

También se pueden serializar:
- **Objetos personalizados**: Siempre que tengan los métodos adecuados.
- **Mapas y listas**: Se convierten a JSON con claves y valores correspondientes.
- **Enumeraciones**: Se serializan según su nombre o valor específico.