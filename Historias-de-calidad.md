## 1. Introducción  
Este documento describe la arquitectura inicial del sistema de gestión de órdenes y entregas, incluyendo requisitos funcionales, requisitos de calidad y restricciones clave que deben ser consideradas en el diseño del software.

**Equipo:** _[JS Code]_  
**Integrantes:** _[Juan Camilo Diaz Valencia, Jhony Fernando Duque Villada, Jairo Andrés Gomez Cardona, Carlos Stiven Ruiz Rojas]_
**Fecha:** _[07/03/2025]_  

---
## 2. Requisitos Funcionales  
Los requisitos funcionales se presentan en forma de **historias de usuario**, especificando los **criterios de aceptación**.

## 3. Requisitos de Calidad  
Los requisitos de calidad del proyecto se presentan a continuación en forma de **historias de calidad**, siguiendo la estructura de Len Bass.

### **Historias de Calidad**
| **ID**   | **Fuente** | **Estímulo** | **Artefactos** | **Entorno** | **Respuesta** | **Medida de Respuesta** |
|----------|-----------|-------------|---------------|------------|-------------|-----------------|
| **RQ-01** | Desarrollador | Se solicita modificar la lógica de asignación de pedidos para incluir nuevos criterios de prioridad. | Código y configuración de reglas de negocio. | Tiempo de ejecución | Se debe modificar, probar y desplegar la nueva lógica de asignación. | El esfuerzo requerido no debe superar 2 horas de trabajo y no deben generarse más de 2 defectos nuevos. |
| **RQ-02** | _Administrador del Sistema_ | _Un servicio de microservicio deja de responder debido a una sobrecarga de solicitudes._ | _Sistema de monitoreo, balanceador de carga._ | _Pico de carga en el sistema._ | _Se debe escalar automáticamente la cantidad de instancias del microservicio afectado._ | _La latencia del servicio no debe superar los 500ms en el 95% de las solicitudes y el sistema debe escalar en menos de 5 segundos_ |
| **RQ-03** | _Equipo de seguridad_ | _Se detecta un intento de acceso no autorizado a un microservicio._ | _Autenticación_ | _Ataque en curso o intento de intrusión_ | _Se debe registrar el intento, bloquear la IP y notificar al equipo de seguridad._ | _El intento de acceso debe registrarse en menos de 5 segundos, la IP debe ser bloqueada en menos de 10 segundos._ |
| **RQ-04** | _Usuario Final_ | _La respuesta de consulta de órdenes tarda demasiado en procesarse._ | _API de órdenes, base de datos._ | _Consulta con gran cantidad de datos._ | _Se debe optimizar la consulta._ | _El tiempo de respuesta no debe superar los 300 ms en el 95% de las consultas._ |

### **Lista de Restricciones**