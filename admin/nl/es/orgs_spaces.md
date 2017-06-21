---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-03"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Creación de organizaciones y espacios
{: #orgsspacesusers}

Como propietario de la cuenta, puede gestionar las organizaciones y los espacios desde la página Gestionar organizaciones. Los gestores de organizaciones también pueden utilizar la página Gestionar organizaciones para gestionar todas las organizaciones en las que se han establecido como gestor.
{:shortdesc}

Para gestionar organizaciones y espacios, en la barra de menús de {{site.data.keyword.Bluemix_notm}} pulse **Gestionar** &gt; **Cuenta** &gt; **Organizaciones**. 

**Nota**: Debe ser el propietario de la cuenta de Pago según uso para crear una organización.

## Creación de organizaciones
{: #createorg}

Las organizaciones pueden abarcar varias regiones y se definen por los siguientes elementos:

<dl>
<dt>Miembros del equipo</dt>
<dd>El rol con permiso básico en las organizaciones y los espacios. Debe asignarse previamente a una organización
para que se le puedan otorgar otros permisos a los espacios en el seno de la organización. Para ver información detallada,
consulte [Usuarios y roles](/docs/iam/users_roles.html#userrolesinfo).</dd>
<dt>Dominios</dt>
<dd>Proporciona la ruta en Internet que se asigna a la organización. Una ruta tiene un subdominio y un dominio. Un subdominio suele ser el nombre de la app. Un dominio puede ser un dominio del sistema o un dominio personalizado que ha registrado para la aplicación. Consulte [Gestión de dominios personalizados](/docs/admin/manageorg.html#managedomains).<br/>
<p>**Nota:** Si añade un dominio personalizado, debe configurar el servidor DNS para resolver el dominio personalizado para que apunte al dominio del sistema de {{site.data.keyword.Bluemix_notm}}. De este modo, cuando {{site.data.keyword.Bluemix_notm}} recibe una solicitud para el dominio personalizado, puede direccionarlo correctamente a la app.</p></dd>
<dt>Cuota</dt>
<dd>Representa recursos disponibles para una organización, incluido el número de servicios y la cantidad de memoria que se puede asignar para que la utilice la organización. Las cuotas se asignan cuando se crean organizaciones. Cualquier aplicación o servicio en un espacio de una organización contribuye al uso de la cuota asignada. Con los planes Pague según uso o Suscripción, puede ajustar su cuota para los contenedores y apps de Cloud Foundry a medida que cambien las necesidades de su organización. Consulte [Gestión de cuota](/docs/admin/manageorg.html#managequota).
<p>**Nota:** En la cuenta de Suscripción, la cuota es un límite definido por el usuario que desencadena notificaciones de gastos.</p></dd>
</dl>

En {{site.data.keyword.Bluemix_notm}}, puede utilizar organizaciones para habilitar la colaboración entre miembros del equipo y facilitar la agrupación lógica de recursos de proyecto de las siguientes maneras:

<ul>
<li>Puede agrupar un conjunto de espacios, aplicaciones, servicios, dominios, rutas y miembros del equipo juntos en organizaciones.</li>
<li>Puede gestionar el acceso a los espacios y a las organizaciones usuario a usuario.</li>
</ul>

Cuando se crea una organización, el nombre de la organización debe ser exclusivo en {{site.data.keyword.Bluemix_notm}}. Si el nombre de la organización ya lo utiliza otro usuario local, dedicado o público de {{site.data.keyword.Bluemix_notm}}, debe especificar un nuevo nombre. Después de crear la organización, se le asignará automáticamente el permiso *Gestor de organización*, lo que le permite editar el nombre de la organización, añadir miembros de equipo y crear o suprimir espacios en la organización.

Utilice el mandato [`bx iam org-delete`](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_iam_org_delete) para suprimir organizaciones. Cuando se suprime una organización, todos los espacios, apps y servicios dentro de la organización se suprimen.

Los siguientes [roles de usuario](/docs/iam/users_roles.html#userrolesinfo) pueden asignarse a miembros del equipo en una organización:

<ul>
<li>Gestor de organización</li>
<li>Gestor de facturación de organización</li>
<li>Auditor de organización</li>
</ul>

Solamente los propietarios de cuentas con cuentas Pago según uso pueden crear una organización. Puede crear una organización completando los siguientes pasos:

1. Pulse **Gestionar** &gt; **Cuenta** &gt; **Organizaciones**.
2. Pulse **Añadir una nueva organización**.
3. Escriba el nombre de la organización.
4. Pulse **Añadir**.

<!-- Add info on Manage infrastructure option under a space -->

## Creación de espacios
{: #spaceinfo}

En el seno de una organización, podrá utilizar espacios para agrupar un conjunto de aplicaciones, servicios y miembros del equipo. Los espacios están vinculados a una región específica en {{site.data.keyword.Bluemix_notm}}.

Tras añadir miembros del equipo a una organización, puede otorgarles permisos a los espacios. Similar a las organizaciones, los espacios también tienen un conjunto de [roles de usuario](/docs/iam/users_roles.html#userrolesinfo) que se pueden asignar a los miembros del equipo:

<ul>
<li>Gestor de espacio</li>
<li>Desarrollador de espacio</li>
<li>Auditor de espacio</li>
</ul>

**Nota**: a un miembro del equipo se le puede asignar como mínimo uno de los permisos en el espacio.

Puede crear espacios en la organización; por ejemplo, un espacio *dev* como entorno de desarrollo, un espacio *test* como entorno de prueba y un espacio *production* como entorno de producción. Luego puede asociar sus apps a los espacios. Complete los siguientes pasos para crear un espacio:

1. Pulse **Gestionar** &gt; **Cuenta** &gt; **Organizaciones**.
2. Identifique la organización a la que desea añadir un espacio y seleccione **Ver detalles**.
4. Pulse **Añadir un espacio**.
5. Especifique el nombre de espacio.
6. Pulse **Añadir**.
