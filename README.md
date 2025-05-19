Sistema Tunomático — Modelado Arquitectónico Profesional
Descripción General
El Sistema Tunomático es una solución digital para la gestión automatizada de turnos en entornos donde se requiere organización de filas y atención secuencial (clínicas, bancos, oficinas públicas, etc.). El sistema permite:

Generación digital de turnos con diferentes prioridades

Asignación automática a módulos de atención

Notificación a clientes vía múltiples canales

Gestión estadística de tiempos de espera

Integración con sistemas externos (ej: historiales médicos en clínicas)

Diagrama de Casos de Uso



Diagrama de Casos de Uso Tunomático

Descripción y justificación:

Actores principales: Cliente (solicita turnos), Recepcionista (gestiona excepciones), Administrador (configura sistema)

Relaciones <<include>>: "Tomar turno" incluye "Seleccionar servicio" ya que es un paso obligatorio

Relaciones <<extend>>: "Notificar vía SMS" extiende "Notificar turno" como opción adicional

Casos de uso secundarios como "Generar reportes" muestran funcionalidad administrativa

Diagrama de Clases



Diagrama de Clases Tunomático

Patrones aplicados y justificación:

Singleton (<<Singleton>>) en TurneroDigital:

Garantiza una única instancia global del sistema de turnos

Centraliza el control de concurrencia para evitar duplicados

Prototype (<<Prototype>>) en Turno:

Permite clonar turnos base preconfigurados (ej: "Consulta rápida", "Trámite largo")

Optimiza creación de objetos similares reduciendo inicializaciones costosas

Adapter (<<Adapter>>) en AdaptadorSMS:

Adapta interfaz de servicio SMS externo a nuestra interfaz INotificador

Permite integración transparente con múltiples proveedores de notificación

Bridge (<<Bridge>>) en GeneradorTurno/MotorPrioridad:

Separa abstracción (generación de turnos) de implementación (lógica de prioridad)

Permite cambiar algoritmos de priorización sin afectar el generador

Relaciones clave:

Composición fuerte entre TurneroDigital y ColaTurnos (ciclo de vida vinculado)

Agregación entre ModuloAtencion y Atendedor (relación flexible)

Diagrama de Implementación



Diagrama de Implementación Tunomático

Decisiones técnicas:

Nodos físicos:

Servidor central con base de datos relacional para consistencia ACID

Dispositivos terminales (tablets) conectados vía API REST

Servicio SMS externo consumido mediante adaptador

Componentes:

turnero-core: Lógica principal con patrones implementados

notificadores: Módulo desacoplado para expansión

adaptadores: Componentes de integración con estereotipos <<Adapter>>

Conectividad:

HTTP/2 para comunicación interna

Cola RabbitMQ para notificaciones asíncronas

WebSockets para actualizaciones en tiempo real a terminales

Reflexiones Finales
Lecciones aprendidas:

El patrón Bridge demostró especial utilidad para la variabilidad en algoritmos de priorización

Singleton generó debate sobre posibles limitaciones en escenarios de alta disponibilidad

Mejoras futuras:

Implementar patrón Observer para notificaciones push

Evaluar patrón Strategy para algoritmos de asignación dinámica

Conclusión:

La combinación de patrones permitió construir un sistema:

Extensible (nuevos tipos de turnos/notificaciones)

Mantenible (bajo acoplamiento)

Escalable (componentes distribuibles)

El modelado refleja fielmente los requisitos funcionales mientras aplica principios arquitectónicos sólidos para calidad de software profesional.
