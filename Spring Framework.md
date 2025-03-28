Spring Framework (también conocido como Spring) es un marco de trabajo (framework) back-end de código abierto para desarrollar aplicaciones Web y Stand-alone para la plataforma Java, provee soporte para la inyección de dependencia, Web MVC, API Restful, JPA, Hibernate, AOP y más.


---
## Beans/Componentes

En **Spring Framework**, un **bean** es un **objeto** que es **gestionado** y **administrado** por el contenedor de **Spring [[IoC (Inversion of Control)]]. Los beans son instanciados, configurados y ensamblados por el contenedor de Spring, y son los bloques fundamentales de una aplicación basada en Spring.

![[{04DFC425-295E-4F70-8A6D-8767687945D0}.png]]
### **Características Clave de un Bean en Spring**

1. **Gestión del Ciclo de Vida**: Spring es responsable de crear, inicializar, destruir y administrar el ciclo de vida del bean.
2. **Inyección de Dependencias**: Los beans pueden recibir sus dependencias automáticamente a través de [[Patrón de Inyección de Dependencia]], lo que permite un desacoplamiento entre los componentes de la aplicación.
3. **Configuración Declarativa**: Los beans se pueden definir y configurar de manera declarativa mediante anotaciones o archivos de configuración XML.