---



copyright:

  years: 2015, 2016
lastupdated: "2016-12-05"  


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestión de organizaciones y espacios
{: #orgsspacesusers}

Como propietario de la cuenta, puede gestionar las organizaciones accediendo a la página **Gestionar organizaciones**. Los gestores de organizaciones también pueden utilizar la página Gestionar organizaciones para gestionar todas las organizaciones en las que se han establecido como gestor.
{:shortdesc}

Las tareas de gestión incluyen las siguientes:

* Creación de una organización o un espacio
* Cambio de nombre de una organización
* Supresión de una organización o un espacio existente
* Listado de los miembros del equipo añadidos a la cuenta u organización
* Gestión o visualización de la cuota
* Gestión de dominios personalizados

**Nota**: Debe ser el propietario de la cuenta de Pago según uso para crear una organización.

## Organizaciones
{: #orginfo}

Las organizaciones pueden abarcar varias regiones y se definen por los siguientes elementos:

<dl>
<dt>Miembros del equipo</dt>
<dd>El rol con permiso básico en las organizaciones y los espacios. Debe asignarse previamente a una organización
para que se le puedan otorgar otros permisos a los espacios en el seno de la organización. Para ver información detallada,
consulte [Usuarios y roles](users_roles.html#userrolesinfo).</dd>
<dt>Dominios</dt>
<dd>Proporciona la ruta en Internet que se asigna a la organización. Una ruta tiene un subdominio y un dominio. Un subdominio suele ser el nombre de la app. Un dominio puede ser un dominio del sistema o un dominio personalizado que ha registrado para la aplicación. Consulte [Gestión de dominios personalizados](orgs_spaces.html#managedomains).<br/>
<p>**Nota**: Si añade un dominio personalizado, debe configurar el servidor DNS para resolver el dominio personalizado para que apunte al dominio del sistema de {{site.data.keyword.Bluemix_notm}}. De este modo, cuando {{site.data.keyword.Bluemix_notm}} recibe una solicitud para el dominio personalizado, puede direccionarlo correctamente a la app.</p></dd>
<dt>Cuota</dt>
<dd>Representa los límites de recursos para la organización, incluido el número de servicios y la cantidad de memoria que se puede asignar para que la utilice la organización. Las cuotas se asignan cuando se crean organizaciones. Cualquier app o servicio en un espacio de la organización contribuye al uso de la cuota. La cuota no es un límite aplicado. Es un desencadenante para notificaciones de gasto. Con los planes Pague según uso o Suscripción, puede ajustar su cuota para los contenedores y apps de Cloud Foundry a medida que cambien las necesidades de su organización. Consulte [Gestión de cuota](orgs_spaces.html#managequota).</dd>
</dl>

En {{site.data.keyword.Bluemix_notm}}, puede utilizar organizaciones para habilitar la colaboración entre miembros del equipo y facilitar la agrupación lógica de recursos de proyecto de las siguientes maneras:

<ul>
<li>Puede agrupar un conjunto de espacios, aplicaciones, servicios, dominios, rutas y miembros del equipo juntos en organizaciones.</li>
<li>Puede gestionar el acceso a los espacios y a las organizaciones usuario a usuario.</li>
</ul>

Cuando se crea una organización, el nombre de la organización debe ser exclusivo en {{site.data.keyword.Bluemix_notm}}. Si el nombre de la organización ya lo utiliza otro usuario local, dedicado o público de {{site.data.keyword.Bluemix_notm}}, debe especificar un nuevo nombre. Después de crear la organización, se le asignará automáticamente el permiso *Gestor de organización*, lo que le permite editar el nombre de la organización, añadir miembros de equipo y crear o suprimir espacios en la organización.

Debe ponerse en contacto con el [equipo de soporte de {{site.data.keyword.Bluemix_notm}} ![icono de enlace externo](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window} para suprimir una organización. Cuando solicita al equipo de soporte que suprima una organización, se suprimen todos los espacios, aplicaciones y servicios dentro de la organización.

Los siguientes [roles de usuario](/docs/admin/users_roles.html#userrolesinfo) pueden asignarse a miembros del equipo en una organización:

<ul>
<li>Gestor de organización</li>
<li>Gestor de facturación de organización</li>
<li>Auditor de organización</li>
</ul>

<!-- Add info on Manage infrastructure option under a space -->

## Espacios
{: #spaceinfo}

En el seno de una organización, podrá utilizar espacios para agrupar un conjunto de aplicaciones, servicios y miembros del equipo. Los espacios están vinculados a una región específica en {{site.data.keyword.Bluemix_notm}}.

Tras añadir miembros del equipo a una organización, puede otorgarles permisos a los espacios. Similar a las organizaciones, los espacios también tienen un conjunto de [roles de usuario](/docs/admin/users_roles.html#userrolesinfo) que se pueden asignar a los miembros del equipo:

<ul>
<li>Gestor de espacio</li>
<li>Desarrollador de espacio</li>
<li>Auditor de espacio</li>
</ul>

**Nota**: a un miembro del equipo se le puede asignar como mínimo uno de los permisos en el espacio.

## Creación de organizaciones y espacios
{: #createorg}

Solamente los propietarios de cuentas con cuentas Pago según uso pueden crear una organización. Puede crear una organización completando los siguientes pasos:

1. Pulse la página **Cuenta** &gt; **Gestionar organizaciones**.
2. Pulse **Añadir una nueva organización**.
3. Escriba el nombre de la organización.
4. Pulse **Añadir**.

Puede crear espacios en la organización; por ejemplo, un espacio *dev* como entorno de desarrollo, un espacio *test* como entorno de prueba y un espacio *production* como entorno de producción. Luego puede asociar sus apps a los espacios. Complete los siguientes pasos para crear un espacio:

1. Pulse la página **Cuenta** &gt; **Gestionar organizaciones**.
2. Identifique la organización a la que desea añadir un espacio y seleccione **Ver detalles**.
4. Pulse **Añadir un espacio**.
5. Especifique el nombre de espacio.
6. Pulse **Añadir**.

## Cambio de nombre de una organización
{: #orgrename}

Siga los pasos siguientes para cambiar el nombre de la organización:

1. Pulse la página **Cuenta** &gt; **Gestionar organizaciones**.
2. Identifique la organización que desea editar y seleccione **Ver detalles**.
3. Seleccione **Editar organización**.
4. Seleccione **Editar** para el título de la organización.
5. Escriba el nuevo nombre de organización.
6. Pulse **GUARDAR**.

## Supresión de una organización o un espacio existente
{: #deleteorgs}

Como propietario de la cuenta, puede ponerse en contacto con el [equipo de soporte de {{site.data.keyword.Bluemix_notm}} ![icono de enlace externo](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window} para suprimir una organización. 

**Nota**: La supresión de operaciones no se puede invertir. Perderá todas las apps y servicios asociados a la app.

Puede suprimir un espacio desde la página **Gestionar organizaciones**:

1. Pulse la página **Cuenta** &gt; **Gestionar organizaciones**.
2. Identifique la organización que desea editar y seleccione **Ver detalles**.
3. Identifique el espacio que desea suprimir y seleccione **Editar espacio**.
4. Pulse **Suprimir espacio**.

## Listado de miembros
{: #listmembers}

Complete los siguientes pasos para listar los miembros para una organización específica:

1. Pulse la página **Cuenta** &gt; **Gestionar organizaciones**.
2. Identifique la organización para la que desea ver los miembros y pulse **Ver detalles**.
3. Pulse **Editar organización**.
4. Puede ver los miembros de su organización y sus roles en el separador **USUARIOS**.

Complete los siguientes pasos para listar los miembros para un espacio específico:

1. Pulse la página **Cuenta** &gt; **Gestionar organizaciones**.
2. Identifique la organización para la que desea ver los miembros y pulse **Ver detalles**.
3. Identifique el espacio para el que desea ver los miembros y pulse **Editar espacio**.
4. Puede ver los miembros de su espacio y sus roles en el separador **USUARIOS**.

## Gestión de cuota
{: #managequota}

Como propietario de cuenta o gestor de organización de {{site.data.keyword.Bluemix_notm}}, puede ver la cuota utilizada y asignada para una organización. La cuota representa los límites de recursos para la organización que está asignada cuando se crea la organización. El límite no es una restricción que se aplica a una organización; es un desencadenante de notificaciones de gasto. Según si tiene una cuenta de prueba o una cuenta facturable, los recursos que están disponibles para una organización varían. Cualquier aplicación o servicio de un espacio de la organización contribuye al uso de la cuota asignada.

Para ver la cuota utilizada y asignada para una organización, realice los pasos siguientes:

1. Pulse la página **Cuenta** &gt; **Gestionar organizaciones**.
2. Identifique la organización para la que desea ver la cuota y pulse **Ver detalles**.
3. Pulse **Editar organización**.
4. Si tiene espacios definidos en más de una región, seleccione la región específica que desee ver.
5. Pulse **CUOTA**. 
6. De forma predeterminada, se abrirá la página de cuota **Cloud Foundry**. Puede ver los detalles de la cuota para los siguientes recursos:
 * MEMORIA
 * SERVICIOS
 * PLAN
 * PRECIO
7. Pulse **Contenedores** para ver la asignación de cuota de contenedor utilizada y disponible. La asignación de contenedor varía en función del plan de precios. Puede ver los detalles de la cuota para los siguientes recursos:
 * MEMORIA
 * IP PÚBLICA

**Nota:** Los contenedores no están disponibles en la región Sídney de {{site.data.keyword.Bluemix_notm}}. 

Para obtener más información sobre los contenedores, consulte [Cuota](/docs/containers/container_planning_org_ov.html#container_planning_quota) en la documentación de Contenedores.
Para cambiar la cuota asignada para una organización, debe abrir una incidencia de soporte. Para obtener más información sobre la apertura de una incidencia de soporte, consulte [Obtención de soporte al cliente](/docs/support/index.html#contacting-support). 

## Gestión de dominios
{: #managedomains}

Como propietario de cuenta o gestor de organización, puede ver el dominio del sistema y añadir dominios personalizados para aplicaciones que están incluidas dentro una organización y sus espacios. Como gestor de espacios, el separador **Dominios** para un espacio es una lista de solo lectura de los dominios asignados al espacio. 

1. Pulse la página **Cuenta** &gt; **Gestionar organizaciones**.
2. Identifique la organización para la que desea ver o editar los dominios.
3. Seleccione **Ver detalles** para esa organización.
4. Pulse **Editar organización**.
5. Pulse **DOMINIOS**.

Si añade un dominio personalizado, debe configurar el servidor DNS para resolver el dominio personalizado para que apunte al dominio del sistema de {{site.data.keyword.Bluemix_notm}}. De este modo, cuando {{site.data.keyword.Bluemix_notm}} recibe una solicitud para el dominio personalizado, puede direccionarlo correctamente a la app. El dominio del sistema siempre está disponible en un espacio y también se pueden asignar dominios personalizados a un espacio. Las aplicaciones creadas en un espacio pueden utilizar cualquiera de los dominios listados para ese espacio. Para obtener más información sobre cómo crear y utilizar dominios personalizados, consulte [Utilización de un dominio personalizado](/docs/manageapps/updapps.html#domain).
