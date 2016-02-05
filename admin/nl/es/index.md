{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

#Administración de {{site.data.keyword.Bluemix_notm}}
{: #administer}
*Última actualización: 20 de enero de 2016*

Gestione sus organizaciones, espacios y usuarios asignados pulsando el icono **Cuenta y soporte** ![Cuenta y soporte](../support/images/account_support.svg) y, a continuación, seleccione **Gestionar organizaciones**. Si es un usuario de {{site.data.keyword.Bluemix_notm}} local o un usuario de {{site.data.keyword.Bluemix_notm}} dedicado, consulte [Gestión de {{site.data.keyword.Bluemix_notm}} local y {{site.data.keyword.Bluemix_notm}} dedicado](index.html#mng) para obtener más información sobre la administración de su instancia local o dedicada.
{:shortdesc}

##Gestión de la cuenta
{: #mngacct}

En {{site.data.keyword.Bluemix}} Public, puede gestionar organizaciones y espacios, incluido el acceso de usuario desde el panel de control en la interfaz de usuario. También puede supervisar el uso y la facturación.
{:shortdesc}

###Organizaciones y espacios
{: #orgsandspaces}

Como gestor de organización o propietario de la cuenta, puede utilizar la página Gestionar organizaciones para ver y gestionar los valores de la organización o del espacio, incluido el acceso de usuario. Para abrir la página Gestionar organizaciones, pulse el icono **Cuenta y soporte** ![Cuenta y soporte](../support/images/account_support.svg) y, a continuación, seleccione **Gestionar organizaciones**.

####Organizaciones

Una organización está definida por los elementos siguientes:

<dl>
<dt>Users</dt>
<dd>El rol con permiso básico en las organizaciones y los espacios. Debe asignarse previamente a una organización
para que se le puedan otorgar otros permisos a los espacios en el seno de la organización. Para ver información detallada,
consulte [Usuarios y roles](index.html#userroles).</dd>
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

####Espacios

En el seno de una organización, podrá utilizar espacios para agrupar un conjunto de apps, servicios y usuarios.

Tras añadir usuarios a una organización, puede otorgarles permisos a los espacios en el seno de la organización. Similar a las organizaciones, los espacios también tienen un conjunto de permisos que se pueden asignar a los usuarios:

<ul>
<li>Gestor de espacio</li>
<li>Desarrollador de espacio</li>
<li>Auditor de espacio</li>
</ul>

**Nota**: A un usuario se le puede asignar como mínimo uno de los permisos en el espacio.

El separador **Dominios** para un espacio es una lista de sólo lectura de los dominios que están asignados al espacio. El dominio del sistema siempre está disponible en un espacio y también se pueden asignar dominios personalizados al espacio. Las aplicaciones que se crearon en el espacio pueden utilizar cualquiera de los dominios listados para el espacio.

###Usuarios y roles
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

####Roles de usuario

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

###Gestión de la organización
{: #orgmng}

Como gestor de la organización o propietario de la cuenta, puede gestionar sus organizaciones. Las tareas de gestión incluyen la creación de una organización, el cambio de nombre de una organización, la creación de un espacio, la invitación de usuarios a un espacio, el cambio de roles de usuario y la supresión de una organización existente.

<ul>
<li>Creación de una organización
<p>Solo los usuarios con cuentas de pago pueden crear una organización. Con una cuenta de pago, puede crear una organización siguiendo estos pasos:</p>
<ol>
<li>Vaya al Panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el icono **Cuenta y soporte** ![Cuenta y soporte](../support/images/account_support.svg) y, a continuación, seleccione **Gestionar organizaciones**.</li>
<li>Pulse **Crear una organización** y siga las indicaciones para crear la organización.</li>
</ol>
</li>
<li>Cambio de nombre de una organización
<p>Siga estos pasos para cambiar el nombre de la organización:</p>
<ol>
<li>Vaya al Panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el icono **Cuenta y soporte** ![Cuenta y soporte](images/account_support.svg), y seleccione **Gestionar organizaciones**.</li>
<li>Seleccione la organización cuyo nombre desea cambiar.</li>
<li>Escriba un nombre nuevo en el campo **Organización** y pulse **Guardar**.</li>
</ol>
</li>
<li>Listado de miembros
<p>Realice los pasos siguientes para listar los miembros de su organización o espacio:</p>
<ol>
<li>Vaya al Panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el icono **Cuenta y soporte** ![Cuenta y soporte](../support/images/account_support.svg) y, a continuación, seleccione **Gestionar organizaciones**. Puede ver los miembros de su organización y sus roles en el separador **Usuarios**.</li>
<li>Pulse el nombre de espacio en su organización para ver los miembros de este espacio y sus roles.</li>
</ol>
</li>
<li>Creación de un espacio
<p>Puede crear espacios en la organización; por ejemplo, un espacio *dev* como entorno de desarrollo, un espacio *test* como entorno de prueba y un espacio *production* como entorno de producción. Luego puede asociar sus apps a los espacios. Siga estos pasos para crear un espacio:</p>
<ol>
<li>Vaya al Panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el icono **Cuenta y soporte** ![Cuenta y soporte](images/account_support.svg) y, a continuación, seleccione **Gestionar organizaciones**.</li>
<li>Pulse **Crear un espacio** siguiendo el nombre de la organización, y siga las indicaciones para crear el espacio.</li>
</ol>
</li>
<li>Invitación de usuarios a un espacio
<p>Puede invitar usuarios a su organización como colaboradores. También puede añadir usuarios de la organización a distintos espacios. Los usuarios solo pueden acceder al espacio al que se han añadido. Siga estos pasos para añadir un usuario a un espacio:</p>
<ol>
<li>Vaya al Panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el icono **Cuenta y soporte** ![Cuenta y soporte](../support/images/account_support.svg) y, a continuación, seleccione **Gestionar organizaciones**. A continuación, pulse **Añadir usuario** en su organización y siga las indicaciones para añadir el usuario a la organización.</li>
<li>Añada el usuario a un espacio. Seleccione el espacio en el panel de navegación, pulse **Añadir usuario** y siga las indicaciones para añadir el usuario al espacio.</li>
</ol>
</li>
<li>Cambio de roles de usuario
<p>Siga estos pasos para cambiar los roles de usuario:</p>
<ol>
<li>Desde la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, pulse el icono **Cuenta y soporte** ![Cuenta y soporte](images/account_support.svg) y, a continuación, seleccione **Gestionar organizaciones**.</li>
<li>Seleccione el recuadro de selección **MANAGER**, **BILLING MANAGER** o **AUDITOR** en el separador **USERS** para cambiar roles de usuarios en su organización. O bien, seleccione un espacio desde el panel de navegación y, a continuación, seleccione el recuadro de selección **MANAGER**, **DEVELOPER** o **AUDITOR** en el separador **USERS** para cambiar roles de usuarios en el espacio. </li>
<li>Pulse **GUARDAR**.</li>
</ol>
</li>
<li>Supresión de una organización existente
<p>Póngase en contacto con el soporte de registros y de ID de {{site.data.keyword.Bluemix_notm}} para suprimir la organización.</p>
<p>**Nota**: La supresión de operaciones no se puede invertir. Perderá todas las apps y servicios asociados a la app.</p>
</li>
</ul>

## Gestión de {{site.data.keyword.Bluemix_notm}} Local y {{site.data.keyword.Bluemix_notm}} Dedicado
{: #mng}

Si tiene acceso de administrador para {{site.data.keyword.Bluemix_notm}} Local o {{site.data.keyword.Bluemix_notm}} Dedicado, vaya a la página **Administración** para gestionar recursos, supervisar el uso de cuota, administrar permisos de usuarios, planificar las notificaciones de actualización, ver informes y registros de seguridad, etc. Puede gestionar sus organizaciones mediante la creación de espacios y la configuración de roles y permisos de usuarios; consulte [Gestión de las organizaciones](index.html#orgmng).
{:shortdesc}

*Tabla 1. Tareas administrativas para gestionar la instancia local o dedicada de {{site.data.keyword.Bluemix_notm}}*

| ¿Qué puedo hacer? | Detalles |    
|----------------|---------|
|Supervisar el uso del sistema | Pulse **ADMINISTRACIÓN &gt; USO**. Visualice la información del sistema, supervise el uso de la CPU y planifique el uso para tomar las mejores decisiones para su empresa.|
|Gestionar el catálogo | Pulse **ADMINISTRACIÓN &gt; GESTIÓN DE CATÁLOGOS**. Gestione los servicios que son visibles para los usuarios.|
|Administrar organizaciones | Pulse **ADMINISTRACIÓN &gt; ADMINISTRACIÓN DE LA ORGANIZACIÓN**. Cree organizaciones, supervise cuotas para organizaciones y tome decisiones basadas en sus necesidades de forma rápida.|
|Crear espacios y asignar roles de usuario | Pulse el icono **Cuenta y soporte** ![Cuenta y soporte](../support/images/account_support.svg) y, a continuación, seleccione **Gestionar organizaciones**. Cree espacios en sus organizaciones. Añada usuarios y asigne roles de organización y de espacio a los usuarios. |
|Gestionar permisos de usuarios administrativos | Pulse **ADMINISTRACIÓN &gt; ADMINISTRACIÓN DE USUARIOS**. Añada usuarios, elimine usuarios y ajuste los permisos de usuarios. |
|Revisar informes y registros | Pulse **ADMINISTRACIÓN &gt; INFORMES Y REGISTROS**. Visualice informes de seguridad y registros de auditoría para la instancia.|
|Ver información del sistema | Pulse **ADMINISTRACIÓN &gt; INFORMACIÓN DEL SISTEMA**. Visualice información del sistema como actualizaciones pendientes, el nombre y la versión de la instancia, la región, la URL de API, la URL de CLI, los detalles de configuración de LDAP, las correlaciones de usuario y de grupo, las estadísticas y los dominios compartidos.  |

### Visualización de la información del sistema
{: #oc_system}

Para ver información del sistema, pulse **ADMINISTRACIÓN &gt; INFORMACIÓN DEL SISTEMA**.

Puede expandir y visualizar diversas secciones sobre detalles de configuración de actualizaciones pendientes, información general del sistema y LDAP.

* En la sección Actualizaciones, puede ver cualquiera de las actualizaciones pendientes
que requieren acción por su parte. También puede realizar un seguimiento de forma sencilla de las actualizaciones utilizando el enlace al calendario
para importar las actualizaciones planificadas en una app de calendario.

<ol>
<li>Para realizar una acción para una actualización específica, siga estos pasos:
<ol type="a">
<li>Pulse <strong><em>Número</em> de actualizaciones pendientes</strong> para ver todas las actualizaciones pendientes.</li>
<li>Seleccione una actualización para realizar una acción o ver los detalles de la actualización, que incluyen la ventana de actualización,
el estado planificado o el estado de interrupción.</li>
<li>Pulse <strong>ESTABLECER FECHAS DE NO DISPONIBILIDAD</strong> para establecer días específicos en la ventana de actualización
que no son convenientes para que se aplique la actualización. Si establece fechas de no disponibilidad, IBM aprobará y planificará
la actualización en función de las selecciones. Recibirá una notificación cuando se apruebe y se planifique la actualización.</li>
<li>Pulse <strong>APROBAR</strong> para aprobar la actualización, si no tiene ninguna fecha no disponible. Si aprueba, la actualización se aplicará durante la ventana de actualización planificada. IBM enviará una
notificación cuando se inicie y se detenga el despliegue de actualización.</li>
</ol>
</li>
<li>Para importar sus actualizaciones planificadas en una app de calendario de su elección, lleve a cabo los pasos siguientes:
<ol type="a">
<li>Abra la app de calendario.</li>
<li>Importe las actualizaciones del calendario pegando el **URL del calendario** listado en la página Información del sistema de su app. O bien, descargue el archivo de calendario pulsando el URL de calendario y, a continuación, impórtelo a la app de calendario mediante el archivo `.ics`.</li>
<li>Escriba sus credenciales.</li>
<li>Visualice las actualizaciones planificadas.</li>
</ol>
</li>
</ol>

* En la sección Información general, puede ver la siguiente información:
    * Información básica sobre el build de {{site.data.keyword.Bluemix_notm}}.
    * Información de API (versión, URL, región y enlace a la documentación de CLI).
    * Información de dominio compartido sobre el sistema y el servicio.
    * Estadísticas sobre el número total de apps, usuarios y organizaciones.
* En la sección Detalles de la configuración de LDAP, puede seleccionar el servidor de LDAP
y ver información sobre las correlaciones de usuarios y grupos. Si utiliza {{site.data.keyword.IBM}} Web ID, se especifica en la sección Detalles de la configuración de LDAP.

### Visualización de la información de uso
{: #oc_resource}

Para ver información de recursos, pulse **ADMINISTRACIÓN &gt; USO**.

En la sección Supervisión de recursos, puede ver la siguiente
información:

* Información sobre uso del recurso, como el número de GB de memoria y el número de GB de espacio de disco utilizados. Puede ver el promedio de uso de la CPU de todos los agentes de ejecución de gotas (DEA). Pulse el mosaico **CPU** y verá el uso de CPU de cada DEA. El DEA que tiene el uso más alto aparece primero, y todos ellos están identificados con su trabajo y su dirección IP. El uso de CPU se divide
en tres categorías que incluyen la cantidad de CPU utilizada en los procesos del sistema, la cantidad de CPU
utilizada en los procesos de usuario y la cantidad de CPU utilizada en los procesos de espera.
* Información sobre uso de red correspondiente a entrada y salida de ancho de banda durante el último día, semana o mes.
Los datos que se muestran se basan en la suma del tráfico de entrada y de salida de las redes públicas y privadas.
* Tiempo medio de respuesta para {{site.data.keyword.Bluemix_notm}} en los últimos 10 minutos, hora y día.
* Promedio de transacciones por segundo para {{site.data.keyword.Bluemix_notm}} durante los últimos 10
minutos, hora y día.

### Visualización de informes
{: #oc_report}

Puede ver informes de seguridad y registros, como por ejemplo DataPower&trade;, el cortafuegos y la auditoría de inicio de sesión, para
la instancia de {{site.data.keyword.Bluemix_notm}}.

Para visualizar informes y registros, pulse **ADMINISTRACIÓN &gt; INFORMES Y REGISTROS**.

Seleccione una de las opciones siguientes:

* Puede seleccionar fechas de inicio y finalización en los campos para filtrar los informes y registros que se muestran.
* Puede expandir y visualizar distintos informes desde el panel de navegación.
* Puede buscar dentro del conjunto de informes y registros. La búsqueda se aplica a los nombres de informes y al contenido de texto que se incluye en los informes y los registros. También puede optar por filtrar
la búsqueda por **Sucesos de administración**, **Informes de DataPower**, **Cortafuegos** y **Auditoría
de inicio de sesión**.
* Cuando visualice un informe o un registro, puede pulsar el icono ![Descargar](images/icon_download.svg)
para descargar el informe.

### Visualización del estado
{: #oc_status}

Puede supervisar el estado de la instancia de {{site.data.keyword.Bluemix_notm}} mediante la página de Estado de {{site.data.keyword.Bluemix_notm}}. La página Estado es el recurso central para buscar notificaciones y anuncios sobre sucesos clave que afectan a la plataforma {{site.data.keyword.Bluemix_notm}} y a los servicios principales de {{site.data.keyword.Bluemix_notm}}.

Puede suscribirse a un hilo RSS para recibir notificaciones de forma que no tenga que comprobar si se han publicado. Para obtener más información sobre la página Estado y la configuración del hilo RSS, consulte [Visualización de {{site.data.keyword.Bluemix_notm}}](../troubleshoot/getting_customer_support.html#status).

### Gestión del catálogo
{: #oc_catalog}

Puede gestionar qué servicios e iniciadores de {{site.data.keyword.Bluemix_notm}} podrán ver los usuarios en el Catálogo de {{site.data.keyword.Bluemix_notm}}. Pulse **ADMINISTRACIÓN &gt; GESTIÓN DE CATÁLOGOS**.

Seleccione un mosaico de servicios o iniciadores para editar la visibilidad del plan de servicios o iniciadores. Para editar la visibilidad, seleccione una de las siguientes opciones:
* Para mostrar el servicio o iniciador oculto para que esté visible para los usuarios en el
Catálogo, seleccione **HABILITAR TODOS LOS PLANES**.
* Para ocultar el servicio o el iniciador de los usuarios en el Catálogo de {{site.data.keyword.Bluemix_notm}},
seleccione **INHABILITAR TODOS LOS PLANES**.
* Para controlar la visibilidad de un plan individual, seleccione el nombre del plan y utilice el menú desplegable para seleccionar **Habilitar para todas las organizaciones**, **Inhabilitar para todas las organizaciones** o **Habilitar plan para organizaciones específicas**.

### Administración de organizaciones
{: #oc_organizations}

Puede gestionar sus organizaciones creando y suprimiendo organizaciones, añadiendo gestores a las organizaciones y supervisando el uso de cuota.

Pulse **ADMINISTRACIÓN &gt; ADMINISTRACIÓN DE LA ORGANIZACIÓN**.

Puede expandir y visualizar diversas secciones. También puede revisar y gestionar los planes de cuotas de sus organizaciones.

* Para crear una nueva organización y añadir gestores, pulse <strong>CREAR ORGANIZACIÓN</strong>.
Especifique un nombre para la organización, e indique el nombre o el correo electrónico de la persona que desea añadir como gestor. Puede añadir más de un gestor especificando y seleccionando varios nombres. Pulse <strong>CREAR ORGANIZACIÓN</strong> para guardar los cambios y crear la organización.
* En la sección Supervisión de cuotas puede expandir la sección y ver la siguiente información:
    * Uso de memoria del entorno. En esta sección se proporcionan detalles sobre el uso de memoria del entorno del sistema completo.
	En el diagrama se proporciona información que incluye la memoria del sistema utilizada, la memoria total del sistema, la cuota utilizada y la cuota total asignada. En la siguiente lista de términos se definen los tipos de uso de memoria que se visualizan en el diagrama.
	<dl>
	<dt><strong>Memoria del sistema utilizada</strong></dt>
	<dd>Memoria física utilizada por el entorno.</dd>
	<dt><strong>Memoria total del sistema</strong></dt>
	<dd>Memoria física total disponible en el entorno.</dd>
	<dt><strong>Cuota desplegada</strong></dt>
	<dd>La suma de la memoria asignada para todas las apps desplegadas en todas las organizaciones. La suma de
	la cuota desplegada puede superar la memoria física total del sistema de su entorno. Por ejemplo, si tiene una memoria total del sistema de 16 GB y asigna 4 GB de memoria para cinco organizaciones distintas, la cuota total excede la memoria total del sistema que se ha asignado a todas las organizaciones. Sin embargo, en muchos casos las organizaciones no utilizan la cuota total que se ha asignado a cada una de ellas. Además, es posible que las organizaciones no utilicen su asignación de memoria de cuota total al mismo tiempo. </dd>
	<dt><strong>Cuota total</strong></dt>
	<dd>La memoria total asignada en todas las organizaciones.</dd>
	</dl>
	* Uso de memoria de la organización. En esta sección se proporcionan detalles del uso de memoria a nivel de organización. Puede ver la concesión de cuota total y la cuota desplegada para cada organización. En el gráfico se proporciona información que aparece ordenada por el uso de memoria más alto por organización; la organización que utiliza la cantidad de memoria más elevada aparece en primer lugar de forma predeterminada. Puede ordenar por **Uso de memoria más alto** y **Asignación de memoria excesiva**.
	<dl>
	<dt><strong>Uso de memoria máximo</strong></dt>
	<dd>Utilice esta opción para identificar la organización que utiliza la mayor cantidad de memoria. Ordene por uso de memoria más alto
	para identificar las organizaciones que utilizan la mayor cantidad de memoria. La lista está ordenada por cuota desplegada. </dd>
	<dt><strong>Asignación de memoria excesiva</strong></dt>
	<dd>Utilice esta opción para identificar las organizaciones que tienen un plan de cuotas superior al necesario:
	ordene por uso de memoria excesivo para identificar las organizaciones que utilizan la cantidad de memoria más pequeña para la cuota que se les ha asignado. </dd>
	</dl>
* Para cambiar el plan de cuotas de una organización, pulse la barra del gráfico de la organización que desea editar en la sección Uso de memoria de la organización, o bien seleccione el nombre de la organización en la sección Lista de organizaciones. En la página Editar organización puede cambiar el plan de cuotas, cambiar el nombre de la organización y añadir o eliminar gestores. Si selecciona un plan de cuotas insuficiente para el uso actual de la organización, recibirá un mensaje. Para guardar los cambios que haya efectuado en la página Editar
organización, pulse **GUARDAR**.
* En la sección Lista de organizaciones, puede ver todas las organizaciones del entorno
de {{site.data.keyword.Bluemix_notm}}.
	* Para suprimir la organización, pulse ![Suprimir](images/icon_trash.svg) en la columna Acciones.
	* Para ver y editar el plan de cuotas de una organización, pulse el nombre de la organización en la lista.
	* Para editar el nombre de la organización y añadir o eliminar gestores, pulse el nombre de la organización en la lista.

### Gestión de usuarios y permisos
{: #oc_useradmin}

Puede añadir usuarios a la instancia de {{site.data.keyword.Bluemix_notm}} del registro de usuarios de la empresa mediante LDAP. Puede añadir usuarios individualmente o en grupos, y ver los permisos de usuario. Si tiene asignado el permiso `admin`, también puede establecer y gestionar permisos de otros usuarios. Pulse **ADMINISTRACIÓN &gt; ADMINISTRACIÓN DE USUARIOS**.

La página Administración de usuarios muestra todos los usuarios para la instancia local o dedicada.
Se muestran los permisos para cada usuario. Los permisos pueden ser los siguientes: Ninguno, `Admin`, `Catalog`, `Login`,
`Reports` y `Users`. Los permisos se pueden habilitar o bien se puede asignar al usuario capacidad `view` o `write` para dicho permiso, representado mediante iconos. Consulte [Permisos](#permissions) para ver las descripciones
de cada tipo y las explicaciones de los iconos.

Elija una de las opciones siguientes:
* Localizar usuarios. Puede localizar usuarios en la tabla mediante el campo **Buscar**.
* Añadir usuarios. Si tiene el permiso `admin` o el permiso `users` con la capacidad `write`, puede añadir usuarios. Para añadir un usuario o un grupo de usuarios, pulse **AÑADIR UN SOLO USUARIO** o **AÑADIR GRUPO DE USUARIOS**. En el campo **Buscar**, escriba el nombre de usuario o nombre de grupo que desea buscar y seleccione la organización a la que desea añadir el usuario o el grupo de usuarios en la lista **Org**. Cuando encuentre el usuario o grupo que desea añadir, pulse el nombre de usuario y luego pulse **AÑADIR USUARIO** o **AÑADIR USUARIOS** para añadirlos.
Los grupos de más de 50 usuarios se añaden mediante un trabajo por lotes en segundo plano. Cuando la operación de añadir finaliza correctamente, el usuario o grupo se añade a la tabla para que lo pueda ver y buscar. Cuando se añaden usuarios, no tienen ningún permiso asignado.
* Editar permisos y organizaciones. Si tiene el permiso `admin`, puede editar permisos y organizaciones de otros usuarios. Para editar permisos, localice el usuario y pulse el nombre de usuario. Para habilitar o inhabilitar permisos, seleccione una de las opciones siguientes en la ventana que se abre:
	* Seleccione **Activado** en la lista para habilitar un permiso.
	* Seleccione **Leer** en la lista para que el usuario tenga la capacidad
`view` (solo lectura) sobre dicho permiso, o seleccione **Escribir** para asignar la
capacidad `write` (editar o añadir y eliminar) para dicho permiso.
	* Seleccione **Desactivado** para inhabilitar el permiso.
Para editar organizaciones, seleccione una de las siguientes opciones:
	* Para añadir el usuario a una organización, utilice el campo de búsqueda para localizar una organización, pulse para seleccionar una de las opciones y pulse **AÑADIR**.
	* Para eliminar un usuario de una organización, pulse el icono ![Eliminar, representado mediante un signo menos](images/icon_remove.svg).
Cuando termine, pulse **GUARDAR**.
* Eliminar usuarios. Si tiene el permiso `admin` o el permiso `users` con la capacidad `write`, puede eliminar usuarios.
Para eliminar un usuario, localice el usuario y pulse el icono ![Suprimir](images/icon_trash.svg) y, a continuación, **Eliminar**.

### Permisos
{: #permissions}

Se pueden asignar los siguientes permisos a los usuarios:

| **Permiso de usuario** | **Descripción** |       
|-----------------|-------------------|
| Admin | Los usuarios con el permiso `admin` pueden editar los permisos de otros usuarios. |
| Catálogo | A los usuarios con el permiso `catálogo` se les puede asignar la capacidad para `ver` o `grabar` (modificar) los servicios que están disponibles en la instancia local o dedicada. |  
| Login | Los usuarios con el permiso `login` pueden ver la página Administración. Sin este permiso, los usuarios no pueden ver la opción de menú Administración. |
| Reports | A los usuarios con el permiso `reports` se les puede asignar la capacidad `view` o `write` (modificar) sobre los informes de seguridad. |
| Users | A los usuarios con el permiso `users` se les puede asignar la capacidad `view` sobre la lista de usuarios o `write` (añadir o eliminar) sobre los usuarios. Este permiso no le permite definir permisos para otros usuarios.|

*Tabla 2. Permisos*

Los permisos se pueden habilitar o bien se puede asignar al usuario capacidad `view` o `write` para dicho permiso, representado mediante los siguientes iconos:

* El icono ![Habilitado, representado mediante una marca de selección](images/icon_enabled.svg) junto a un permiso significa que está habilitado.
* El icono ![Ver, representado mediante un ojo](images/icon_read.svg) significa que el usuario tiene la capacidad `view` (solo lectura) sobre dicho permiso.
* El icono ![Escribir, representado mediante un lápiz](images/icon_write.svg) significa que el usuario tiene la capacidad `write` (editar, añadir o eliminar) sobre dicho permiso.

### Gestión de usuarios con la API REST de administración
{: #usingadminapi}

Puede utilizar la API REST `Admin` para añadir y eliminar usuarios de la instancia de
{{site.data.keyword.Bluemix_notm}}.
Se proporcionan puntos finales de la API REST `Admin` y respuestas JSON a modo experimental para habilitar operaciones básicas desde una línea de mandatos. Los puntos finales y URL de los ejemplos de esta información pueden cambiar o pueden ser retirados previo aviso.

Las herramientas siguientes constituyen requisitos previos para utilizar los ejemplos siguientes. También puede utilizar otras herramientas.
* cURL, para especificar solicitudes de la API REST como mandatos. cURL es un programa de utilidad gratuito que puede utilizar para enviar solicitudes HTTP a un servidor y recibir las respuestas del servidor a través de una interfaz de línea de mandatos. Puede descargar
cURL del [Sitio de descargas de cURL](http://curl.haxx.se/download.html){: new_window}.
* Python, para utilizar la herramienta JSON pretty-print de Python. Esta herramienta opcional toma texto JSON como entrada y genera información de salida de fácil lectura. Puede descargar Python del [Sitio de descargas de Python](https://www.python.org/downloads){: new_window}.

#### Inicio de sesión en la consola de administración

Para poder ejecutar cualquier solicitud de la API `Admin`, debe iniciar una sesión en la consola de administración. Si tiene el permiso `admin` o el permiso `users` con la capacidad `write`, puede añadir o eliminar usuarios. Debe tener el permiso `admin` para poder editar los permisos de otros usuarios.

Para iniciar la sesión en la Consola de administración, puede utilizar la autenticación de acceso básica en el punto final
`https://<su_host>.ibm.com/login`. El servidor devuelve una cookie con la sesión. Utilice dicha cookie para todas las operaciones con la consola de administración.

**Nota:** La sesión deja de ser válida si no se utiliza durante unas cuantas horas.

Para iniciar una sesión en la consola de administración, ejecute el mandato siguiente:

`curl --user <id_usuario>:<contraseña> -c ./cookies.txt --header "Accept: application/json" https://<su_host>.ibm.com/login | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">--user <em>id_usuario</em>:<em>contraseña</em></dt>
<dd class="pd">Acepta el ID de usuario y la contraseña y envía una cabecera de autorización básica.</dd>


<dt class="pt dlterm">-c <em>nombre_archivo</em></dt>
<dd class="pd">Almacena el ID de usuario y la contraseña especificados como una cookie en el archivo especificado.</dd>


<dt class="pt dlterm">--header</dt>
<dd class="pd">Envía una cabecera de aceptación.</dd>

</dl>

El siguiente ejemplo muestra la salida de este mandato:
```
{
    "message": "Logged in",
    "name": {
        "familyName": "*apellido*",
        "givenName": "*nombre*"
    }
}
```
{: screen}

#### Listado de organizaciones
{: #listingorg}

Cuando añada un usuario, debe especificar una organización. Puede utilizar la API REST `Admin` para obtener una lista de todas las organizaciones. Debe tener el permiso
`users` con capacidad `read` para poder listar
organizaciones. Para listar todas las organizaciones, ejecute el mandato siguiente:

`curl -b ./cookies.txt https://<su_host>.ibm.com/codi/v1/organizations | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">-b <em>nombre_archivo</em></dt>
<dd class="pd">Pasa el ID de usuario y la contraseña que se han almacenado anteriormente con la opción <samp class="ph codeph">-c</samp> en el archivo al servidor HTTP como una cookie.</dd>

</dl>

Para cada organización, los resultados incluyen la siguiente información:
* `"guid"`, GUID de la organización
* `"name"`, nombre de la organización

El siguiente ejemplo muestra la salida de este mandato:
```
{
     "resources": [
         {
             "guid": "05af098d-d476-4fb0-8b87-a84350e72af3",
             "name": "org-1"
         },
         {
             "guid": "5129a5a8-37c2-4ee4-a9b2-bebae3531db5",
             "name": "org-2"
         },

		 		 ....

		 ],
		 "total_results": 284
}
```
{: screen}

#### Listado de usuarios
{: #listingusr}

Puede determinar si un usuario ya se ha añadido al entorno de
{{site.data.keyword.Bluemix_notm}} mediante
la API REST de `Admin` para obtener una lista de los usuarios registrados. Debe tener
el permiso `users` con capacidad `read` para poder listar usuarios registrados.
Para listar todos los usuarios, ejecute el mandato siguiente:

`curl -b ./cookies.txt https://<su_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>nombre_archivo</em></dt>
<dd class="pd">Pasa el ID de usuario y la contraseña que se han almacenado anteriormente con la opción <samp class="ph codeph">-c</samp> en el archivo al servidor HTTP como una cookie.</dd>
</dl>

Para cada usuario registrado, los resultados incluyen la siguiente información:
* `"first_name"` (nombre) y
                                `"last_name"` (apellido)
* `"user_id"`, ID de usuario y dirección de correo electrónico
* `"guid"`, GUID de la organización.
* `"permissions"` asignados al usuario para la consola de administración.

El siguiente ejemplo muestra la salida de este mandato:

```
{
    "next_url": "/codi/v1/users?results_per_page=100&amp;page=2",
    "prev_url": "",
    "resources": [
        {
            "active": true,
            "created_at": "2015-04-08T17:38:51.788Z",
            "created_by": "",
            "first_name": "some first name",
            "guid": "5d5268cf-39c0-48d3-96ae-7afe928e5dd7",
            "last_name": "some last name",
            "permissions": [
                {
                    "display": "ops.admin"
                },
                {
                    "display": "ops.catalog.write"
                },
                {
                    "display": "ops.reports.write"
                },
                {
                    "display": "ops.catalog.read"
                },
                {
                    "display": "ops.users.write"
                },
                {
                    "display": "ops.reports.read"
                },
                {
                    "display": "ops.login"
                },
                {
                    "display": "ops.users.read"
                }
            ],
            "user_id": "someid@us.ibm.com"
        },
		 		 ...


     }
    ],
    "total_pages": 395,
    "total_results": 39421
}

```
{: screen}

#### Adición de un usuario

Puede utilizar la API REST `Admin` para añadir usuarios a la instancia de
{{site.data.keyword.Bluemix_notm}}. Debe tener el permiso `users` con capacidad `write` para poder añadir usuarios.

Puede añadir un usuario o una lista de usuarios. Puede añadir usuarios a una única
organización, o a varias organizaciones.-->Para
añadir un usuario, debe proporcionar la información siguiente:

* Nombre y apellido del usuario. Especifique
`"nombre"` y `"apellido"` de [Listado de usuarios](index.html#listingusr).
* Dirección de correo electrónico e ID de usuario: especifique el `"id_usuario"` del [Listado de usuarios](index.html#listingusr) tanto para la dirección de correo electrónico como para el ID de usuario.
* `"guid"`. Especifique el GUID de la organización de [Listado de organizaciones](index.html#listingorg).

Debe proporcionar la información en un archivo JSON.

`curl -b ./cookies.txt https://<su_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>nombre_archivo</em></dt>
<dd class="pd">Pasa el ID de usuario y la contraseña que se han almacenado anteriormente con la opción <samp class="ph codeph">-c</samp> en el archivo al servidor HTTP como una cookie.</dd>
</dl>

<ol>
<li>Cree un archivo JSON que contenga la información en un formato JSON adecuado.
<p>Por ejemplo, cree un archivo llamado `user.json` con el siguiente contenido:</p>
<pre>
{
    "members": [
        {
            "emails": [
                "some_user_id@domain.com"
            ],
            "first_name": "Some_first_name",
            "last_name": "Some_last_name",
            "user_id": "some_user_id@domain.com"
        }
    ],
    "organization_roles": [
        {
            "id": "7a891f9c-e4e7-46c7-8b4e-dffaa7eb3bcd"
        }
    ]
}
</pre>
</li>
<li>Publique el contenido del archivo JSON en el punto final del usuario mediante la ejecución del mandato
siguiente:<br/><br/>
<code>
curl -v -b ./cookies.txt -X POST -H "Content-Type: application/json" -d @./user.json https://<su_host>.ibm.com/codi/v1/users
</code>
</li>
</ol>

<dl class="parml">

<dt class="pt dlterm">-v </dt>
<dd class="pd">Especifica salida detallada.</dd>


<dt class="pt dlterm">-X POST</dt>
<dd class="pd">Especifica una solicitud POST, alterando temporalmente la solicitud GET predeterminada.</dd>


<dt class="pt dlterm">-H "Content-Type: application/json"</dt>
<dd class="pd">Especifica la cabecera content-type, que en este caso es JSON.</dd>


<dt class="pt dlterm">-d *datos*</dt>
<dd class="pd">Especifica los datos, en este caso el archivo `user.json`, que se van a enviar en la solicitud POST al servidor HTTP.</dd>

</dl>



El siguiente ejemplo muestra la salida de este mandato:

```
* Connected to localhost (127.0.0.1) port 3000 (#0)
 > POST /codi/v1/users HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 > Content-Type: application/json
 > Content-Length: 333
 >
 * upload completely sent off: 333 out of 333 bytes
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < vary: X-HTTP-Method-Override
 < content-type: application/json
 < date: Wed, 22 Apr 2015 19:32:54 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 5612 msec
 ```
{: screen}

#### Eliminación de un usuario

Puede utilizar la API REST `Admin` para eliminar usuarios de la instancia de
{{site.data.keyword.Bluemix_notm}}. Debe tener el permiso `users` con capacidad `write` para poder eliminar usuarios.

Para eliminar un usuario, debe especificar el ID del usuario. Ejecute el mandato siguiente:

`curl -v -b ./cookies.txt -X DELETE https://<su_host>.ibm.com/codi/v1/users?user_id=<some_user_id@domain.com>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-X DELETE</dt>
<dd class="pd">Especifica una solicitud DELETE.</dd>
</dl>

El siguiente ejemplo muestra la salida de este mandato:

```
 * connect to ::1 port 3000 failed: Connection refused
 *   Trying 127.0.0.1...
 * Connected to localhost (127.0.0.1) port 3000 (#0)
 > DELETE /codi/v1/users?user_id=exampleuser@domain.com HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 >
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < content-type: application/json
 < date: Wed, 22 Apr 2015 21:01:09 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 1922 msec
 <
 ```
{: screen}

### API de servicio personalizado
{: #servicebrokerapi}

Hay tres API que puede utilizar para registrar o crear un nuevo servicio, actualizar un servicio y suprimir un servicio.

Todas las API son relativas a <code>https://opsconsole.&lt;subdomain&gt;.bluemix.net/</code>.

<dl>
<dt><strong>&lt;subdominio&gt;</strong></dt>
<dd>Este valor es el nombre de la instancia local o dedicada. El nombre del subdominio de la instancia {{site.data.keyword.Bluemix}} se ha asignado
durante la incorporación.</dd>
</dl>

### Registro de un nuevo servicio

Utilice la siguiente API y ejemplos de código para registrar un nuevo servicio.

#### Ruta

```
POST /codi/v1/serviceBrokers
```
{: screen}

#### Solicitud

*Tabla 3. Campos*

| **Nombre** | **Descripción** |
|-----------------|-------------------|
| name | Nombre del intermediario de servicio. |
| auth_username | Nombre de usuario utilizado para conectarse con el intermediario de servicio. |
| auth_password | Contraseña utilizada para conectarse con el intermediario de servicio. |
| broker_url | URL utilizada para conectarse al intermediario de servicio. |
| owningOrganization | Organización inicial con la que incluir en la lista blanca el servicio. |

##### Cuerpo

```
{
  "name" : "Service broker's name",
  "auth_username" : "username",
  "auth_password" : "password",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

##### Cabeceras

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### Respuesta

##### Estado

```
201 Created
```
{: screen}

##### Cuerpo

```
{
  "entity": {
    "name": "Service broker's name",
    "broker_url": "https://provision-broker.comp.bluemix.net/bmx/provisioning/brokers/2063580064-8f23230c-7f36-4ce5-a298-2ab4108f1120",
    "auth_username": "username",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "49f3adcc-ecc2-46fa-83c1-03322f04b3b1",
    "created_at": "2015-12-07T19:51:50Z",
    "updated_at": null,
    "url": "/v2/service_brokers/49f3adcc-ecc2-46fa-83c1-03322f04b3b1"
  }
}
```
{: screen}

### Actualización de un servicio

Utilice la siguiente API y ejemplos de código para actualizar un servicio.

#### Ruta

`PUT /codi/v1/serviceBrokers`
{: screen}

#### Solicitud

*Tabla 4. Campos*

| **Nombre** | **Descripción** |
|-----------------|-------------------|
| name | Nombre del intermediario de servicio. Este nombre no puede modificarse a partir del nombre con el que se ha creado el servicio. |
| auth_username | Nombre de usuario utilizado para conectarse con el intermediario de servicio. |
| auth_password | Contraseña utilizada para conectarse con el intermediario de servicio. |
| broker_url | URL utilizada para conectarse al intermediario de servicio. |
| owningOrganization | Organización inicial con la que incluir en la lista blanca el servicio. |

##### Cuerpo

```
{
  "name" : "Service Broker's name",
  "auth_username" : "username",
  "auth_password" : "newPassword",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

##### Cabeceras

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### Respuesta

##### Estado

```
201 Created
```
{: screen}

##### Cuerpo

```
{
  "entity": {
    "name": "Service Broker's name",
    "broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-d11bdd84-7556-469f-858d-2098b531f7f2",
    "auth_username": "username",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "2cbdb812-d37f-443b-894a-a96de31e5c38",
    "created_at": "2015-12-07T20:11:08Z",
    "updated_at": "2015-12-07T20:11:19Z",
    "url": "/v2/service_brokers/2cbdb812-d37f-443b-894a-a96de31e5c38"
  }
}
```
{: screen}

### Supresión de un servicio

Utilice la siguiente API y ejemplos de código para suprimir un servicio.

*Tabla 5. Parámetro*

| **Nombre** | **Descripción** |
|-----------------|-------------------|
| name | Nombre del intermediario de servicio. Este nombre no puede modificarse a partir del nombre con el que se ha creado el servicio. |

#### Ruta

```
DELETE /codi/v1/serviceBrokers?name=name of service broker
```
{: screen}

#### Solicitud

##### Cabeceras

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### Respuesta

##### Estado

```
204 No Content
```
{: screen}

### Gestión de usuarios con la CLI cf
{: #usingadmincli}

Puede gestionar usuarios del entorno Local o Dedicado de
{{site.data.keyword.Bluemix_notm}} o {{site.data.keyword.Bluemix_notm}} mediante
la interfaz de línea de mandatos de Cloud Foundry con el plug-in CLI de administración de
{{site.data.keyword.Bluemix_notm}}. Por ejemplo, puede añadir usuarios de un registro
de LDAP.

Antes de empezar, instale la interfaz de línea de mandatos cf. El plug-in CLI de administración de {{site.data.keyword.Bluemix_notm}} necesita
cf versión 6.11.2 o posterior. [Descargue la interfaz de línea de mandatos
de Cloud Foundry](https://github.com/cloudfoundry/cli/releases){: new_window}

**Restricción:** Cygwin no admite la interfaz de línea de mandatos de Cloud Foundry. Utilice esta interfaz en una ventana de línea de mandatos que no sea la ventana de Cygwin.

#### Adición del plug-in CLI de administración de {{site.data.keyword.Bluemix_notm}}

Una vez instalada la interfaz de línea de mandatos cf, puede añadir el plug-in CLI de administración de {{site.data.keyword.Bluemix_notm}}.

Siga estos pasos para añadir el repositorio e instalar
el plug-in:

<ol>
<li>Para añadir el repositorio de plugin de administración de {{site.data.keyword.Bluemix_notm}}, ejecute el mandato siguiente:<br/><br/> <code>
cf add-plugin-repo BluemixAdmin https://opsconsole.&lt;subdominio&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;subdominio&gt;</dt>
<dd class="pd">Subdominio del URL correspondiente a la instancia de {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>
</li>
<li>Para instalar el plug-in de CLI de administración de {{site.data.keyword.Bluemix_notm}}, ejecute el siguiente mandato:<br/><br/> <code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

Para ver una lista de mandatos, ejecute el mandato siguiente:

`cf plugins`
{: codeblock}

Para obtener más ayuda sobre un mandato, utilice la opción `-help`.

Para obtener más información sobre cómo trabajar con el plug-in CLI de administración de {{site.data.keyword.Bluemix_notm}}, consulte Administración de [{{site.data.keyword.Bluemix_notm}}](../cli/plugins/bluemix_admin/index.html).
