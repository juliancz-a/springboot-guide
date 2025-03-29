Cuando se maneja una solicitud HTTP, [Spring MVC](../core-concepts/Spring%20MVC.md) o Java Servlets proporcionan una instancia de `HttpServletRequest` al controlador o servlet para que pueda acceder a la información de la solicitud. Otra manera de obtener información es con @RequestParams como anotación propia de Spring MVC.

---

### **Métodos Comunes de `HttpServletRequest`**

| Método                                | Descripción                                                              |
| ------------------------------------- | ------------------------------------------------------------------------ |
| `getParameter(String name)`           | Devuelve el valor del parámetro de solicitud con el nombre especificado. |
| `getParameterMap()`                   | Devuelve un mapa de todos los parámetros de la solicitud.                |
| `getHeader(String name)`              | Obtiene el valor de un encabezado HTTP específico.                       |
| `getSession()`                        | Devuelve la sesión actual o crea una nueva si no existe.                 |
| `getRequestURL()`                     | Devuelve la URL completa de la solicitud.                                |
| `getRequestURI()`                     | Devuelve la URI de la solicitud.                                         |
| `getMethod()`                         | Devuelve el método HTTP usado (GET, POST, PUT, DELETE, etc.).            |
| `getCookies()`                        | Devuelve un array de cookies enviadas con la solicitud.                  |
| `getAttribute(String name)`           | Obtiene un atributo de la solicitud.                                     |
| `setAttribute(String name, Object o)` | Establece un atributo de la solicitud.                                   |
| `getRemoteAddr()`                     | Devuelve la dirección IP del cliente que hizo la solicitud.              |