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

# Niveles de acceso para los roles de usuarios

Las tablas siguientes muestran el nivel de acceso para cada uno de los roles de usuario predeterminados.

Las tablas muestran niveles de acceso para:
- [Operaciones de dispositivo](#user-device-ops)
- [Operaciones de registro](#user-log-ops)
- [Operaciones de memoria caché](#user-cache-ops)
<!-- [Historian Operations](#user-historian) -->
- [Operaciones de organización](#user-org-ops)
- [Operaciones de control de acceso](#user-access-ops)
- [Operaciones analíticas](#user-analytics-ops)
- [Operaciones de terceros](#user-third-party)  
<!-- - [Risk Management Operations](#user-risk-mgt) -->

## Permisos del rol de usuario {: #user-roles}

### Operaciones de dispositivo {: #user-device-ops}

Operaciones de dispositivo ||| Roles de usuario|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrador** | **Operador** | **Desarrollador** | **Analista** | **Lector**
Crear, actualizar o suprimir dispositivos | X | X | X | - | -
Ver dispositivos | X | X | X | X | X
Activar dispositivo | X | X | X | - | -
Publicar un suceso | - | - | - | - | -
Suscribirse a un suceso | X | X | X | X | X
Publicar un mandato | X | X | X | - | -
Suscribirse a un mandato | - | - | - | - | -
Iniciar la acción de gestión de dispositivo | X | X | X | - | -
Ver acciones de gestión de dispositivos | X | X | X | X | X
Borrar acciones de gestión de dispositivos | X | X | X | - | -
Gestionar paquetes de acción de gestión de dispositivos | X | X | X | - | -
Crear, actualizar o suprimir tipos de dispositivos | X | X | X | - | -
Ver tipos de dispositivos | X | X | X | X | X
Gestionar los registros de diagnóstico | X | X | X | - | -
Ver los registros de diagnóstico | X | X | X | - | -

### Operaciones de registro {: #user-log-ops}

Operaciones de registro ||| Roles de usuario|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrador** | **Operador** | **Desarrollador** | **Analista** | **Lector**
Ver los registros del servidor | X | X | X | X | X

### Operaciones de memoria caché {: #user-cache-ops}

Operaciones de memoria caché ||| Roles de usuario|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrador** | **Operador** | **Desarrollador** | **Analista** | **Lector**
Ver datos en tiempo real (memoria caché de sucesos) | X | X | X | X | X
Gestionar datos activos (memoria caché de sucesos) | X	| X | X |	X	| -

### Operaciones de organización {: #user-org-ops}

Operaciones de organización ||| Roles de usuario|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrador** | **Operador** | **Desarrollador** | **Analista** | **Lector**
Configurar parámetros de almacenamiento|	X| - |-|-|-				
Configurar proveedor de autenticación|	X|-|-|-|-				
Crear, ver, actualizar, suprimir la configuración del correo	|X|-|-|-|-				
Ver proveedores de correo IoTP disponibles	|X|	X|-|-|-			
Crear, ver, actualizar, suprimir plantillas de correo	|X	|X	|-|-|-		
Crear, actualizar, suprimir usuarios	|X|	X|-|-|-			
Ver usuarios	|X|	X|	X|	X|-
Crear, actualizar, suprimir invitaciones de usuario|	X	|X	| -|-|-		
Ver invitaciones de usuario	|X	|X	|- |- |-		
Completar invitación	|X|	X|	X|	X|	X
Crear, actualizar, suprimir claves de API	|X	|X	| -|-|-		
Ver claves de API	|X	|X	|- |- |-		
Ver información de uso de la organización	|X	|X	| -|-|-		

### Operaciones de control de acceso {: #user-access-ops}

Operaciones de control de acceso ||| Roles de usuario|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrador** | **Operador** | **Desarrollador** | **Analista** | **Lector**
Ver propiedades de los usuarios, incluidos los derechos de acceso	|X|	X|	X|	X| -
Ver propiedades de los propios usuarios, incluidos los derechos de acceso	|X|	X|	X|	X|	X
Gestionar usuarios, incluidos los derechos de acceso	|X	|X	|-|-|-		
Ver las propiedades de claves de API, incluidos los derechos de acceso|	X|	X|	X|	X|-
Ver las propiedades de las propias claves de API, incluidos los derechos de acceso	|-|	-|	-| -| -		
Crear, actualizar, suprimir la clave de API, incluidos los derechos de acceso	|X	|X	|-|-|-		
Ver las propiedades del dispositivo, incluidos los derechos de acceso	|X|	X|	X|	X|	X
Ver las propiedades propias del dispositivo, incluidos los derechos de acceso	|-	|- |- |- |-
Crear, actualizar, suprimir el dispositivo, incluidos los derechos de acceso	|X|	X|	X|	-| -
Ver roles	|X	|X	|X	|X	|X
Crear, actualizar, suprimir roles personalizados	|X	|X |- |- |-
Ver operaciones*	|X	|X	|X	|X	|X

### Operaciones analíticas {: #user-analytics-ops}

Operaciones analíticas ||| Roles de usuario|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrador** | **Operador** | **Desarrollador** | **Analista** | **Lector**
Ver reglas analíticas|	X|	X|	X|	X|	X
Gestionar reglas analíticas|	X|	X|	X|	X| -
Ver acciones analíticas|	X|	X|	X|	X|	X
Gestionar acciones analíticas|	X|	X|	X|	X| -
Ver alertas analíticas|	X|	X|	X|	X|	X
Ver esquemas de mensajes analíticos|	X|	X|	X|	X|	X
Gestionar esquemas de mensaje analítico|	X|	X|	X|	X| -

### Operaciones de servicios de terceros {: #user-third-party}

Operaciones de servicios de terceros ||| Roles de usuario|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrador** | **Operador** | **Desarrollador** | **Analista** | **Lector**
Procesar notificaciones por lotes desde la plataforma externa	|X|	X	|X |-|-
Procesar notificaciones por lotes y enviarlas a la plataforma externa	|X|	X	|X| -| -
Publicar un suceso para un dispositivo	|X|	X	|X|	- |-
Suscribirse a sucesos desde un dispositivo	|X	|X	|X |-| -
Establecer un URL de devolución de llamada para la plataforma externa	|X	|X	|X|	-| -
Establecer el nivel de suscripción de la plataforma externa|	X|	X|	X |- |-
Obtener el estado de salud del conector	|X|	X	|X	|- |-
Verificar si un sistema externo está activo y validar las credenciales	|X	|X|	X	|- |-
