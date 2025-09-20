## Modelado de Arquitecturas de Software C4 UML

### 1 Análisis Inicial

#### Requerimientos Funcionales

El sistema debe gestionar las siguientes funcionalidades

* [cite_start]Gestión de Cursos y Clases Creación edición y visualización de cursos y clases para administradores y estudiantes [cite: 5]
* [cite_start]Inscripción Proceso de inscripción de estudiantes con validación de prerrequisitos y disponibilidad [cite: 6]
* [cite_start]Gestión de Pagos Generación de facturas procesamiento de pagos en línea a través de una pasarela externa y registro de transacciones [cite: 8]
* [cite_start]Gestión de Usuarios y Roles Autenticación y autorización para estudiantes profesores y administrativos [cite: 9]
* [cite_start]Notificaciones Envío de notificaciones automáticas vía correo electrónico y/o SMS [cite: 10]
* [cite_start]Reportes Generación de informes sobre inscripciones pagos y ocupación [cite: 11]

---

#### Atributos de Calidad Prioritarios

Los atributos de calidad más importantes para esta evolución de la arquitectura son

* [cite_start]Escalabilidad El sistema debe escalar horizontalmente para soportar picos de carga durante los periodos de inscripción [cite: 14]
* [cite_start]Disponibilidad Alta disponibilidad y tolerancia a fallos para garantizar el acceso 24/7 [cite: 15]
* [cite_start]Seguridad Protección de datos sensibles de usuarios y pagos cumpliendo con los estándares de seguridad de la industria [cite: 16]
* [cite_start]Mantenibilidad La arquitectura modular debe facilitar el desarrollo despliegue y actualización de funcionalidades de manera independiente [cite: 17]

---

### 2 Modelado Arquitectónico Modelo C4

#### Nivel 1 Diagrama de Contexto

[cite_start]Muestra el sistema en el centro con sus interacciones clave con usuarios y sistemas externos [cite: 22] [cite_start]El sistema de gestión universitaria es una nueva plataforma SaaS para estudiantes y administrativos [cite: 25, 26] [cite_start]Se conecta con una Pasarela de Pagos que procesa pagos seguros [cite: 28, 29] [cite_start]un Servicio de Notificaciones que envía correos y SMS [cite: 32, 33] [cite_start]y un Sistema Heredado que almacena información histórica [cite: 30, 31]

---

#### Nivel 2 Diagrama de Contenedores

[cite_start]Descompone el sistema en aplicaciones bases de datos y microservicios [cite: 35]

---

### 3 Diagrama de Despliegue UML

[cite_start]Muestra la arquitectura en un entorno de nube usando Google Cloud Platform como ejemplo [cite: 64] [cite_start]Los usuarios acceden al sistema a través de sus dispositivos y un balanceador de carga distribuye el tráfico a un API Gateway [cite: 69, 70, 73, 74] [cite_start]Este gestiona las solicitudes a los microservicios de Pagos Inscripciones y Notificaciones que están alojados en un clúster de Kubernetes [cite: 71, 75, 76, 77, 78, 79, 80]

---

### 4 Decisiones Arquitectónicas ADR

#### ADR 001 Arquitectura de Microservicios

* [cite_start]**Decisión** Migrar del sistema monolítico a una arquitectura de microservicios [cite: 83]
* [cite_start]**Justificación** El sistema monolítico actual presenta problemas de escalabilidad y mantenimiento [cite: 84] [cite_start]La arquitectura de microservicios permitirá escalar cada componente de forma independiente para manejar picos de demanda y facilitará el desarrollo ágil [cite: 85]

#### ADR 002 Persistencia Políglota

* [cite_start]**Decisión** Utilizar diferentes tipos de bases de datos para cada microservicio [cite: 87]
* [cite_start]**Justificación** Cada dominio de datos tiene necesidades distintas [cite: 88] [cite_start]PostgreSQL es ideal para inscripciones MongoDB para perfiles de usuario y Cassandra para el alto volumen de pagos [cite: 88] [cite_start]Esta decisión maximiza el rendimiento y la eficiencia [cite: 89]

#### ADR 003 Autenticación con JSON Web Tokens JWT

* [cite_start]**Decisión** Implementar la autenticación a través de JWT en lugar de un enfoque de sesión centralizada [cite: 90]
* [cite_start]**Justificación** En una arquitectura de microservicios la autenticación debe ser sin estado stateless [cite: 92] [cite_start]JWT permite al API Gateway validar la autenticidad y los permisos de un usuario de manera rápida sin consultar un servicio de autenticación en cada petición lo que reduce la latencia y mejora la escalabilidad [cite: 93]
