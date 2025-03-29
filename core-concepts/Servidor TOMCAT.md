
**Tomcat** es un servidor de aplicaciones de código abierto. Está diseñado para ejecutar aplicaciones web basadas en **Java** y es ampliamente utilizado para servir páginas web dinámicas que utilizan tecnologías como **Java Servlets**, **JavaServer Pages (JSP)**, y **WebSockets**.

### Características principales:

- **Servidor de Servlets**: Implementa las especificaciones de Servlets de Java.
- **Soporte para JSP**: Permite servir páginas JSP que generan contenido dinámico.
- **WebSockets**: Admite conexiones WebSockets para aplicaciones en tiempo real.
- **Gestión de sesiones**: Maneja sesiones de usuario para aplicaciones web.
- **Escalabilidad**: Puede integrarse con otros servidores web como Apache HTTP Server para manejar grandes volúmenes de tráfico.

### Uso común:

- Despliegue de aplicaciones web Java empresariales.
- Pruebas de desarrollo local para aplicaciones web.
- Proyectos que requieren contenedores ligeros y configurables.

Tomcat no es un servidor de aplicaciones completo como **JBoss** o **GlassFish**, ya que no implementa completamente la especificación **Java EE** (ahora Jakarta EE), pero es suficiente para muchas aplicaciones web estándar.

# Tecnologías donde TOMCAT actúa como contenedor:

### **Java Servlets**

Un **Servlet** es una clase de Java que se ejecuta en un servidor web para manejar solicitudes HTTP y generar respuestas dinámicas. Los servlets son una parte fundamental de las aplicaciones web Java y permiten construir contenido dinámico (como HTML o JSON) basado en las entradas del usuario.

- **Funcionalidad**: Procesa solicitudes GET o POST.
- **Ciclo de vida**: Incluye métodos como `init()`, `service()`, y `destroy()`.
- **Ejemplo de uso**: Un servlet puede manejar un formulario de inicio de sesión y verificar las credenciales del usuario.

---

### **JSP (JavaServer Pages)**

**JSP (JavaServer Pages)** es una tecnología que permite a los desarrolladores crear contenido dinámico en páginas web usando una combinación de HTML, CSS y código Java embebido. Se compilan en servlets por detrás.

- **Uso principal**: Crear vistas dinámicas en aplicaciones web.
- **Sintaxis**: Usa expresiones y directivas de Java (`<% %>`) para incrustar lógica.
- **Ventaja**: Separa la presentación de la lógica de negocio, facilitando el mantenimiento del código.

---

### **WebSockets**

**WebSockets** es una tecnología que permite una comunicación bidireccional y persistente entre un cliente (como un navegador) y un servidor. A diferencia de HTTP, que es de naturaleza de solicitud-respuesta, los WebSockets permiten enviar y recibir datos continuamente después de establecer una conexión inicial.

- **Funcionalidad clave**: Permite actualizaciones en tiempo real (sin necesidad de nuevas solicitudes HTTP).
- **Uso común**: Aplicaciones de chat, paneles en tiempo real, juegos en línea.
- **Soporte en Java**: Java EE incluye una API de WebSockets que se puede usar en Tomcat.

**Ejemplo de uso**: Un servidor WebSocket puede enviar actualizaciones a todos los clientes conectados sobre los cambios en una tabla de precios sin que los clientes realicen una solicitud.