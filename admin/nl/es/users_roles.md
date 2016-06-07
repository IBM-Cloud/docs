---



copyright:

  years: 2015, 2016



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestión de roles y miembros del equipo
{: #userroles}
*Última actualización: 16 de mayo de 2016*

En la página **Directorio del equipo** para la cuenta, puede gestionar los miembros del equipo existentes y sus roles en la organización y espacios, así como invitar a nuevos miembros del equipo. Para acceder al directorio de equipo para su cuenta, vaya al icono **Cuenta y soporte** ![icono Cuenta y soporte](../admin/images/account_support.svg) &gt; **Cuenta** &gt; *su_nombre_cuenta* &gt; **Directorio del equipo**.
{:shortdesc}

Los propietarios de cuentas llevan a cabo todas las operaciones en las organizaciones y los espacios incluida la gestión de miembros del equipo y sus roles asignados. Los gestores de organización tienen acceso a invitar a miembros del equipo y gestionar roles. Los gestores de espacio pueden utilizar la página **Gestionar organizaciones** para añadir miembros de cuentas existentes al espacio y ajustar sus roles. Consulte la siguiente información para aprender más sobre roles. 

## Roles
{: #userrolesinfo}

En el nivel de cuenta, hay dos roles que permiten acceder a distintas características de gestiones de cuentas:


*Tabla 1. Roles de cuentas y permisos*

| Rol de cuenta | Permisos |    
|----------------|---------|
|Propietario | Un propietario para la cuenta tiene acceso a su perfil, directorio de equipo, información de facturación, notificaciones de gasto y panel de control de uso. En la página de directorio del equipo, el propietario puede invitar a nuevos miembros del equipo y ajustar roles.
El propietario también puede añadir créditos promocionales, establecer o cambiar el límite de facturación, establecer acceso de servicios y gestionar organizaciones y espacios.  |
|Miembro | Un miembro tiene acceso a su perfil, directorio de equipo y créditos de cuenta y límites de facturación en la cabecera de {{site.data.keyword.Bluemix_notm}}.
Sin embargo, en la página de directorio de equipo, un miembro solamente puede ver los miembros del equipo dentro de la cuenta.
 |

 Todos los miembros del equipo se añaden como un miembro de la cuenta. Puede asignar roles de organización y espacio a invitados para habilitar vistas y permisos específicos en {{site.data.keyword.Bluemix_notm}}. De forma predeterminada, a los nuevos miembros añadidos a una organización se les asigna el rol de organización de auditor. Para un espacio específico, puede elegir asignar el rol de desarrollador o auditor a los invitados. Una vez que los invitados aceptan la invitación y se unen a {{site.data.keyword.Bluemix_notm}}, puede editar sus roles en la página **Directorio del equipo**.

Los siguientes roles se pueden asignar a nivel de organización: 

*Tabla 2. Roles de organización y permisos*

| Rol de organización | Permisos |    
|-------------------|-------------|
|Gestor | Los gestores de organización pueden crear, ver, editar o suprimir espacios dentro de la organización, ver la cuota y el uso de la organización, invitar a miembros del equipo a la organización, gestionar quién tiene acceso a la organización y sus roles en la organización, y gestionar dominios personalizados para la organización.  |
|Gestor de facturación | Los gestores de facturación pueden ver la información de uso de tiempo de ejecución y servicio para la organización de la página Panel de control de uso.   |
|Auditor | Los auditores de organización pueden ver el contenido de aplicación y servicio en la organización. Los auditores también pueden ver los miembros del equipo de la organización y sus roles asignados, y la cuota para la organización. Este rol se asigna a todos los invitados de forma predeterminada.|

Los siguientes roles se pueden asignar a nivel de espacio: 

*Tabla 3. Roles de espacio y permisos*

| Rol de espacio | Permisos |    
|------------|-------------|
|Gestor | Los gestores de espacios pueden añadir miembros de equipo existentes y gestionar roles dentro del espacio. Los gestores de espacios también pueden ver el número de instancias, enlaces de servicio y uso de recursos para cada aplicación en el espacio.  |
|Desarrollador | Los desarrolladores de espacios pueden crear, suprimir y gestionar aplicaciones y servicios dentro del espacio. Algunas de las tareas de gestión incluyen el desarrollo de apps, el inicio o la detención de apps, el cambio de nombre de una app, la supresión de una app, el enlace o desenlace de un servicio con una aplicación, ver el número o instancias, enlaces de servicio y uso de recursos para cada aplicación en el espacio. Además, el desarrollador de espacios puede asociar un URL interno o externo con una aplicación en el espacio.    |
|Auditor | Los auditores del espacio tienen acceso de solo lectura a toda la información sobre el espacio, como la información sobre el número de instancias, enlaces de servicio y uso de recursos para cada aplicación en el espacio.  |

**Nota**: los miembros del equipo que tienen asignado el rol de espacio de gestor o desarrollador puede acceder a la variable de entorno VCAP_SERVICES. Sin embargo, un miembro del equipo que tienen asignado el rol de auditor no puede acceder a VCAP_SERVICES.

## Invitación a miembros del equipo
{: #inviteteammembers}

Los propietarios de cuentas y gestores de organizaciones pueden invitar a los miembros del equipo a las organizaciones desde la página Invitar miembros del equipo. Cuando añade nuevos miembro del equipo, se les asignan automáticamente los roles de auditor. Puede cambiar los roles más adelante en la página Directorio del equipo. Para invitar a un miembro del equipo, realice estos pasos:


<ol>
<li>Vaya al icono **Cuenta y soporte** ![icono Cuenta y soporte](../admin/images/account_support.svg) &gt; **Cuenta** &gt; *su_nombre_cuenta* &gt; **Invitar a miembro del equipo**.</li>
<li>Seleccione la organización a la que desea invitar los miembros del equipo. </li>
<li>Pulse **Siguiente**.</li>
<li>Seleccione los espacios a los que desea permitir acceso a los miembros del equipo.</li>
<li>Seleccione el rol que se le va a asignar para los espacios seleccionados en la organización.</li>
<li>Seleccione la opción para confirmar que tiene responsabilidad financiera para todos los cargos que se producen en la cuenta. </li>
<li>Escriba la dirección de correo electrónico para un miembro del equipo individual, o direcciones de correo electrónico para varios miembros del equipo:
<ul>
<li>Para añadir un único miembro del equipo, escriba la dirección de correo electrónico y pulse **Enviar**.</li>
<li>Para añadir más de un miembro del equipo, pulse **Invitarlos a todos a la vez**. Escriba las direcciones de correo electrónico utilizando una lista separada por comas, espacios o saltos de línea. A continuación, pulse **Siguiente** para verificar las direcciones de correo electrónico a las que enviar las invitaciones y pulse **Enviar**.</li>
</ul>
</li>
</ol>

Pulse **Ver pendiente** para comprobar si hay invitaciones pendientes o aceptadas. Puede elegir reenviar el correo electrónico de invitación o cancelar la invitación para una invitación pendiente en cualquier momento. 

## Editar roles 
{: #editinguserroles}

Los propietarios de cuentas y gestores de organizaciones pueden editar roles de organización y espacio para miembros del equipo existentes en la página **Directorio del equipo**. 

1. Vaya al icono **Cuenta y soporte**  ![icono Cuenta y soporte](../admin/images/account_support.svg) &gt; **Cuenta** &gt; *su_nombre_cuenta* &gt; **Directorio del equipo**.
2. Localice el miembro del equipo cuyos roles desea editar.
3. Pulse **Ver roles**.
4. Seleccione o elimine las selecciones del rol de organización para modificar el acceso de organización para el miembro del equipo.
5. Pulse **Ver espacios** para añadir o eliminar roles de espacios.
6. Seleccione o elimine la selección de rol de espacio para modificar el acceso al espacio para el miembro del equipo. 
7. Pulse **Cerrar espacios**.
8. Pulse **Guardar** al final de la página.

Los gestores de espacio pueden editar roles para los miembros del equipo en su espacio en la página **Gestionar organizaciones**.

1. Vaya al icono **Cuenta y soporte** ![icono Cuenta y soporte](../admin/images/account_support.svg) &gt; **Cuenta** &gt; *su_nombre_cuenta* &gt; **Gestionar organizaciones**.
2. Localice la organización en la que está su espacio.
3. Pulse **Ver detalles**.
4. Localice el espacio y pulse **Editar espacio**.
5. Seleccione el separador **Usuarios**.
6. Seleccione o quite la marca de selección de la opción de rol de espacio para el rol que desea añadir o eliminar para el miembro del equipo. 
7. Pulse **Guardar**.
