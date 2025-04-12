Los **códigos de estado HTTP** son respuestas del servidor a una solicitud realizada por un cliente. Se dividen en **5 categorías**, según su función.

---

## ✅ **1. Códigos 1xx - Informativos**

Estos códigos indican que la solicitud está en proceso.

| **Código**                | **Descripción**                                                            |
| ------------------------- | -------------------------------------------------------------------------- |
| `100 Continue`            | El servidor recibió parte de la solicitud y espera el resto.               |
| `101 Switching Protocols` | El cliente ha solicitado cambiar el protocolo y el servidor lo acepta.     |
| `102 Processing`          | El servidor está procesando la solicitud, pero aún no tiene una respuesta. |

---

## ✅ **2. Códigos 2xx - Éxito**

Indican que la solicitud fue procesada correctamente.

|**Código**|**Descripción**|
|---|---|
|`200 OK`|Solicitud exitosa.|
|`201 Created`|Un recurso ha sido creado correctamente.|
|`202 Accepted`|La solicitud fue aceptada, pero aún está en proceso.|
|`204 No Content`|La solicitud fue procesada con éxito, pero no hay contenido en la respuesta.|

---

## ✅ **3. Códigos 3xx - Redirección**

Indican que el cliente debe hacer algo más para completar la solicitud.

|**Código**|**Descripción**|
|---|---|
|`301 Moved Permanently`|El recurso ha cambiado de URL permanentemente.|
|`302 Found`|El recurso ha cambiado temporalmente de URL.|
|`304 Not Modified`|El recurso no ha cambiado desde la última vez que fue solicitado.|

---

## ✅ **4. Códigos 4xx - Errores del Cliente**

Indican que la solicitud tiene un error por parte del cliente.

| **Código**                 | **Descripción**                                            |
| -------------------------- | ---------------------------------------------------------- |
| `400 Bad Request`          | La solicitud tiene una sintaxis incorrecta.                |
| `401 Unauthorized`         | Se requiere autenticación para acceder al recurso.         |
| `403 Forbidden`            | No tienes permiso para acceder al recurso.                 |
| `404 Not Found`            | El recurso solicitado no existe.                           |
| `405 Method Not Allowed`   | El método HTTP utilizado no está permitido.                |
| `409 Conflict`             | Conflicto en la solicitud, por ejemplo, un dato duplicado. |
| `422 Unprocessable Entity` | La solicitud es válida pero contiene datos incorrectos.    |

---

## ✅ **5. Códigos 5xx - Errores del Servidor**

Indican que el servidor falló al procesar la solicitud.

| **Código**                  | **Descripción**                                                 |
| --------------------------- | --------------------------------------------------------------- |
| `500 Internal Server Error` | Error general en el servidor.                                   |
| `502 Bad Gateway`           | El servidor recibió una respuesta inválida desde otro servidor. |
| `503 Service Unavailable`   | El servidor está temporalmente fuera de servicio.               |
| `504 Gateway Timeout`       | Tiempo de espera agotado al comunicarse con otro servidor.      |