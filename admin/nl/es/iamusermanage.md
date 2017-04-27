---

copyright:

  years: 2015, 2017

lastupdated: "2017-03-03"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestión de cuentas y accesos de usuarios
{: #iamusermanage}

Según las opciones de acceso que esté autorizado a gestionar, puede ver y gestionar usuarios de la cuenta o de la organización. Como propietario de una cuenta, puede gestionar los usuarios de cualquiera de las opciones de acceso que administre y a las que el usuario tenga acceso asignado, independientemente del rol, en la cuenta actual. Puede asignar, editar y eliminar el acceso para los usuarios de cualquiera de las opciones de acceso que gestione.
{:shortdesc}

Para gestionar usuarios de su cuenta, en la barra de menús pulse **Gestionar** &gt; **Cuenta** &gt; **Usuarios**. La ventana Usuarios muestra una lista de los usuarios con sus direcciones de correo electrónico y el estado actual en las cuentas que gestiona. En la ventana Usuarios, seleccione el usuario que desea gestionar o pulse **Gestionar usuario** en el menú **Acciones**. Verá las tablas de políticas correspondientes a las opciones de acceso que puede gestionar para dicho usuario.

## Gestión de servicios habilitados para Identity and Access
{: #iammanidaccser}

Si el usuario tiene asignado el acceso a un **Servicio habilitado para Identity and Access**, puede ver información sobre las políticas asignadas desde la ventana Gestionar usuario. Lo que se muestra para dicho usuario o grupo depende de las políticas que se han asignado. Si no se ha asignado ninguna política, verá un mensaje que le solicita si desea asignar una política. Si ya se han asignado políticas, se muestra una lista de las políticas con el rol del usuario o grupo y una descripción de los atributos de recurso para cada política. Puede asignar políticas desde la página Asignar políticas pulsando **Asignar políticas de servicio**. La opción **Asignar políticas de servicio** está habilitada si tiene autorización para crear políticas. Puede gestionar las políticas existentes pulsando la política en la lista o pulsando **Editar política** bajo **Acciones** en la fila de la política que desee editar.

## Gestión del acceso a los servicios de Cloud Foundry
{: #iammancfser}

Si el usuario tiene asignado acceso a **Cloud Foundry**, puede ver las organizaciones y los espacios que el usuario tiene asignados desde la ventana Gestionar usuario. Puede eliminar el usuario de una organización o puede cambiar el rol asignado para una organización o un espacio. Puede añadir un usuario a otra organización pulsando **Asignar organización** si es el gestor de una organización de la que el usuario aún no es miembro. Puede gestionar roles existentes de espacio y de organización pulsando **Editar rol de espacio** o **Editar rol de organización** en la fila del rol que desea editar.

### Gestión de políticas
{: #iamusermanpol}

Puede asignar y gestionar políticas para un usuario que tenga acceso a los **servicios habilitados para Identity and Access**. Una política asigna a un usuario uno o varios roles sobre un conjunto de recursos utilizando una combinación de atributos para definir el conjunto de recursos aplicable. 

Cuando se asigna una política a un usuario, primero hay que especificar el servicio que se va a asignar. La lista **Servicio** proporciona la opción para servicios específicos, incluida una opción para asignar todos los servicios disponibles. También debe seleccionar el rol o los roles que desea asignar. 

Hay más opciones de configuración disponibles en función del servicio que seleccione. Puede seleccionar un servicio para ver las opciones para dicho servicio.

Puede reducir la lista de opciones de servicio que se muestran. Pulse **Especificar contexto de servicio opcional** para especificar opciones adicionales, como por ejemplo regiones e instancias de servicio. Es posible que no desee especificar todas las opciones que se muestran, sino elegir las que desea configurar.

Puede asignar y gestionar políticas si tiene el rol adecuado. En la tabla siguiente se muestran las tareas de gestión de políticas y el rol necesario para cada una de ellos.


{: #iamui_table1}

| Acción | Rol necesario |
|----------|---------|
| Crear una política en una cuenta | Administrador en la cuenta |
| Crear una política en todos los servicios de una cuenta | Administrador en la cuenta |
| Crear una política en todas instancias de servicio de una cuenta | Administrador en la cuenta |
| Crear una política en un servicio de una cuenta | Administrador en la cuenta o administrador en el servicio de la cuenta |
| Crear una instancia de servicio | Administrador o editor en la cuenta o administrador o editor en el servicio de la cuenta |
| Crear una política en una instancia de servicio | Administrador en la cuenta o administrador en el servicio de la cuenta o administrador en la instancia de servicio |
{: caption="Table 1. Administrative tasks for managing **Identity and access enabled services** policies" caption-side="top"}

### Asignación y gestión de roles
{: #iamusermanrol}

Los roles son una colección de acciones; las acciones que están correlacionadas con estos roles son específicas del servicio.
Puesto que las acciones se agrupan como roles, puede utilizar un pequeño conjunto de roles definidos para dar soporte a cualquier acción correspondiente a cualquier servicio y a cualquier recurso. Por ejemplo, si necesita un administrador para máquinas virtuales, almacenamiento y red, puede definir el usuario como administrador para las tres funciones cambiando el destino de la política. Por lo tanto, debe establecer la política de modo que incluya el administrador de máquinas virtuales, el administrador de almacenamiento y el administrador de red. 

Los recursos no se basan en roles, de modo que no se crean nuevos nombres de rol para cada tipo de recurso que se incorpora en el sistema. Por ejemplo, no necesita un rol de administrador de máquina virtual, un rol de administrador de almacenamiento y un rol de administrador de red para cubrir la administración de recursos correspondientes a máquinas virtuales, almacenamiento y red.

Además de las descripciones de los roles que se proporcionan en la interfaz de usuario, la tabla siguiente proporciona ejemplos de algunas de las tareas que pueden realizar los usuarios asignados a cada rol. 

{: #iamui_table2}

| Rol | Descripción de acciones | Acciones de ejemplo|
|:-----------------|:-----------------|:-----------------|
| Visor | Realiza acciones que no cambian el estado; solo acciones de lectura | <ul><li>Enumerar dispositivos</li><li>Leer objeto de almacenamiento</li><li>Ejecutar consultas</li><li>Ejecutar búsquedas</li></ul>|
| Editor | Realiza acciones que modifican el estado y crean o suprimen subrecursos |<ul><li>Crear o suprimir máquinas virtuales</li><li>Conectar almacenamiento</li><li>Rearrancar</li><li>Iniciar o detener</li><li>Renombrar</li></ul> |
| Administrador | Realiza todas las acciones, incluida la capacidad para gestionar el control de accesos |<ul><li>Invitar a usuarios</li><li>Crear o suprimir máquinas virtuales</li><li>Actualizar políticas de acceso de usuarios</li><li>Enumerar dispositivos</li><li>Conectar almacenamiento</li><li>Rearrancar</li><li>Iniciar o detener</li><li>Renombrar</li><li>Hacer copia de seguridad y restaurar</li></ul>|
{: caption="Table 2. Administrative tasks for managing **Identity and access enabled services** policies" caption-side="top"}

Para obtener información más específica acerca de los roles de los usuarios que tienen asignado acceso a Cloud Foundry, consulte [Roles de usuario](/docs/admin/users_roles.html#userrolesinfo).

Cuando añada usuarios, debe seleccionar como mínimo un rol y puede añadir varios roles. Cuando seleccione un rol, verá su definición para poder determinar el rol o los roles que va a proporcionar. Los roles que asigne tienen distintas opciones de acceso pero a los mismos atributos de recurso que especifique.

Si ha seleccionado el servicio **Cloud Foundry**, los roles que asigne se asocian a las organizaciones y los espacios que ha seleccionado.
