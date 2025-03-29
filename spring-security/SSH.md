# 🔑 **¿Qué es SSH (Secure Shell)?**

**SSH (Secure Shell)** es un **protocolo de red** que permite acceder de forma segura a sistemas remotos a través de una conexión cifrada. Se usa principalmente para **administrar servidores, transferir archivos y ejecutar comandos de manera remota**.

---

## 🚀 **1. Características Principales de SSH**

✅ **Cifrado seguro**: Protege la comunicación entre cliente y servidor.  
✅ **Autenticación con claves SSH**: Más segura que contraseñas.  
✅ **Túneles y reenvío de puertos**: Permite acceder a servicios remotos de manera segura.  
✅ **Transferencia de archivos**: Usando SCP (Secure Copy) o SFTP (SSH File Transfer Protocol).

---

## 🔧 **2. ¿Cómo Funciona SSH?**

SSH usa el **modelo cliente-servidor**:

1. **El cliente SSH** se conecta al servidor SSH a través del puerto **22**.
2. **El servidor SSH** valida la identidad del cliente mediante:
    - **Contraseña (menos segura)**
    - **Clave SSH pública/privada (más segura)**
3. **Una vez autenticado**, el usuario puede ejecutar comandos y administrar el sistema de forma remota.