Los **interceptores HTTP** en aplicaciones web son componentes que permiten interceptar y modificar solicitudes y respuestas HTTP antes de que lleguen al controlador o después de haber salido del controlador. Son una forma poderosa de manejar aspectos transversales, como autenticación, registro de eventos o manipulación de datos, en aplicaciones web basadas en **Spring** o **otros frameworks HTTP**.

---

### **Interceptores en Spring Framework**

En **Spring**, los interceptores se utilizan para procesar solicitudes entrantes y respuestas salientes. Se implementan mediante la interfaz `HandlerInterceptor` o la clase abstracta `HandlerInterceptorAdapter` (antes de Spring 5). También pueden ser definidos como **filtros** para tareas más generales.


![[../resources/{F1095BA1-964B-454F-8E43-D66BEE26B008} 1.png]]

![[../resources/{49C101F5-BE4C-4ADB-84F2-C66C0DF52804} 1.png]]

### **Interfaz `HandlerInterceptor`**

Contiene los siguientes métodos:

1. `preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)`  
    Se ejecuta **antes** de que la solicitud llegue al controlador. Puede usarse para:
    
    - Autenticación y autorización.
    - Validación de datos de la solicitud.
2. `postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView)`  
    Se ejecuta **después** de que el controlador procese la solicitud, pero **antes** de que la respuesta sea generada. Puede usarse para:
    
    - Modificar datos de respuesta antes de que se renderice la vista.
3. `afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex)`  
    Se ejecuta **después de que la respuesta ha sido enviada al cliente**. Ideal para:
    
    - Registro de actividad.
    - Manejo de excepciones no controladas.



### **Pasos para Registrar un Interceptor**

1. Crea una clase que implemente `HandlerInterceptor` o extiende de `HandlerInterceptorAdapter` (antes de Spring 5).
2. Implementa los métodos del interceptor: `preHandle`, `postHandle`, y/o `afterCompletion`.
3. Registra el interceptor en una clase de configuración que implemente `WebMvcConfigurer` y sobrescribir el método `addInterceptors`.

#### Método addInterceptors

Utilizar el parametro registry de tipo InterceptorRegistry que tiene el método **addInterceptor**.

**addInterceptor** devuelve un objeto del tipo InterceptorRegistration, que nos permite utilizar los siguientes métodos:

- **addPathPatterns**: Especifica las rutas donde el interceptor se aplicará.
- **excludePathPatterns**: Define rutas que el interceptor debe omitir.

