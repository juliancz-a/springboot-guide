Un **caché** es un mecanismo que almacena temporalmente datos que se usan con frecuencia, para que futuras peticiones a esos datos se resuelvan más rápido, evitando recalcularlos o consultarlos de nuevo desde su origen (por ejemplo, desde una base de datos o una API externa).

**Ejemplo:**  
Si una aplicación recibe muchas solicitudes para consultar los productos más vendidos, en lugar de consultar la base de datos cada vez, guarda esa lista en caché y la devuelve directamente durante un tiempo determinado.

## ¿Cómo funciona el caché?

1. Se solicita un dato.
2. Si está en caché (**cache hit**), se devuelve directamente.
3. Si no está (**cache miss**), se obtiene desde su origen, se guarda en caché, y se devuelve.
4. Opcionalmente, después de un tiempo configurado o por políticas definidas, el dato en caché expira o se invalida.


## Integración de Caché en **Spring**

Spring tiene soporte integrado para caché a través de anotaciones, usando una abstracción que permite trabajar con distintos proveedores de caché como:

- ConcurrentHashMap (por defecto)
- EhCache
- Redis
- [Caffeine](caffeine.md)
- Entre otros.

---
##  Diferencias entre un **HashMap** y un **Caché**

| 📖 Concepto               | **HashMap**                                                                             | **Caché**                                                                                      |
| ------------------------- | --------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| 📌 **Qué es**             | Una estructura de datos que almacena pares clave-valor.                                 | Un mecanismo para almacenar temporalmente datos que se usan con frecuencia.                    |
| 📌 **Propósito**          | Guardar datos en memoria sin política de expiración.                                    | Optimizar accesos a datos costosos o lentos, controlando su validez.                           |
| 📌 **Expiración**         | No tiene. Los datos permanecen hasta que se eliminan manualmente o se destruye el mapa. | Tiene políticas de expiración o limpieza (por tiempo, espacio o acceso).                       |
| 📌 **Capacidad**          | Limitada solo por la memoria disponible.                                                | Puede tener límites definidos (cantidad, tamaño, TTL).                                         |
| 📌 **Gestión automática** | No tiene. El programador debe eliminar o limpiar entradas.                              | Puede limpiar automáticamente datos antiguos o no usados.                                      |
| 📌 **Uso típico**         | Guardar datos temporales en memoria dentro de una app.                                  | Almacenar resultados de consultas costosas, accesos a disco o red, resultados de métodos, etc. |
| 📌 **Soporte multi-hilo** | `HashMap` no es seguro para hilos. `ConcurrentHashMap` sí.                              | Los cachés suelen estar pensados para multi-hilo y alto rendimiento.                           |
| 📌 **Implementaciones**   | Java Standard: `HashMap`, `ConcurrentHashMap`.                                          | EhCache, Caffeine, Redis, Guava Cache, etc.                                                    |