## 🔐 **UserDetailsService Implementation**

En **Spring Security**, `UserDetails` y `UserDetailsService`son interfaces clave para la autenticación y autorización de usuarios. 

### 0. **Clase `User`

En **Spring Security**, la clase `User` es una implementación lista para usar de la interfaz `UserDetails`.

📌 En lugar de crear nuestra propia clase personalizada de `UserDetails`, podemos usar directamente `User`, que ya proporciona todo lo necesario para la autenticación.

La clase `User` tiene un constructor que permite definir:

- **Nombre de usuario** (`username`)
- **Contraseña** (`password`)
- **Si la cuenta está habilitada o no**
- **Si la cuenta está expirada o no**
- **Si las credenciales están expiradas o no**
- **Si la cuenta está bloqueada o no**
- **Lista de roles o permisos** (`GrantedAuthority`)

#### 1. **`UserDetails`**

Esta es una interfaz que representa a un usuario dentro de Spring Security. Define los métodos que Spring Security necesita para verificar credenciales, roles y estados del usuario.

**Métodos principales de `UserDetails`:**

- `getUsername()`: Devuelve el nombre de usuario.
- `getPassword()`: Devuelve la contraseña (generalmente encriptada).
- `getAuthorities()`: Devuelve los roles o permisos del usuario.
- `isAccountNonExpired()`: Indica si la cuenta ha expirado.
- `isAccountNonLocked()`: Indica si la cuenta está bloqueada.
- `isCredentialsNonExpired()`: Indica si las credenciales han expirado.
- `isEnabled()`: Indica si la cuenta está activa.

### 2. **`UserDetailsService`**

Esta interfaz es utilizada por Spring Security para obtener detalles del usuario desde una fuente de datos (como una base de datos).  
Solo tiene un método:

```java
UserDetails loadUserByUsername(String username) throws UsernameNotFoundException;
```

Este método se encarga de buscar al usuario y devolver un objeto `UserDetails`.

### 3.**`GrantedAuthority`**

`GrantedAuthority` es una interfaz en **Spring Security** que representa un permiso o rol de usuario. Se usa en la autenticación y autorización para determinar qué acciones puede realizar un usuario en el sistema.

###### **Implementaciones Comunes**

####### **📌 `SimpleGrantedAuthority` (Implementación por defecto)**

La forma más común de usar `GrantedAuthority` es con la clase `SimpleGrantedAuthority`, que simplemente almacena un String como autoridad.
```Java
GrantedAuthority roleAdmin = new SimpleGrantedAuthority("ROLE_ADMIN");
```

---
### **Spring Security: Autenticación con Username y Password** 
**IMPLEMENTACIÓN DEL FILTRO**

En Spring Security, la autenticación con nombre de usuario y contraseña se gestiona con varias clases clave. 

## 🔹 **1. `UsernamePasswordAuthenticationFilter`**

📌 Es un **filtro de Spring Security** que intercepta las solicitudes de inicio de sesión.  
📌 Se ejecuta antes de que un usuario acceda a un recurso protegido.  
📌 Verifica las credenciales y delega la autenticación a `AuthenticationManager`.

Por defecto, Spring Security lo aplica en `/login` mediante una petición **POST** con `username` y `password`.

**📌 Flujo del filtro:**

1. Intercepta la solicitud de inicio de sesión (`/login`).
2. Extrae las credenciales del cuerpo de la solicitud.
3. Crea un objeto `UsernamePasswordAuthenticationToken`.
4. Pasa el token al `AuthenticationManager` para validación.
5. Si la autenticación es correcta, genera un **Token JWT o una sesión**.
6. Si la autenticación falla, devuelve un error 401.


## 🔹 **2. `AuthenticationManager`**

📌 Es el componente central en la autenticación en Spring Security.  
📌 Se encarga de **validar las credenciales** usando `AuthenticationProvider`.  
📌 Generalmente, delega la autenticación a `DaoAuthenticationProvider`, que consulta los datos desde `UserDetailsService`.

## 🔹 **3.**`attemptAuthentication(HttpServletRequest request, HttpServletResponse response)`**

📌 Es un método de `UsernamePasswordAuthenticationFilter`.  
📌 **Extrae las credenciales del request y las envía al `AuthenticationManager`.**  
📌 Devuelve un objeto `Authentication` si la autenticación es exitosa, o lanza una excepción si falla.

✔ Extrae `username` y `password`.  
✔ Crea un `UsernamePasswordAuthenticationToken`.  
✔ Lo envía al `AuthenticationManager` para validar.

## **4. `UsernamePasswordAuthenticationToken`**

📌 Es un **objeto que representa una autenticación en Spring Security**.  
📌 Se usa para pasar las credenciales del usuario a `AuthenticationManager`.

✔ Si el usuario es válido, `Authentication` almacena sus detalles y roles.  
✔ Si es inválido, Spring Security lanza una excepción.

---
### ***Ejemplo de la autenticación***

