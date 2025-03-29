En JPA, las relaciones entre entidades pueden cargarse de dos maneras:

1. **EAGER (CARGA ANSIOSA)** → Se carga la relación **inmediatamente** cuando se recupera la entidad principal.
2. **LAZY (CARGA PEREZOSA)** → La relación **se carga solo cuando se necesita** (cuando se accede a la propiedad relacionada). **Problema con LAZY:** Puede generar `LazyInitializationException` si la sesión de Hibernate está cerrada.

📌 **Se configura con el atributo `fetch` en las anotaciones `@OneToOne`, `@OneToMany`, `@ManyToOne` y `@ManyToMany`**.


### **@OneToMany y @ManyToOne**

Por defecto:

- `@OneToMany` → **LAZY**
- `@ManyToOne` → **EAGER**

✅ **Si usamos LAZY en `@OneToMany`, no se cargarán los pedidos al traer un Cliente, solo se cargarán cuando accedamos a `cliente.getPedidos()`.**  
❌ **Si usamos EAGER en `@OneToMany`, puede generar muchas consultas innecesarias (problema N+1).**

|Relación|**EAGER (Carga Inmediata)** 🚀|**LAZY (Carga Diferida)** 💤|
|---|---|---|
|`@OneToOne`|Solo si **siempre** se necesita la relación.|Recomendado para evitar consultas innecesarias.|
|`@OneToMany`|No recomendado (puede generar muchas consultas).|✅ Recomendado para mejor rendimiento.|
|`@ManyToOne`|✅ Por defecto (está bien en la mayoría de casos).|Solo si hay problemas de rendimiento.|
|`@ManyToMany`|No recomendado, puede ser peligroso si hay muchas relaciones.|✅ Recomendado (evita sobrecargar la memoria).|

## 🔄 **Cómo Hibernate maneja la sesión**

Hibernate usa el **contexto de persistencia**, que se encuentra dentro de la **sesión de Hibernate**.

1️⃣ **Cuando llamas a un metodo`findById`, Hibernate solo carga la entidad `primaria`, pero no su relación `asociada`.**

- Si la relación es `LAZY`, en memoria se almacena un **proxy** de la lista de objetos de la entidad hija, pero la consulta real a la base de datos no se ejecuta todavía.

2️⃣ **Cuando intentas acceder a `EntidadPrimaria.getListaObjsDeLaOtraEntidad()` en otro punto del código (otro scope), Hibernate necesita hacer una consulta a la base de datos para obtener las direcciones.**

- Si la sesión de Hibernate sigue abierta, se ejecuta la consulta y se llena la lista.
- **Si la sesión ya se cerró, Hibernate lanza una `LazyInitializationException`.**

Ejemplo

```Java
@Transactional
public void oneToManyFindById() {
    Optional<Client> optClient = clientRepository.findById(2L); // Hibernate abre la sesión y carga Client, pero NO las direcciones

    optClient.ifPresent(client -> {
        System.out.println(client.getAddresses()); // Aquí intenta cargar las direcciones, pero la sesión ya se cerró ❌
    });
}
```

Resolver con
```
spring.jpa.properties.hibernate.enable_lazy_load_no_trans=true
```

Sin embargo es un antipatrón.

Otra manera es con Join Fetch ->  Ver [Spring Data JPA](Spring%20Data%20JPA.md)