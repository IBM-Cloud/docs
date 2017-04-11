---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Niveles de acceso para los roles de aplicaciones

Las tablas siguientes muestran el nivel de acceso para cada uno de los roles de la aplicación.

Las tablas muestran niveles de acceso para:
- [Operaciones de dispositivo](#app-device-ops)
- [Operaciones de registro](#app-log-ops)
- [Operaciones de memoria caché](#app-cache-ops)
<!-- [Historian Operations](#app-historian) -->
- [Operaciones de organización](#app-org-ops)
- [Operaciones de control de acceso](#app-access-ops)
- [Operaciones analíticas](#app-analytics-ops)
- [Operaciones de terceros](#app-third-party)  
<!-- - [Risk Management Operations](#app-risk-mgt) -->

## Roles de aplicación
{: #app-roles}

### Operaciones de dispositivo {: #app-device-ops}

Operaciones de dispositivo ||| Roles de aplicación||||
:--------: | -------------|-------------|---------------|-----|---
           | **Aplicación estándar** | **Aplicación de operaciones** | **Aplicación de confianza de programa de fondo** | **Aplicación de procesador de datos** | **Aplicación de visualización** | **Aplicación de dispositivo**
Crear, actualizar o suprimir dispositivos|X|X|X|-|-|-
Ver dispositivos|X|X|X|X|X|-
Activar dispositivo|X|X|X|-|-|-
Publicar un suceso|X|-|X|-|-|X
Suscribirse a un suceso|X|X|X|X|X|X
Publicar un mandato|X|X|X|X|-|-
Suscribirse a un mandato|X|-|X|-|-|X
Iniciar acción de gestión de dispositivos|X|X|-|-|-|-
Ver acciones de gestión de dispositivos|X|X|-|-|-|X
Borrar acciones de gestión de dispositivos|X|X|-|-|-|-
Gestionar paquetes de acción de gestión de dispositivos|X|X|-|-|-|-
Crear, actualizar o suprimir tipos de dispositivos|X|X|X|-|-|-
Ver tipos de dispositivos|X|X|X|X|-|-
Gestionar registros de diagnóstico|X|X|-|-|-|X
Ver registros de diagnóstico|X|X|X|-|-|-

### Operaciones de registro {: #app-log-ops}

Operaciones de registro ||| Roles de aplicación||||
:--------: | -------------|-------------|---------------|-----|---
           | **Aplicación estándar** | **Aplicación de operaciones** | **Aplicación de confianza de programa de fondo** | **Aplicación de procesador de datos** | **Aplicación de visualización** | **Aplicación de dispositivo**
Ver registros de servidor|X|X|X|-|-|-

### Operaciones de memoria caché {: #app-cache-ops}

Operaciones de memoria caché ||| Roles de aplicación||||
:--------: | -------------|-------------|---------------|-----|---
           | **Aplicación estándar** | **Aplicación de operaciones** | **Aplicación de confianza de programa de fondo** | **Aplicación de procesador de datos** | **Aplicación de visualización** | **Aplicación de dispositivo**
Ver datos activos (memoria caché de sucesos)|X|X|X|X|X|X
Gestionar datos activos (memoria caché de sucesos)|X|X|X|X|X|X

### Operaciones de organización {: #app-org-ops}

Operaciones de organización ||| Roles de aplicación||||
:--------: | -------------|-------------|---------------|-----|---
           | **Aplicación estándar** | **Aplicación de operaciones** | **Aplicación de confianza de programa de fondo** | **Aplicación de procesador de datos** | **Aplicación de visualización** | **Aplicación de dispositivo**
Configurar parámetros de almacenamiento|-|-|-|-|-|-
Configurar proveedor de autenticación|-|-|-|-|-|-
Crear, ver, actualizar o suprimir la configuración del correo|-|-|-|-|-|-
Ver los proveedores de correo disponibles|X|X|-|-|-|-
Crear, ver, actualizar o suprimir las plantillas de correo|X|X|-|-|-|-
Crear, actualizar o suprimir usuarios|-|X|-|-|-|-
Ver usuarios|X|X|-|-|-|-
Crear, actualizar o suprimir invitaciones de usuario|-|X|-|-|-|-
Ver invitaciones de usuario|X|X|-|-|-|-
Completar invitación|X|X|-|-|-|-
Crear, actualizar o suprimir claves de API|-|X|-|-|-|-
Ver claves de API|X|X|-|-|-|-
Ver información de uso de la organización|X|X|-|-|-|-

### Operaciones de control de acceso {: #app-access-ops}

Operaciones de control de acceso ||| Roles de aplicación||||
:--------: | -------------|-------------|---------------|-----|---
           | **Aplicación estándar** | **Aplicación de operaciones** | **Aplicación de confianza de programa de fondo** | **Aplicación de procesador de datos** | **Aplicación de visualización** | **Aplicación de dispositivo**
Ver propiedades de usuarios, incluidos los derechos de acceso|X|X|-|-|-|-
Ver propiedades de los propios usuarios, incluidos los derechos de acceso|-|-|-|-|-|-
Gestionar usuarios, incluidos los derechos de acceso|-|X|-|-|-|-
Ver las propiedades de claves de API, incluidos los derechos de acceso|X|X|-|-|-|-
Ver las propiedades de las propias claves de API, incluidos los derechos de acceso|X|X|X|X|X|X
Crear, actualizar, suprimir claves de API, incluidos los derechos de acceso|-|X|-|-|-|-
Ver las propiedades del dispositivo, incluidos los derechos de acceso|X|X|X|X|X|-
Ver las propiedades del propio dispositivo, incluidos los derechos de acceso|-|-|-|-|-|-
Crear, actualizar, suprimir el dispositivo, incluidos los derechos de acceso|X|X|X|-|-|-
Ver roles|X|X|-|-|-|-
Crear, actualizar, suprimir roles personalizados|-|X|-|-|-|-
Ver operaciones*|X|X|-|-|-|-

### Operaciones analíticas {: #app-analytics-ops}

Operaciones analíticas ||| Roles de aplicación||||
:--------: | -------------|-------------|---------------|-----|---
           | **Aplicación estándar** | **Aplicación de operaciones** | **Aplicación de confianza de programa de fondo** | **Aplicación de procesador de datos** | **Aplicación de visualización** | **Aplicación de dispositivo**
Ver reglas analíticas|X|X|-|X|X|-
Gestionar reglas analíticas|X|X|-|X|-|-
Ver acciones analíticas|X|X|-|X|X|-
Gestionar acciones analíticas|X|X|-|X|X|-
Ver alertas analíticas|X|X|-|X|X|X
Ver esquemas de mensajes analíticos|X|X|-|X|X|-
Gestionar esquemas de mensajes analíticos|X|X|-|X|-|-

### Operaciones de servicios de terceros {: #app-third-party}

Operaciones de servicios de terceros ||| Roles de aplicación||||
:--------: | -------------|-------------|---------------|-----|---
           | **Aplicación estándar** | **Aplicación de operaciones** | **Aplicación de confianza de programa de fondo** | **Aplicación de procesador de datos** | **Aplicación de visualización** | **Aplicación de dispositivo**
Procesar notificaciones por lotes desde la plataforma externa|X|X|-|-|-|-
Procesar notificaciones por lotes y enviarlas a la plataforma externa|X|X|-|-|-|-
Publicar un suceso para un dispositivo|X|X|-|-|-|-
Suscribirse a sucesos desde un dispositivo|X|X|-|-|-|-
Establecer un URL de devolución de llamada para la plataforma externa|X|X|-|-|X|-
Establecer el nivel de suscripción de la plataforma externa|X|X|-|-|X|-
Obtener el estado de salud del conector|X|X|X|-|X|-
Verificar si un sistema externo está activo y validar las credenciales|X|X|X|-|X|-
