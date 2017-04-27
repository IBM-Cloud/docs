---

copyright:

  years: 2015, 2017
lastupdated: "2017-03-08"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Invitación a usuarios, asignación y gestión de acceso
{: #iamuserinv}

Puede invitar a los usuarios de servicios de {{site.data.keyword.Bluemix_notm}}, aplicaciones e infraestructura de {{site.data.keyword.Bluemix_notm}} desde una sola ubicación. Puede asignar acceso a los usuarios cuando los invite, asignarles roles, políticas y las cuentas u organizaciones, o ambos, a las que pueden acceder. Según las opciones de acceso que esté autorizado a gestionar, puede invitar y proporcionar acceso a usuarios de la cuenta o de la organización. Como propietario de una cuenta, puede asignar opciones de acceso a su cuenta para un usuario cuando tanto usted como el usuario sean miembros, independientemente del rol. {:shortdesc}

Para invitar a usuarios y gestionar invitaciones en su cuenta, en la barra de menús pulse **Gestionar** &gt; **Cuenta** &gt; **Usuarios**. La ventana Usuarios muestra una lista de los usuarios con sus direcciones de correo electrónico y el estado actual en las cuentas que gestiona.  

Para invitar a usuarios y gestionar invitaciones pendientes, debe ser propietario de cuenta o gestor de la organización o bien debe tener permisos de la infraestructura para añadir usuarios. Puede invitar a usuarios, cancelar invitaciones y volver a enviar una invitación pendiente a un usuario invitado. Puede invitar a un solo usuario o, si proporciona el mismo acceso para todos los miembros de un grupo de usuarios, puede invitar a varios usuarios a la vez. 

Para invitar a usuarios, pulse **Invitar a usuarios**, especifique la dirección de correo electrónico o el ID de IBM del usuario y luego añádalos a una o varias de las opciones de acceso que gestiona. Debe asignar al menos una opción de acceso y configurar los valores para el usuario en cada opción de acceso que asigne. Para las opciones de acceso adicionales que no desee añadir y configurar, se asigna el valor predeterminado *no access* (sin acceso). Es posible que vea una o todas las siguientes opciones de acceso, en función de las opciones que está autorizado a gestionar:

**Servicios habilitados de Identity and Access**
Seleccione esta opción para asignar servicios, regiones, instancias de servicios y roles a los usuarios que invite.
**Nota**: Si selecciona la opción **Otorgar acceso automáticamente cuando se añadan nuevos servicios**, no se le indicará que deseleccione cada nuevo servicio de {{site.data.keyword.Bluemix_notm}} para dicho usuario cuando se añadan servicios más adelante. 

**Acceso a Cloud Foundry**
Seleccione esta opción para asignar servicios, regiones, espacios y roles de espacios a los usuarios que invite. Consulte [Roles de usuario](/docs/admin/users_roles.html#userrolesinfo) para obtener información más específica sobre estos valores. Puede añadir varios roles, de uno en uno. 

**Acceso a infraestructura** Asigne al usuario uno de estos permisos sobre la infraestructura:  
<dl>
<dt>Solo visualización</dt>
<dd>Los usuarios con este permiso solo pueden ver los elementos del sistema.</dd>
<dt>Usuario básico</dt>
<dd>Los usuarios con este permiso pueden realizar acciones básicas en el sistema, como, por ejemplo, añadir una incidencia y gestionar dispositivos. </dd>
<dt>Superusuario</dt>
<dd>Los usuarios con este permiso pueden realizar todas las acciones disponibles en el sistema.</dd>
</dl>
**Nota**: Los permisos reales asignados se limitan automáticamente al subconjunto de permisos que tiene.
Si proporciona el mismo acceso a varios usuarios, puede seleccionar **Invitar a varios usuarios** para especificar una lista de los usuarios a los que desea invitar. Separe las entradas de ID de usuario con comas.  

Si determina que un usuario no necesita acceso, también puede cancelar una invitación para cualquier usuario que se muestre en estado **Procesando** o **Pendiente** en la columna **Estado**. Si un usuario invitado no ha recibido una invitación, también puede volver a enviar la invitación a cualquier usuario en estado **Pendiente**. Estas opciones están disponibles para los usuarios en el estado adecuado en el menú **Acciones** de la ventana de Usuarios.

Para obtener información específica sobre la configuración de acceso para usuarios, incluidos roles y políticas, consulte [Gestión de cuentas y accesos de usuarios](/docs/admin/iamusermanage.html).
