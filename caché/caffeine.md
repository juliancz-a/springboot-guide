**Caffeine** es una librería Java de alto rendimiento para caché en memoria. Es el sucesor mejorado de **Guava Cache** de Google y es muy popular en aplicaciones Spring Boot porque:

- Es **rápida**
- Soporta políticas avanzadas de expiración y tamaño
- Es **thread-safe**
- Tiene **near-optimal hit rates**
- Se integra fácilmente con Spring Boot

El cache en caffeine puede:
- Puede **expirar por tiempo**
- Puede **expirar por inactividad**
- Puede limitar el **número máximo de entradas**
- Permite **eliminar automáticamente los menos usados**
- Ofrece métricas de rendimiento
- Permite carga automática con `CacheLoader`