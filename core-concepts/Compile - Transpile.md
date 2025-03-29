### **📌 Diferencias entre Transpilar y Compilar** 🚀

Tanto **transpilar** como **compilar** son procesos de transformación de código, pero tienen propósitos distintos.

| **Característica**         | **Compilar**                                                             | **Transpilar**                                                                   |
| -------------------------- | ------------------------------------------------------------------------ | -------------------------------------------------------------------------------- |
| **¿Qué hace?**             | Convierte código de alto nivel a código máquina (ejecutable por la CPU). | Convierte código de un lenguaje a otro similar (ejemplo: ES6 → ES5).             |
| **Ejemplo de entrada**     | C (alto nivel) → Código máquina                                          | JavaScript moderno (ES6) → JavaScript compatible con navegadores antiguos (ES5). |
| **Ejemplo de herramienta** | GCC (para C/C++), Java Compiler (para Java).                             | Babel (para JS), TypeScript Compiler (tsc).                                      |
| **Resultado final**        | Un archivo binario ejecutable.                                           | Código fuente en otro lenguaje o versión.                                        |
| **Ejemplo en JS**          | No aplica (JS no se compila a código máquina directamente).              | Transpilar `const` y `let` a `var` con Babel.                                    |
