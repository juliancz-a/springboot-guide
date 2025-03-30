![Pasted image 20250220021115 1.png](../res/Pasted%20image%2020250220021115%201.png)mo funciona OAuth?

1. **Flujo típico (Authorization Code Flow):**
    
    - El usuario intenta acceder a un recurso protegido en una aplicación.
    - La aplicación redirige al usuario a un **servidor de autorización** (por ejemplo, Google, Facebook, etc.).
    - El usuario inicia sesión y autoriza a la aplicación para acceder a sus recursos.
    - El servidor de autorización devuelve un **código de autorización** a la aplicación.
    - La aplicación intercambia el código de autorización por un **token de acceso**.
    - La aplicación utiliza el token de acceso para acceder a los recursos protegidos en nombre del usuario.
        
2. **Roles en OAuth:**
    
    - **Resource Owner**: El usuario que posee los recursos (por ejemplo, tu cuenta de Google).
    - **Client**: La aplicación que quiere acceder a los recursos (por ejemplo, una app de terceros).
    - **Resource Server**: El servidor que aloja los recursos protegidos (por ejemplo, la API de Google Drive).
    - **Authorization Server**: El servidor que emite tokens de acceso después de autenticar al usuario y obtener su consentimiento.
        
3. **Casos de uso comunes:**
    
    - Permitir que una aplicación acceda a tu cuenta de Google Drive.
    - Autorizar a una app de redes sociales para publicar en tu nombre.
    - Integrar servicios de terceros sin compartir credenciales.

### **🔹 Flujos de OAuth 2.1 más utilizados**

| **Flujo**                     | **Uso**                                                  |
| ----------------------------- | -------------------------------------------------------- |
| **Authorization Code + PKCE** | Para aplicaciones frontend y móviles sin backend seguro. |
| **Client Credentials**        | Para comunicación entre servidores sin usuarios.         |
| **Device Code Flow**          | Para dispositivos sin navegador (ejemplo: Smart TVs).    |
Spring Boot maneja OAuth2 a través de **tres roles principales**, cada uno con su propia dependencia:

| **Rol**                         | **Descripción**                                              |
| ------------------------------- | ------------------------------------------------------------ |
| [OAuth2 Authorization Server](OAuth2%20Authorization%20Server.md) | Gestiona la autenticación y emisión de tokens.               |
| [OAuth2 Client](OAuth2%20Client.md)               | Cliente que solicita tokens para acceder a recursos.         |
| [OAuth2 Resource Server](OAuth2%20Resource%20Server.md)      | API protegida que valida tokens y permite acceso a recursos. |
