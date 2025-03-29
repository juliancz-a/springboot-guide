La **Inversión de Control (IoC, Inversion of Control)** es un principio de diseño utilizado en la programación orientada a objetos, donde el control del flujo del programa y la creación de dependencias se delegan a un contenedor o framework en lugar de ser gestionados manualmente por el código de la aplicación. Este enfoque permite que los componentes del sistema sean **menos acoplados**, lo que facilita su reutilización, prueba y mantenimiento.

---

### **Conceptos Clave de IoC**

1. **Inyección de Dependencias (Dependency Injection)**: Es la técnica más común para implementar IoC. Las dependencias de un objeto se proporcionan desde el exterior (generalmente por el contenedor IoC), en lugar de que el objeto las cree por sí mismo.
    
2. **Contenedor IoC**: Es un componente que gestiona la creación de objetos y sus dependencias. En el contexto de **Spring Framework**, el contenedor IoC se encarga de gestionar los beans definidos en la aplicación.