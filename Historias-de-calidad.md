## 1. Introducción  
Este documento describe la arquitectura inicial del sistema de gestión de órdenes y entregas, incluyendo requisitos funcionales, requisitos de calidad y restricciones clave que deben ser consideradas en el diseño del software.

**Equipo:** _JS Code_  
**Integrantes:** _Juan Camilo Diaz Valencia, Jhony Fernando Duque Villada, Jairo Andrés Gomez Cardona, Carlos Stiven Ruiz Rojas, Juan David Rojas Narvaez_
**Fecha:** _[07/03/2025]_  

---
## 2. Requisitos Funcionales  
Los requisitos funcionales se presentan en forma de **historias de usuario**, especificando los **criterios de aceptación**.

### **Historias de Usuario**

| **ID**    | **Historia de Usuario**                                                                                                           | **Criterios de Aceptación** |
| --------- | --------------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| **US-01** | Como usuario, deseo registrarme en la app con mis datos personales. | - El usuario debe ingresar su nombre, correo electrónico y contraseña.<br>- Se debe validar que el correo no esté registrado previamente.<br>- Si el registro es exitoso, el usuario recibe un correo de confirmación. |
| **US-02** | Como usuario, deseo iniciar sesión en la aplicación. | - El usuario debe ingresar un correo y contraseña válidos.<br>- Si las credenciales son correctas, el usuario es redirigido al menú principal.<br>- Si las credenciales son incorrectas, se muestra un mensaje de error sin revelar detalles específicos.<br>- El usuario puede solicitar un restablecimiento de contraseña. |
| **US-03** | Como usuario, deseo poder restablecer mi contraseña en caso de olvido. | - El usuario debe ingresar su correo electrónico para solicitar un restablecimiento.<br>- Se debe enviar un correo con un enlace de restablecimiento.<br>- El enlace debe expirar después de un tiempo definido por seguridad.<br>- El usuario debe ingresar una nueva contraseña segura para completar el proceso. |
| **US-04** | Como usuario, deseo visualizar los productos disponibles para su compra. | - El sistema debe mostrar una lista de productos con nombre, imagen, precio y disponibilidad.<br>- Los productos deben poder ordenarse por precio o popularidad. |
| **US-05** | Como usuario, deseo poder reservar productos en un carrito de compra. | - El usuario puede agregar productos a su carrito.<br>- Los productos deben mantenerse en el carrito hasta que el usuario complete la compra o los elimine manualmente. |
| **US-06** | Como usuario, deseo poder modificar mis datos personales. | - El usuario puede actualizar su nombre, correo y contraseña.<br>- Se debe solicitar la contraseña actual para confirmar los cambios. |
| **US-07** | Como usuario, deseo poder realizar el pago por los productos de mi carrito. | - El sistema debe permitir el pago con tarjeta de crédito, débito o billetera digital.<br>- Se debe generar una confirmación de pago tras una transacción exitosa. |
| **US-08** | Como usuario, deseo realizar seguimiento a mi orden de compra. | - El usuario debe poder visualizar el estado de su orden en tiempo real.<br>- Se deben mostrar actualizaciones de ubicación cuando el pedido esté en entrega. |
| **US-09** | Como usuario, deseo poder cancelar mi orden de compra. | - El usuario puede cancelar la orden antes de que sea enviada.<br>- Se debe mostrar una confirmación antes de proceder con la cancelación. |
| **US-10** | Como usuario, deseo poder realizar la devolución de mi pedido. | - El usuario puede solicitar una devolución dentro de un período determinado.<br>- Se debe generar una etiqueta de devolución con instrucciones. |
| **US-11** | Como usuario, deseo poder eliminar mi cuenta. | - El usuario debe confirmar su decisión antes de eliminar la cuenta.<br>- Se debe eliminar toda la información personal del usuario. |
| **US-12** | Como usuario, deseo recibir una notificación cuando se genere mi orden de compra. | - El usuario recibe una notificación por correo y en la app al realizar una compra. |
| **US-13** | Como usuario, deseo recibir una notificación cuando se cancele una orden de compra. | - Se debe enviar una notificación inmediata cuando una orden es cancelada. |
| **US-14** | Como usuario, deseo recibir una notificación cuando se genere mi orden de devolución. | - Se debe notificar al usuario cuando la solicitud de devolución sea procesada. |
| **US-15** | Como usuario, deseo poder filtrar los productos por categorías o búsqueda. | - El sistema debe permitir la búsqueda por palabras clave y filtrar por categorías. |
| **US-16** | Como usuario, deseo recibir una notificación cuando se agote un producto de mi carrito. | - Si un producto en el carrito queda sin stock, el usuario recibe una alerta. |
| **US-17** | Como usuario, deseo poder cambiar mi método de pago. | - El usuario puede modificar su método de pago antes de completar la compra. |

