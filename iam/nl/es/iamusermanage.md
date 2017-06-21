---

copyright:

  years: 2015, 2017

lastupdated: "2017-05-17"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestión de accesos y usuarios
{: #iamusermanage}

Según las opciones de acceso que esté autorizado a gestionar, puede ver y gestionar usuarios de la cuenta o de la organización. Como propietario de una cuenta, puede gestionar cualquiera de las opciones de acceso que administre de los usuarios y el acceso que asignará a los mismos en la cuenta actual. {:shortdesc}

Complete los siguientes pasos para gestionar los usuarios de su cuenta: 

1. Desde la barra de menús, pulse **Gestionar** &gt; **Cuenta** &gt; **Usuarios**. La ventana Usuarios muestra una lista de los usuarios con sus direcciones de correo electrónico y el estado actual en las cuentas que gestiona. 
2. Seleccione el nombre de usuario o pulse **Gestionar usuario** desde el menú **Acciones**.  
3. A continuación, dependiendo de los accesos que pueda gestionar, actualice el acceso para el usuario en las secciones de roles de Cloud Foundry o políticas de servicios, o pulse el enlace para acceder a la página Asignación de acceso de infraestructura. 

Revise las siguientes secciones para obtener información adicional sobre la gestión de cada tipo de acceso e información sobre cómo utilizar el Directorio del equipo. 

Si necesita revisar su acceso asignado en una cuenta a la que ha sido añadido, complete los siguientes pasos: 

1. Desde la barra de menús, pulse **Gestionar** &gt; **Seguridad** &gt; **Identity & Access** &gt; **Usuarios**.  
2. Seleccione su nombre.  
3. Revise los roles que tiene asignados. 

Si necesita cambiar su política de servicio o rol, debe ponerse en contacto con el gestor de la organización o el propietario de la cuenta para actualizar el rol de Cloud Foundry o el administrador para el servicio o instancia de servicio para actualizar la política de servicio. 

## Acceso de Cloud Foundry
{: #iammancfser}

Para gestionar el acceso a espacios y organizaciones de la cuenta, debe ser el propietario de la cuenta, un gestor de organización o un gestor de espacio: 

1. Desde la barra de menús, pulse **Gestionar** &gt; **Seguridad** &gt; **Identity & Access** &gt; **Usuarios**.  
2. Seleccione el usuario al que desea editar sus roles. 
3. En el menú **Acciones** en la sección de Cloud Foundry, puede: 

  * Eliminar el usuario de la organización
  * Editar el rol de la organización
  * Editar el rol de espacio

También puede añadir un usuario a otra organización pulsando **Asignar organización**, si es el gestor de una organización a la que todavía no pertenezca el usuario.  


## Servicios habilitados para identificación y acceso
{: #iammanidaccser}

Para gestionar políticas de servicio o asignar nuevas políticas de servicio a los usuarios, debe ser un administrador de cuenta local o el administrador asignado para la instancia de servicio o servicio concreto. 

1. Desde la barra de menús, pulse **Gestionar** &gt; **Seguridad** &gt; **Identity & Access** &gt; **Usuarios**.  
2. Seleccione el usuario al que desea asignar políticas de servicios. 
3. Seleccione **Asignar políticas de servicio** para crear una nueva política de servicio o desde el menú **Acciones** en la sección Políticas de servicio, podrá: 
  
  * Editar la política
  * Eliminar la política

Para obtener información sobre los roles y las políticas de servicio, consulte [Políticas y roles para la gestión de acceso e identidades](/docs/iam/users_roles.html#iamusermanpol).

## Servicios de infraestructura

Si tiene acceso para la asignación de permisos de infraestructura, puede establecer los siguientes roles para el usuario: Solo visualización, Usuario básico o Superusuario. Pulse el enlace **Asignar acceso de infraestructura** para actualizar o asignar nuevos permisos. 

Para obtener más información sobre los permisos, consulte [Permisos de infraestructura](/docs/iam/users_roles.html#infrapermissions).

## Gestión de roles de Cloud Foundry en el Directorio del equipo
{: #editinguserroles}

Desde la página Directorio del equipo, los propietarios de las cuentas pueden gestionar usuarios solo de plataforma. Sin embargo, si va a la página **Gestionar** &gt; **Cuenta** &gt; **Usuarios**, podrá gestionar desde un único lugar todos los usuarios de servicios de infraestructura y plataforma. 

Los gestores de organización pueden editar roles de organización y espacio para usuarios existentes en la página de Directorio del equipo.

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
