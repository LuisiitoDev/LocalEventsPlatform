# Plataforma Integral de Gestión de Eventos y Actividades Locales

Este repositorio contiene la solución desarrollada para la plataforma de gestión de eventos y actividades orientada a una municipalidad turística. El sistema permite a turistas y funcionarios gestionar y participar en eventos y actividades culturales, deportivas y recreativas.

---

## ✨ Diagramas Clave

### Diagrama de Contexto (C4 Nivel 1)
Representa las interacciones entre los actores principales (ciudadano, turista, funcionario) y el sistema. Muestra las integraciones externas (Microsoft Entra, SendGrid, Stripe, Google Maps).

![C4 L1](https://github.com/user-attachments/assets/f5b62603-2661-4fc5-82d9-8f3587a3cf0d)

### Diagrama de Contenedores (C4 Nivel 2)
Visualiza la arquitectura modular basada en microservicios: User Service, Reservation Service, Activity Service, Attraction Service, Checkout, Payment, Notification, Application Gateway y Message Broker.

![C4 L2](https://github.com/user-attachments/assets/fcfb80ac-326f-46f7-ba54-95353525f925)


### Diagramas de Componentes (C4 Nivel 3)
Desglosa la lógica interna de los microservicios principales:
- User Service: perfil, preferencias, historial
- Reservation Service: disponibilidad, inscripciones, cancelaciones
- Activity Service: actividades comunitarias
- Attraction Service: lugares turísticos y culturales

User Service

![userService](https://github.com/user-attachments/assets/38254570-cbab-4cb6-a00b-668aa7792ce0)

![usermicroservice](https://github.com/user-attachments/assets/176b81b2-3d21-44d0-8acc-f078f2b0f41e)

Reservation Service

![image](https://github.com/user-attachments/assets/41c58886-a710-4009-9fb7-66779f65b9bc)

![image](https://github.com/user-attachments/assets/8b9c3f45-7c9e-43a9-9924-043d48986f2f)

Attraction Service

![image](https://github.com/user-attachments/assets/77fee551-0ad7-4107-85c0-556fd42ed66d)

![image](https://github.com/user-attachments/assets/d57734d6-e718-4015-9be6-fcdfb9d5d225)

Activity Service

![image](https://github.com/user-attachments/assets/3d817ed3-f054-431a-80c4-2bfef6139cae)

![image](https://github.com/user-attachments/assets/ee4e19fb-51f5-45a8-a741-544c4dca5f65)





### Diagramas de Casos de Uso UML
Incluyen los principales flujos funcionales:
- Turista: consultar atracciones, reservar eventos
- Funcionario: publicar actividades, cancelar eventos

![WhatsApp Image 2025-04-24 at 1 10 59 PM](https://github.com/user-attachments/assets/441fed1b-5ebd-40d7-a395-ab0c1f5ad0f8)


### Diagramas de Secuencia UML
Representan los flujos clave:
- Autenticación con Microsoft Entra
- Consulta de eventos categorizados por atraciones
- Reservacion de eventos o actividades (con pago y notificación)

  ![flow](https://github.com/user-attachments/assets/e6a0c1b3-e0a2-407c-883a-d34def1feb7d)




---

## ⚖️ Consideraciones Técnicas

### Backend
- **Lenguaje**: C#
- **Framework**: .NET 8 Web API
- **Justificación**:Soporte nativo con microservicios y orquestador de microservicios con .NET Aspire.

### Frontend Web
- **Framework**: React
- **Justificación**: Componentes reutilizables, facilidad de SEO.

### Base de Datos
- **Tipo**: Relacional (SQL Server)
- **Justificación**: Datos estructurados.

### Colas de Mensajes
- **Tecnología**: RabbitMQ
- **Justificación**: Procesamiento de eventos como notificaciones.

### Seguridad
- **Autenticación**: Microsoft Entra (Azure AD B2C)
- **Autorización**: Claims en JWT
- **Protección de datos**: HTTPS, CORS,

### 🧩 Patrones de Diseño (Backend)

En el backend de la plataforma, se utilizaron tres patrones fundamentales que favorecen la separación de responsabilidades, la mantenibilidad del código y la escalabilidad del sistema:

---

#### 1. 🧱 Repository Pattern

**Importancia:**  
Permite abstraer el acceso a la base de datos, desacoplando la lógica de negocio del almacenamiento de datos.

**Aplicación en el proyecto:**  
Cada microservicio implementa su propio repositorio para acceder a sus datos. Por ejemplo, `ReservationRepository` encapsula la lógica de acceso a la tabla de reservas y permite consultarlas, crearlas o cancelarlas sin exponer directamente el contexto de la base de datos al resto del sistema.

---

#### 2. 🧠 Service Layer Pattern

**Importancia:**  
Organiza la lógica de negocio en una capa intermedia entre los controladores (API) y los repositorios. Esto permite centralizar las reglas de negocio, evitar duplicación de lógica y promover la reutilización.

**Aplicación en el proyecto:**  
Servicios como `UserService`, `ReservationService` y `ActivityService` manejan la lógica principal de cada dominio (validaciones, reglas, transacciones) y son invocados por los controladores expuestos por cada microservicio.

---

#### 3. 📬 Event-Driven Architecture (Publisher/Subscriber)

**Importancia:**  
Permite la comunicación entre microservicios de forma desacoplada, basada en eventos. Mejora la escalabilidad y la resiliencia, ya que los servicios no se invocan directamente entre sí.

**Aplicación en el proyecto:**  
Cuando se confirma una reserva, el `ReservationService` publica un evento (`ReservationConfirmed`) en RabbitMQ. Este evento es consumido por el `NotificationService`, que envía el correo o notificación correspondiente al usuario, sin que exista una llamada directa entre servicios.

---



---

## 📊 Arquitectura Global

- **Estilo**: Microservicios con API Gateway
- **Justificación**:
  - Escalabilidad horizontal por microservicio
  - Bajo acoplamiento y alta cohesión
  - Integraciones externas desacopladas (Stripe, SendGrid)

### Ventajas
- Escalable, mantenible, ideal para altos picos turístico
- Facilidad de integración y despliegue continuo
- Separación de responsabilidades clara

### Desventajas
- Mayor complejidad operativa
- Costos iniciales más altos
- Deploys por separados
- Necesidad de Monitoreo distribuido
- Resilencia y tolerancia a fallos

---

## 📱 Aplicación Móvil

### Alcance
- Consulta de eventos y atracciones cercanas (con GPS)
- Inscripción y pagos
- Notificaciones push
- Gestionar perfil del usuario
- Autenticación con MS Entra

### Tecnología
- **Plataforma**: .NET MAUI
- **Justificación**:
  - Código compartido (iOS/Android)
  - Buen rendimiento
  - Acceso nativo a funcionalidades del dispositivo
  - Mismo stack que el Backend

---

### Recursos

https://app.icepanel.io/landscapes/1YAy4ElBkoOsEIIvp2ni/versions/latest/diagrams/editor?diagram=5c4th1b67ph&model=BldNqIkNHa&overlay_tab=tags&x1=-261.9&y1=48.5&x2=1649.2&y2=989.1


---

© Proyecto Final - Arquitectura de Software Moderno - 2025
