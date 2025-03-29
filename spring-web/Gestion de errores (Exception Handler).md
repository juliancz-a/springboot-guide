Cuando desarrollamos aplicaciones con **Spring Boot**, es fundamental manejar los errores de manera adecuada para brindar respuestas claras y estructuradas a los clientes (por ejemplo, aplicaciones front-end o consumidores de una API).

Spring proporciona la anotación `@ExceptionHandler` para capturar y manejar excepciones de manera personalizada. También se puede usar `@ControllerAdvice` para centralizar el manejo de excepciones en toda la aplicación.

#### Manejo básico de excepciones con `@ExceptionHandler`

Si un controlador lanza una excepción, podemos capturarla con `@ExceptionHandler` dentro del mismo controlador.

#### Manejo global de errores con `@RestControllerAdvice`

Para evitar repetir código en cada controlador, podemos centralizar la gestión de excepciones en una clase con `@RestControllerAdvice`.

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UsuarioNoEncontradoException.class)
    public ResponseEntity<String> manejarUsuarioNoEncontrado(UsuarioNoEncontradoException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
    }

    @ExceptionHandler(Exception.class) // Captura cualquier otra excepción no manejada
    public ResponseEntity<String> manejarErroresGenerales(Exception ex) {
        return new ResponseEntity<>("Ocurrió un error inesperado: " + ex.getMessage(), HttpStatus.INTERNAL_SERVER_ERROR);
    }
}

```