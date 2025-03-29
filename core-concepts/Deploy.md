Hacer un **deploy** (o despliegue) significa **poner una aplicación o sistema en un entorno de ejecución**, haciéndola accesible para los usuarios o clientes. Es el proceso mediante el cual el software desarrollado se configura y publica en un servidor o infraestructura para ser utilizado en producción o en otras etapas, como desarrollo o pruebas.

---

### **Pasos Generales del Deploy**

1. **Compilación del Código**: Convertir el código fuente en un archivo ejecutable o empaquetado (`.jar`, `.war`, `.exe`). -> Maven Wrapper (mvnw.cmd)
		./mvnw clean (limpia carpeta target) package
2. **Configuración del Entorno**: Ajustar las propiedades, variables de entorno y dependencias necesarias para que la aplicación funcione correctamente.
3. **Transferencia de Archivos**: Copiar los archivos del proyecto al servidor o sistema de destino.
4. **Ejecución del Software**: Iniciar la aplicación o servicio en el servidor.
		java -jar /target/java_app_v1.jar
5. **Verificación**: Asegurarse de que la aplicación funcione como se espera en el entorno de despliegue.

---

### **Tipos de Deploy**

1. **Local**: Ejecutar la aplicación en tu máquina de desarrollo.
2. **Servidor Remoto**: Desplegar en un servidor accesible por red (ej. AWS, Azure, Heroku).
3. **Contenedores**: Usar tecnologías como **Docker** o **Kubernetes**.
4. **En la Nube**: Utilizar plataformas de cloud computing para gestionar el deploy (ej. Google Cloud, Amazon Web Services).

---

### **Herramientas Comunes para Deploy**

- **Spring Boot**: Permite generar archivos `jar` autoejecutables.
- **Maven/Gradle**: Herramientas para construir proyectos.
- **Tomcat, Jetty**: Servidores de aplicaciones Java para archivos `.war`.
- **CI/CD**: Herramientas de automatización como **Jenkins**, **GitLab CI**, o **GitHub Actions**.