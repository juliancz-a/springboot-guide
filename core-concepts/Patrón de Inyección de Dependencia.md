El **patrón de Inyección de Dependencia (DI, por sus siglas en inglés Dependency Injection)** es un patrón de diseño estructural que permite la **desacoplar** las clases y sus dependencias. En lugar de que una clase cree y gestione sus propias dependencias (como objetos de otras clases que necesita para funcionar), estas dependencias se **inyectan** en la clase desde el exterior, generalmente a través de un contenedor o framework de inyección de dependencias.

### **Objetivo**

El objetivo principal de la Inyección de Dependencia es **reducir el acoplamiento** entre clases, facilitando la modularidad, la reutilización del código y la capacidad de prueba de la aplicación. Esto se logra al permitir que las dependencias de una clase sean proporcionadas externamente, lo que simplifica la creación y la gestión de objetos.

### **Cómo funciona la Inyección de Dependencia**

- **Clase A** necesita una instancia de **Clase B** para realizar su tarea.
- En vez de crear una instancia de **Clase B** dentro de **Clase A**, **Clase B** es inyectada en **Clase A**.
- El framework o contenedor de DI (como **Spring** en Java) se encarga de proporcionar las instancias de las dependencias necesarias. Ambos objetos deben estar manejados por este.
- El contenedor maneja la creación de los objetos. Se debe tener un constructor sin parametros, ya que el contenedor los crea de manera implicita, en favor de la inyección de dependencia, todo de manera automatica. -> @Autowired

### **Tipos de Inyección de Dependencia**

1. **Inyección por Constructor (Constructor Injection)**
    
    - Las dependencias se proporcionan a través del constructor de la clase.
    - Se usa comúnmente en muchos frameworks como Spring.

2. **Inyección por Setter (Setter Injection)**

	- Las dependencias se proporcionan a través de métodos setter (mutadores).
	- Se usa cuando las dependencias pueden cambiar después de la construcción del objeto.

3. **Inyección por Interfaz (Interface Injection)**

	- La clase proporciona un método para que la dependencia sea inyectada, pero esta técnica es menos común y no es soportada nativamente por muchos frameworks.
	- La clase necesita exponer un método para recibir la dependencia
### **Ventajas de la Inyección de Dependencia**

1. **Desacoplamiento**: Las clases no necesitan saber cómo crear o gestionar las instancias de sus dependencias. Esto facilita la reutilización y el mantenimiento del código.
2. **Facilidad de pruebas (Testabilidad)**: La inyección de dependencias permite pasar dependencias "simuladas" o **mock** en las pruebas unitarias, mejorando la capacidad de prueba.
3. **Flexibilidad y Configuración**: La configuración de las dependencias se puede hacer externamente (por ejemplo, a través de un contenedor de DI), lo que facilita cambiar la implementación de una clase sin afectar a las clases que dependen de ella.
4. **Centralización de la gestión de dependencias**: Utilizando un contenedor de dependencias (como **Spring IoC container**), puedes gestionar todas las instancias de objetos de manera centralizada.

### **Ejemplo en Spring Framework**

En **Spring**, el contenedor de **Inversión de Control (IoC)** se encarga de gestionar las dependencias e inyectarlas automáticamente. (MODEL).
Maneja por debajo un patron llamado Service Locator.

**Configuración de Spring:**

- Spring se encarga de crear instancias de **Servicio** y **Repositorio**, inyectando **Repositorio** dentro de **Servicio**.
- Usando anotaciones como `@Service`, `@Repository` y `@Autowired`, Spring automáticamente gestionará las dependencias sin necesidad de que el desarrollador las configure explícitamente.

## Principio Hollywood
Su lema es:  **"No nos llames, nosotros te llamaremos."**
### **Explicación del Principio**

Este principio sugiere que, en lugar de que las clases dependientes controlen el flujo de ejecución llamando directamente a sus dependencias, es un **contenedor o marco de trabajo** (framework) el que se encarga de la gestión de las instancias y la ejecución de sus métodos.

--- 
![[../res/spring-w.png]]

@Controller
@Service
@Repository o DAO 
Son todos @Component de Spring que utilizan **estereotipos**
Todos manejados por el contenedor.