Spring Data JPA es un módulo de Spring que simplifica la interacción con bases de datos mediante **Hibernate**. Proporciona una capa de abstracción sobre JPA (Java Persistence API) y permite escribir consultas con **poco o nada de código SQL**.

---

## 📌 **Características Principales**

✅ **Reducción de código repetitivo**: Genera automáticamente consultas CRUD.  
✅ **Uso de interfaces en lugar de implementaciones**.  
✅ **Soporte para HQL, JPQL, Criteria API y SQL nativo**.  
✅ **Gestión automática de transacciones**.

--- 
Mas declarativo que trabajar con Hibernate vanilla. Trabaja con interfaces y anotaciones.

## 🌿 **Principales Interfaces en Spring Data JPA**

Spring Data JPA proporciona varias interfaces clave para interactuar con bases de datos mediante JPA (Java Persistence API). Estas interfaces facilitan la creación de repositorios sin necesidad de escribir implementaciones manuales.

| **Interfaz**                   | **Extiende**               | **Características**                           |
| ------------------------------ | -------------------------- | --------------------------------------------- |
| **JpaRepository**              | PagingAndSortingRepository | CRUD completo + paginación/ordenación         |
| **CrudRepository**             | Repository                 | Solo operaciones CRUD básicas                 |
| **PagingAndSortingRepository** | CrudRepository             | CRUD + paginación y ordenación                |
| **QuerydslPredicateExecutor**  | Repository                 | Soporte para consultas dinámicas con QueryDSL |
| **JpaSpecificationExecutor**   | Repository                 | Consultas avanzadas con Criteria API          |
## 🔹  JpaRepository<T, ID>

📌 **Extiende:** `PagingAndSortingRepository<T, ID>` → `CrudRepository<T, ID>`

📌 **Uso:** Proporciona todas las operaciones CRUD y paginación/sorting.

📌 **Métodos heredados**:  
✔ `save(T entity)`: Guarda o actualiza una entidad.  
✔ `findById(ID id)`: Encuentra una entidad por ID.  
✔ `findAll()`: Recupera todas las entidades.  
✔ `delete(T entity)`: Elimina una entidad.  
✔ `deleteById(ID id)`: Elimina una entidad por ID.  
✔ `existsById(ID id)`: Verifica si una entidad existe.  
✔ `count()`: Cuenta el total de entidades.

---


## 🔍 **Métodos Query en Spring Data JPA**
#### 📌 1. Utilizando palabras clave en métodos

| **Keyword**            | **Sample**                                                      | **JPQL snippet**                                                                      |
| ---------------------- | --------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| **Distinct**           | `findDistinctByLastnameAndFirstname`                            | `select distinct … where x.lastname = ?1 and x.firstname = ?2`                        |
| **And**                | `findByLastnameAndFirstname`                                    | `… where x.lastname = ?1 and x.firstname = ?2`                                        |
| **Or**                 | `findByLastnameOrFirstname`                                     | `… where x.lastname = ?1 or x.firstname = ?2`                                         |
| **Is, Equals**         | `findByFirstname`, `findByFirstnameIs`, `findByFirstnameEquals` | `… where x.firstname = ?1` (or `… where x.firstname IS NULL` if the argument is null) |
| **Between**            | `findByStartDateBetween`                                        | `… where x.startDate between ?1 and ?2`                                               |
| **LessThan**           | `findByAgeLessThan`                                             | `… where x.age < ?1`                                                                  |
| **LessThanEqual**      | `findByAgeLessThanEqual`                                        | `… where x.age <= ?1`                                                                 |
| **GreaterThan**        | `findByAgeGreaterThan`                                          | `… where x.age > ?1`                                                                  |
| **GreaterThanEqual**   | `findByAgeGreaterThanEqual`                                     | `… where x.age >= ?1`                                                                 |
| **After**              | `findByStartDateAfter`                                          | `… where x.startDate > ?1`                                                            |
| **Before**             | `findByStartDateBefore`                                         | `… where x.startDate < ?1`                                                            |
| **IsNull, Null**       | `findByAge(Is)Null`                                             | `… where x.age is null`                                                               |
| **IsNotNull, NotNull** | `findByAge(Is)NotNull`                                          | `… where x.age is not null`                                                           |
| **Like**               | `findByFirstnameLike`                                           | `… where x.firstname like ?1`                                                         |
| **NotLike**            | `findByFirstnameNotLike`                                        | `… where x.firstname not like ?1`                                                     |
| **StartingWith**       | `findByFirstnameStartingWith`                                   | `… where x.firstname like ?1` (parameter bound with appended `%`)                     |
| **EndingWith**         | `findByFirstnameEndingWith`                                     | `… where x.firstname like ?1` (parameter bound with prepended `%`)                    |
| **Containing**         | `findByFirstnameContaining`                                     | `… where x.firstname like ?1` (parameter bound wrapped in `%`)                        |
| **OrderBy**            | `findByAgeOrderByLastnameDesc`                                  | `… where x.age = ?1 order by x.lastname desc`                                         |
| **Not**                | `findByLastnameNot`                                             | `… where x.lastname <> ?1`                                                            |
| **In**                 | `findByAgeIn(Collection<Age> ages)`                             | `… where x.age in ?1`                                                                 |
| **NotIn**              | `findByAgeNotIn(Collection<Age> ages)`                          | `… where x.age not in ?1`                                                             |
| **True**               | `findByActiveTrue()`                                            | `… where x.active = true`                                                             |
| **False**              | `findByActiveFalse()`                                           | `… where x.active = false`                                                            |
| **IgnoreCase**         | `findByFirstnameIgnoreCase`                                     | `… where UPPER(x.firstname) = UPPER(?1)`                                              |

