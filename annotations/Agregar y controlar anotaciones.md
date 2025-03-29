Las anotaciones en Java se utilizan para agregar metadatos a clases, métodos, campos y otros elementos del código. Para controlar el **alcance y uso** de una anotación, se utilizan las anotaciones **@Retention** y **@Target**.

## **🔹 @Retention y RetentionPolicy**

📌 La anotación `@Retention` define **cuánto tiempo** estará disponible una anotación en el código.  
📌 Se usa junto con `RetentionPolicy`, que puede tomar tres valores:

| **RetentionPolicy** | **Descripción**                                                                                                                                            |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`SOURCE`**        | La anotación **se elimina** en la fase de compilación y no estará en el bytecode. Se usa para herramientas como **Lombok**.                                |
| **`CLASS`**         | La anotación **se mantiene** en el bytecode, pero **no está disponible en tiempo de ejecución**. Es el valor **por defecto**.                              |
| **`RUNTIME`**       | La anotación **se mantiene** en el bytecode **y está disponible en tiempo de ejecución**. Se usa para **Reflection y frameworks como Spring o Hibernate**. |

## **🔹 @Target**

📌 La anotación `@Target` **especifica en qué elementos del código puede aplicarse una anotación**.  
📌 Se usa junto con `ElementType`, que define los posibles objetivos:

| **ElementType**       | **Se aplica a...**          |
| --------------------- | --------------------------- |
| **`TYPE`**            | Clases, interfaces y enums. |
| **`METHOD`**          | Métodos.                    |
| **`FIELD`**           | Atributos de clase.         |
| **`PARAMETER`**       | Parámetros de métodos.      |
| **`CONSTRUCTOR`**     | Constructores.              |
| **`LOCAL_VARIABLE`**  | Variables locales.          |
| **`ANNOTATION_TYPE`** | Otras anotaciones.          |
| **`PACKAGE`**         | Paquetes.                   |


## Crear validaciones personalizadas

En **Jakarta Validation**, la anotación `@Constraint` se usa para **crear validaciones personalizadas**, y su propiedad `validatedBy` especifica la clase que implementará la lógica de validación.

---

## **1️⃣ @Constraint**

📌 `@Constraint` indica que una anotación es una **restricción de validación personalizada**.

📌 Se usa junto con `validatedBy`, que apunta a una **clase validadora** que implementa la lógica de validación.

---
## **2️⃣ `validatedBy`**

📌 Define la **clase validadora**, la cual debe implementar `ConstraintValidator<A, T>`.

- `A`: La anotación de la validación.
- `T`: El tipo de dato que se validará.