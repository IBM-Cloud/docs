---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-11"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Asignación de acceso de usuario
{: #assignaccess}

Puede asignar acceso a los usuarios cuando los invite, asignarles roles, políticas y las cuentas u organizaciones, o ambos, a las que pueden acceder. Según las opciones de acceso que esté autorizado a gestionar, puede invitar y proporcionar acceso a usuarios de la cuenta, organización, espacio e instancias de servicio. Como propietario de una cuenta, puede asignar opciones de acceso a su cuenta para un usuario cuando tanto usted como el usuario sean miembros, independientemente del rol. En las secciones siguientes se describen los tres tipos de acceso que se pueden asignar a un usuario invitado.
{:shortdesc}

## Servicios habilitados para identificación y acceso

Puede asignar una política de servicio individual cuando invite a un nuevo usuario. Una vez que el usuario ha aceptado la invitación, puede añadir políticas de servicio adicionales. 

1. Desde la pantalla **Invitar a usuarios**, amplíe la sección **Servicios habilitados para Identity and Access**. 
2. Seleccione **Todos los servicios habilitados para Identity and Access**, o seleccione un servicio individual.  **Nota**: Si selecciona la opción **Otorgar acceso automáticamente cuando se añadan nuevos servicios**, no se le indicará que deseleccione cada nuevo servicio de {{site.data.keyword.Bluemix_notm}} para dicho usuario cuando se añadan servicios más adelante.
3. Seleccione **Todas las regiones actuales** o una región específica. 
4. Seleccione **Todas las instancias de servicio actuales** o seleccione una instancia de servicio específica. 
5. Seleccione un rol para definir el ámbito del acceso para la política. 
6. Opcional: Seleccione **Añadir rol** para especificar un rol adicional para la política.

Consulte [Roles y políticas de gestión de acceso e identidad](/docs/iam/users_roles.html#iamusermanpol) para obtener información específica sobre la creación de valores para las políticas de servicio. 

## Acceso de Cloud Foundry

De forma predeterminada, a todos los usuarios se les asigna un rol de organización de auditor. Puede actualizar este rol a gestor de facturación, gestor de organización, o rol de no organización después de que el usuario acepte la invitación. Durante el proceso de la invitación, es posible añadir varios roles de espacio, uno a la vez. 

1. Desde la pantalla **Invitar usuarios**, expanda la sección **Acceso de Cloud Foundry**. 
2. Seleccione una organización para añadirla al usuario. 
3. Seleccione **Todas las regiones actuales** o una región específica. 
4. Seleccione **Todos los espacios actuales** o un espacio específico. 
5. Seleccione un rol para definir el ámbito del acceso. 
6. Opcional: Seleccione **Añadir rol** para especificar un rol adicional para la política.

Consulte [Roles de Cloud Foundry](/docs/iam/users_roles.html#cfroles) para obtener información más específica sobre estos roles. 

## Acceso de infraestructura

Si tiene permiso, verá la opción de asignar permisos de infraestructura. Los permisos reales asignados se limitan automáticamente al subconjunto de permisos que posee.
Para obtener más información sobre los permisos y las acciones que puede desempeñar el usuario, consulte [Permisos de infraestructura](/docs/iam/users_roles.html#infrapermissions).

1. Desde la pantalla **Invitar usuarios**, expanda la sección **Acceso de infraestructura**.  
2. Seleccione un permiso para definir el ámbito del acceso. 

Para obtener información sobre la configuración del acceso para los usuarios después de que hayan sido añadidos a su cuenta, consulte [Gestión de accesos y cuentas de usuario](/docs/iam/iamusermanage.html).
