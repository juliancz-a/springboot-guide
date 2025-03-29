## DAO

Las **clases DAO (Data Access Object)** son un patrón de diseño utilizado para proporcionar una abstracción sobre las operaciones de acceso a datos. Su propósito principal es separar la lógica de negocio de la lógica que interactúa directamente con la base de datos, permitiendo un código más limpio, reutilizable y fácil de mantener.

### **Características de las Clases DAO**

1. **Encapsulan el acceso a la base de datos**: Proveen métodos para realizar operaciones como `insert`, `update`, `delete` y `select`.
2. **Abstracción de persistencia**: La lógica para conectarse a la base de datos y ejecutar consultas está contenida en estas clases, sin mezclarla con la lógica de negocio.
3. **Interfaz definida**: Es común definir una interfaz para los DAOs, lo que facilita el uso de diferentes implementaciones.

---
## DTO

Una **clase DTO (Data Transfer Object)** es un patrón de diseño utilizado para transportar datos entre diferentes capas de una aplicación sin exponer directamente las entidades del dominio. Su propósito es mejorar la **seguridad**, **modularidad** y **mantenimiento** del código al separar los datos de la lógica de negocio. Actúa como intermediario, transportando y formateando datos.

### **Características de una Clase DTO**

- Contiene solo **atributos y métodos de acceso (getters y setters)**, sin lógica de negocio.
- Se usa para transferir datos entre el **controlador** y la **capa de servicio**, o entre el **cliente** y el **servidor** en una aplicación web.
- Evita exponer directamente las entidades persistentes (modelos de base de datos), mejorando el control sobre los datos transferidos.

---
## DIFERENCIAS


| **Aspecto**         | **DTO (Data Transfer Object)**                                                                       | **DAO (Data Access Object)**                                                                                            |
| ------------------- | ---------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| **Propósito**       | Transferir datos entre capas de una aplicación (como la capa de servicio y la capa de presentación). | Manejar la lógica de acceso a la base de datos (CRUD: crear, leer, actualizar, eliminar registros).                     |
| **Responsabilidad** | Contiene solo datos, sin lógica de negocio o acceso a base de datos.                                 | Proporciona métodos para interactuar con la base de datos y ejecutar consultas SQL o usar un ORM.                       |
| **Ubicación**       | Se usa principalmente entre el controlador y la capa de servicios, o entre cliente y servidor.       | Se usa en la capa de persistencia, interactuando con la base de datos.                                                  |
| **Contenido**       | Atributos, constructores, getters, y setters para encapsular datos.                                  | Métodos para insertar, actualizar, eliminar y consultar datos.                                                          |
| **Ejemplo**         | `UsuarioDTO` para transportar solo nombre y correo de un usuario.                                    | `UsuarioDAO` con métodos `insertarUsuario()`, `buscarUsuarioPorId()`, etc.                                              |
| **Acoplamiento**    | Ayuda a desacoplar las capas de presentación y negocio al no exponer las entidades directamente.     | Facilita el desacoplamiento de la lógica de negocio con la base de datos al encapsular las operaciones de persistencia. |