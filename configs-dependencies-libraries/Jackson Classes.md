# ObjectMapper

`ObjectMapper` es una clase fundamental en la biblioteca **Jackson** de Java que se utiliza para convertir entre **objetos Java y JSON**. Proporciona métodos para **serializar** objetos Java a JSON y **deserializar** JSON a objetos Java.

### **Métodos Comunes**

|Método|Descripción|
|---|---|
|`writeValueAsString(Object obj)`|Convierte un objeto Java en una cadena JSON.|
|`writeValue(File file, Object obj)`|Escribe un objeto Java en un archivo como JSON.|
|`readValue(String content, Class<T> valueType)`|Convierte una cadena JSON a un objeto del tipo especificado.|
|`readTree(String content)`|Lee JSON en una estructura `JsonNode`.|

---
### 📌 `addMixIn` en `ObjectMapper`

El método `addMixIn` de la clase `ObjectMapper` en **Jackson** permite agregar **Mixins**, que son una forma de **modificar la serialización/deserialización de una clase sin modificar su código fuente**.

## ✅ **1. ¿Para qué se usa `addMixIn`?**

Se usa cuando:  
✔ **No puedes modificar la clase original**, pero necesitas cambiar cómo se serializa/deserializa.  
✔ Quieres **ocultar campos**, cambiar nombres o agregar anotaciones sin tocar la clase real.  
✔ Es útil en **frameworks** donde las clases son externas (como en una API de terceros).

```Java
objectMapper.addMixIn(CLASE_ORIGINAL.class, MIXIN.class);
```

--- 
### Ejemplo de uso:

🔹 **CLASE_ORIGINAL:** Es la clase cuyo comportamiento de serialización queremos modificar.  

```Java
public final class SimpleGrantedAuthority implements GrantedAuthority {

  

    private static final long serialVersionUID = SpringSecurityCoreVersion.SERIAL_VERSION_UID;

    private final String role;

    public SimpleGrantedAuthority(String role) { //queremos cambiar el nombre de este parametro al ser serializado

        Assert.hasText(role, "A granted authority textual representation is required");

        this.role = role;

    }
```

🔹 **MIXIN:** Es una clase abstracta o interfaz con anotaciones de Jackson (`@JsonIgnore`, `@JsonProperty`, etc.).

```Java
public abstract class SimpleGrantedAuthorityJsonCreator {

    @JsonCreator
    public SimpleGrantedAuthorityJsonCreator(@JsonProperty("authority") String role) {} // para que sea mapeado a la llave que posee el nombre "authority"
}
```