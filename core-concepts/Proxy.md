Un **proxy** es un objeto que actúa como intermediario o representante de otro objeto. Permite controlar el acceso al objeto real, agregar funcionalidades adicionales o realizar operaciones específicas antes o después de interactuar con él. Los **proxies** se utilizan en diversos contextos, como patrones de diseño, redes, y frameworks como **Spring**.

### Concepto General

Un proxy proporciona un nivel de indirecta para:

- Controlar el acceso a un recurso.
- Añadir lógica adicional sin modificar el objeto original.
- Retrasar la creación de un objeto (carga diferida o _lazy loading_).


Spring utiliza proxies para manejar aspectos transversales, como transacciones, seguridad o logging, implementando el patrón **Aspect-Oriented Programming (AOP)**.

- **Proxy dinámico (JDK)**: Implementa interfaces del objeto original.
- **Proxy basado en CGLIB**: Utiliza herencia para crear un proxy cuando no hay interfaces.