En el contexto de APIs y aplicaciones web, los métodos de autenticación son mecanismos que permiten verificar la identidad de un usuario o cliente antes de permitirle acceder a recursos protegidos. 

---

### **1. Basic Authentication**

Es uno de los métodos de autenticación más simples y antiguos. Consiste en enviar las credenciales del usuario (nombre de usuario y contraseña) en cada solicitud HTTP.

#### **¿Cómo funciona?**

1. El cliente combina el nombre de usuario y la contraseña en una cadena de la forma `usuario:contraseña`.
2. Esta cadena se codifica en **Base64**.
3. La cadena codificada se envía en el encabezado HTTP `Authorization` de la siguiente manera:
		`Authorization: Basic <credenciales_en_base64>`
4. El servidor decodifica la cadena Base64, verifica las credenciales y, si son válidas, permite el acceso.

#### **Ventajas**
- Sencillo de implementar.
- Ampliamente soportado.
#### **Desventajas**
- **No seguro**: Las credenciales se envían en texto plano (solo codificadas en Base64, no cifradas).
- **Sin expiración**: Las credenciales son estáticas y no caducan.
- **Reutilización de credenciales**: El cliente debe enviar las credenciales en cada solicitud.

### **2. Bearer Token Authentication**

Este método es más moderno y seguro. Utiliza **tokens** (generalmente tokens JWT) para autenticar las solicitudes. El token es una cadena cifrada que contiene información sobre el usuario y sus permisos.

#### **¿Cómo funciona?**

1. El cliente primero autentica al usuario (por ejemplo, mediante un formulario de inicio de sesión o [OAuth2](OAuth2.md)).
2. El servidor genera un **token** (por ejemplo, un JWT) y lo devuelve al cliente.
3. El cliente envía este token en el encabezado HTTP `Authorization` de la siguiente manera:
	`Authorization: Bearer <token>`
4. El servidor verifica el token y, si es válido, permite el acceso.
#### **Ventajas**
- **Seguro**: Los tokens pueden estar firmados y cifrados.
- **Sin estado**: El servidor no necesita almacenar el token, ya que toda la información necesaria está contenida en el token.
- **Caducidad**: Los tokens pueden tener un tiempo de vida limitado.
- **Flexibilidad**: Los tokens pueden contener información adicional (claims) como roles, permisos, etc.

#### **Desventajas**
- Complejidad: Requiere un mecanismo para generar, firmar y verificar tokens.
- Revocación: La revocación de tokens no es trivial (a menos que se use un mecanismo como una lista negra).


### **3. Otros métodos de autenticación**

Además de Basic y Bearer, existen otros métodos de autenticación comunes:

#### **a. [OAuth2](OAuth2.md)**

- **Descripción**: Un protocolo de autorización que permite a las aplicaciones acceder a recursos en nombre de un usuario sin compartir credenciales.
- **Uso**: Integración con proveedores de identidad (Google, Facebook, etc.).
- **Ejemplo**: Un usuario autoriza a una aplicación para acceder a su cuenta de Google Drive.

#### **b. API Keys**

- **Descripción**: Una clave única que identifica a un cliente o aplicación.
- **Uso**: Autenticación en APIs de terceros.
- **Ejemplo**: `Authorization: ApiKey <clave_api>`.
    

#### **c. Digest Authentication**

- **Descripción**: Una mejora sobre Basic Authentication que usa un hash para evitar enviar credenciales en texto plano.
- **Uso**: Menos común, pero más seguro que Basic.
    

#### **d. Certificados de cliente**

- **Descripción**: Usa certificados digitales para autenticar al cliente.
- **Uso**: Entornos de alta seguridad (banca, gobierno).