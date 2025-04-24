# Plataforma Integral de Gestión de Eventos y Actividades Locales

Este repositorio contiene la solución desarrollada para la plataforma de gestión de eventos y actividades orientada a una municipalidad turística. El sistema permite a ciudadanos, turistas y funcionarios gestionar y participar en eventos y actividades culturales, deportivas y recreativas.

---

## ✨ Diagramas Clave

### Diagrama de Contexto (C4 Nivel 1)
Representa las interacciones entre los actores principales (ciudadano, turista, funcionario) y el sistema. Muestra las integraciones externas (Microsoft Entra, SendGrid, Stripe, Google Maps).

### Diagrama de Contenedores (C4 Nivel 2)
Visualiza la arquitectura modular basada en microservicios: User Service, Reservation Service, Activity Service, Attraction Service, Checkout, Payment, Notification, Application Gateway y Message Broker.

### Diagramas de Componentes (C4 Nivel 3)
Desglosa la lógica interna de los microservicios principales:
- User Service: perfil, preferencias, historial
- Reservation Service: disponibilidad, inscripciones, cancelaciones
- Activity Service: actividades comunitarias
- Attraction Service: lugares turísticos y culturales

### Diagramas de Casos de Uso UML
Incluyen los principales flujos funcionales:
- Turista: consultar atracciones, reservar eventos
- Ciudadano: gestionar perfil, ver historial
- Funcionario: publicar actividades, cancelar eventos

### Diagramas de Secuencia UML
Representan los flujos clave:
- Registro de usuario (autenticación con Microsoft Entra)
- Consulta de eventos geolocalizados
- Inscripción a evento (con pago y notificación)

---

## ⚖️ Consideraciones Técnicas

### Backend
- **Lenguaje**: C#
- **Framework**: .NET 8 Web API
- **Justificación**: Alto rendimiento, soporte a microservicios, integración con Azure.

### Frontend Web
- **Framework**: React
- **Justificación**: Componentes reutilizables, alto rendimiento en SPA, compatible con Azure Static Web Apps.

### Base de Datos
- **Tipo**: Relacional (SQL Server)
- **Justificación**: Integridad transaccional, soporte nativo en Azure, consultas geoespaciales.

### Colas de Mensajes
- **Tecnología**: RabbitMQ
- **Justificación**: Desacoplamiento, resiliencia, procesamiento de eventos como notificaciones y pagos.

### Seguridad
- **Autenticación**: Microsoft Entra (Azure AD B2C)
- **Autorización**: Roles y claims en JWT
- **Protección de datos**: HTTPS, CORS, rate limiting y secrets en KeyVault

### Patrones de Diseño (Backend)
1. **Repository Pattern**: Abstrae el acceso a datos.
2. **Service Layer**: Encapsula lógica de negocio.
3. **Event-driven Pattern**: Comunicación desacoplada mediante eventos (RabbitMQ).

---

## 📊 Arquitectura Global

- **Estilo**: Microservicios con API Gateway
- **Justificación**:
  - Escalabilidad horizontal por microservicio
  - Bajo acoplamiento y alta cohesión
  - Integraciones externas desacopladas (Stripe, SendGrid, Maps)

### Ventajas
- Escalable, mantenible, ideal para altos picos turísticos
- Facilidad de integración y despliegue continuo
- Separación de responsabilidades clara

### Desventajas
- Mayor complejidad operativa
- Costos iniciales más altos
- Requiere gobernanza de microservicios y observabilidad

---

## 📱 Aplicación Móvil

### Alcance
- Consulta de eventos y atracciones cercanas (con GPS)
- Inscripción y pagos
- Notificaciones push
- Gestionar perfil del usuario

### Tecnología
- **Plataforma**: .NET MAUI
- **Justificación**:
  - Código compartido (iOS/Android)
  - Buen rendimiento
  - Acceso nativo a funcionalidades del dispositivo

---

## 📄 Documentación

- Todo el contenido está documentado en Markdown
- Incluye diagramas C4, UML, decisiones tecnológicas y flujos
- Compatible con presentaciones técnicas y evaluaciones académicas

---

© Proyecto académico - Arquitectura de Software - 2025
