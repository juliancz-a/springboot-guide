Una [API](API.md) **RESTful** es una API que sigue los principios de la arquitectura **REST (Representational State Transfer)**, un estilo de diseño para sistemas distribuidos basado en recursos y en el uso de los protocolos HTTP. RESTful es una implementación común para crear servicios web escalables y flexibles.

#### **Características de una API RESTful:**

1. **Basada en Recursos**: Cada entidad o dato se trata como un recurso identificado por una URI única. Ver: [Endpoint Mappings](<Endpoint Mappings.md>)
2. **Uso de HTTP**: Emplea los métodos estándar del protocolo HTTP:
    - `GET`: Para recuperar datos de un recurso.
    - `POST`: Para crear un nuevo recurso.
    - `PUT` o `PATCH`: Para actualizar un recurso existente.
    - `DELETE`: Para eliminar un recurso.
3. **Stateless (Sin estado)**: Cada solicitud del cliente al servidor debe contener toda la información necesaria para entenderla, sin depender de sesiones mantenidas en el servidor.
4. **Representaciones**: Los recursos pueden representarse en diferentes formatos, como **JSON** o **XML**, aunque JSON es el más común.
5. **Soporte de Caching**: Los datos pueden ser almacenados en caché para mejorar el rendimiento.


Podemos devolver cualquier objeto serializable, tipicamente cualquier [POJO](POJO.md) o DTA, Maps, Lists/Collections, Sets, entre otros. Serán serializados en JSON preferentemente.

### **HATEOAS (Hypermedia as the Engine of Application State)**

HATEOAS es un principio de las **APIs REST** que permite que los clientes naveguen por los recursos del sistema dinámicamente a través de enlaces proporcionados en las respuestas.

🔹 **¿Cómo funciona?**  
En lugar de que el cliente tenga que conocer todas las rutas de la API de antemano, el servidor **proporciona enlaces (hypermedia)** en las respuestas, guiando al cliente sobre qué acciones puede realizar a continuación.

En resumen:
El servicio proporciona toda la información al cliente para que pueda interactuar con nuestro back-end, sin pasar por controladores o services

**Respuesta (sin HATEOAS):**

```Java
{
  "id": 1,
  "nombre": "Juan Pérez",
  "email": "juan@example.com"
}
```
🔹 **Ejemplo con HATEOAS:**  
La respuesta incluiría enlaces a acciones relacionadas:
```Java
{
  "id": 1,
  "nombre": "Juan Pérez",
  "email": "juan@example.com",
  "_links": {
    "self": { "href": "/usuarios/1" },
    "editar": { "href": "/usuarios/1", "method": "PUT" },
    "eliminar": { "href": "/usuarios/1", "method": "DELETE" }
  }
}
```

🔹 **Ventajas de HATEOAS:**  
✅ Reduce el acoplamiento entre cliente y servidor.  
✅ Facilita la evolución de la API sin romper clientes existentes.  
✅ Permite descubrir nuevas funcionalidades sin necesidad de documentación externa.

Interfaz de configuracion -> RepositoryRestConfigurer
	Debe ser implementada en un componente de configuración, nos permite manejar los elementos de manera que podemos, por ejemplo, exponer los ID's de la entidades a través del método configureRepositoryRestConfiguration

```Java
@Configuration
public class DataRestConfig implements RepositoryRestConfigurer{

    @Override
    public void configureRepositoryRestConfiguration(RepositoryRestConfiguration config, CorsRegistry cors) {
        config.exposeIdsFor(Product.class)}
```
## Serialización JSON

Spring utiliza **Jackson** como la biblioteca predeterminada para convertir objetos Java en JSON. Cualquier clase que cumpla con los requisitos de un **POJO** (Plain Old Java Object) puede ser convertida automáticamente a formato JSON si:

- Tiene un **constructor por defecto** o accesible.
- Proporciona **métodos getters y setters** públicos.
- No utiliza propiedades cíclicas que no puedan resolverse.

También se pueden serializar:
- **Objetos personalizados**: Siempre que tengan los métodos adecuados.
- **Mapas y listas**: Se convierten a JSON con claves y valores correspondientes.
- **Enumeraciones**: Se serializan según su nombre o valor específico.