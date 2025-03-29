En **Thymeleaf** y **Spring MVC**, las acciones de **`forward`** y **`redirect`** son mecanismos para redirigir la respuesta de una solicitud HTTP a otro recurso. Ambos enfoques tienen diferencias clave en cómo se manejan las solicitudes y las respuestas.

---
### **Forward**

El **`forward`** permite enviar la solicitud a otro controlador o vista dentro del servidor sin realizar una nueva solicitud HTTP. El cliente (navegador) no se da cuenta de la redirección porque la URL no cambia.

`return "forward:/ruta/destino";`
#### **Características del `forward`**:

- No cambia la URL en el navegador.
- Mantiene los datos de la solicitud original. Se mantienen los parametros del request.
- Útil para compartir lógica de negocio sin afectar la navegación del usuario.

---
### **Redirect**

El **`redirect`** envía una respuesta HTTP al navegador indicando que debe hacer una nueva solicitud a otra URL. La URL del navegador se actualiza.

`return "redirect:/ruta/destino";`
#### **Características del `redirect`**:

- Cambia la URL en el navegador.
- Se hace una nueva solicitud HTTP. Se pierden los parametros del request.
- Útil para evitar la repetición de envíos de formularios después de una acción de POST (PRG: **Post/Redirect/Get**).