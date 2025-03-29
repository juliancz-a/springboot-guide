
`slf4j.Logger` es una interfaz en el marco de registro de mensajes (logging) en Java, proporcionada por la librería **SLF4J** (Simple Logging Facade for Java). Se utiliza para generar registros de eventos en una aplicación, facilitando la depuración y el monitoreo.

### **Características Clave**

- **Independencia de Implementación**: SLF4J es una fachada que permite trabajar con diferentes implementaciones de logging como **Logback**, **Log4j**, o incluso el propio **java.util.logging**.
- **Optimización de Desempeño**: Los mensajes de registro se construyen solo si el nivel de registro es habilitado, lo que mejora el rendimiento.


Se obtiene una instancia del logger usando la fábrica proporcionada por `LoggerFactory`.

### **Niveles de Registro**

Los niveles definen la importancia del mensaje:

1. **TRACE**: Detalles más finos que `DEBUG`, útil para seguimiento detallado.
2. **DEBUG**: Información de depuración, común en desarrollo.
3. **INFO**: Información general sobre el estado de la aplicación.
4. **WARN**: Indicaciones de posibles problemas.
5. **ERROR**: Mensajes para errores críticos.