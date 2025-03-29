- **SQL**: Es un lenguaje estándar para gestionar y manipular bases de datos relacionales. Funciona directamente con tablas, columnas y filas.
- **HQL/JPQL**: Son lenguajes orientados a objetos utilizados en frameworks como Hibernate y JPA. Trabajan con entidades y objetos en lugar de tablas y columnas.

## 💡| Ejemplos


1. Seleccionar todos los empleados de la tabla `employees`.

```sql
SELECT * FROM employees;
```

```java
SELECT e FROM Employee e;
```

2. Seleccionar empleados con salario mayor a 5000.

```sql
SELECT * FROM employees WHERE salary > 5000;
```

```java
SELECT e FROM Employee e WHERE e.salary > 5000;
```

