
### **Spring Web**: 

Proporciona las herramientas para construir aplicaciones web, incluyendo soporte para MVC (Model-View-Controller) y APIs REST.

### **Spring DevTools**: 

Mejora la experiencia de desarrollo con características como reinicios automáticos y recarga de plantillas.

### **Thymeleaf**: 

Un motor de plantillas para generar vistas dinámicas en aplicaciones web, integrándose fácilmente con Spring MVC.

**Compatibilidad con HTML y XML:** Thymeleaf está diseñado para generar **HTML válido**. Puedes trabajar directamente con plantillas HTML, lo que facilita el desarrollo de vistas sin preocuparte por la sintaxis específica del motor de plantillas. Esto lo hace muy conveniente en comparación con otros motores que requieren un formato de plantilla distinto.
	    
**Procesamiento en el servidor:** Thymeleaf procesa las plantillas en el lado del servidor antes de enviarlas al cliente. El motor reemplaza las etiquetas dinámicas de la plantilla con datos del modelo proporcionado por el controlador, y luego genera un HTML final que se envía al navegador.
	    
**Sintaxis similar a HTML:** Thymeleaf utiliza una sintaxis que es **muy similar a HTML**. Esto permite que los archivos de plantilla puedan ser editados fácilmente por diseñadores sin tener que aprender un nuevo lenguaje o sintaxis, lo que lo convierte en una opción ideal para aplicaciones donde los diseñadores de frontend y desarrolladores de backend colaboran.
			
	    
**Lógica en plantillas:** Thymeleaf soporta el uso de estructuras de control como bucles, condiciones y expresiones lógicas dentro de las plantillas. Esto permite generar contenido dinámico basándose en la lógica de negocio. Accede a atributos de objetos utilizando los getter de manera interna.
			-Variables/Objetos => th:text="${object}"
			-Estructuras de control => th:if / th:each
			-Enlaces =>  th:href = @{}
	    
**Internacionalización:** Thymeleaf facilita la **internacionalización** y la creación de aplicaciones multilingües mediante el uso de archivos de propiedades, lo que facilita la localización del contenido en diferentes idiomas.
	    
**Integración con Spring:** Thymeleaf se integra de manera fluida con **Spring Boot** y **Spring MVC**. Usando **Spring MVC**, Thymeleaf puede ser configurado como el motor de plantillas para renderizar vistas a partir de los controladores. Esto hace que sea fácil crear aplicaciones web basadas en **Modelo-Vista-Controlador (MVC)**.

### Actuator:

En **Spring Boot**, la dependencia **Actuator** proporciona funcionalidades para monitorear y gestionar aplicaciones en producción. Incluye varios puntos finales (endpoints) que ofrecen métricas, información de la aplicación, y datos operativos sobre la salud de la aplicación.

### **Características de Actuator**

- **Monitoreo de Salud** (`/actuator/health`): Indica si la aplicación está funcionando.
- **Métricas** (`/actuator/metrics`): Proporciona métricas sobre la memoria, el uso de CPU, y otros recursos.
- **Información de la Aplicación** (`/actuator/info`): Muestra información personalizada definida por el desarrollador.
- **Configuraciones y Propiedades**: Permite consultar el estado de las propiedades y beans de la aplicación.