#### 📌 2. Utilizando @Query

```Java
public interface UsuarioRepository extends JpaRepository<Usuario, Long> {

    // Buscar usuarios cuyo nombre coincida exactamente
    @Query("SELECT u FROM Usuario u WHERE u.nombre = :nombre")
    List<Usuario> buscarPorNombre(@Param("nombre") String nombre);

    // Buscar usuarios con edad mayor a un valor dado
    @Query("SELECT u FROM Usuario u WHERE u.edad > :edad")
    List<Usuario> mayoresDe(@Param("edad") int edad);
}
```


--- 

## JOIN Comparaciones

|Tipo de JOIN|Incluye registros sin coincidencia|Devuelve `NULL` cuando no hay coincidencia|
|---|---|---|
|**INNER JOIN**|❌ No|❌ No|
|**LEFT JOIN**|✅ Sí (de la tabla izquierda)|✅ En las columnas de la tabla derecha|
|**RIGHT JOIN**|✅ Sí (de la tabla derecha)|✅ En las columnas de la tabla izquierda|
### JOIN FETCH
Se usa para realizar una **carga ansiosa (Eager Loading)** de relaciones `@OneToMany`, `@ManyToOne`, `@OneToOne` o `@ManyToMany`.

**Por qué usar `JOIN FETCH`?**  
En JPA, las relaciones `@OneToMany` y `@ManyToMany` suelen cargarse de forma **Lazy** (perezosa) por defecto. Esto puede generar problemas de `LazyInitializationException` si intentamos acceder a una colección fuera del contexto de persistencia. `JOIN FETCH` permite recuperar las entidades relacionadas en la misma consulta SQL, evitando múltiples queries (`N+1 problem`).


### **🔍 Problema: Múltiples `JOIN FETCH` en consultas JPQL con Listas**

Cuando se usa `JOIN FETCH` con **dos relaciones `@OneToMany` o `@ManyToMany`**, Hibernate puede lanzar una excepción como:

> _"Cannot simultaneously fetch multiple bags"_

💡 **Esto ocurre porque Hibernate no permite hacer `JOIN FETCH` con más de una colección (`List<>`) en la misma consulta**. Si intentas hacerlo, los datos pueden volverse inconsistentes debido a la duplicación de filas en los resultados.

## ✅ Soluciones

| Solución                        | Pros                                                         | Contras                                     |
| ------------------------------- | ------------------------------------------------------------ | ------------------------------------------- |
| `DISTINCT` en la consulta       | Evita duplicados                                             | Puede no resolver el problema completamente |
| `@EntityGraph`                  | Carga eficiente y evita `JOIN FETCH` en múltiples relaciones | No funciona en todas las bases de datos     |
| Consultas separadas             | Evita problemas de duplicación y mejora rendimiento          | Necesita múltiples llamadas a la BD         |
| Usar `Set<>` en vez de `List<>` | Hibernate lo maneja mejor                                    | Puede cambiar la lógica del código          |

📌 **Recomendación:**  
🔹 **Si puedes usar `@EntityGraph`, es la mejor solución.**  
🔹 **Si necesitas `JOIN FETCH`, intenta usar `Set<>` en lugar de `List<>`.**  
🔹 **Si persisten los errores, usa múltiples consultas para cargar los datos.** 
