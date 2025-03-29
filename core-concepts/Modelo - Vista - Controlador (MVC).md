![](../resources/mvc_diagram.png)


**MVC (Model-View-Controller)** es un patrón de diseño de software ampliamente utilizado en el desarrollo de interfaces de usuario y aplicaciones web. Divide una aplicación en tres componentes interconectados para separar la lógica de la interfaz de usuario, los datos y las reglas de negocio, facilitando el mantenimiento y la escalabilidad del software.

Se lo puede considerar un patrón de arquitectura, pues engloba a varios patrones de diseño.

### **Componentes de MVC**

1. **Modelo (Model)**:
    
    - Representa los datos y la lógica de negocio de la aplicación.
    - Se encarga de la gestión del estado de la aplicación y de interactuar con la base de datos o servicios externos.
    - Utilizan componentes(beans) como @Service, @Repository.
    - Mapeado a tablas de BD.
    - Ejemplo: Una clase que define la estructura de un usuario y contiene métodos para recuperar o actualizar datos.
    
1. **Vista (View)**:
    
    - Es la interfaz de usuario que se muestra al usuario final.
    - Solo se encarga de la presentación de la información.
    - Ejemplo: Una página web o una ventana gráfica que muestra los datos del modelo.


		HTTP REQUEST DEL TIPO POST (lo recibe el controlador):
		
	 ![](../resources/{D7884FF9-D966-402B-B1C1-28E8F9DF67F6}.png)
	 
1. **Controlador (Controller)**:
    
    - Maneja la lógica de interacción del usuario.
    - Responde a las acciones del usuario, actualiza el modelo y selecciona la vista que debe mostrarse.
    - Ejemplo: Una clase que gestiona solicitudes de formularios y realiza las acciones necesarias.

---

### **Flujo de trabajo en MVC**

1. El **usuario** interactúa con la **vista**.
2. La vista envía la solicitud al **controlador**.
3. El controlador procesa la solicitud, actualiza el **modelo** si es necesario, y selecciona una vista para mostrar los resultados.
4. La vista se actualiza con los datos proporcionados por el modelo.

---

### **Ventajas de MVC**

- **Separación de responsabilidades**: Facilita el mantenimiento y la evolución del código.
- **Reutilización de componentes**: Las vistas y los controladores se pueden cambiar sin afectar al modelo.
- **Escalabilidad**: El diseño modular permite agregar nuevas funcionalidades con menos impacto.

---

### **Ejemplos de frameworks MVC**

- **Java**: Spring MVC, JSF
- **JavaScript**: Angular, React (aunque usa un enfoque derivado)
- **Python**: Django
- **PHP**: Laravel, CodeIgniter

MVC es una arquitectura muy adoptada debido a su enfoque estructurado y limpio para organizar aplicaciones complejas, especialmente en el desarrollo web.