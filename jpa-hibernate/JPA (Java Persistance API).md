**JPA (Java Persistence API)** es una especificación de Java que proporciona un estándar para mapear objetos de Java a bases de datos relacionales, permitiendo la persistencia de datos. Es una parte de la plataforma **Java EE** (ahora Jakarta EE) y se utiliza en aplicaciones Java para realizar operaciones CRUD (Crear, Leer, Actualizar y Eliminar) de manera más eficiente y con menos código repetitivo.

### **Conceptos Clave de JPA**

1. **Especificación, no implementación**: JPA define una serie de interfaces y reglas, pero no proporciona una implementación concreta. Frameworks como **Hibernate**, **EclipseLink** y **OpenJPA** son implementaciones de JPA.
2. **Mapeo objeto-relacional (ORM)**: Permite mapear clases Java a tablas de bases de datos, atributos a columnas y relaciones entre objetos a relaciones entre tablas.

### **Componentes Principales de JPA**

1. **Entidades**: Clases [POJO](../core-concepts/POJO.md) anotadas con **`@Entity`**, que representan tablas en la base de datos.
2. **EntityManager**: Interfaz para realizar operaciones de persistencia como guardar, actualizar, eliminar y consultar entidades.
3. **Persistence Context**: Área administrada por JPA donde se manejan las entidades.
4. **JPQL (Java Persistence Query Language)**: Lenguaje similar a SQL, diseñado para realizar consultas sobre entidades JPA.


### **Principales Anotaciones de JPA**

- **`@Entity`**: Marca una clase como una entidad persistente. (Hibernate)
- **`@Id`**: Define la clave primaria de la entidad.
- **`@GeneratedValue`**: Especifica la estrategia para la generación de valores de la clave primaria.
- **`@Column`**: Personaliza el mapeo de un atributo a una columna de la base de datos.
- **`@OneToMany`, `@ManyToOne`, `@OneToOne`, `@ManyToMany`**: Definen relaciones entre entidades.`**