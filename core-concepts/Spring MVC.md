Parte del ecosistema de Spring Framework.

Es un framework web basado en [Modelo - Vista - Controlador (MVC)](<Modelo - Vista - Controlador (MVC).md>), que toma ventajas de los siguientes principios:

1. [Modelo - Vista - Controlador (MVC)](<Modelo - Vista - Controlador (MVC).md>)
2. [Patrón de Inyección de Dependencia](<Patrón de Inyección de Dependencia.md>)
3. Orientación al uso de interfaces
4. Uso de clases [POJO](POJO.md)

## Front Controller
El **Front Controller** es un componente central que se encarga de recibir todas las solicitudes HTTP de una aplicación web. En **Spring MVC**, el Front Controller está representado por la clase `DispatcherServlet`.

#### **Funciones del DispatcherServlet**

1. **Recibir las solicitudes HTTP**: Todas las solicitudes pasan primero por el `DispatcherServlet`.
2. **Delegar la solicitud al controlador adecuado**: Usa un mapeo de URL para encontrar el controlador que debe manejar la solicitud. (Handler mapping). @RequestMapping, @GetMapping, @PostMapping, entre otros mapeos.
3. **Procesar la lógica de negocio**: El controlador llama a los servicios y repositorios para procesar la solicitud. Envia datos a la vista usando el objeto Model (Map, Model, etc)
4. **Seleccionar la vista**: El controlador devuelve un nombre de vista, y el `DispatcherServlet` usa un `ViewResolver` para resolver la vista adecuada. HTML (Thymeleaf)
5. **Enviar la respuesta**: La vista generada se envía de vuelta al cliente como una respuesta HTTP, utilizando los datos del Model Object.

---

#### **Diagrama del Flujo de Trabajo**

1. El cliente realiza una solicitud HTTP (`GET`, `POST`, etc.).
2. La solicitud es interceptada por el `DispatcherServlet`.
3. El `HandlerMapping` determina qué controlador debe manejar la solicitud.
4. El controlador procesa la solicitud y llama a la capa de servicio.
5. Se devuelve un modelo y un nombre de vista al `DispatcherServlet`.
6. El `ViewResolver` resuelve el nombre de la vista a un archivo (por ejemplo, una plantilla HTML o JSP).
7. Se genera la respuesta y se envía al cliente.}


## Separación clara en funciones:


- **Controller**:  
    Es responsable de manejar las solicitudes HTTP entrantes, procesar datos, interactuar con la lógica de negocio y devolver una vista para la respuesta. Se define con la anotación `@Controller` o `@RestController` para servicios REST.
    
- **Validadores**:  
    Se utilizan para validar los datos de entrada del formulario antes de procesarlos. Se implementan utilizando la interfaz `Validator` o con anotaciones como `@Valid` y `@NotNull` de **Bean Validation** (JSR 380).
    
- **Object Form (Form-backing Object)**:  
    Es un objeto Java que actúa como modelo para vincular los datos del formulario web con los atributos del objeto en el controlador. Los datos del formulario se asignan automáticamente a este objeto. Es bidireccional, mapeado a los objetos de la tabla como a los campos del form.
    
- **DispatcherServlet**:  
    Es el **Front Controller** de Spring MVC. Gestiona todas las solicitudes HTTP, las delega a los controladores apropiados, maneja las respuestas y resuelve las vistas.
    
- **HandlerMapping**:  
    Se encarga de encontrar el controlador correspondiente para manejar una solicitud específica. Usa configuraciones basadas en anotaciones (`@RequestMapping`) o en archivos XML.
    
- **ViewResolver**:  
    Determina qué vista se debe renderizar para una respuesta, a partir de un nombre de vista devuelto por el controlador. Resuelve plantillas de vistas como **Thymeleaf**, **JSP**, o **FreeMarker**.