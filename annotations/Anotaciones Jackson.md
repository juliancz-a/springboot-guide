### **`@JsonProperty` 

La anotación `@JsonProperty` en **Jackson** (biblioteca para trabajar con JSON en Java) se usa para:  
✔ **Modificar el nombre de la propiedad** en la serialización/deserialización.  
✔ **Ignorar campos nulos o vacíos.**  
✔ **Modificar el orden de las propiedades en JSON.**

| **Propiedad**                               | **Descripción**                                                          |
| ------------------------------------------- | ------------------------------------------------------------------------ |
| `@JsonProperty("nombre")`                   | Cambia el nombre de la propiedad en JSON.                                |
| `@JsonProperty(access = Access.READ_ONLY)`  | Solo lectura (aparece en JSON, pero no se puede escribir).               |
| `@JsonProperty(access = Access.WRITE_ONLY)` | Solo escritura (se puede recibir en JSON, pero no aparece en la salida). |
| `@JsonProperty(index = N)`                  | Ordena los campos en la salida JSON.                                     |

### `@JsonIgnore`

Esta anotación se utiliza a **nivel de campo o método** para indicar que un campo específico debe ser ignorado durante la serialización y deserialización. Es decir, el campo no se incluirá en el JSON generado ni se esperará en el JSON de entrada.

### `@JsonIgnoreProperties`

Esta anotación se utiliza a **nivel de clase, nivel de campo o método** para especificar una lista de propiedades que deben ser ignoradas durante la serialización y deserialización. Puede ser útil cuando no tienes control sobre la clase (por ejemplo, si es una clase de una biblioteca externa) y quieres ignorar ciertos campos.