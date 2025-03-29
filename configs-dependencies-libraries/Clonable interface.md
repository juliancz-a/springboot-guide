
La **interfaz `Cloneable`** en Java es parte del paquete `java.lang` y permite a las clases que la implementan definir cómo sus objetos pueden ser **clonados**. Su propósito es crear copias exactas de objetos mediante el método `clone()`.

---

### **Características de la Interfaz Cloneable**

- No contiene métodos abstractos, sino que actúa como una **marca** que habilita el método `clone()` del objeto.
- La implementación correcta de `Cloneable` requiere sobreescribir el método `clone()` de la clase `Object`.
- Si una clase implementa `Cloneable` pero no sobrescribe `clone()`, se lanzará una excepción `CloneNotSupportedException`.