```Java
public class CustomAuthenticationFilter extends UsernamePasswordAuthenticationFilter {

    private final AuthenticationManager authenticationManager;

    public CustomAuthenticationFilter(AuthenticationManager authenticationManager) {
        this.authenticationManager = authenticationManager;
    }

    @Override
    public Authentication attemptAuthentication(HttpServletRequest request, HttpServletResponse response) throws AuthenticationException {
        try {
            // Leer JSON con username y password desde el request
            Map<String, String> credentials = new ObjectMapper().readValue(request.getInputStream(), Map.class);

            String username = credentials.get("username");
            String password = credentials.get("password");

            // Crear el token de autenticación
            UsernamePasswordAuthenticationToken authenticationToken =
                    new UsernamePasswordAuthenticationToken(username, password);

            // Delegar la autenticación al AuthenticationManager
            return authenticationManager.authenticate(authenticationToken);

        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }

    @Override
    protected void successfulAuthentication(HttpServletRequest request, HttpServletResponse response, FilterChain chain, Authentication authResult) throws IOException, ServletException {
        response.getWriter().write("Autenticación exitosa: " + authResult.getName());
    }
}
```

--- 
## **Resumen**


| **Componente**                             | **Función**                                                                                           |
| ------------------------------------------ | ----------------------------------------------------------------------------------------------------- |
| **`UsernamePasswordAuthenticationFilter`** | Captura las credenciales del request y delega la autenticación a `AuthenticationManager`.             |
| **`attemptAuthentication()`**              | Método en el filtro que extrae username y password del request y los envía a `AuthenticationManager`. |
| **`UsernamePasswordAuthenticationToken`**  | Representa una solicitud de autenticación con nombre de usuario y contraseña.                         |
| **`AuthenticationManager`**                | Se encarga de validar las credenciales usando `AuthenticationProvider`.                               |


---

### 🔹 **Método `successfulAuthentication`**

El método `successfulAuthentication` se usa en **`UsernamePasswordAuthenticationFilter`** y se ejecuta cuando la autenticación es exitosa.  
Se puede sobrescribir para realizar acciones personalizadas, como generar un **JWT**, almacenar información en la sesión o registrar el acceso del usuario.

```Java


    @Override
    protected void successfulAuthentication(HttpServletRequest request, HttpServletResponse response,  FilterChain chain, Authentication authResult) 
 throws IOException, ServletException {

        User user = (User) authResult.getPrincipal();

        // Generar JWT
        String token = Jwts.builder()
            .setSubject(user.getUsername())
            .setIssuedAt(new Date())
            .setExpiration(new Date(System.currentTimeMillis() + 3600000))
            .signWith(SignatureAlgorithm.HS256, secretKey)
            .compact();

        // Enviar JWT en la respuesta
        response.setHeader("Authorization", "Bearer " + token);

        // También se puede devolver en el cuerpo de la respuesta
        Map<String, String> responseBody = new HashMap<>();
        responseBody.put("token", token);
        responseBody.put("message", "¡Autenticación exitosa!");

        response.setContentType("application/json");
        new ObjectMapper().writeValue(response.getOutputStream(), responseBody);
    }
}
```

- **Generar un JWT y enviarlo en la respuesta** ✅
- **Registrar el acceso del usuario en logs** ✅
- **Configurar cookies de sesión** ✅
- **Actualizar datos del usuario en la base de datos (último login, etc.)** ✅
- **Redirigir a una página de inicio si usas sesiones en lugar de JWT** ✅

--- 
## Bearer

El término **`Bearer`** en la cabecera **Authorization** se refiere a un esquema de autenticación basado en **tokens**. Se usa principalmente con **JSON Web Tokens (JWT)** para autorizar solicitudes en APIs.

🔹 `Bearer` significa **"portador"** en inglés, indicando que quien posea el token tiene acceso a los recursos protegidos.  
🔹 Se diferencia de otros esquemas de autenticación como **Basic Auth** (usuario/contraseña en Base64).  
🔹 Es un estándar definido en **OAuth 2.0** y usado en APIs REST.

---
### **Método`unsuccessfulAuthentication`**

El método `unsuccessfulAuthentication` se ejecuta cuando un usuario **no logra autenticarse** en Spring Security. Esto puede deberse a:  
✅ Credenciales incorrectas (usuario/contraseña inválidos).  
✅ Token inválido o expirado.  
✅ Cuenta bloqueada o deshabilitada.


```Java
@Override
protected void unsuccessfulAuthentication(HttpServletRequest request, HttpServletResponse response, AuthenticationException failed) 
  throws IOException, ServletException {
    
    response.setStatus(HttpServletResponse.SC_UNAUTHORIZED); // 401 Unauthorized
    
    // Crear un cuerpo de respuesta en JSON
    Map<String, String> errorResponse = new HashMap<>();
    errorResponse.put("error", "Error de autenticación");
    errorResponse.put("message", failed.getMessage());

    // Configurar la respuesta en formato JSON
    response.setContentType("application/json");
    new ObjectMapper().writeValue(response.getOutputStream(), errorResponse);
}
```

✅ `unsuccessfulAuthentication` se ejecuta cuando la autenticación falla.  
✅ Devuelve un **HTTP 401 (Unauthorized)**.  
✅ Envía un **JSON con el mensaje de error**. (failed contiene el mensaje de error)
✅ Se puede personalizar para mostrar diferentes mensajes según el error.