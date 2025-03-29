## 🏛️ **Anotaciones Principales en Hibernate** y JPA

### 📌 **1. @Entity**

Indica que una clase Java representa una tabla en la base de datos.

```Java
@Entity 
public class Cliente { 
// Código aquí...
}
```
### 📌 **2. @Table**

Define el nombre de la tabla en la base de datos (opcional, si no se especifica, usa el nombre de la clase).

```Java
@Entity 
@Table(name = "clientes") 
public class Cliente { 
// Código aquí... 
}
```
### 📌 **3. @Id y @GeneratedValue**

Marca la clave primaria y la estrategia para generarla automáticamente.
```Java
@Entity 
public class Cliente { 

@Id 
@GeneratedValue(strategy = GenerationType.IDENTITY) // Autoincremental 
private Long id; 

private String nombre; 
}
```

### 📌 **4. @Column**

Personaliza la columna en la base de datos.

```Java
@Column(name = "correo_electronico", nullable = false, unique = true)
private String email;
```

---

## 🔗 **Relaciones entre Entidades**

### 📌 **5. @OneToOne** (Uno a Uno)

java
```Java
@Entity
public class Cliente {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @OneToOne(cascade = CascadeType.ALL)
    @JoinColumn(name = "direccion_id", referencedColumnName = "id")
    private Direccion direccion;
}

```
---

### 📌 **6. @OneToMany** (Uno a Muchos)

```Java
@Entity
public class Cliente {
    
    @OneToMany(mappedBy = "cliente", cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    private List<Pedido> pedidos;
}
```

---

### 📌 **7. @ManyToOne** (Muchos a Uno)
```Java
@Entity
public class Pedido {
    
    @ManyToOne
    @JoinColumn(name = "cliente_id")
    private Cliente cliente;
}

```

---

### 📌 **8. @ManyToMany** (Muchos a Muchos)

```Java
@Entity
public class Estudiante {
    @ManyToMany
    @JoinTable(
        name = "estudiante_curso",
        joinColumns = @JoinColumn(name = "estudiante_id"),
        inverseJoinColumns = @JoinColumn(name = "curso_id")
    )
    private List<Curso> cursos;
}

```
---

## 🎯 **Otras Anotaciones Útiles**

| Anotación     | Descripción                                         |
| ------------- | --------------------------------------------------- |
| `@Lob`        | Para almacenar datos grandes como texto o imágenes. |
| `@Temporal`   | Para fechas (`DATE`, `TIME`, `TIMESTAMP`).          |
| `@Transient`  | Indica que un atributo **no se almacena** en la BD. |
| `@Enumerated` | Para mapear `enum` en la BD.                        |

--- 
## 🔄 **Fases del Ciclo de Vida de una Entidad**


Una entidad en JPA pasa por distintos estados:

1️⃣ **Transient** → La entidad no está en el contexto de persistencia ni en la base de datos.  
2️⃣ **Managed** → La entidad está gestionada por el `EntityManager` y sincronizada con la base de datos.  
3️⃣ **Detached** → La entidad ha sido separada del contexto de persistencia, pero aún existe en la BD. 
4️⃣ **Removed** → La entidad ha sido marcada para eliminación, pero no se ha eliminado aún de la BD.


#### 🏷 **Anotaciones de Persistencia para Eventos del Ciclo de Vida**

 🔸 `@PrePersist`

📌 **Ejecuta código antes de insertar una entidad en la base de datos.**


 🔸 `@PostPersist`

📌 **Ejecuta código después de que una entidad ha sido insertada en la base de datos.**


 🔸 `@PreUpdate`

📌 **Ejecuta código antes de actualizar una entidad en la base de datos.**


 🔸 `@PostUpdate`

📌 **Ejecuta código después de actualizar una entidad en la base de datos.**


🔸 `@PreRemove`

📌 **Ejecuta código antes de eliminar una entidad de la base de datos.**


 🔸 `@PostRemove`

📌 **Ejecuta código después de eliminar una entidad de la base de datos.**


 🔸 `@PostLoad`

📌 **Ejecuta código después de que una entidad ha sido cargada desde la base de datos.**

--- 
## 🔹 **Anotaciones `@Embedded` y `@Embeddable` en JPA 

En JPA, **`@Embedded` y `@Embeddable`** permiten modelar objetos **reutilizables y componibles** dentro de una entidad. Estas anotaciones ayudan a agrupar atributos en clases separadas sin necesidad de crear una nueva tabla en la base de datos.

### **📌 `@Embeddable (Integrable)`**

