---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Administración de 
{: #administer}
*Última actualización: 29 de febrero de 2016*

Gestione sus organizaciones, espacios y usuarios asignados pulsando el icono **Cuenta y soporte** ![Cuenta y soporte](../support/images/account_support.svg) y, a continuación, seleccione **Gestionar organizaciones**. Si es un usuario de {{site.data.keyword.Bluemix_notm}} local o un usuario de {{site.data.keyword.Bluemix_notm}} dedicado, consulte [Gestión de {{site.data.keyword.Bluemix_notm}} local y {{site.data.keyword.Bluemix_notm}} dedicado](../admin/index.html#mng) para obtener más información sobre la administración de su instancia local o dedicada.
{:shortdesc}

## Gestión de {{site.data.keyword.Bluemix_notm}} Public
{: #mngacct}

En {{site.data.keyword.Bluemix}} Public, puede gestionar organizaciones y espacios, incluido el acceso de usuario desde el panel de control en la interfaz de usuario. También puede supervisar el uso y la facturación.
{:shortdesc}

### Organizaciones y espacios
{: #orgsandspaces}

Como gestor de organización o propietario de la cuenta, puede utilizar la página Gestionar organizaciones para ver y gestionar los valores de la organización o del espacio, incluido el acceso de usuario. Para abrir la página Gestionar organizaciones, pulse el icono **Cuenta y soporte** ![Cuenta y soporte](../support/images/account_support.svg) y, a continuación, seleccione **Gestionar organizaciones**.

#### Organizaciones

Una organización está definida por los elementos siguientes:

<dl>
<dt>Users</dt>
<dd>El rol con permiso básico en las organizaciones y los espacios. Debe asignarse previamente a una organización
para que se le puedan otorgar otros permisos a los espacios en el seno de la organización. Para ver información detallada,
consulte [Usuarios y roles](adminpublic.html#userroles).</dd>
<dt>Dominios</dt>
<dd>Proporciona la ruta en Internet que se asigna a la organización. Una ruta tiene un subdominio y un dominio. Un subdominio suele ser el nombre de la app. Un dominio puede ser un dominio del sistema o un dominio personalizado que ha registrado para la app.<br/>
<p>**Nota**: Si añade un dominio personalizado, debe configurar el servidor DNS para resolver el dominio personalizado para que apunte al dominio del sistema de {{site.data.keyword.Bluemix_notm}}. De este modo, cuando {{site.data.keyword.Bluemix_notm}} recibe una solicitud para el dominio personalizado, puede direccionarlo correctamente a la app.</p></dd>
<dt>Cuota</dt>
<dd>Representa los límites de recursos para la organización, incluido el número de servicios y la cantidad de memoria que se puede asignar para que la utilice la organización. Las cuotas se asignan cuando se crean organizaciones. Cualquier app o servicio en un espacio de la organización contribuye al uso de la cuota. Con los planes Pague según uso o Subscription, puede ajustar su cuota para los contenedores y apps de Cloud Foundry a medida que cambien las necesidades de su organización.</dd>
</dl>

En {{site.data.keyword.Bluemix_notm}},
puede utilizar organizaciones para habilitar la colaboración entre usuarios y para facilitar la agrupación lógica de recursos del proyecto de las maneras siguientes:

<ul>
<li>Puede agrupar un conjunto de espacios, apps, servicios, dominios, rutas y usuarios conjuntamente en organizaciones.</li>
<li>Puede gestionar el acceso a los espacios y a las organizaciones usuario a usuario.</li>
</ul>

Cuando se crea una organización, el nombre de la organización debe ser exclusivo en {{site.data.keyword.Bluemix_notm}}. Después de crear la organización, se le asigna automáticamente el permiso de *Gestor de organizaciones*, que le permite editar el nombre de la organización, suprimir la organización y crear espacios en la organización.

Cuando se suprime una organización, todos los espacios, apps y servicios dentro de la organización se suprimen.

{{site.data.keyword.Bluemix_notm}} habilita la colaboración en proyectos asignando usuarios en el seno de una organización y en el seno de los espacios en la organización. Puede utilizar el separador **Usuarios** para mostrar y gestionar usuarios de la organización. También puede invitar a usuarios a su organización pulsando el enlace **Invitar a un nuevo usuario** del separador **Usuarios**. Se pueden asignar los permisos siguientes a usuarios de una organización:

<ul>
<li>Usuario de organización</li>
<li>Gestor de organización</li>
<li>Gestor de facturación de organización</li>
<li>Auditor de organización</li>
</ul>

#### Espacios

En el seno de una organización, podrá utilizar espacios para agrupar un conjunto de apps, servicios y usuarios.

Tras añadir usuarios a una organización, puede otorgarles permisos a los espacios en el seno de la organización. Similar a las organizaciones, los espacios también tienen un conjunto de permisos que se pueden asignar a los usuarios:

<ul>
<li>Gestor de espacio</li>
<li>Desarrollador de espacio</li>
<li>Auditor de espacio</li>
</ul>

**Nota**: A un usuario se le puede asignar como mínimo uno de los permisos en el espacio.

El separador **Dominios** para un espacio es una lista de sólo lectura de los dominios que están asignados al espacio. El dominio del sistema siempre está disponible en un espacio y también se pueden asignar dominios personalizados al espacio. Las aplicaciones que se crearon en el espacio pueden utilizar cualquiera de los dominios listados para el espacio.

### Usuarios y roles
{: #userroles}

Los propietarios de cuentas realizan todas las operaciones en organizaciones y espacios.

####Tipos de usuario

Puede ser un miembro o un colaborador de una cuenta.

<dl>
<dt>Miembro</dt>
<dd>Es un miembro de una cuenta de {{site.data.keyword.Bluemix_notm}} si ha creado la cuenta o ha sido invitado a la misma y luego se ha registrado desde la invitación, como su primera
experiencia con {{site.data.keyword.Bluemix_notm}}. </dd>
<dt>Colaborador</dt>
<dd>Es un colaborador de una cuenta de {{site.data.keyword.Bluemix_notm}} si anteriormente ha utilizado {{site.data.keyword.Bluemix_notm}} con una cuenta distinta, pero luego ha sido
invitado a esta cuenta y ha aceptado la invitación.</dd>
</dl>

#### Roles de usuario

A los usuarios se les pueden asignar los permisos
siguientes para que asuman distintos roles de usuario en una organización o espacio:

<dl>
<dt>Gestores de organizaciones</dt>
<dd>Los gestores de la organización tienen los permisos siguientes:
<ul>
<li>Crea o suprime espacios en la organización.</li>
<li>Invitar a los usuarios a la organización si también es miembro de la organización o el propietario de cuenta.</li>
<li>Gestionar los usuarios existentes que ya están en la organización.</li>
<li>Gestiona dominios de la organización.</li>
</ul>
<p>**Nota**: Si ya tiene el tipo de usuario de colaborador, y ha utilizado anteriormente {{site.data.keyword.Bluemix_notm}} con una cuenta distinta, no puede invitar a usuarios a la organización, incluso si le han asignado el rol de gestor de la organización. Debe tener el tipo de usuario de miembro para invitar usuarios. Consulte <a href="../troubleshoot/index.html#ts_adduser">No se pueden añadir usuarios a una organización</a> para obtener información sobre cómo solucionar temporalmente el problema.</p>
</dd>
<dt>Gestores de facturación</dt>
<dd>Los Gestores de facturación tienen permiso para ver información de uso de tiempo de ejecución y servicio para la organización.</dd>
<dt>Auditores de la organización</dt>
<dd>Los Auditores de la organización tienen permiso para ver el contenido de la app y el servicio en el espacio.</dd>
<dt>Gestores de espacios</dt>
<dd>Los gestores de espacios tienen los permisos siguientes:
<ul>
<li>Añaden a usuarios al espacio y gestionan usuarios.</li>
<li>Habilitan características para el espacio</li>
</ul>
</dd>
<dt>Desarrolladores de espacios</dt>
<dd>Los Desarrolladores de espacios tienen los permisos siguientes:
<ul>
<li>Crean, suprimen y gestionan apps y servicios en el espacio.</li>
<li>Tienen acceso a registros en el espacio</li>
</ul>
</dd>
<dt>Auditores de espacios</dt>
<dd>Los Auditores de espacios tienen acceso de sólo lectura a toda la información acerca del espacio como, por ejemplo, información sobre apps y servicios, valores, informes y registros.</dd>
</dl>

**Nota**: Los usuarios que están asignados al rol de gestor o desarrollador pueden acceder a la variable de entorno
VCAP_SERVICES. No obstante, un usuario asignado al rol auditor no puede acceder a VCAP_SERVICES. 

### Gestión de las organizaciones
{: #orgmng}

Como gestor de la organización o propietario de la cuenta, puede gestionar sus organizaciones. Las tareas de gestión incluyen la creación de una organización, el cambio de nombre de una organización, la creación de un espacio, la invitación de usuarios a un espacio, el cambio de roles de usuario y la supresión de una organización existente.

#### Creación de una organización

Solo los usuarios con cuentas de pago pueden crear una organización. Con una cuenta de pago, puede crear una organización siguiendo estos pasos:

<ol>
<li>Vaya al Panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el icono **Cuenta y soporte** ![Cuenta y soporte](../support/images/account_support.svg) y, a continuación, seleccione **Gestionar organizaciones**.</li>
<li>Pulse **Crear una organización** y siga las indicaciones para crear la organización.</li>
</ol>

#### Cambio de nombre de una organización

Siga estos pasos para cambiar el nombre de la organización:

<ol>
<li>Vaya al Panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el icono **Cuenta y soporte** ![Cuenta y soporte](images/account_support.svg), y seleccione **Gestionar organizaciones**.</li>
<li>Seleccione la organización cuyo nombre desea cambiar.</li>
<li>Escriba un nombre nuevo en el campo **Organización** y pulse **Guardar**.</li>
</ol>

#### Listado de miembros 

Realice los pasos siguientes para listar los miembros de su organización o espacio:

<ol>
<li>Vaya al Panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el icono **Cuenta y soporte** ![Cuenta y soporte](../support/images/account_support.svg) y, a continuación, seleccione **Gestionar organizaciones**. Puede ver los miembros de su organización y sus roles en el separador **Usuarios**.</li>
<li>Pulse el nombre de espacio en su organización para ver los miembros de este espacio y sus roles.</li>
</ol>

#### Creación de un espacio

Puede crear espacios en la organización; por ejemplo, un espacio *dev* como entorno de desarrollo, un espacio *test* como entorno de prueba y un espacio *production* como entorno de producción. Luego puede asociar sus apps a los espacios. Siga estos pasos para crear un espacio:

<ol>
<li>Vaya al Panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el icono **Cuenta y soporte** ![Cuenta y soporte](images/account_support.svg) y, a continuación, seleccione **Gestionar organizaciones**.</li>
<li>Pulse **Crear un espacio** siguiendo el nombre de la organización, y siga las indicaciones para crear el espacio.</li>
</ol>

#### Invitación de usuarios a un espacio

Puede invitar a usuarios a sus organizaciones y espacios por la dirección de correo electrónico. Los usuarios solo pueden acceder al espacio al que se han añadido. 

Según si el invitado tiene o no un ID de IBM, dicho usuario se asigna como si tuviera el rol `miembro` o `colaborador` para la cuenta. En la tabla siguiente se ofrecen detalles sobre cómo se asignan los roles de cuenta por tipo de invitación.

*Tabla 1. Asignaciones de roles de cuenta*

| **Tipo de correo invitado** | **Rol de cuenta asignado** | 
|----------------|------------------|
|El usuario tiene cuenta de ID de IBM enlazado a dirección de correo invitado  | Miembro  | 
|El usuario no tiene un ID de IBM | Se crea un ID de IBM que coincide con la dirección de correo enviada, y se añade al usuario como Miembro. | 
|Una dirección de correo para un usuario actual de {{site.data.keyword.Bluemix_notm}} | Colaborador | 

Realice los pasos siguientes para añadir usuarios con roles asignados a espacios específicos para una organización elegida:

<ol>
<li>Acceda a **Cuenta y soporte** &gt; **Cuenta** &gt; **Gestionar organizaciones**.</li>
<li>Seleccione **Invitar usuarios**.</li>
<li>Especifique la dirección de correo electrónico de la persona que quiera invitar.</li>
<li>Seleccione el rol para la organización a la que tiene pensado invitar al usuario nuevo.</li>
<li>Seleccione el rol para el espacio al que tiene pensado invitar al usuario nuevo.</li>
<li>Seleccione **Invitar**.</li>
<li>En la sección **Pendiente** puede ver la confirmación de que la invitación se ha enviado. Seleccione
**Reenviar correo** o **Cancelar invitación** para actuar sobre una invitación pendiente.</li>
</ol>

#### Cambio de roles de usuario

Siga estos pasos para cambiar los roles de usuario:

<ol>
<li>Desde la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, pulse el icono **Cuenta y soporte** ![Cuenta y soporte](images/account_support.svg) y, a continuación, seleccione **Gestionar organizaciones**.</li>
<li>Seleccione el recuadro de selección **MANAGER**, **BILLING MANAGER** o **AUDITOR** en el separador **USERS** para cambiar roles de usuarios en su organización. O bien, seleccione un espacio desde el panel de navegación y, a continuación, seleccione el recuadro de selección **MANAGER**, **DEVELOPER** o **AUDITOR** en el separador **USERS** para cambiar roles de usuarios en el espacio. </li>
<li>Pulse **GUARDAR**.</li>
</ol>

#### Supresión de una organización existente

Póngase en contacto con el soporte de registros y de ID de {{site.data.keyword.Bluemix_notm}} para suprimir la organización.

**Nota**: La supresión de operaciones no se puede invertir. Perderá todas las apps y servicios asociados a la app.

