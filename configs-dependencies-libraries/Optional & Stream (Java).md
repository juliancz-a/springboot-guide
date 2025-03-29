### **1. Stream**

La clase `Stream` permite realizar operaciones sobre secuencias de datos de manera funcional. Se utiliza principalmente para procesar colecciones de manera más declarativa, como filtrar, mapear, ordenar y reducir elementos.

```java
public class StreamExample {
    public static void main(String[] args) {
        List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        // Filtrar números mayores a 5, y luego multiplicarlos por 2
        List<Integer> resultado = numeros.stream()
                                         .filter(n -> n > 5)     
                                         .map(n -> n * 2)         
                                         .collect(Collectors.toList()); 

        // Imprimir el resultado
        System.out.println(resultado);  // [12, 14, 16, 18, 20]
    }
}
```


#### **Métodos Comunes de Stream**

| Método                   | Descripción                                                  |
| ------------------------ | ------------------------------------------------------------ |
| `filter(Predicate)`      | Filtra elementos según una condición.                        |
| `map(Function)`          | Transforma elementos aplicando una función.                  |
| `flatMap(Function)`      | Desanida estructuras de datos, como listas dentro de listas. |
| `forEach(Consumer)`      | Itera sobre cada elemento (operación terminal).              |
| `collect(Collector)`     | Recoge los resultados en una colección, lista, o mapa.       |
| `reduce(BinaryOperator)` | Combina elementos para producir un solo valor.               |
| `sorted(Comparator)`     | Ordena los elementos según un comparador.                    |
| `distinct()`             | Elimina duplicados del flujo.                                |
| `limit(long)`            | Limita el flujo a un número máximo de elementos.             |
| `skip(long)`             | Salta un número determinado de elementos iniciales.          |
| `anyMatch(Predicate)`    | Devuelve `true` si algún elemento cumple la condición.       |
| `allMatch(Predicate)`    | Devuelve `true` si todos los elementos cumplen la condición. |
| `noneMatch(Predicate)`   | Devuelve `true` si ningún elemento cumple la condición.      |
| `count()`                | Devuelve el número de elementos del flujo.                   |
### **Optional**

La clase `Optional` se utiliza para representar un valor que puede estar presente o ausente, lo que ayuda a evitar el uso explícito de `null`. Es muy útil para evitar excepciones de tipo `NullPointerException`. Promueve un manejo más seguro de valores nulos.
```Java
    // Simulando la búsqueda de un cliente por su ID
	    Optional<String> cliente = buscarClientePorId(1);

        // Si el cliente existe, mostrar su nombre; si no, mostrar un mensaje por defecto
        String nombreCliente = cliente.orElse("Cliente no encontrado");
        System.out.println(nombreCliente);  // "Juan Pérez"
        
        // Otra forma de manejar el valor presente
        cliente.ifPresent(nombre -> System.out.println("Cliente encontrado: " + nombre));
    }

    // Método que simula la búsqueda de un cliente en una base de datos
    public static Optional<String> buscarClientePorId(int id) {
        if (id == 1) {
            return Optional.of("Juan Pérez");  // Cliente encontrado
        } else {
            return Optional.empty();  // Cliente no encontrado
        }
    }
}

```


#### **Métodos Comunes de Optional**

| Método                  | Descripción                                                        |
| ----------------------- | ------------------------------------------------------------------ |
| `of(T value)`           | Crea un `Optional` con el valor dado (no permite nulos).           |
| `ofNullable(T value)`   | Crea un `Optional` que puede contener un valor nulo.               |
| `empty()`               | Devuelve una instancia de `Optional` vacía.                        |
| `get()`                 | Devuelve el valor si está presente, lanza excepción si está vacío. |
| `isPresent()`           | Devuelve `true` si contiene un valor.                              |
| `ifPresent(Consumer)`   | Ejecuta una acción si el valor está presente.                      |
| `orElse(T other)`       | Devuelve el valor si está presente, o `other` si no.               |
| `orElseGet(Supplier)`   | Devuelve el valor o genera otro con una función `Supplier`.        |
| `orElseThrow(Supplier)` | Lanza una excepción si el valor no está presente.                  |
| `map(Function)`         | Aplica una función si el valor está presente.                      |
| `flatMap(Function)`     | Similar a `map` pero no envuelve el resultado en otro `Optional`.  |
