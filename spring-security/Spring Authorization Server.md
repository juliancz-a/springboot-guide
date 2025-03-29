Spring Authorization Server es un **framework oficial de Spring** para implementar un **servidor de autorización** basado en **OAuth 2.1 y OpenID Connect 1.0**.

🚀 **Permite gestionar la autenticación y autorización en APIs y aplicaciones web.**

---

## ✅ **1. ¿Qué es [OAuth2](OAuth2.md)?**

OAuth es un **protocolo de autorización** que permite a las aplicaciones acceder a recursos protegidos en nombre de un usuario sin necesidad de compartir sus credenciales (como nombre de usuario y contraseña). En su lugar, OAuth utiliza **tokens de acceso** para autorizar el acceso a los recursos.

#### **2. ¿Qué es OpenID Connect (OIDC)?**

OpenID Connect es un protocolo de **autenticación** construido sobre OAuth 2.0. Mientras que OAuth se centra en la autorización, OIDC se enfoca en **verificar la identidad del usuario**(autenticación) y proporcionar información básica sobre él.

#### **¿Cómo funciona OpenID Connect?**

1. **Flujo típico:**
    
    - Similar a OAuth, el usuario es redirigido a un **servidor de autorización** (también conocido como **Identity Provider** o IdP).        
    - El usuario inicia sesión y autoriza a la aplicación.
    - El servidor de autorización devuelve un **ID Token** (en formato JWT) junto con el token de acceso.
    - El **ID Token** contiene información sobre el usuario, como su nombre, correo electrónico y otros datos de perfil.
        
2. **Componentes clave:**
    
    - **ID Token**: Un token JWT que contiene información sobre el usuario autenticado.
    - **UserInfo Endpoint**: Un endpoint al que la aplicación puede llamar para obtener más información sobre el usuario.
    - **Standard Claims**: Datos estándar sobre el usuario, como `sub` (identificador único), `name`, `email`, etc.
        
3. **Casos de uso comunes:**
    
    - Iniciar sesión en una aplicación usando tu cuenta de Google, Facebook o Microsoft.
    - Implementar autenticación única (Single Sign-On, SSO) en múltiples aplicaciones.
    - Obtener información básica del usuario de manera segura.


### **Diferencias clave entre OAuth y OpenID Connect**

| Característica              | OAuth                                   | OpenID Connect (OIDC)                 |
| --------------------------- | --------------------------------------- | ------------------------------------- |
| **Propósito**               | Autorización (acceso a recursos).       | Autenticación (verificar identidad).  |
| **Tokens**                  | Token de acceso.                        | Token de acceso + ID Token (JWT).     |
| **Información del usuario** | No proporciona información del usuario. | Proporciona información del usuario.  |
| **Uso típico**              | Acceder a APIs protegidas.              | Iniciar sesión y autenticar usuarios. |

---
