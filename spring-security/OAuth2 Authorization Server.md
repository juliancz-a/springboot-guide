
Este es el **servidor de autorización** que gestiona la autenticación y emite **tokens de acceso** a los clientes autorizados.

📌 **Lo que hace esta dependencia:**

- Implementa un **servidor OAuth2** que gestiona flujos de autorización.
- Soporta **OAuth 2.1** y **OpenID Connect 1.0**.
- Emite **tokens de acceso (Access Token)** y **tokens de identificación (ID Token, si usa OIDC)**.

## Clase de configuración: SecurityConfig

Esta configuración define cómo se manejará la autenticación, la autorización y la generación de tokens en la aplicación.

### **1. `authorizationServerSecurityFilterChain`**

Este método configura el **filtro de seguridad** para el servidor de autorización OAuth 2.1 y OpenID Connect.

#### **¿Qué hace este método?**

1. **Configura los endpoints de OAuth2/OIDC**:
    
    - Aplica la configuración solo a los endpoints relacionados con OAuth2 y OpenID Connect (por ejemplo, `/oauth2/authorize`, `/oauth2/token`, etc.).
    - Habilita OpenID Connect 1.0 mediante `.oidc(Customizer.withDefaults())`.
        
2. **Protege los endpoints**:
    
    - Requiere que todas las solicitudes a estos endpoints estén autenticadas (`anyRequest().authenticated()`).
        
3. **Manejo de excepciones**:
    
    - Si un usuario no autenticado intenta acceder a un recurso protegido, se redirige a la página de inicio de sesión (`/login`).


### **2. `defaultSecurityFilterChain`**

Este método configura el **filtro de seguridad por defecto** para el resto de la aplicación (endpoints no relacionados con OAuth2/OIDC).
#### **¿Qué hace este método?**

1. **Protege todos los endpoints**:
    
    - Requiere que todas las solicitudes estén autenticadas (`anyRequest().authenticated()`).
        
2. **Deshabilita CSRF**:
    
    - Desactiva la protección CSRF, lo cual es común en APIs REST donde no se usan formularios HTML.
        
3. **Habilita el formulario de inicio de sesión**:
    
    - Configura un formulario de inicio de sesión por defecto para autenticar usuarios.

### **3. `userDetailsService`**

Este método define un **servicio de detalles de usuario** en memoria para autenticación.

#### **¿Qué hace este método?**

1. **Crea un usuario en memoria**:
    
    - Define un usuario con nombre de usuario `pepe` y contraseña `12345`.
    - La contraseña no está encriptada (`{noop}`).
        
2. **Retorna un `UserDetailsService`**:
    
    - Proporciona un servicio de autenticación basado en usuarios en memoria.

### **4. `registeredClientRepository`**

Este método configura un **repositorio de clientes registrados** para OAuth2.

#### **¿Qué hace este método?**

1. **Registra un cliente OAuth2**:
    
    - Define un cliente con ID `client-id` y clave `password`.
    - Configura los tipos de concesión (`authorization_code` y `refresh_token`).
    - Define las URIs de redirección y los scopes (alcances) que el cliente puede solicitar.
        
2. **Retorna un `RegisteredClientRepository`**:
    
    - Proporciona un repositorio en memoria para almacenar clientes registrados.


### **5. `jwkSource`**

Este método genera y configura una **fuente de claves JSON Web Key (JWK)** para firmar y verificar tokens JWT.

#### **¿Qué hace este método?**

1. **Genera un par de claves RSA**:
    
    - Crea una clave pública y privada para firmar y verificar tokens JWT.
        
2. **Configura una fuente de claves JWK**:
    
    - Retorna una fuente de claves que se usa para firmar tokens JWT.

### **6. `jwtDecoder`**

Este método configura un **decodificador de tokens JWT**.

#### **¿Qué hace este método?**

1. **Crea un decodificador de tokens JWT**:
    
    - Usa la fuente de claves JWK para verificar la firma de los tokens JWT.

### **7. `authorizationServerSettings`**

Este método configura las **propiedades del servidor de autorización**.


### 📌 **Authorization Grant Type y Client Authentication Method

En **OAuth2**, los clientes necesitan una forma de **obtener un token de acceso** para acceder a recursos protegidos.  
Esto se logra a través de diferentes **tipos de concesión (grant types)** y **métodos de autenticación del cliente (client authentication methods)**.

---

## ✅ **1. Authorization Grant Type** (Tipos de concesión de autorización)

Los **grant types** son los **mecanismos utilizados por los clientes** para solicitar un token de acceso desde el **Authorization Server**.

### 📌 **Principales `AuthorizationGrantType` en Spring Security**

|**Grant Type**|**Descripción**|**Ejemplo de uso**|
|---|---|---|
|`AUTHORIZATION_CODE`|Permite a un usuario autenticarse y autorizar a un cliente para acceder en su nombre. **Usa un código temporal y requiere redirección.**|Aplicaciones web y móviles que inician sesión con Google, GitHub, etc.|
|`IMPLICIT` _(Deprecado en OAuth 2.1)_|Similar a `AUTHORIZATION_CODE`, pero sin código intermedio (inseguro).|No recomendado en OAuth 2.1|
|`PASSWORD` _(Deprecado en OAuth 2.1)_|Permite que un cliente use directamente las credenciales del usuario para obtener un token.|Aplicaciones que necesitan autenticarse con usuario/contraseña.|
|`CLIENT_CREDENTIALS`|Permite que un cliente se autentique **sin usuario**, solo con su `client_id` y `client_secret`.|Servicios backend y microservicios.|
|`REFRESH_TOKEN`|Permite a un cliente obtener un nuevo token de acceso sin que el usuario vuelva a autenticarse.|Aplicaciones que necesitan mantener sesiones largas.|
- **`AUTHORIZATION_CODE`** → El cliente obtiene un código de autorización antes de recibir un token.
- **`REFRESH_TOKEN`** → Permite renovar tokens sin que el usuario vuelva a autenticarse.


## ✅ **2. Client Authentication Method** (Métodos de autenticación del cliente)

Los **métodos de autenticación del cliente** determinan **cómo el cliente se autentica ante el Authorization Server** cuando solicita un token.

### 📌 **Principales `ClientAuthenticationMethod` en Spring Security**

| **Método**            | **Descripción**                                                                                        | **Ejemplo de uso**                                     |
| --------------------- | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------ |
| `CLIENT_SECRET_BASIC` | El cliente envía `client_id` y `client_secret` en el **encabezado HTTP Authorization** con Basic Auth. | Autenticación segura con credenciales en el header.    |
| `CLIENT_SECRET_POST`  | El cliente envía `client_id` y `client_secret` en el **cuerpo de la solicitud HTTP POST**.             | Autenticación menos segura, pero a veces necesaria.    |
| `CLIENT_SECRET_JWT`   | El cliente usa un **JWT firmado** con su secreto para autenticarse.                                    | Microservicios y API que requieren mayor seguridad.    |
| `PRIVATE_KEY_JWT`     | Similar a `CLIENT_SECRET_JWT`, pero usa una **clave privada** en lugar de un secreto compartido.       | Aplicaciones que usan certificados para autenticarse.  |
| `NONE`                | No se requiere autenticación del cliente.                                                              | Flujos públicos, como apps móviles sin backend seguro. |