---

copyright:

  years: 2015, 2016
lastupdated: "2017-03-01"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestión del acceso de usuarios y roles a los servicios de Cloud Foundry en Directorio del equipo
{: #userroles}

Puede gestionar el acceso a los servicios Cloud Foundry asignados a los usuarios de la plataforma desde la página Directorio del equipo de su cuenta. Puede gestionar los miembros del equipo existentes y sus roles en su organización y en sus espacios.
{:shortdesc}

Puede acceder al Directorio del equipo de su cuenta desde un enlace situado en la parte superior de la nueva página Usuarios. Para acceder a la página Usuarios, en el menú {{site.data.keyword.Bluemix_notm}} pulse **Gestionar** &gt; **Cuenta** &gt; **Usuarios**.

Los propietarios de cuentas llevan a cabo todas las operaciones en las organizaciones y los espacios incluida la gestión de miembros del equipo y sus roles asignados. Los gestores de organización tienen acceso para gestionar roles. Los gestores de espacio pueden utilizar la página **Gestionar organizaciones** para añadir miembros de cuentas existentes al espacio y ajustar sus roles. Consulte la siguiente información para aprender más sobre roles.

## Roles de usuario
{: #userrolesinfo}

En el nivel de cuenta, hay dos roles que permiten acceder a distintas características de gestiones de cuentas:

| Rol de cuenta | Permisos |
|----------------|---------|
|Propietario | Un propietario para la cuenta tiene acceso a su perfil, directorio de equipo, información de facturación, notificaciones de gasto y panel de control de uso. En la página de directorio del equipo, el propietario puede invitar a nuevos miembros del equipo y ajustar roles. El propietario también puede añadir créditos promocionales, establecer o cambiar el límite de facturación, establecer acceso de servicios y gestionar organizaciones y espacios. |
|Miembro | Un miembro tiene acceso a su perfil, directorio de equipo y créditos de cuenta y límites de facturación en la cabecera de {{site.data.keyword.Bluemix_notm}}. Sin embargo, en la página de directorio de equipo, un miembro solamente puede ver los miembros del equipo dentro de la cuenta. |
{:caption="Table 1. Account roles and permissions" caption-side="top"}

Todos los miembros del equipo se añaden como un miembro de la cuenta. Puede asignar roles de organización y espacio a invitados para habilitar vistas y permisos específicos en {{site.data.keyword.Bluemix_notm}}. De forma predeterminada, a los nuevos miembros añadidos a una organización, excepto en un entorno local o dedicado, se les asigna el rol de organización de auditor. Para un espacio específico, puede elegir asignar el rol de desarrollador o auditor a los invitados. Una vez que los invitados aceptan la invitación y se unen a {{site.data.keyword.Bluemix_notm}}, puede editar sus roles en la página Directorio del equipo.

Los siguientes roles se pueden asignar a nivel de organización:

| Rol de organización | Permisos |
|-------------------|-------------|
|Gestor | Los gestores de organización pueden crear, ver, editar o suprimir espacios dentro de la organización, ver la cuota y el uso de la organización, invitar a miembros del equipo a la organización, gestionar quién tiene acceso a la organización y sus roles en la organización, y gestionar dominios personalizados para la organización. |
|Gestor de facturación | Los gestores de facturación pueden ver la información de uso de tiempo de ejecución y servicio para la organización de la página Panel de control de uso.  |
|Auditor | Los auditores de organización pueden ver el contenido de aplicación y servicio en la organización. Los auditores también pueden ver los miembros del equipo de la organización y sus roles asignados, y la cuota para la organización. Este rol se asigna a todos los invitados de forma predeterminada, excepto en entornos locales o dedicados. |
{:caption="Table 2. Organization roles and permissions" caption-side="top"}

Los siguientes roles se pueden asignar a nivel de espacio:

| Rol de espacio | Permisos |
|------------|-------------|
|Gestor | Los gestores de espacios pueden añadir miembros de equipo existentes y gestionar roles dentro del espacio. Los gestores de espacios también pueden ver el número de instancias, enlaces de servicio y uso de recursos para cada aplicación en el espacio. |
|Desarrollador | Los desarrolladores de espacios pueden crear, suprimir y gestionar aplicaciones y servicios dentro del espacio. Algunas de las tareas de gestión incluyen el desarrollo de apps, el inicio o la detención de apps, el cambio de nombre de una app, la supresión de una app, el enlace o desenlace de un servicio con una aplicación, ver el número o instancias, enlaces de servicio y uso de recursos para cada aplicación en el espacio. Además, el desarrollador de espacios puede asociar un URL interno o externo con una aplicación en el espacio.   |
|Auditor | Los auditores del espacio tienen acceso de solo lectura a toda la información sobre el espacio, como la información sobre el número de instancias, enlaces de servicio y uso de recursos para cada aplicación en el espacio. |
{:caption="Table 3. Space roles and permissions" caption-side="top"}

**Nota**: los miembros del equipo que tienen asignado el rol de espacio de gestor o desarrollador puede acceder a la variable de entorno VCAP_SERVICES. Sin embargo, un miembro del equipo que tienen asignado el rol de auditor no puede acceder a VCAP_SERVICES.

## Editar roles
{: #editinguserroles}

Los propietarios de cuentas y gestores de organizaciones pueden editar roles de organización y espacio para miembros del equipo existentes en la página Directorio del equipo. 

1. Localice y seleccione el miembro del equipo cuyos roles desea editar.
2. Pulse **Ver roles**.
3. Seleccione o elimine la selección de rol de espacio para modificar el acceso al espacio para el miembro del equipo.
4. Pulse **Guardar**.

Los gestores de espacio pueden editar roles para los miembros del equipo en su espacio. 

1. Localice y seleccione el miembro del equipo cuyos roles desea editar.
2. Pulse **Ver roles**.
3. Pulse **Ver espacios**.
4. Seleccione o quite la marca de selección de la opción de rol de espacio para el rol que desea añadir o eliminar para el miembro del equipo.
5. A continuación, pulse **Guardar**.

## Invitación a miembros del equipo
{: #inviteteammembers}

Puede añadir un usuario en la ventana Directorio del equipo si el ID de usuario no es una cuenta enlazada y si es un propietario de cuenta o un gestor de la organización. Cuando añade nuevos miembros del equipo, excepto en un entorno local o dedicado, se les asignan automáticamente los roles de auditor. Puede cambiar los roles más adelante en la página Directorio del equipo. Para invitar a un miembro del equipo, realice estos pasos:

<ol>
<li>Pulse **Invitar a un usuario**.</li>
<li>Escriba la dirección de correo electrónico del usuario que desea invitar. </li>
<li>Seleccione el rol que se va a asignar para la organización.</li>
<li>Seleccione el rol que se va a asignar para un espacio o espacios de la organización.</li>
<li>Seleccione la opción para confirmar que tiene responsabilidad financiera para todos los cargos que se producen en la cuenta.</li>
<li>Pulse **Invitar**. </li>
</ol>

El usuario se añade a la lista que aparece de los miembros del equipo para la cuenta.

## Eliminación de miembros del equipo
{: #removingteammembers}

Si el usuario se ha añadido desde el Directorio del equipo y no es una cuenta enlazada, los propietarios de cuentas y gestores de organizaciones pueden eliminar miembros del equipo de una cuenta utilizando la página Directorio del equipo. Para eliminar a un miembro del equipo, realice estos pasos:

1. Localice el usuario que desea eliminar y pulse el icono **Eliminar usuario** ![icono Eliminar](../icons/icon_remove_teamuser.svg). 
2. Pulse **Eliminar** para confirmar que desea eliminar el usuario especificado de la cuenta.

El usuario se elimina de la lista que aparece de los miembros del equipo para la cuenta.
