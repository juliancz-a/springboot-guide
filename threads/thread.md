Un **hilo** es una unidad de ejecución dentro de un proceso.  
Un proceso puede tener **uno o varios hilos** que se ejecutan en paralelo (o concurrentemente) compartiendo la memoria del mismo proceso.

**Ejemplo:**

- Un servidor web recibe 50 peticiones concurrentes.
- Puede crear 50 hilos para procesarlas al mismo tiempo.

## ¿Cómo maneja Spring los hilos?

Spring, por defecto, no crea hilos por cada método o acción que escribes.  
Pero cuando ocurre:

- Una petición HTTP (en Spring MVC o REST)
- Una tarea programada (`@Scheduled`)
- Una operación asíncrona (`@Async`)
- Una cola de mensajes (Kafka)
    
Spring gestiona los hilos usando **ThreadPools** (pools de hilos reutilizables).

---
### 🧵 **ThreadPool (pool de hilos)**

Es un grupo de hilos que se pueden reutilizar para ejecutar tareas concurrentes.

👉 Ventaja: no se crean hilos nuevos cada vez → ahorro de recursos y control del máximo de concurrencia.

---
## Cómo se asegura Spring de que los hilos no se bloqueen?

Usando:

- **Thread-safe**: asegurarse de que el acceso a variables o recursos compartidos se haga de forma segura entre hilos.
    
- **Concurrent collections**: como `ConcurrentHashMap`, `CopyOnWriteArrayList`.
    
- **Locks** o sincronización cuando se requiere.
    
- **Thread pools**: para controlar cuántos hilos trabajan a la vez.