---

copyright:

  years: 2015, 2016
lastupdated: "2017-05-17"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Permisos y roles de usuario
{: #userroles}

Gestione usuarios en los servicios de infraestructura y plataforma {{site.data.keyword.Bluemix_notm}} desde la página **Usuarios** de su cuenta. Desde la página Usuarios hay también un enlace a la página Directorio del equipo, si solo desea gestionar el acceso de Cloud Foundry de los usuarios de la plataforma a las organizaciones y los espacios. Sin embargo, no tiene que dejar la página Usuarios para gestionar el acceso de Cloud Foundry.
{:shortdesc}

Para acceder a la página Usuarios, en el menú {{site.data.keyword.Bluemix_notm}} pulse **Gestionar** &gt; **Cuenta** &gt; **Usuarios**. Los propietarios de cuentas llevan a cabo todas las operaciones en las organizaciones y los espacios incluida la gestión de usuarios y sus roles asignados. Los gestores de espacios y organizaciones también tienen acceso para gestionar roles.  

Si usted es un usuario que ha sido añadido a otra cuenta personal, y desea ver sus permisos y roles asignados, vaya a **Gestionar** &gt; **Seguridad** &gt; **Identity & Access** &gt; **Usuarios** y, a continuación, pulse en su nombre. 

## Roles de cuenta
{: #userrolesinfo}

En el nivel de cuenta, hay dos roles que permiten acceder a distintas características de gestiones de cuentas:

| Rol de cuenta | Permisos |
|----------------|---------|
|Propietario | Un propietario para la cuenta tiene acceso a su perfil, directorio de equipo, información de facturación, notificaciones de gasto y panel de control de uso. En la página de usuarios o de directorio del equipo, el propietario puede invitar a nuevos miembros del equipo y ajustar roles. El propietario también puede añadir créditos promocionales, establecer o cambiar el límite de facturación, establecer acceso de servicios y gestionar organizaciones y espacios. |
|Miembro | Un miembro tiene acceso a su perfil, directorio de equipo y créditos de cuenta y límites de facturación en la cabecera de {{site.data.keyword.Bluemix_notm}}. Sin embargo, en la página de directorio de equipo, un miembro solamente puede ver los miembros del equipo dentro de la cuenta. |
{:caption="Tabla 1. Permisos y roles de cuenta" caption-side="top"}

Todos los nuevos usuarios se añaden como un miembro de la cuenta. Puede asignar roles de organización y espacio a invitados para habilitar vistas y permisos específicos en {{site.data.keyword.Bluemix_notm}}. De forma predeterminada, a los nuevos miembros añadidos a una organización, excepto en un entorno local o dedicado, se les asigna el rol de organización de auditor. Para un espacio específico, puede elegir asignar el rol de desarrollador o auditor a los invitados. Una vez que los invitados aceptan la invitación y se unen a {{site.data.keyword.Bluemix_notm}}, puede editar sus roles en la página Usuarios o Directorio del equipo.

## Roles de Cloud Foundry
{: #cfroles}

Los roles de Cloud Foundry incluyen permisos de acceso para las organizaciones y espacios definidos dentro de la cuenta. Los siguientes roles se pueden asignar a nivel de organización:

| Rol de organización | Permisos |
|-------------------|-------------|
|Gestor | Los gestores de organización pueden crear, ver, editar o suprimir espacios dentro de la organización, ver la cuota y el uso de la organización, invitar a miembros del equipo a la organización, gestionar quién tiene acceso a la organización y sus roles en la organización, y gestionar dominios personalizados para la organización. |
|Gestor de facturación | Los gestores de facturación pueden ver la información de uso de tiempo de ejecución y servicio para la organización de la página Panel de control de uso.  |
|Auditor | Los auditores de organización pueden ver el contenido de aplicación y servicio en la organización. Los auditores también pueden ver los usuarios de la organización y sus roles asignados, y la cuota para la organización. Este rol se asigna a todos los invitados de forma predeterminada, excepto en entornos locales o dedicados. |
{:caption="Tabla 2. Permisos y roles de organización" caption-side="top"}

Los siguientes roles se pueden asignar a nivel de espacio:

| Rol de espacio | Permisos |
|------------|-------------|
|Gestor | Los gestores de espacios pueden añadir usuarios existentes y gestionar roles dentro del espacio. Los gestores de espacios también pueden ver el número de instancias, enlaces de servicio y uso de recursos para cada aplicación en el espacio. |
|Desarrollador | Los desarrolladores de espacios pueden crear, suprimir y gestionar aplicaciones y servicios dentro del espacio. Algunas de las tareas de gestión incluyen el desarrollo de apps, el inicio o la detención de apps, el cambio de nombre de una app, la supresión de una app, el enlace o desenlace de un servicio con una aplicación, ver el número o instancias, enlaces de servicio y uso de recursos para cada aplicación en el espacio. Además, el desarrollador de espacios puede asociar un URL interno o externo con una aplicación en el espacio.   |
|Auditor | Los auditores del espacio tienen acceso de solo lectura a toda la información sobre el espacio, como la información sobre el número de instancias, enlaces de servicio y uso de recursos para cada aplicación en el espacio. |
{:caption="Tabla 3. Permisos y roles de espacio" caption-side="top"}

**Nota**: Los usuarios que tienen asignado el rol de espacio de gestor o desarrollador pueden acceder a la variable de entorno VCAP_SERVICES. Sin embargo, un usuario que tienen asignado el rol de auditor no puede acceder a VCAP_SERVICES.

## Políticas y roles para la gestión de acceso e identidades
{: #iamusermanpol}

A los propietarios de las cuentas se les asigna de forma automática el rol de administrador de acceso de cuenta para la gestión de acceso e identidades que permite asignar y gestionar políticas de servicio. Este tipo de control de acceso permite asignar políticas por servicio o instancia de servicio para permitir niveles de acceso para gestionar recursos y usuarios dentro del contexto asignado. 

### Políticas de servicio 

Una política asigna a un usuario uno o varios roles sobre un conjunto de recursos utilizando una combinación de atributos para definir el conjunto de recursos aplicable. Cuando se asigna una política a un usuario, primero hay que especificar el servicio que se le va a asignar, incluida una opción de asignar todos los servicios disponibles. A continuación, se debe seleccionar el rol o los roles que desea asignar. En función del servicio que seleccione, podrían haber disponibles opciones de configuración adicionales. 

Puede asignar y gestionar políticas si tiene el rol adecuado. En la tabla siguiente se muestran las tareas de gestión de políticas y el rol necesario para cada una de ellos.

{: #iamui_table1}

| Acción | Rol necesario |
|----------|---------|
| Crear una política en una cuenta | Administrador de acceso de cuenta |
| Crear una política en todos los servicios de una cuenta | Administrador de acceso de cuenta |
| Crear una política en todas instancias de servicio de una cuenta | Administrador de acceso de cuenta |
| Crear una política en un servicio de una cuenta | Administrador de acceso de cuenta o administrador en el servicio en la cuenta |
| Crear una instancia de servicio | Editor o administrador de acceso de cuenta o editor o administrador en el servicio en la cuenta  |
| Crear una política en una instancia de servicio | Administrador de acceso de cuenta o administrador en el servicio en la cuenta o administrador en la instancia de servicio  |
{: caption="Tabla 4. Tareas administrativas para gestionar políticas de servicios habilitados para identidad y acceso" caption-side="top"}

### Roles de política de servicio
{: #iamusermanrol}

Los roles son una colección de acciones; las acciones que están correlacionadas con estos roles son específicas del servicio. Consulte la documentación del servicio seleccionado para obtener más información sobre los tipos de acciones que permite cada rol. 

Además de las descripciones de los roles que se proporcionan en la consola, la siguiente tabla proporciona ejemplo de algunas de las tareas que los usuarios asignados a cada rol podría hacer dependiendo del servicio seleccionado.  

{: #iamui_table2}

| Rol | Descripción de acciones | Acciones de ejemplo|
|:-----------------|:-----------------|:-----------------|
| Visor | Realiza acciones que no cambian el estado; solo acciones de lectura | <ul><li>Enumerar dispositivos</li><li>Leer objeto de almacenamiento</li><li>Ejecutar consultas</li><li>Ejecutar búsquedas</li></ul>|
| Editor | Realiza acciones que modifican el estado y crean o suprimen subrecursos |<ul><li>Crear o suprimir máquinas virtuales</li><li>Conectar almacenamiento</li><li>Rearrancar</li><li>Iniciar o detener</li><li>Renombrar</li></ul> |
| Administrador | Realiza todas las acciones, incluida la capacidad para gestionar el control de accesos |<ul><li>Invitar a usuarios</li><li>Crear o suprimir máquinas virtuales</li><li>Actualizar políticas de acceso de usuarios</li><li>Enumerar dispositivos</li><li>Conectar almacenamiento</li><li>Rearrancar</li><li>Iniciar o detener</li><li>Renombrar</li><li>Hacer copia de seguridad y restaurar</li></ul>|
{: caption="Tabla 5. Tareas administrativas para gestionar políticas de servicios habilitados para identidad y acceso" caption-side="top"}

## Permisos de infraestructura
{: #infrapermissions}

Si tiene permiso para asignar roles de infraestructura, podría establecer los siguientes permisos para el usuario:  

| Permisos de infraestructura | Descripción de acciones |
|---------------------------|------------------------|
|Solo visualización | Los usuarios con este permiso solo pueden ver los elementos del sistema.|
|Usuario básico | Los usuarios con este permiso pueden realizar acciones básicas en el sistema, como, por ejemplo, añadir una incidencia y gestionar dispositivos. |
|Superusuario | Los usuarios con este permiso pueden realizar todas las acciones disponibles en el sistema. |
{:caption="Tabla 6. Permisos de infraestructura" caption-side="top"}

