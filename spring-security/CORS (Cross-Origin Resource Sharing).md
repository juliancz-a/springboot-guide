CORS (**Cross-Origin Resource Sharing**) es un **mecanismo de seguridad** que permite o restringe solicitudes HTTP entre diferentes dominios (orígenes).

Por defecto, los **navegadores bloquean** las solicitudes de una página web a un dominio diferente al de la página que la cargó (**Same-Origin Policy**). **CORS** permite definir qué dominios pueden hacer solicitudes a nuestra API.

---

## ✅ **1. ¿Por qué es importante CORS?**

Si una aplicación frontend (React, Angular, Vue) intenta consumir una API en otro dominio, el navegador **bloqueará la solicitud** por seguridad.

Ejemplo de error en consola:
```
Access to fetch at 'http://api.ejemplo.com/datos' from origin 'http://frontend.com' has been blocked by CORS policy.
```