#### **Administrador**

| **ID** | **Historia de Usuario** | **Criterios de Aceptación** |
| ------ | ---------------------- | -------------------------- |
| **US-A1** | Como administrador, deseo crear productos nuevos para su venta en la app. | - El administrador puede agregar productos con nombre, descripción, precio e imagen. |
| **US-A2** | Como administrador, deseo poder editar la información de los productos disponibles para su compra. | - Se debe permitir la modificación de los detalles del producto. |
| **US-A3** | Como administrador, deseo poder eliminar un producto de la app. | - Solo los productos sin pedidos pendientes pueden eliminarse. |
| **US-A4** | Como administrador, deseo recibir notificaciones cuando un producto alcance stock bajo. | - Se debe generar una alerta cuando el stock sea menor a un umbral definido. |

#### **Repartidor**

| **ID** | **Historia de Usuario** | **Criterios de Aceptación** |
| ------ | ---------------------- | -------------------------- |
| **US-R1** | Como repartidor, deseo recibir una notificación cuando se genera una orden de entrega. | - Se debe enviar una notificación cuando haya una nueva asignación de entrega. |
| **US-R2** | Como repartidor, deseo poder visualizar las órdenes de entrega asignadas. | - El repartidor puede ver un listado de órdenes pendientes y en curso. |
| **US-R3** | Como repartidor, deseo poder cambiar el estado de una entrega. | - Se debe permitir cambiar el estado a "En camino" y "Entregado". |
| **US-R4** | Como repartidor, deseo poder cambiar mi estado de disponibilidad. | - Se debe permitir activar o desactivar la disponibilidad del repartidor. |
| **US-R5** | Como repartidor, deseo poder escoger entre aceptar una orden de entrega o rechazarla. | - Se debe permitir rechazar órdenes con un motivo válido. |


## 3. Requisitos de Calidad  
Los requisitos de calidad del proyecto se presentan a continuación en forma de **historias de calidad**, siguiendo la estructura de Len Bass.

