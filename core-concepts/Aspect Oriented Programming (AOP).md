
La **Programación Orientada a Aspectos (POA)** es un paradigma de programación que busca separar las preocupaciones transversales (cross-cutting concerns) del código principal de una aplicación. Estas preocupaciones transversales son funcionalidades que afectan a múltiples partes de un sistema, como la gestión de logs, la seguridad, la transaccionalidad, la sincronización, la gestión de errores, entre otros.

### Objetivo principal:

La POA permite modularizar estas preocupaciones transversales en unidades llamadas **aspectos**, evitando que se mezclen con la lógica principal del programa. Esto mejora la **modularidad**, la **reusabilidad** y la **mantenibilidad** del código.

#### 🛠️ **Conceptos Claves de POA**

1. **Aspectos (Aspects)**  
    Un módulo que encapsula una preocupación transversal. Contiene **puntos de corte**(pointcuts) y **consejos** (advices).
    
2. **Enlaces (Join Points)**  
    Son los lugares específicos en el código donde se pueden aplicar los aspectos, como la ejecución de un método.

    
3. **Consejos (Advices)**  
    Es el código que se ejecuta en los puntos de corte. Puede ejecutarse antes (**before**), después (**after**) o alrededor (**around**) de la ejecución del punto de corte.

	After returning -> luego de retorno
	After throwing -> luego de lanzar una excepción
	After (finally) -> luego del metodo sin importar si retorna o lanza excepción

    
4. **Puntos de Corte (Pointcuts)**  
    Define los puntos específicos en la ejecución del programa donde se aplicará el aspecto (por ejemplo, la llamada a un método o la ejecución de una función).

Ej:
    ![[../resources/{6DE22BB3-8F38-4A82-954C-19832543B2E6} 1.png]]
	Se aplica a cualquier package de la app -> ..
	Se aplica a cualquier clase, y método -> *
	Los argumentos son desconocidos -> (..)

	 
1. **Inyección de Aspectos (Weaving)**  
    Es el proceso de integrar los aspectos con el código principal. Puede realizarse en tiempo de compilación, carga o ejecución.

### Ventajas de la POA:

- **Separación de preocupaciones**: El código principal se mantiene limpio y enfocado en su funcionalidad principal.
    
- **Reusabilidad**: Los aspectos pueden reutilizarse en diferentes partes del sistema o en otros proyectos.
    
- **Mantenibilidad**: Cambiar una preocupación transversal (como el logging) solo requiere modificar el aspecto, no todo el código.
    

### Desventajas de la POA:

- **Complejidad**: Introducir aspectos puede aumentar la complejidad del sistema, especialmente en la depuración.
    
- **Herramientas limitadas**: No todos los lenguajes de programación tienen soporte nativo para POA, aunque existen frameworks como **AspectJ** para Java o **PostSharp** para .NET.

## Anotaciones principales:

  - **@Before**: Ejecuta antes del join point.
  - **@After**: Ejecuta después del join point.
  - **@AfterReturning**: Ejecuta después de un retorno exitoso.
  - **@AfterThrowing**: Ejecuta después de una excepción.
  - **@Around**: Rodea el join point.
  - **@Order**: Define el orden de ejecución de los aspectos.
  - **@Pointcut**: Define un punto de corte reusable.

--- 
# 📍JOIN POINTS

El concepto de **JoinPoint** es fundamental en POA porque permite identificar los lugares exactos en los que un aspecto puede intervenir para agregar comportamiento adicional (como logging, seguridad, transacciones, etc.).
### Características de un JoinPoint:

2. **Representa un evento en la ejecución del programa**:
    
    - Llamada a un método (`method call`).
    - Ejecución de un método (`method execution`).
    - Inicialización de un objeto (`constructor call`).
    - Acceso a un atributo (`field access`).
    - Lanzamiento de una excepción (`exception handling`).
        
3. **Proporciona información contextual**:
    
    - Un `JoinPoint` contiene detalles sobre el punto de ejecución, como el método que se está ejecutando, los argumentos pasados, el objeto objetivo, etc.
        
4. **Es interceptado por un aspecto**:
    
    - Los aspectos usan **pointcuts** para seleccionar `JoinPoints` y aplicar **advices** (consejos) en esos puntos.
        

---
### Métodos comunes de JoinPoint:

En frameworks como **AspectJ**, el objeto `JoinPoint` proporciona métodos útiles para obtener información sobre el punto de ejecución:

- **`getSignature()`**: Devuelve la firma del método o constructor interceptado.
- **`getArgs()`**: Devuelve los argumentos pasados al método o constructor.
- **`getTarget()`**: Devuelve el objeto objetivo (la instancia de la clase donde se ejecuta el método).
- **`getThis()`**: Devuelve el objeto proxy (en caso de que se use AOP con proxies).
- **`toString()`**: Devuelve una representación en cadena del `JoinPoint`.
---
### Diferencia entre JoinPoint y Pointcut:

- **JoinPoint**: Es un punto específico en la ejecución del programa (por ejemplo, la ejecución de un método).
    
- **Pointcut**: Es una expresión que selecciona uno o varios `JoinPoints` donde se aplicará un aspecto. Por ejemplo, `execution(* MiClase.*(..))` es un pointcut que selecciona todos los métodos de la clase `MiClase`.

## Proceeding Join Point

Un **Proceeding Join Point** es una subclase de `JoinPoint` utilizada en aspectos con el tipo de consejo (**Advice**) **@Around**. Permite no solo obtener información sobre el Join Point, sino también **controlar su ejecución**.

Con **ProceedingJoinPoint**, puedes:

- **Ejecutar o evitar** la ejecución del método original.
- **Modificar el valor de retorno**.
- **Manejar excepciones** antes de que sean propagadas.

![[../resources/{EF00D2CC-AAF7-40C3-A0D8-3DBFBB617F66} 1.png]]