📌 Marca una clase como **un tipo de dato embebible**, es decir, un conjunto de atributos que pueden formar parte de otra entidad. Almacena campos a reutilizar -> clase integrable y anexable a otras clases @Entity

✅ **No es una entidad independiente**, sino que será **insertada dentro de otra entidad**.


### **📌 `@Embedded (Incorporado)`**

📌 Indica que una clase embebible (`@Embeddable`) se usa dentro de una **entidad principal**.

---
##  `@JoinTable` y `@JoinColumn` en JPA

Las anotaciones `@JoinTable` y `@JoinColumn` se usan en JPA para definir cómo se establecen las relaciones entre entidades en la base de datos.

#### 1️⃣ **`@JoinColumn`**

Se usa en relaciones **`@ManyToOne` y `@OneToOne`** para indicar qué columna en la tabla de la entidad actual se usará como **clave foránea**.

```Java
@Entity
public class Empleado {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String nombre;

    @ManyToOne
    @JoinColumn(name = "departamento_id")  // Clave foránea en la tabla `empleado`
    private Departamento departamento;
}
```

#### 2️⃣ **`@JoinTable`**

Se usa en relaciones **`@ManyToMany`** para definir la **tabla intermedia** que se creará para mapear la relación. 

```Java
@Entity
public class Estudiante {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String nombre;

    @ManyToMany
    @JoinTable(
        name = "estudiante_curso",  // Nombre de la tabla intermedia
        joinColumns = @JoinColumn(name = "estudiante_id"),  // Clave foránea de Estudiante
        inverseJoinColumns = @JoinColumn(name = "curso_id")  // Clave foránea de Curso
    )
    private List<Curso> cursos;
}
```

Si se crea la tabla intermedia de manera automática (@OneToMany), es útil para cambiar el nombre de la entidad y la de las columnas. Ejemplo:

```Java
@OneToMany(cascade = CascadeType.ALL, orphanRemoval=true)
@JoinTable(name="tbl_clientes_direcciones", joinColumns = @JoinColumn (name="id_client"), inverseJoinColumns = @JoinColumn(name="id_address"))
private List<Address> addresses;
```

---
##### **Propiedades

✨ `joinColumns`

Define la clave foránea de la entidad que **contiene la anotación `@JoinTable`**.

✨ `inverseJoinColumns`

Define la clave foránea de la entidad que **no contiene la anotación `@JoinTable`** (la otra entidad en la relación).

✨ `UniqueConstraints`

Una restricción que **involucra múltiples columnas** . Definir **varias restricciones en la misma entidad**. Ejemplo
```Java
uniqueConstraints = @UniqueConstraint(columnNames = {"email", "empresa_id"})
```

|Anotación|Relación|Ubicación|Uso|
|---|---|---|---|
|`@JoinColumn`|`@ManyToOne`, `@OneToOne`|Se coloca en el **lado dueño** de la relación|Define **una sola clave foránea** en la tabla de la entidad|
|`@JoinTable`|`@ManyToMany`|Se coloca en **uno de los lados** de la relación|Crea **una tabla intermedia** para mapear la relación|


--- 
## Relaciones bidireccionales

Cuando usamos una relación bidireccional entre entidades en JPA con `@OneToMany` y `@ManyToOne`,
debemos definir **quién es el dueño de la relación**. Esto se logra usando la propiedad `mappedBy`.

- **El lado `@ManyToOne` es el dueño de la relación**.
- **El lado `@OneToMany` usa `mappedBy` para referenciar el nombre del atributo en el lado dueño**.

## **📌 Diferencias entre `@OneToMany` y `@ManyToOne`**

|Relación|Ubicación de `@JoinColumn`|Propiedad clave|
|---|---|---|
|**`@OneToMany`**|No la tiene (usa `mappedBy`)|`mappedBy = "cliente"`|
|**`@ManyToOne`**|Tiene `@JoinColumn`|`@JoinColumn(name = "cliente_id")`|

Si ambas entidades incluyen la relación en `toString()`, se genera una **StackOverflowError** por recursión infinita. Por ejemplo:

- Si intentamos imprimir un `Cliente`, su `toString()` intentará imprimir **todos sus `Pedidos`**.
- Pero cada `Pedido` intentará imprimir su `Cliente`, que a su vez intentará imprimir **todos los `Pedidos`** nuevamente.

Para evitarlo:
✔ Excluir la relación en uno de los `toString()`.  
✔ Usar `@JsonIgnore` en APIs REST. [Anotaciones Jackson](Anotaciones%20Jackson.md)