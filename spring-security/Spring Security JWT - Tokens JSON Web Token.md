Estándar abierto para implementar seguridad en aplicaciones API REST. Basado en la especificación RFC 7519
## **🔹 ¿Qué es JWT (JSON Web Token)?**

🔑 **JWT (JSON Web Token)** es un **token seguro y autocontenido** que se usa para transmitir información entre el cliente y el servidor de forma segura.

🔹 **Ejemplo de un JWT:**

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9 .eyJzdWIiOiJ1c3VhcmlvMSIsImV4cCI6MTcxNzI3NzEyNH0 .TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
```

🔹 **Estructura de un JWT:**  

1️⃣ **Header** (Encabezado) → Define el algoritmo de firma (Ej: HS256).  
2️⃣ **Payload** (Cuerpo) → Contiene los datos del usuario (Ej: roles, expiración).  
3️⃣ **Signature** (Firma) → Verifica que el token no ha sido modificado.

🔹 **Características:** 
1️⃣ **Escalables:** se pueden integrar en varias aplicaciones.
2️⃣ **Codificado y decodificado en Base64**: su estructura. 
3️⃣ **Contienen reclamaciones o claims**: el servidor las interpreta (poseen información del client).
4️⃣ **Está firmado mediante una llave secreta**: solo se guarda en el servidor. Sirve para la autenticidad del token.
5️⃣ **Es compacto**: se envia en las cabeceras HTTP, por ejemplo
6️⃣ **Es autónomo**: contiene toda la información necesaria. No depende del servidor.
7️⃣ **Seguridad**: esta encriptado en doble vía. Se puede saber si fue manipulado (se corrompe la firma). No puede contener información sensible por seguridad.

--- 
## **🔹 ¿Cómo funciona JWT en Spring Security?**

1️⃣ **El usuario envía credenciales** (usuario y contraseña).  
2️⃣ **El servidor valida las credenciales** y genera un **JWT**. 
3️⃣ **El cliente guarda el token** y lo envía en cada petición (mediante el `Authorization: Bearer <token>`).  
4️⃣ **El servidor valida el token** en cada petición y permite el acceso si es válido.

![{1F7C9309-6F9C-4539-BB4A-C396F2A11B80} 1.png](../resources/{1F7C9309-6F9C-4539-BB4A-C396F2A11B80}%201.png)

![{612A2A03-8BF4-4171-93C9-C94DE4423D1F} 1.png](../resources/{612A2A03-8BF4-4171-93C9-C94DE4423D1F}%201.png)

--- 
### Resumen
| Característica            | Explicación                                               |
| ------------------------- | --------------------------------------------------------- |
| **JWT**                   | Token para autenticación sin sesiones.                    |
| **Spring Security**       | Maneja la seguridad en Spring Boot.                       |
| **Autenticación con JWT** | Usuario se loguea → Recibe JWT → Lo usa en cada petición. |
| **Ventajas**              | Escalabilidad, seguridad, sin estado (stateless).         |


--- 
### 🔐 **Password Encoder en Spring Security**

📌 **PasswordEncoder** en Spring Security se usa para **cifrar contraseñas** antes de almacenarlas y para **verificarlas** al autenticar usuarios.
## **🔹 Tipos de PasswordEncoder en Spring Security**

Spring Security proporciona varias implementaciones de `PasswordEncoder`, entre ellas:

|**Clase**|**Descripción**|
|---|---|
|`BCryptPasswordEncoder`|Usa el algoritmo **bcrypt**, que es seguro y resistente a ataques de fuerza bruta. ✅ **Recomendado**|
|`Pbkdf2PasswordEncoder`|Usa PBKDF2 con un número configurable de iteraciones.|
|`Argon2PasswordEncoder`|Usa **Argon2**, el ganador del concurso de hashing de contraseñas de 2015.|
|`SCryptPasswordEncoder`|Usa **scrypt**, diseñado para dificultar ataques de hardware.|
|`NoOpPasswordEncoder`|No cifra la contraseña (solo para pruebas, **NO USAR EN PRODUCCIÓN**). ❌|

---
### 🔐 **SecurityFilterChain en Spring Security**

📌 En Spring Security, **`SecuriytFilterChain`** define la **configuración de seguridad** para controlar el acceso a los endpoints de una aplicación. Reemplaza la configuración basada en `WebSecurityConfigurerAdapter` desde Spring Boot 3 y Spring Security 6. Podemos configurar los filtros, tales como [Spring Security - Autenticación (Filtro)](Spring%20Security%20-%20Autenticación%20(Filtro).md) o [Spring Security - Validación Token (Filtro)](Spring%20Security%20-%20Validación%20Token%20(Filtro).md)

✔ **`authorizeHttpRequests()`** → Configura reglas de acceso.  
✔ **`requestMatchers()`** → Especifica rutas con permisos.
✔ **`csrf().disable()`** → Deshabilita CSRF (para APIs REST sin sesiones).
✔ **`addFilter()`** → Agrega filtros.

--- 
### 🔹 **¿Qué son los algoritmos de firma en JWT?**

En **JSON Web Tokens (JWT)**, los algoritmos de firma se utilizan para garantizar la integridad y autenticidad del token. Esto evita que alguien pueda modificar el contenido del token sin ser detectado.

Los algoritmos de firma en JWT se dividen en dos categorías:

1. **Simétricos (HMAC)** → Usan la misma clave para firmar y verificar el token.
2. **Asimétricos (RSA, ECDSA, EdDSA)** → Usan un par de claves (pública y privada).
3. 
#### 🔹 **1. Algoritmos Simétricos (`HMAC`)**

📌 **Usan una clave secreta compartida para firmar y verificar el JWT.**

- Son más rápidos y eficientes.
- El problema es que la misma clave debe ser protegida, ya que cualquier persona con acceso puede firmar tokens.

##### **📌 Algoritmos HMAC más usados:**

|Algoritmo|Tamaño de la clave recomendada|
|---|---|
|**HS256**|256 bits|
|**HS384**|384 bits|
|**HS512**|512 bits|
#### 🔹 **2. Algoritmos Asimétricos (`RSA`, `ECDSA`, `EdDSA`)**

📌 **Usan un par de claves (privada para firmar, pública para verificar).**

- Más seguros que HMAC, pero más lentos.
- Útiles cuando diferentes partes necesitan validar JWT sin exponer la clave privada.

### **📌 Algoritmos Asimétricos más usados:**

| Algoritmo                  | Tipo  | Longitud de clave recomendada |
| -------------------------- | ----- | ----------------------------- |
| **RS256**                  | RSA   | Mínimo 2048 bits              |
| **RS384**                  | RSA   | Mínimo 2048 bits              |
| **RS512**                  | RSA   | Mínimo 2048 bits              |
| **ES256**                  | ECDSA | Clave de 256 bits             |
| **ES384**                  | ECDSA | Clave de 384 bits             |
| **ES512**                  | ECDSA | Clave de 512 bits             |
| **EdDSA (Ed25519, Ed448)** | EdDSA | Claves de 256 y 448 bits      |

📌 **Diferencias entre RSA, ECDSA y EdDSA:**

- **RSA (`RS256`, `RS384`, `RS512`)**
    - Clave privada firma, clave pública verifica.
    - Requiere claves largas (mínimo 2048 bits).
    - Más lento que HMAC.
- **ECDSA (`ES256`, `ES384`, `ES512`)**
    - Basado en curvas elípticas (más eficiente que RSA).
    - Claves más cortas con la misma seguridad.
- **EdDSA (`Ed25519`, `Ed448`)**
    - Más rápido y seguro que ECDSA.
    - Ideal para alto rendimiento y seguridad.



### 📌 **Configurar permisos en Spring Security con `@PreAuthorize`**

En **Spring Security**, la anotación `@PreAuthorize` permite **restringir el acceso a métodos específicos** según los **roles o permisos** del usuario autenticado.
✅ Se debe **habilitar con `@EnableMethodSecurity`** en la configuración.
#### Ejemplos de uso

|**Expresión**|**Descripción**|
|---|---|
|`hasRole('ADMIN')`|Solo permite acceso a usuarios con el rol `ADMIN`.|
|`hasAnyRole('ADMIN', 'USER')`|Permite acceso a usuarios con cualquiera de los roles.|
|`hasAuthority('USER_CREATE')`|Permite acceso a usuarios con el permiso `USER_CREATE`.|
|`hasAnyAuthority('USER_CREATE', 'USER_DELETE')`|Permite acceso si el usuario tiene alguno de estos permisos.|
|`isAuthenticated()`|Permite acceso a cualquier usuario autenticado.|
|`permitAll()`|Permite acceso sin restricciones.|
|`denyAll()`|Bloquea el acceso a todos.|

📌 **Diferencia entre `hasRole()` y `hasAuthority()`**

- `hasRole('ADMIN')` → Espera que el rol venga con el prefijo `"ROLE_"` en la base de datos (`ROLE_ADMIN`).
- `hasAuthority('ADMIN')` → Usa el nombre exacto sin prefijo (`ADMIN`).