### **Historias de Calidad**
| **ID**   | **Fuente** | **Estímulo** | **Artefactos** | **Entorno** | **Respuesta** | **Medida de Respuesta** |
|----------|-----------|-------------|---------------|------------|-------------|-----------------|
| **RQ-01** | Desarrollador | Se solicita modificar la lógica de asignación de pedidos para incluir nuevos criterios de prioridad. | Código y configuración de reglas de negocio. | Tiempo de ejecución | Se debe modificar, probar y desplegar la nueva lógica de asignación. | El esfuerzo requerido no debe superar 2 horas de trabajo y no deben generarse más de 2 defectos nuevos. |
| **RQ-02** | _Administrador del Sistema_ | _Un servicio de microservicio deja de responder debido a una sobrecarga de solicitudes._ | _Sistema de monitoreo, balanceador de carga._ | _Pico de carga en el sistema._ | _Se debe escalar automáticamente la cantidad de instancias del microservicio afectado._ | _La latencia del servicio no debe superar los 500ms en el 95% de las solicitudes y el sistema debe escalar en menos de 5 segundos_ |
| **RQ-03** | _Equipo de seguridad_ | _Se detecta un intento de acceso no autorizado a un microservicio._ | _Autenticación_ | _Ataque en curso o intento de intrusión_ | _Se debe registrar el intento, bloquear la IP y notificar al equipo de seguridad._ | _El intento de acceso debe registrarse en menos de 5 segundos, la IP debe ser bloqueada en menos de 10 segundos._ |
| **RQ-04** | _Usuario Final_ | _La respuesta de consulta de órdenes tarda demasiado en procesarse._ | _API de órdenes, base de datos._ | _Consulta con gran cantidad de datos._ | _Se debe optimizar la consulta._ | _El tiempo de respuesta no debe superar los 300 ms en el 95% de las consultas._ |
| **RQ-05** | Administrador | Se requiere garantizar la trazabilidad de las órdenes de compra y devolución. | Sistema de logs y auditoría de pedidos. | Operación normal del sistema. | Se debe registrar cada cambio de estado de las órdenes y garantizar su disponibilidad en reportes. | Los logs deben almacenarse por **6 meses** y ser accesibles en **menos de 3 segundos** en consultas de historial. |
| **RQ-06** | Repartidor | La actualización de estado de una entrega debe reflejarse en tiempo real. | API de entregas, WebSockets. | Comunicación en tiempo real. | Se debe garantizar la sincronización instantánea entre el repartidor y el sistema. | Los cambios de estado deben reflejarse en **menos de 2 segundos** tras su actualización. |
| **RQ-07** | Administrador del sistema | Se requiere auditar las acciones realizadas por los administradores en el inventario. | Sistema de control de cambios. | Mantenimiento de productos. | Cada modificación en el inventario debe quedar registrada con usuario, fecha y cambio realizado. | El historial debe mostrar cambios en **menos de 2 segundos** al consultar. |
| **RQ-08** | Cliente | Se debe garantizar la privacidad de datos personales de los usuarios. | Sistema de autenticación y permisos. | Cualquier acceso no autorizado. | Se debe evitar la exposición de datos sensibles y permitir la eliminación de cuenta bajo solicitud. | Ningún usuario sin permisos debe acceder a información ajena. **Eliminación de datos en menos de 24 horas tras solicitud.** |
| **RQ-09** | Administrador | Se requiere asegurar que las notificaciones de stock bajo lleguen sin retraso. | Servicio de notificaciones y eventos. | Pedido cercano a agotarse. | La notificación debe generarse de inmediato y ser enviada al administrador. | La alerta debe emitirse en **menos de 5 segundos** tras detectar stock bajo. |
| **RQ-10** | Cliente | Se requiere que el proceso de pago no se interrumpa ante una caída del servicio. | API de pagos y sistema de respaldo. | Falla del servicio de pago. | Se debe garantizar un mecanismo de reintento y recuperación automática. | Si el pago falla, debe reintentarse hasta **3 veces** antes de cancelarse. |


### **Lista de Restricciones**

| **Tipo de Restricción** | **Descripción** |
|------------------------|----------------|
| **Tecnológica** | El sistema debe desarrollarse utilizando **Spring Boot y PostgreSQL**, debido a la infraestructura actual de la empresa y su compatibilidad con otros sistemas internos. |
| **Tecnológica** | Se debe utilizar **Kubernetes** para la gestión y escalabilidad de los microservicios. |
| **Tecnológica** | La comunicación entre microservicios debe realizarse mediante **RabbitMQ o Kafka** para garantizar la entrega de mensajes sin pérdida ni duplicación. |
| **Tecnológica** | La autenticación debe implementarse con **OAuth2 y JWT**, sin permitir otros métodos no especificados. |
| **Regulatoria** | El sistema debe cumplir con la **Ley 1581 de 2012 y el Decreto 1377 de 2013**, asegurando la protección y privacidad de los datos personales de los usuarios. |
| **Regulatoria** | Toda la información personal debe encriptarse y almacenarse de manera segura, con controles de acceso estrictos. |
| **Infraestructura** | El sistema debe garantizar **alta disponibilidad**, con balanceo de carga y recuperación ante fallos. |
| **Infraestructura** | Se debe implementar **Prometheus y Grafana** para el monitoreo de rendimiento y detección de fallos en tiempo real. |
| **Negocio** | Los permisos de acceso están restringidos a **clientes, administradores y repartidores**, asegurando que cada usuario tenga acceso solo a sus funcionalidades correspondientes. |

