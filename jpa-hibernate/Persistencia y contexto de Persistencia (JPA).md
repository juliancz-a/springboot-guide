## **¿Qué es la persistencia en JAVA?**

La persistencia en Java es la capacidad de almacenar y recuperar datos de forma permanente, generalmente en una base de datos. En Java, la persistencia de datos es importante en las aplicaciones empresariales, que necesitan acceder a bases de datos relacionales. 

Java Persistence API (JPA) es una especificación estándar que permite gestionar la persistencia de datos en aplicaciones Java. JPA es un marco de mapeo relacional de objetos (ORM) que permite asignar objetos Java a tablas de bases de datos.
## 🔹 **¿Qué es el Contexto de Persistencia en JPA/Spring?**

El **contexto de persistencia** es un concepto fundamental en **JPA (Java Persistence API)** que representa el **área de memoria** donde las entidades gestionadas por el **EntityManager** son rastreadas.

📌 **Funciona como una caché de primer nivel**, asegurando que los objetos en memoria estén sincronizados con la base de datos y evitando consultas innecesarias.

## ✅ **Características del Contexto de Persistencia**

1️⃣ **Gestión de Entidades**

- Las entidades dentro del contexto están en **estado "managed"** (gestionado).
- Cualquier cambio en la entidad se sincroniza automáticamente con la base de datos (cuando se confirma la transacción).

2️⃣ **Sincronización Automática con la Base de Datos**

- Al ejecutar `commit`, todas las entidades **modificadas** en el contexto se actualizan en la base de datos.

3️⃣ **Estrategias de Propagación**

- El contexto puede compartirse entre transacciones o ser independiente.

---

## 📌 **Estados de una Entidad en el Contexto de Persistencia**

| Estado        | Descripción                                                                  | Ejemplo                           |
| ------------- | ---------------------------------------------------------------------------- | --------------------------------- |
| **Transient** | La entidad no está en el contexto ni en la base de datos.                    | `new Usuario();`                  |
| **Managed**   | La entidad está en el contexto y sincronizada con la base de datos.          | `entityManager.persist(usuario);` |
| **Detached**  | La entidad ya no está gestionada, pero sigue existiendo en la base de datos. | `entityManager.detach(usuario);`  |
| **Removed**   | La entidad ha sido marcada para eliminarse de la base de datos.              | `entityManager.remove(usuario);`  |
