# Sistema Tunomático — Modelado Arquitectónico Profesional

## ✅ Descripción General del Sistema

Este proyecto consiste en el modelado arquitectónico completo de un Sistema de Gestión de Turnos Digitales, denominado **Tunomático**, orientado a optimizar la gestión y asignación automática de turnos en entornos diversos, como clínicas, oficinas o servicios públicos.

El sistema busca automatizar y digitalizar todo el proceso de reserva, confirmación y gestión de turnos, incorporando funcionalidades críticas como:

- Registro de usuarios y validación de datos.
- Solicitud, asignación y cancelación de turnos.
- Notificaciones automáticas vía email o SMS.
- Gestión de listas de espera y reasignación dinámica.
- Administración diferenciada para usuarios, operadores y administradores.
- Integración con sistemas externos para autenticación o notificaciones.

## 🔍 Objetivos del Modelado

- Representar con claridad la transición desde la visión funcional (casos de uso) hasta la arquitectura física (despliegue e implementación).
- Aplicar al menos tres patrones de diseño (Singleton, Prototype, Adapter, Bridge) para garantizar flexibilidad, escalabilidad y mantenimiento.
- Reflejar buenas prácticas en diseño orientado a objetos, modularidad y separación de responsabilidades.
- Construir un modelo arquitectónico que sirva como base profesional para futuras implementaciones.

---

## 🔹 1. Diagrama de Casos de Uso UML

