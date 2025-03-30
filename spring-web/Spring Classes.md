---

---
 
---
# Environment

El objeto **`Environment`** en Spring Framework es una interfaz que proporciona acceso a las propiedades de configuración de la aplicación, incluyendo variables de entorno y propiedades definidas en archivos como `application.properties` o `application.yml`. Es fundamental para gestionar configuraciones externas de manera flexible y desacoplada.

### **Funciones Clave del Objeto `Environment`**

1. **Obtener Propiedades**: Permite acceder a propiedades específicas.
2. **Verificar Perfiles Activos**: Soporta la gestión de perfiles para configuraciones específicas.
3. **Verificar Propiedades Disponibles**: Comprueba si una propiedad o variable de entorno exist

### **Métodos Importantes**

- `getProperty(String key)`: Devuelve el valor de la propiedad especificada o `null` si no existe.
- `getProperty(String key, Class<T> targetType)`: Devuelve la propiedad convertida al tipo especificado.
- `containsProperty(String key)`: Verifica si una propiedad existe.
- `getActiveProfiles()`: Devuelve los perfiles actualmente activos.
- `getDefaultProfiles()`: Devuelve los perfiles predeterminados.

---
# ClassPathResource

Proporciona una manera conveniente de acceder a recursos ubicados en el **classpath** de una aplicación. Permite cargar archivos como configuraciones, propiedades, imágenes, archivos XML, etc., directamente desde la estructura de directorios del proyecto o desde un archivo JAR.

---
# *ResponseEntity

Representa una respuesta HTTP completa, incluyendo el **cuerpo**, los **códigos de estado HTTP** y los **encabezados**. Es ampliamente utilizada en aplicaciones REST para proporcionar control granular sobre las respuestas enviadas al cliente.

### **Constructor de `ResponseEntity`**

Se pueden construir instancias de `ResponseEntity` utilizando sus constructores o el método estático `ResponseEntity.ok()`, entre otros.

### **Componentes Principales de `ResponseEntity`**

1. **Body**: El cuerpo de la respuesta (puede ser un objeto, texto, etc.).
2. **HTTP Status**: El código de estado de la respuesta (por ejemplo, 200 OK, 404 Not Found).
3. **Headers**: Los encabezados HTTP.
