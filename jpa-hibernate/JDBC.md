JDBC (**Java Database Connectivity**) es una API de Java que permite la conexión y manipulación de bases de datos relacionales desde aplicaciones Java. Proporciona métodos estándar para ejecutar consultas SQL y manejar resultados.

🔹 **Características principales de JDBC**:  
✔ Conexión directa con la base de datos.  
✔ Requiere escribir sentencias SQL manualmente.  
✔ Usa `DriverManager` para gestionar controladores de bases de datos.  
✔ Ofrece `PreparedStatement` para consultas parametrizadas y `ResultSet` para manejar resultados.

## 🔍 **Diferencias Clave entre JDBC y JPA**

|**Aspecto**|**JDBC**|**JPA**|
|---|---|---|
|**Nivel de abstracción**|Bajo (requiere SQL manualmente)|Alto (ORM, sin necesidad de SQL directo)|
|**Facilidad de uso**|Más complejo, manejo manual de conexiones y transacciones|Más sencillo, gestiona transacciones automáticamente|
|**Lenguaje de consulta**|SQL estándar|JPQL, Criteria API, SQL Nativo|
|**Mapeo Objeto-Relacional (ORM)**|No soporta ORM, trabaja con filas y columnas|Soporta ORM, trabaja con objetos Java|
|**Manejo de transacciones**|Manual (`commit()`, `rollback()`)|Automático con `@Transactional`|
|**Optimización y caché**|No tiene caché incorporado|Soporta caché de primer y segundo nivel|
|**Código repetitivo**|Alto (declaración de conexión, consultas, cierre de recursos)|Bajo (solo se definen entidades y repositorios)|

---

## 🎯 **¿Cuándo Usar JDBC vs JPA?**

|**Escenario**|**Recomendado**|
|---|---|
|Aplicaciones pequeñas con acceso simple a BD|**JDBC**|
|Cuando se necesita **máximo control sobre consultas SQL**|**JDBC**|
|Aplicaciones grandes con **estructura orientada a objetos**|**JPA**|
|Cuando se requiere **compatibilidad con múltiples BD sin cambios en el código**|**JPA**|
|Para proyectos que deben **optimizar consultas específicas**|**JPA con SQL nativo**|