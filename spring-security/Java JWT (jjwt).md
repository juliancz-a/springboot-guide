`jjwt` (**Java JWT**) es una librería en Java para generar, firmar y validar **JSON Web Tokens (JWT)** de forma sencilla.

📌 **Características principales:**  
✅ Creación de **JWT firmados** con HMAC, RSA y ECDSA.  
✅ **Parsing y validación** de JWT.  
✅ Compatible con **Spring Security** y APIs REST.

## Crear JWT

🔹 `Jwts.builder()` → Crea un **JWT** con un **subject (usuario)** y fecha de expiración.  
🔹 `signWith(SignatureAlgorithm.HS256, SECRET_KEY)` → Firma el token con HMAC-SHA256.  
🔹 `Jwts.parser().setSigningKey(SECRET_KEY).parseClaimsJws(token)` → **Valida el token** y extrae los claims.

## Claims

En `jjwt`, la clase `Claims` representa los **datos (claims)** contenidos en un **JWT**. Estos claims incluyen información como el usuario, la fecha de expiración, roles, etc.

📌 **Claims se utilizan para almacenar información dentro del JWT**, y pueden ser:  
✅ **Claims estándar** (definidos en el estándar JWT)  
✅ **Claims personalizados** (agregados según la aplicación)

---

## 📌  Claims estándar en JWT

Algunos claims comunes en un JWT:

| Claim                  | Descripción                                     |
| ---------------------- | ----------------------------------------------- |
| **`sub` (subject)**    | Identificación del usuario (ejemplo: "user123") |
| **`iss` (issuer)**     | Quién generó el token (ejemplo: "miapp.com")    |
| **`exp` (expiration)** | Fecha de expiración del token                   |
| **`iat` (issued at)**  | Fecha de emisión del token                      |
| **`aud` (audience)**   | Destinatario del token                          |