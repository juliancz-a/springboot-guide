En **Spring**, los **alcances de beans (Bean Scopes)** determinan el **ciclo de vida** y la **visibilidad** de los objetos gestionados por el contenedor IoC. Esto define cuántas instancias de un bean se crean y cómo se utilizan en la aplicación.

Alcance de vida que tiene un componente

---

### **Tipos de Alcances de Beans en Spring**

| **Scope**       | **Descripción**                                                                                                                                         | Anotación         |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- |
| **singleton**   | (Predeterminado) Se crea **una única instancia** del bean por contenedor Spring. Se guarda en la aplicación.                                            |                   |
| **prototype**   | Se crea **una nueva instancia** cada vez que se solicita el bean.                                                                                       |                   |
| **request**     | (Solo aplicaciones web) Una instancia por **solicitud HTTP**. El ciclo de vida es hasta la ejecución de un request.                                     | @RequestScope     |
| **session**     | (Solo aplicaciones web) Una instancia por **sesión de usuario**.                                                                                        | @SessionScope     |
| **application** | (Solo aplicaciones web) Una instancia por **ciclo de vida del servlet context**. Varias aplicaciones desplegadas en Tomcat. Es más amplio que Singleton | @ApplicationScope |
| **websocket**   | (Desde Spring 4.0) Una instancia por **ciclo de vida de la sesión WebSocket**.                                                                          |                   |
