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

# Niveles de acceso para los roles de pasarelas

Las tablas siguientes muestran el nivel de acceso para cada uno de los roles de pasarela.

Las tablas muestran niveles de acceso para:
- [Operaciones de dispositivo](#gateway-device-ops)
- [Operaciones de registro](#gateway-log-ops)
- [Operaciones de memoria caché](#gateway-cache-ops)
<!-- [Historian Operations](#gateway-historian) -->
- [Operaciones de organización](#gateway-org-ops)
- [Operaciones de control de acceso](#gateway-access-ops)
- [Operaciones analíticas](#gateway-analytics-ops)
- [Operaciones de terceros](#gateway-third-party)  
<!-- - [Risk Management Operations](#gateway-risk-mgt) -->

## Roles de pasarela
{: #gateway-roles}

### Operaciones de dispositivo {: #gateway-device-ops}

Operaciones de dispositivo || Roles de pasarela|
:--------: | ---------------------|------------------------
           | **Pasarela estándar** | **Pasarela privilegiada**
Crear, actualizar o suprimir dispositivos|-|X
Ver dispositivos|X|X
Activar dispositivo|-|X
Publicar un suceso|X|X
Suscribirse a un suceso|-|-
Publicar un mandato|-|-
Suscribirse a un mandato|X|X
Iniciar acción de gestión de dispositivos|X|X
Ver acciones de gestión de dispositivos|X|X
Borrar acciones de gestión de dispositivos|-|-
Gestionar paquetes de acción de gestión de dispositivos|-|X
Crear, actualizar o suprimir tipos de dispositivos|-|-
Ver tipos de dispositivos|X|X
Gestionar los registros de diagnóstico|-|-
Ver los registros de diagnóstico|-|-

### Operaciones de registro {: #gateway-log-ops}

Operaciones de registro || Roles de pasarela|
:--------: | ---------------------|------------------------
           | **Pasarela estándar** | **Pasarela privilegiada**
Ver los registros del servidor|-|-

### Operaciones de memoria caché {: #gateway-cache-ops}

Operaciones de memoria caché || Roles de pasarela|
:--------: | ---------------------|------------------------
           | **Pasarela estándar** | **Pasarela privilegiada**
Ver datos en tiempo real (memoria caché de sucesos)|-|-
Gestionar datos en tiempo real (memoria caché de sucesos)|-|-


### Operaciones de organización {: #gateway-org-ops}

Operaciones de organización || Roles de pasarela|
:--------: | ---------------------|------------------------
           | **Pasarela estándar** | **Pasarela privilegiada**
Configurar parámetros de almacenamiento|-|-
Configurar proveedor de autenticación|-|-
Crear, ver, actualizar o suprimir la configuración del correo|-|-
Ver los proveedores de correo disponibles|-|-
Crear, ver, actualizar o suprimir las plantillas de correo|-|-
Crear, actualizar o suprimir usuarios|-|-
Ver usuarios|-|-
Crear, actualizar, suprimir invitaciones de usuario|-|-
Ver invitaciones de usuario|-|-
Completar invitación|-|-
Crear, actualizar o suprimir claves de API|-|-
Ver claves de API|-|-
Ver información de uso de la organización|-|-

### Operaciones de control de acceso {: #gateway-access-ops}

Operaciones de control de acceso || Roles de pasarela|
:--------: | ---------------------|------------------------
           | **Pasarela estándar** | **Pasarela privilegiada**
Ver las propiedades de usuarios (incl. los derechos de acceso)|-|-
Ver las propias propiedades de los usuarios (incl. los derechos de acceso)|-|-
Gestionar usuarios (incl. los derechos de acceso)|-|-
Ver las propiedades de claves de API (incl. los derechos de acceso)|-|-
Ver las propias propiedades de la clave de API (incl. los derechos de acceso)|-|-
Crear, actualizar o suprimir claves de API (incl. los derechos de acceso)|-|-
Ver las propiedades del dispositivo (incl. los derechos de acceso)|X|X
Ver las propias propiedades del dispositivo (incl. los derechos de acceso)|X|X
Crear, actualizar, suprimir dispositivo (incl. los derechos de acceso)|-|X
Ver roles|-|-
Crear, actualizar, suprimir roles personalizados|-|-
Ver operaciones|-|-

### Operaciones analíticas {: #gateway-analytics-ops}

Operaciones analíticas || Roles de pasarela|
:--------: | ---------------------|------------------------|
           | **Pasarela estándar** | **Pasarela privilegiada** |
Ver reglas analíticas|-|-
Gestionar reglas analíticas|-|-
Ver acciones analíticas|-|-
Gestionar acciones analíticas|-|-
Ver alertas analíticas|-|-
Ver esquemas de mensajes analíticos|-|-
Gestionar esquemas de mensajes analíticos|-|-

### Operaciones de servicios de terceros {: #gateway-third-party}

Operaciones de servicios de terceros || Roles de pasarela|
:--------: | ---------------------|------------------------
           | **Pasarela estándar** | **Pasarela privilegiada**
Procesar notificaciones por lotes desde la plataforma externa|-|-
Procesar notificaciones por lotes y enviarlas a la plataforma externa|-|-
Publicar un suceso para un dispositivo|-|-
Suscribirse a sucesos desde un dispositivo|-|-
Establecer un URL de devolución de llamada para la plataforma externa|-|-
Establecer el nivel de suscripción de la plataforma externa|-|-
Obtener el estado de salud del conector|-|-
Verificar si un sistema externo está activo y validar las credenciales|-|-