![Captura de pantalla 2025-05-16 185239](https://github.com/user-attachments/assets/11649eb8-55cc-4d72-b37e-1a210a4cfe9d)

### Descripción general


El análisis funcional permitió identificar con claridad los actores involucrados y las funcionalidades críticas del sistema **Tunomático**. Se aplicaron correctamente las relaciones `<<include>>` y `<<extend>>` para reflejar acciones obligatorias y opcionales en los distintos flujos operativos, siguiendo buenas prácticas de diseño UML.

---

### 👥 Actores Principales Identificados

- **Usuario**: Solicita, consulta y cancela turnos de manera autónoma.
- **Recepcionista / Operador**: Registra llegada de pacientes, gestiona turnos diarios, y emite reportes de atención.
- **Administrador del Sistema**: Configura parámetros globales, horarios, reglas del sistema, y gestiona usuarios y auditorías.
- **Sistema de Notificaciones Externo**: Envía confirmaciones y recordatorios de turnos vía email o SMS.
- **Sistema de Autenticación Externo**: Valida credenciales de usuarios y controla acceso según perfil.

---

### 🧩 Casos de Uso Destacados y Relaciones Aplicadas

- **Solicitar Turno**  
  Caso de uso base del sistema, obligatorio para iniciar cualquier atención.  
  - `<<include>>` **Validar Disponibilidad**: obligatorio para confirmar disponibilidad de turnos.  
  - `<<extend>>` **Seleccionar Profesional Específico**: si el usuario desea o requiere un profesional particular.  
  - `<<extend>>` **Confirmar Turno por Email/SMS**: según preferencias o configuración.

- **Cancelar Turno**  
  Permite liberar el espacio agendado.  
  - `<<extend>>` **Enviar Notificación**: el sistema puede notificar la cancelación al paciente u operador.

- **Registrar Llegada del Paciente**  
  Ejecutado por el operador para confirmar asistencia presencial.  
  - `<<include>>` **Generar Reporte de Atención**: para trazabilidad y estadísticas.

- **Generar Reportes de Uso**  
  Módulo de soporte para monitoreo del sistema.  
  - `<<include>>` en procesos de auditoría, control interno y seguimiento de gestión.

- **Administrar Configuración del Sistema**  
  Caso exclusivo del administrador.  
  - `<<include>>` **Gestionar Reglas y Parámetros**: incluye horarios, tipos de servicios, umbrales de cancelación, etc.  
  - `<<extend>>` **Auditar Cambios del Sistema**: en contexto de seguimiento o cambios críticos.

---

### ✔️ Justificación de Relaciones UML

- Se utilizaron relaciones `<<include>>` en procesos donde el caso de uso base **depende obligatoriamente** de otro subproceso, como en la validación al solicitar un turno o generación de reportes en auditoría.
- Se utilizaron relaciones `<<extend>>` para modelar comportamientos **opcionales** o **contextuales**, como la confirmación del turno, la selección personalizada del profesional, o el envío de notificaciones tras ciertas acciones.
- Estas relaciones refuerzan la **modularidad** del sistema, permiten **extender funcionalidades sin acoplamientos innecesarios**, y aseguran un diseño **escalable y mantenible** en el tiempo.
---

## 🔹 2. Diagrama de Clases UML con Patrones Aplicados

![Captura de pantalla 2025-05-16 183012](https://github.com/user-attachments/assets/abb6b753-38d4-4731-941c-c731cd622908)

### 🧩 Justificación Arquitectónica y Patrones Aplicados

**1. Singleton (ConfiguracionTunomatico)**  
*Justificación:*  
Se garantiza una única instancia de configuración centralizada para parámetros clave como horarios, reglas de cancelación y límites de turnos, evitando inconsistencias en múltiples puntos del sistema.

*Intención arquitectónica:*  
Centralizar la configuración para facilitar su consulta y modificación segura en tiempo real.

---

**2. Prototype (PlantillaTurno)**  
*Justificación:*  
Permite clonar configuraciones predefinidas de turnos recurrentes, agilizando la creación rápida de nuevas solicitudes basadas en plantillas comunes, por ejemplo, servicios frecuentes o turnos con condiciones especiales.

*Intención arquitectónica:*  
Reducir la redundancia y acelerar la generación de nuevos turnos manteniendo flexibilidad para modificaciones.

---

**3. Adapter (AdaptadorNotificaciones)**  
*Justificación:*  
Se desacopla el núcleo del sistema de gestión de turnos de diferentes sistemas externos de notificaciones (SMS, email, push), facilitando cambios o integración con nuevos proveedores sin impactar la lógica central.

*Intención arquitectónica:*  
Garantizar independencia tecnológica y facilidad de mantenimiento en la integración externa.

---

**4. Bridge (InterfazUsuario + VistaUsuario, VistaOperador, VistaAdministrador)**  
*Justificación:*  
Se separa la interfaz gráfica de la lógica de negocio para adaptar la experiencia a distintos perfiles y dispositivos, asegurando modularidad y escalabilidad.

*Intención arquitectónica:*  
Facilitar la adaptación y expansión hacia nuevas plataformas y dispositivos sin afectar la lógica subyacente.

---

## 🔹 3. Diagrama de Implementación UML

![Captura de pantalla 2025-05-16 183118](https://github.com/user-attachments/assets/6b6ce31f-e671-4efc-98ad-b99b7bbfd84e)

### Despliegue físico y decisiones técnicas

- Nodos físicos diferenciados para la gestión de usuarios, servicios web, notificaciones y base de datos, garantizando escalabilidad y seguridad.
- El nodo del sistema de notificaciones está desacoplado mediante el patrón Adapter para flexibilizar la integración.
- ConfiguracionTunomatico aislado en nodo dedicado para control centralizado y evitar puntos únicos de fallo.
- Uso de protocolos REST para comunicación entre nodos y servicios externos.
- La arquitectura contempla alta disponibilidad y balanceo de carga en servidores de aplicación.

---

## 🧩 Reflexiones Finales del Modelado

Este modelado refleja una aproximación profesional orientada a la robustez, mantenibilidad y escalabilidad del sistema:

- La selección estratégica de patrones de diseño responde a necesidades concretas del dominio y objetivos técnicos, evitando complejidad innecesaria.
- La trazabilidad entre casos de uso, diseño lógico y arquitectura física asegura un entendimiento claro y una base sólida para desarrollo e implementación.
- La modularización permite actualizaciones y ampliaciones sin comprometer la estabilidad del sistema.
- Este repositorio busca ser una referencia formal para prácticas avanzadas de modelado arquitectónico en proyectos reales.
