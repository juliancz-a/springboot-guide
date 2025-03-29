### **1. URI (Uniform Resource Identifier)**

Un **URI** es una cadena de caracteres que identifica de manera única un recurso en Internet o una red. Puede describir **dónde** está el recurso o simplemente **qué** es.

**Ejemplo**:

- `https://example.com/resources/document`
- `urn:isbn:978-3-16-148410-0`

**Tipos de URI**:

1. **URL** (Localizador de Recursos Uniforme)
2. **URN** (Nombre de Recursos Uniforme)

**Características**:

- Un URI puede ser un **URL** o un **URN**, o ambos al mismo tiempo.

### **2. URL (Uniform Resource Locator)**

Un **URL** es un tipo específico de **URI** que proporciona los medios para localizar un recurso mediante su dirección en la red. Incluye el esquema (protocolo), el nombre de dominio, la ruta, el puerto, etc.

**Ejemplo**:

- `https://www.example.com/index.html`
- `ftp://ftp.example.com/file.txt`

**Componentes de un URL**:

- **Protocolo (https, ftp)**: Especifica cómo acceder al recurso.
- **Dominio o IP**: `www.example.com`
- **Puerto (opcional)**: `:8080`
- **Ruta**: `/index.html`
- **Parámetros (opcional)**: `?id=123`

### **3. URN (Uniform Resource Name)**

Un **URN** es un tipo de URI que nombra un recurso de forma única sin necesidad de indicar su ubicación o cómo acceder a él. Se utiliza para la identificación persistente de recursos.

**Ejemplo**:

- `urn:isbn:978-3-16-148410-0` (Identificador único de un libro basado en su ISBN)

**Características**:

- No indica cómo o dónde obtener el recurso.
- Su propósito es ser un identificador globalmente único y persistente.

---

### **Comparación**

|Característica|URI|URL|URN|
|---|---|---|---|
|**Definición**|Identificador general de recursos|Identificador con la localización|Identificador único|
|**Incluye**|URL y URN|Solo URL|Solo URN|
|**Ejemplo**|`https://example.com/page`|`https://example.com/page`|`urn:isbn:1234-5678`|
|**Propósito**|Identificación de recursos|Localizar un recurso en una red|Nombrar un recurso de forma única|