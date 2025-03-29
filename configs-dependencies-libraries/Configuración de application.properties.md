`spring.application.name=springboot-web `
`server.port=8080 `

#### Personalizar Error 404
```
spring.mvc.throw-exception-if-no-handler-found=true`
spring.web.resources.add-mappings=false`
```

####  Propiedades de conexión a la Base de Datos y de JPA
```
spring.datasource.url=jdbc:mysql://localhost:3306/db_users_springboot

spring.datasource.username=root

spring.datasource.password=admin

spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

spring.jpa.database-platform=org.hibernate.dialect.MySQLDialect

spring.jpa.show-sql=true
```

Crear DDL automaticamente en el motor de DB

```
spring.jpa.hibernate.ddl-auto=create // crea la tabla si no existe, la elimina si existe

spring.jpa.hibernate.ddl-auto=update // crea la tabla si no existe,la actualiza si existen cambios de columnas

```

DML (Insert) desde Spring:

Archivo import.sql con operaciones DML

Configurar Lazy Fetch para colecciones fuera del contexto de persistencia: [FetchType - JPA](../jpa-hibernate/FetchType%20-%20JPA.md)