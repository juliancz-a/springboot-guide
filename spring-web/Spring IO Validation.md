
Spring Boot utiliza **Java Bean Validation (Jakarta Validation, antes javax.validation)** para validar datos en DTOs, servicios y controladores.

---

## 📌 1. Anotaciones Básicas de Validación
### **🔹 `@NotNull`**

✔️ **Asegura que un campo no sea `null`, pero puede estar vacío.**  
🚫 No se aplica a tipos primitivos (`int`, `double`, etc.).
### **🔹 `@NotEmpty`**
✔️ **El campo no puede ser `null` ni vacío (`""`).**  
🚫 No se aplica a tipos numéricos.

### **🔹 `@NotBlank`**

✔️ **No puede ser `null`, vacío ni contener solo espacios en blanco.**  
🚫 Solo se aplica a `String`.

### **🔹 `@Size(min, max)`**

✔️ **Valida la longitud de cadenas o colecciones.**  
🚫 No funciona con tipos numéricos (`int`, `double`).

### **🔹 `@Min` y `@Max`**

✔️ **Define valores mínimos y máximos para números.**  
🚫 Solo funciona con tipos numéricos (`int`, `long`, `double`, etc.).

### **🔹 `@Email`**

✔️ **Valida que un campo tenga formato de email válido.**  
🚫 Solo funciona con `String`.

### **🔹 `@Pattern(regexp)`**

✔️ **Valida un campo con una expresión regular.**

## **📌 2. Validación en Controladores con `@Valid` y `BindingResult`**

Para aplicar estas validaciones en Spring Boot, usamos `@Valid` en los métodos del controlador.

```Java
@RestController
@RequestMapping("/users")
public class UserController {

    @PostMapping("/create")
    public ResponseEntity<?> createUser(@Valid @RequestBody UserDTO user, BindingResult result) {
        if (result.hasErrors()) {
            Map<String, String> errors = new HashMap<>();
            result.getFieldErrors().forEach(error ->
                errors.put(error.getField(), error.getDefaultMessage()));
            return ResponseEntity.badRequest().body(errors);
        }
        return ResponseEntity.ok("Usuario creado correctamente");
    }
}
```

- `@Valid` → Activa la validación de `UserDTO`.
- `BindingResult` → Captura los errores de validación y los devuelve como respuesta.
## **📌 3. Validación en Servicios con `@Validated
`**
Para validar parámetros de métodos dentro de los servicios, usamos `@Validated`.

```Java
@Service
@Validated
public class UserService {

    public void registerUser(@NotBlank String username, @Min(18) int age) {
        System.out.println("Usuario registrado: " + username);
    }
}
```

- `@Validated` en la clase permite que se apliquen validaciones en parámetros de métodos.

## **📌 4. Manejo Global de Errores con `@ControllerAdvice`**

Para capturar los errores de validación y devolver una respuesta más clara, usamos `@RestControllerAdvice`.


- `@RestControllerAdvice` → Se encarga de capturar excepciones globalmente.
- `@ExceptionHandler(MethodArgumentNotValidException.class)` → Captura los errores de validación de `@Valid`.

--- 
✅ **`@Valid` en DTOs** para validar automáticamente en controladores.  
✅ **`@Validated` en servicios** para validar parámetros en métodos.  
✅ **`@ControllerAdvice`** para manejar errores globalmente.