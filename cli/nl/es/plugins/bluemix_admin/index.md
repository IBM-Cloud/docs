---

copyright:

  years: 2015, 2017

lastupdated: "2017-01-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI de admin de {{site.data.keyword.Bluemix_notm}}
{: #bluemixadmincli}


Puede gestionar el entorno de {{site.data.keyword.Bluemix_notm}} Local o {{site.data.keyword.Bluemix_notm}} Dedicated mediante la interfaz de línea de mandatos de Cloud Foundry con el plugin CLI de administración de {{site.data.keyword.Bluemix_notm}}. Por ejemplo, puede añadir usuarios de un registro
de LDAP. Si busca información sobre la gestión de su cuenta {{site.data.keyword.Bluemix_notm}} pública, consulte
[Administración](/docs/admin/adminpublic.html#administer).

Antes de empezar, instale la interfaz de línea de mandatos cf. El plug-in CLI de administración de {{site.data.keyword.Bluemix_notm}} necesita
cf versión 6.11.2 o posterior. [Descargue la interfaz de línea de mandatos
de Cloud Foundry ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}

**Restricción:** Cygwin no admite la interfaz de línea de mandatos de Cloud Foundry. Utilice esta interfaz en una ventana de línea de mandatos que no sea la ventana de Cygwin.

**Nota**: CLI de administración de {{site.data.keyword.Bluemix_notm}} sólo se utiliza para el entorno Local de {{site.data.keyword.Bluemix_notm}} y el entorno Dedicado de {{site.data.keyword.Bluemix_notm}}. No está soportado por {{site.data.keyword.Bluemix_notm}} Público.

## Adición del plug-in CLI de administración de {{site.data.keyword.Bluemix_notm}}

Una vez instalada la interfaz de línea de mandatos cf, puede añadir el plug-in CLI de administración de {{site.data.keyword.Bluemix_notm}}.

**Nota**: si ha instalado previamente el plugin Admin de {{site.data.keyword.Bluemix_notm}}, es posible que
tenga que desinstalarlo, suprimir el repositorio y luego volver a instalarlo para obtener las actualizaciones más recientes.

Siga estos pasos para añadir el repositorio e instalar el plug-in:

<ol>
<li>Para añadir el repositorio de plugin de administración de {{site.data.keyword.Bluemix_notm}}, ejecute el mandato siguiente:<br/><br/> <code>
cf add-plugin-repo BluemixAdmin https://console.&lt;subdominio&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;subdominio&gt;</dt>
<dd class="pd">Subdominio del URL correspondiente a la instancia de {{site.data.keyword.Bluemix_notm}}. Por ejemplo, <code>https://console.mycompany.bluemix.net/cli</code></dd>
</dl>
</li>
<li>Para instalar el plug-in CLI de administración de {{site.data.keyword.Bluemix_notm}}, ejecute el siguiente mandato:<br/><br/> <code>
cf install-plugin BluemixAdminCLI -r BluemixAdmin
</code>
</li>
</ol>

Si necesita desinstalar el plug-in, puede utilizar los mandatos siguientes y, a continuación, puede añadir el repositorio actualizado e instalar el plug-in más reciente:

* Desinstale el plug-in: `cf uninstall-plugin BluemixAdminCLI`
* Elimine el repositorio de plug-ins: `cf remove-plugin-repo BluemixAdmin`


## Utilización del plug-in CLI de administración de {{site.data.keyword.Bluemix_notm}}

Puede utilizar el plug-in CLI de administración de {{site.data.keyword.Bluemix_notm}} para añadir o eliminar usuarios, asignar o desasignar usuarios de organizaciones y para realizar otras tareas de gestión.

Para ver una lista de mandatos, ejecute el mandato siguiente:

```
cf plugins
```
{: codeblock}

Para obtener más ayuda sobre un mandato, utilice la opción `-help`.

### Conexión e inicio de sesión en {{site.data.keyword.Bluemix_notm}}

Para poder utilizar el plug-in CLI de administración, debe conectar e iniciar una sesión si
aún no lo ha hecho.

<ol>
<li>Para conectarse al punto final de API de {{site.data.keyword.Bluemix_notm}}, ejecute el siguiente mandato: <br/><br/>
<code>
cf ba api https://console.&lt;subdomain&gt;.bluemix.net
</code>
<dl class="parml">
<dt class="pt dlterm">&lt;subdominio&gt;</dt>
<dd class="pd">Subdominio del URL correspondiente a la instancia de {{site.data.keyword.Bluemix_notm}}.<br />
</dd>
</dl>
<p>Puede consultar la página Recursos e información de la Consola de administración para ver el URL correcto. El URL se muestra en la sección de información de la API, en el campo **URL de API**.</p>
</li>
<li>Inicie sesión en {{site.data.keyword.Bluemix_notm}} con el siguiente mandato:<br/><br/>
<code>
cf login
</code>
</li>
</ol>

## Administración de usuarios
{: #admin_users}

### Adición de un usuario
{: #admin_add_user}

Para añadir un usuario al entorno de {{site.data.keyword.Bluemix_notm}} desde el registro de usuarios
para su entorno, utilice el mandato siguiente:

```
cf ba add-user <nombre_usuario> <organización>
```
{: codeblock}

**Nota**: para añadir un usuario a una organización específica, debe ser un **Administrador** con el permiso **users.write** (o **Superusuario**). Si es un gestor de organización, también se le puede proporcionar la posibilidad de añadir usuarios a su organización mediante un Superusuario que ejecute el mandato **enable-managers-add-users**.  Consulte [Permitir a los gestores agregar usuarios](index.html#clius_emau) para obtener más información.

<dl class="parml">
<dt class="pt dlterm">&lt;nombre_usuario&gt;</dt>
<dd class="pd">El nombre del usuario en el registro de LDAP.</dd>
<dt class="pt dlterm">&lt;organización&gt;</dt>
<dd class="pd">El nombre o GUID de la organización {{site.data.keyword.Bluemix_notm}} a la que se va a añadir el usuario.</dd>
</dl>

**Sugerencia:** También puede usar **ba au** como alias para un nombre de mandato
de **ba add-user** más largo.

<!-- staging-only commands start. Live for interconnect -->

### Búsqueda de un usuario
{: #admin_search_user}

Para buscar un usuario, utilice el siguiente mandato junto con los parámetros de filtro de búsqueda opcionales
(nombre, permiso, organización y rol):

```
cf ba search-users -name=<user_name_value> -permission=<permission_value> -organization=<organization_value> -role=<role_value>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name_value&gt;</dt>
<dd class="pd">El nombre del usuario en {{site.data.keyword.Bluemix_notm}}. </dd>
<dt class="pt dlterm">&lt;permission_value&gt;</dt>
<dd class="pd">El permiso asignado al usuario. Por ejemplo, superusuario, básico, catálogo, usuario e informes. Para obtener más información sobre los permisos de usuario asignados, consulte [Permisos](/docs/admin/index.html#permissions). No se puede utilizar este parámetro con el parámetro de organización en la misma consulta. </dd>
<dt class="pt dlterm">&lt;organization_value&gt;</dt>
<dd class="pd">El nombre de la organización a la que pertenece el usuario. No se puede utilizar este parámetro con el parámetro de permiso en la misma consulta.</dd>
<dt class="pt dlterm">&lt;role_value&gt;</dt>
<dd class="pd">El rol de organización asignado al usuario. Por ejemplo, gestor, gestor de facturación o auditor de la organización. Especifique la organización con este parámetro. Para obtener más información acerca de los roles, consulte [Roles de usuario](/docs/admin/users_roles.html#userrolesinfo).</dd>

</dl>

**Sugerencia:** También puede usar **ba su** como alias para un nombre de mandato
de **ba search-users** más largo.

### Establecimiento de permisos para un usuario
{: #admin_setperm_user}

Para establecer permisos para un usuario especificado, utilice el siguiente mandato:

```
cf ba set-permissions <nombre_usuario> <permisos> <acceso>
```
{: codeblock}

**Nota**: puede establecer los permisos de uno en uno.

<dl class="parml">
<dt class="pt dlterm">&lt;nombre_usuario&gt;</dt>
<dd class="pd">El nombre del usuario en {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;permiso&gt;</dt>
<dd class="pd">Establecer los permisos para el usuario: Admin (una alternativa válida es Superusuario), Iniciar sesión (una alternativa válida es Básico), Catálogo (acceso de lectura o escritura),
Informes (acceso de lectura o escritura) o Usuarios (acceso de lectura o escritura).</dd>
<dt class="pt dlterm">&lt;acceso&gt;</dt>
<dd class="pd">Para permisos del Catálogo, Informes o Usuarios, también debe tener el nivel de acceso <code>read</code> o <code>write</code> (lectura o escritura).</dd>
</dl>

**Sugerencia:** También puede usar **ba sp** como alias para el nombre de mandato
**ba set-permissions** más largo.

<!-- staging-only commands end -->

### Eliminación de un usuario
{: #admin_remov_user}

Para eliminar un usuario del entorno de {{site.data.keyword.Bluemix_notm}}, utilice el siguiente mandato:

```
cf ba remove-user <nombre_usuario>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;nombre_usuario&gt;</dt>
<dd class="pd">El nombre del usuario en {{site.data.keyword.Bluemix_notm}}.</dd>

</dl>

**Sugerencia:** También puede usar **ba ru** como alias para un nombre de mandato
de **ba remove-user** más largo.

### Permitir a los gestores agregar usuarios
{: #clius_emau}

Si tiene el permiso **Superusuario** en el entorno de {{site.data.keyword.Bluemix_notm}}, puede permitir a los gestores de la organización que agreguen usuarios a las organizaciones que gestionan. Para permitir a los gestores añadir usuarios, utilice el mandato siguiente:

```
cf ba enable-managers-add-users
```
{: codeblock}

**Sugerencia:** también puede usar **ba emau** como alias para el nombre de mandato
**ba enable-managers-add-users** más largo.

### No permitir a los gestores agregar usuarios
{: #clius_dmau}

Si a los gestores de la organización se les permite agregar usuarios a las organizaciones que gestionan en el entorno de {{site.data.keyword.Bluemix_notm}} con el mandato **enable-managers-add-users**, y si tiene el permiso **Superusuario**, puede eliminar este valor.  Para no permitir a los gestores añadir usuarios, utilice el mandato siguiente:

```
cf ba disable-managers-add-users
```
{: codeblock}

**Sugerencia:** también puede usar **ba dmau** como alias para un nombre de mandato
**ba disable-managers-add-users** más largo.

## Administración de organizaciones
{: #admin_orgs}

### Adición de una organización
{: #admin_add_org}

Para añadir una organización, utilice el siguiente mandato:

```
cf ba create-organization <organización> <gestor>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organización&gt;</dt>
<dd class="pd">El nombre o GUID de la organización de {{site.data.keyword.Bluemix_notm}} que va a añadir.</dd>
<dt class="pt dlterm">&lt;gestor&gt;</dt>
<dd class="pd">El nombre de usuario del gestor de la organización.</dd>
</dl>

**Sugerencia:** También puede usar **ba co** como alias para el nombre de mandato
**ba create-organization** más largo.

### Supresión de una organización
{: #admin_delete_org}

Para suprimir una organización, utilice el siguiente mandato:

```
cf ba delete-organization <organización>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organización&gt;</dt>
<dd class="pd">El nombre o GUID de la organización de {{site.data.keyword.Bluemix_notm}} que va a suprimir.</dd>
</dl>

**Sugerencia:** También puede usar **ba do** como alias para un nombre de mandato
de **ba delete-organization** más largo.

### Asignación de un usuario a una organización
{: #admin_ass_user_org}

Para asignar un usuario del entorno de {{site.data.keyword.Bluemix_notm}} a una
organización concreta, utilice el siguiente mandato:

```
cf ba set-org <nombre_usuario> <organización> [<rol>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nombre_usuario&gt;</dt>
<dd class="pd">El nombre del usuario en {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organización&gt;</dt>
<dd class="pd">El nombre o GUID de la organización {{site.data.keyword.Bluemix_notm}} a la que se va a asignar el usuario.</dd>
<dt class="pt dlterm">&lt;rol&gt;</dt>
<dd class="pd">Consulte [Roles](/docs/admin/users_roles.html) para ver los roles de usuario de {{site.data.keyword.Bluemix_notm}} y sus descripciones.</dd>
</dl>

**Sugerencia:** También puede usar **ba so** como alias para el nombre de mandato
**ba set-org** más largo.

### Eliminación de la asignación de un usuario de una organización
{: #admin_unass_user_org}

Para desasignar un usuario del entorno de {{site.data.keyword.Bluemix_notm}} desde una
organización concreta, utilice el siguiente mandato:

```
cf ba unset-org <nombre_usuario> <organización> [<rol>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nombre_usuario&gt;</dt>
<dd class="pd">El nombre del usuario en {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organización&gt;</dt>
<dd class="pd">El nombre o GUID de la organización {{site.data.keyword.Bluemix_notm}} a la que se va a asignar el usuario.</dd>
<dt class="pt dlterm">&lt;rol&gt;</dt>
<dd class="pd">Consulte [Asignación de roles](/docs/admin/users_roles.html) para
roles y descripciones de usuarios de {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>

**Sugerencia:** También puede usar **ba uo** como alias para un nombre de mandato
de **ba unset-org** más largo.

#### Asignación de roles

<dl class="parml">
<dt class="pt dlterm">OrgManager</dt>
<dd class="pd">Gestor de la organización. Un gestor de la organización tiene autorización para realizar las siguientes acciones:
<ul>
<li>Crea o suprime espacios en la organización.</li>
<li>Invita a usuarios a la organización y gestiona usuarios.</li>
<li>Gestiona dominios de la organización.</li>
</ul>
</dd>
<dt class="pt dlterm">BillingManager</dt>
<dd class="pd">Gestor de facturación. Un gestor de facturación puede ver información de uso de tiempo de ejecución y servicio para la organización.</dd>
<dt class="pt dlterm">OrgAuditor</dt>
<dd class="pd">Auditor de la organización. Un auditor de la organización puede ver el contenido de la app y el servicio en el espacio.</dd>
</dl>

### Configuración de una cuota para una organización
{: #admin_set_org_quota}

Para establecer la cuota de uso para una organización concreta, utilice el mandato siguiente:

```
cf ba set-quota <organización> <plan>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organización&gt;</dt>
<dd class="pd">El nombre o GUID de la organización de {{site.data.keyword.Bluemix_notm}} para la que va a definir la cuota.</dd>
<dt class="pt dlterm">&lt;plan&gt;</dt>
<dd class="pd">El plan de cuotas de una organización.</dd>
</dl>

**Sugerencia:** También puede usar **ba sq** como alias para el nombre de mandato
**ba set-quota** más largo.


### Búsqueda de cuotas de contenedor para una organización
{: #admin_find_containquotas}

Para buscar la cuota de contenedores para una organización, utilice el siguiente mandato:

```
cf bluemix-admin containers-quota <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organización&gt;</dt>
<dd class="pd">Nombre o ID de la organización en Bluemix. Este
parámetro es obligatorio.</dd>
</dl>

**Sugerencia:** también puede usar **ba cq** como alias para el nombre de mandato
**bluemix-admin containers-quota** más largo.

### Configuración de cuotas de contenedor para una organización
{: #admin_set_containquotas}

Para definir la cuota de contenedores para una organización, utilice el siguiente mandato con al menos una de las opciones que se incluyen:

```
cf bluemix-admin set-containers-quota <organization> <options>
```
{: codeblock}

**Nota**: puede incluir varias opciones, pero debe incluir al menos una.

<dl class="parml">
<dt class="pt dlterm">&lt;organización&gt;</dt>
<dd class="pd">Nombre o ID de la organización en Bluemix. Este
parámetro es obligatorio.</dd>
<dt class="pt dlterm">&lt;options&gt;</dt>
<dd class="pd">Incluya una o varias de las opciones siguientes en las que el valor debe ser un entero:
<ul>
<li>floating-ips-max &lt;value&gt;</li>
<li>floating-ips-space-default &lt;value&gt;</li>
<li>memory-max &lt;value&gt;</li>
<li>memory-space-default &lt;value&gt;</li>
<li>image-limit &lt;value&gt;</li>
</ul>
</dd>
</dl>

**Consejo:** También puede utilizar los siguientes nombres abreviados como alias de nombres de opciones más largos:
<dl class="parml">
<dt class="pt dlterm">floating-ips-max &lt;value&gt;</dt>
<dd class="pd"><strong>fim</strong></dd>
<dt class="pt dlterm">floating-ips-space-default &lt;value&gt;</dt>
<dd class="pd"><strong>fisd</strong></dd>
<dt class="pt dlterm">memory-max &lt;value&gt;</dt>
<dd class="pd"><strong>mm</strong></dd>
<dt class="pt dlterm">memory-space-default &lt;value&gt;</dt>
<dd class="pd"><strong>msd</strong></dd>
<dt class="pt dlterm">image-limit &lt;value&gt;</dt>
<dd class="pd"><strong>il</strong></dd>
</dl>

Si lo desea, puede especificar un archivo que contenga parámetros de configuración específicos en un objeto JSON válido. Si utiliza la opción **-file**, esta prevalece y las otras opciones se pasan por alto. Para proporcionar un archivo en lugar de definir las opciones, utilice el siguiente mandato:

```
cf bluemix-admin set-containers-quota <organization> <-file path_to_JSON_file>
```
{: codeblock}

El archivo JSON debe tener el formato que se muestra en el ejemplo siguiente:

```
{
  "floating_ips_max": 10,
  "floating_ips_space_default": 0,
  "ram_max": 4096,
  "ram_space_default": 0,
  "image_limit": 10
}
```
{: codeblock}

**Sugerencia:** también puede usar **ba scq** como alias para el nombre de mandato
**bluemix-admin set-containers-quota** más largo.

### Habilitación de servicios para todas las organizaciones
{: #admin_ena_service_org}

Para permitir que un servicio se muestre en el Catálogo de
{{site.data.keyword.Bluemix_notm}} para todas
las organizaciones, utilice el siguiente mandato:

```
cf ba enable-service-plan <identificador_plan>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;identificador_plan&gt;</dt>
<dd class="pd">Nombre o GUID del plan de servicio que desea habilitar. Si especifica un nombre de plan de servicio no exclusivo, por ejemplo "Estándar" o "Básico", se le ofrecerán planes de servicio entre los que elegir. Para identificar el nombre de un plan de servicio, seleccione la categoría de servicio en la página de inicio y, a continuación, seleccione **Añadir** para ver los servicios para dicha categoría. Pulse el nombre de servicio para abrir la vista de detalles y luego podrá ver los nombres de los planes de servicio disponibles para dicho servicio. </dd>
</dl>

**Sugerencia:** También puede usar **ba esp** como alias para el nombre de mandato
**ba enable-service-plan** más largo.

### Inhabilitación de servicios para todas las organizaciones
{: #admin_dis_service_org}

Para no permitir que un servicio sea visible en el Catálogo de {{site.data.keyword.Bluemix_notm}} para todas las
organizaciones, utilice el siguiente mandato:

```
cf ba disable-service-plan <identificador_plan>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;identificador_plan&gt;</dt>
<dd class="pd">Nombre o GUID del plan de servicio que desea habilitar. Si especifica un nombre de plan de servicio no exclusivo, por ejemplo "Estándar" o "Básico", se le ofrecerán planes de servicio entre los que elegir. Para identificar el nombre de un plan de servicio, seleccione la categoría de servicio en la página de inicio y, a continuación, seleccione **Añadir** para ver los servicios para dicha categoría. Pulse el nombre de servicio para abrir la vista de detalles y luego podrá ver los nombres de los planes de servicio disponibles para dicho servicio.</dd>
</dl>

**Sugerencia:** También puede usar **ba dsp** como alias para un nombre de mandato
de **ba disable-service-plan** más largo.

### Adición de la visibilidad de los servicios de las organizaciones
{: #admin_addvis_service_org}

Puede añadir una organización de la lista de organizaciones que pueden ver un servicio específico en el Catálogo de {{site.data.keyword.Bluemix_notm}}. Para permitir que una organización pueda ver un servicio específico en el Catálogo de
{{site.data.keyword.Bluemix_notm}}, utilice el siguiente mandato:

```
cf ba add-service-plan-visibility <identificador_plan> <organización>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;identificador_plan&gt;</dt>
<dd class="pd">Nombre o GUID del plan de servicio que desea habilitar. Si especifica un nombre de plan de servicio no exclusivo, por ejemplo "Estándar" o "Básico", se le ofrecerán planes de servicio entre los que elegir. Para identificar el nombre de un plan de servicio, seleccione la categoría de servicio en la página de inicio y, a continuación, seleccione **Añadir** para ver los servicios para dicha categoría. Pulse el nombre de servicio para abrir la vista de detalles y luego podrá ver los nombres de los planes de servicio disponibles para dicho servicio.</dd>
<dt class="pt dlterm">&lt;organización&gt;</dt>
<dd class="pd">El nombre o GUID de la organización de {{site.data.keyword.Bluemix_notm}} que va a agregar a la lista de visibilidad del servicio.</dd>
</dl>

**Sugerencia:** También puede usar **ba aspv** como alias para el nombre de mandato
**ba add-service-plan-visibility** más largo.

### Eliminación de la visibilidad de los servicios de las organizaciones
{: #admin_remvis_service_org}

Puede eliminar una organización de la lista de organizaciones que pueden ver un servicio
específico en el Catálogo de {{site.data.keyword.Bluemix_notm}}. Para eliminar la visibilidad de un servicio en el Catálogo de
{{site.data.keyword.Bluemix_notm}} de una
organización, utilice el siguiente mandato:

```
cf ba remove-service-plan-visibility <identificador_plan> <organización>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;identificador_plan&gt;</dt>
<dd class="pd">Nombre o GUID del plan de servicio que desea habilitar. Si especifica un nombre de plan de servicio no exclusivo, por ejemplo "Estándar" o "Básico", se le ofrecerán planes de servicio entre los que elegir. Para identificar el nombre de un plan de servicio, seleccione la categoría de servicio en la página de inicio y, a continuación, seleccione **Añadir** para ver los servicios para dicha categoría. Pulse el nombre de servicio para abrir la vista de detalles y luego podrá ver los nombres de los planes de servicio disponibles para dicho servicio.</dd>
<dt class="pt dlterm">&lt;organización&gt;</dt>
<dd class="pd">El nombre o GUID de la organización de {{site.data.keyword.Bluemix_notm}} que va a eliminar de la lista de visibilidad del servicio.</dd>
</dl>

**Sugerencia:** También puede usar **ba rspv** como alias para un nombre de mandato
de **ba remove-service-plan-visibility** más largo.

### Edición de la visibilidad de los servicios de las organizaciones
{: #admin_editvis_service_org}

Puede editar y sustituir la lista de servicios que pueden ver determinadas organizaciones en el Catálogo de {{site.data.keyword.Bluemix_notm}}. Para sustituir todos los servicios visibles existentes de una o varias organizaciones, utilice el mandato siguiente:

```
cf ba edit-service-plan-visibilities <identificador_plan> <organización_1> <organización_2_opcional>
```
{: codeblock}

**Nota:** Este mandato sustituye los servicios visibles existentes de las organizaciones especificadas por el servicio que especifique en el mandato.

<dl class="parml">
<dt class="pt dlterm">&lt;identificador_plan&gt;</dt>
<dd class="pd">Nombre o GUID del plan de servicio que desea habilitar. Si especifica un nombre de plan de servicio no exclusivo, por ejemplo "Estándar" o "Básico", se le ofrecerán planes de servicio entre los que elegir. Para identificar el nombre de un plan de servicio, seleccione la categoría de servicio en la página de inicio y, a continuación, seleccione **Añadir** para ver los servicios para dicha categoría. Pulse el nombre de servicio para abrir la vista de detalles y luego podrá ver los nombres de los planes de servicio disponibles para dicho servicio.</dd>
<dt class="pt dlterm">&lt;organización&gt;</dt>
<dd class="pd">El nombre o GUID de la organización de {{site.data.keyword.Bluemix_notm}} a la que va a agregar visibilidad. Puede habilitar la visibilidad del servicio a más de una organización especificando nombres de organización o GUID adicionales en el mandato.</dd>
</dl>

**Sugerencia:** También puede usar **ba espv** como alias para el nombre de mandato
**ba edit-service-plan-visibility** más largo.

## Administración de informes
{: #admin_add_report}

### Adición de informes
{: #admin_add_report}

Para añadir un informe de seguridad, utilice el siguiente mandato:

```
cf ba add-report <categoría> <fecha> <PDF|TXT|LOG> <RTF>
```
{: codeblock}

**Nota**: Si tiene acceso de escritura para el permiso de informes, puede crear una nueva categoría y añadir un informe en cualquiera de los formatos aceptados para sus usuarios. Especifique el nombre de la nueva categoría para el parámetro `category` o añada su informe en una categoría existente.

<dl class="parml">
<dt class="pt dlterm">&lt;categoría&gt;</dt>
<dd class="pd">La categoría del informe. Utilice las comillas si hay un espacio en el nombre.</dd>
<dt class="pt dlterm">&lt;fecha&gt;</dt>
<dd class="pd">La fecha del informe con el formato <samp class="ph codeph">AAAAMMDD</samp>.</dd>
<dt class="pt dlterm">&lt;PDF|TXT|LOG&gt;</dt>
<dd class="pd">La vía de acceso del PDF del informe, del archivo de texto o de registro que va a cargar.</dd>
<dt class="pt dlterm">&lt;RTF&gt;</dt>
<dd class="pd">Opción para incluir una versión de formato de texto enriquecido (RTF) del PDF. Esta opción solo se aplica si ha incluido una vía de acceso al PDF del informe. La versión RTF se utiliza para indexar y buscar.</dd>
</dl>

**Sugerencia:** También puede usar **ba ar** como alias para un nombre de mandato
de **ba add-report** más largo.

### Supresión de informes
{: #admin_del_report}

Para suprimir un informe de seguridad, utilice el siguiente mandato:

```
cf ba delete-report <categoría> <fecha> <nombre>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;categoría&gt;</dt>
<dd class="pd">La categoría del informe. Utilice las comillas si hay un espacio en el nombre.</dd>
<dt class="pt dlterm">&lt;fecha&gt;</dt>
<dd class="pd">La fecha del informe con el formato <samp class="ph codeph">AAAAMMDD</samp>.</dd>
<dt class="pt dlterm">&lt;nombre&gt;</dt>
<dd class="pd">El nombre del informe.</dd>
</dl>

**Sugerencia:** También puede usar **ba dr** como alias para el nombre de mandato
**ba delete-report** más largo.

### Recuperación de informes
{: #admin_retr_report}

Para recuperar un informe de seguridad, utilice el siguiente mandato:

```
cf ba retrieve-report <categoría> <fecha> <nombre>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;categoría&gt;</dt>
<dd class="pd">La categoría del informe. Utilice las comillas si hay un espacio en el nombre.</dd>
<dt class="pt dlterm">&lt;fecha&gt;</dt>
<dd class="pd">La fecha del informe con el formato <samp class="ph codeph">AAAAMMDD</samp>.</dd>
<dt class="pt dlterm">&lt;nombre&gt;</dt>
<dd class="pd">El nombre del informe.</dd>
</dl>

**Sugerencia:** También puede usar **ba rr** como alias para un nombre de mandato
de **ba retrieve-report** más largo.

## Visualización de información de métricas de recursos
{: #cliresourceusage}

Puede ver información sobre métricas de recursos, incluidos el uso de memoria, de disco y de CPU. Puede ver un resumen de los recursos reservados y físicos disponibles, así como el uso de los recursos reservados y físicos. También puede ver los datos de uso de DEA (Droplet Execution Agent) y el uso del disco y de la memoria histórica. Se mostrarán los datos históricos para el uso de la memoria y del disco, de forma predeterminada, de forma semanal y en orden descendente. Para ver la información de métricas de recursos, utilice el mandato siguiente:

```
cf ba resource-metrics <monthly> <weekly>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;mensualmente&gt;</dt>
<dd class="pd">Ver los datos históricos para el espacio de disco y de memoria al mes a la vez.</dd>
<dt class="pt dlterm">&lt;semanalmente&gt;</dt>
<dd class="pd">Ver los datos históricos para el espacio de disco y de memoria a la semana a la vez. Este es el valor predeterminado.</dd>
</dl>

**Sugerencia:** también puede usar **ba rsm** como alias para el nombre de mandato
**ba resource-metrics** más largo.


## Administración de intermediarios de servicio
{: #admin_servbro}

### Listado de intermediarios de servicio
{: #clilistservbro}

Para listar todos los intermediarios de servicio, utilice el mandato siguiente:

```
cf ba service-brokers <nombre_intermediario>
```
{: codeblock}

**Nota**: Para mostrar una lista de todos los intermediarios de servicio, especifique el mandato sin el parámetro
`nombre_intermediario`.

<dl class="parml">
<dt class="pt dlterm">&lt;nombre_intermediario&gt;</dt>
<dd class="pd">Opcional: El nombre del intermediario de servicio personalizado. Utilice este parámetro, si quiere obtener información
para un intermediario de servicio específico.</dd>
</dl>

**Sugerencia:** También puede usar **ba sb** como alias para un nombre de mandato
de **ba service-brokers** más largo.

### Adición de un intermediario de servicio
{: #cliaddservbro}

Para añadir un intermediario de servicio, con lo que puede añadir un servicio personalizado a su Catálogo de
{{site.data.keyword.Bluemix_notm}}, utilice el siguiente mandato:

```
cf ba add-service-broker <nombre_intermediario> <nombre_usuario> <contraseña> <url_intermediario>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nombre_intermediario&gt;</dt>
<dd class="pd">El nombre del intermediario de servicio personalizado.</dd>
<dt class="pt dlterm">&lt;nombre_usuario&gt;</dt>
<dd class="pd">El nombre de usuario de la cuenta que tiene acceso al intermediario de servicios.</dd>
<dt class="pt dlterm">&lt;contraseña&gt;</dt>
<dd class="pd">La contraseña de la cuenta que tiene acceso al intermediario de servicios.</dd>
<dt class="pt dlterm">&lt;url_intermediario&gt;</dt>
<dd class="pd">El URL del intermediario de servicio.</dd>
</dl>

**Sugerencia:** También puede usar **ba asb** como alias para el nombre de mandato
**ba add-service-broker** más largo.

### Supresión de un intermediario de servicio
{: #clidelservbro}

Para suprimir un intermediario de servicio, para eliminar el servicio personalizado del Catálogo de
{{site.data.keyword.Bluemix_notm}}, utilice el mandato siguiente:

```
cf ba delete-service-broker <intermediario_servicio>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;intermediario_servicio&gt;</dt>
<dd class="pd">El nombre o GUID del intermediario de servicio personalizado.</dd>
</dl>

**Sugerencia:** También puede usar **ba dsb** como alias para un nombre de mandato
de **ba delete-service-broker** más largo.

### Actualización de un intermediario de servicio
{: #cliupdservbro}

Para actualizar un intermediario de servicio, utilice el siguiente mandato:

```
cf ba update-service-broker <broker_name> <user_name> <password> <broker_url>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nombre_intermediario&gt;</dt>
<dd class="pd">El nombre del intermediario de servicio personalizado.</dd>
<dt class="pt dlterm">&lt;nombre_usuario&gt;</dt>
<dd class="pd">El nombre de usuario de la cuenta que tiene acceso al intermediario de servicios.</dd>
<dt class="pt dlterm">&lt;contraseña&gt;</dt>
<dd class="pd">La contraseña de la cuenta que tiene acceso al intermediario de servicios.</dd>
<dt class="pt dlterm">&lt;url_intermediario&gt;</dt>
<dd class="pd">El URL del intermediario de servicio.</dd>
</dl>

**Sugerencia:** También puede usar **ba usb** como alias para el nombre de mandato
**ba update-service-broker** más largo.


## Administración de grupos de seguridad de aplicaciones
{: #admin_secgro}

Para trabajar con grupos de seguridad de aplicaciones (ASG), debe ser un administrador con acceso completo al entorno local o dedicado. Todos los usuarios del entorno pueden mostrar una lista de los ASG disponibles para la organización que el mandato tiene como objetivo. No obstante, para crear, actualizar o enlazar ASG, debe ser administrador del entorno de {{site.data.keyword.Bluemix_notm}}.

Los ASG funcionan como cortafuegos virtuales que controlan el tráfico de salida de las aplicaciones del entorno de
{{site.data.keyword.Bluemix_notm}}. Cada ASG está compuesto por una lista de reglas que permiten comunicaciones y tráfico específicos hacia y desde el exterior de la red. Puede enlazar uno o más ASG con un conjunto de grupos de seguridad específico, por ejemplo, un conjunto de grupos que se utiliza para aplicar el acceso global, o puede enlazar con espacios dentro de la organización en el entorno de
{{site.data.keyword.Bluemix_notm}}.

{{site.data.keyword.Bluemix_notm}} se configura inicialmente con todo el acceso a la red externa restringido. Dos grupos de seguridad creados por IBM, `public_networks` y `dns`, permiten el acceso global a la red externa al enlazar dichos grupos con los conjuntos de grupos de seguridad de Cloud Foundry predeterminados. Los dos conjuntos de grupos de seguridad de Cloud Foundry que se utilizan para aplicar el acceso global son los conjuntos de grupos **Default Staging** y **Default Running**. Estos conjuntos de grupos aplican las reglas para permitir tráfico hacia todas las apps en ejecución o todas las apps en transferencia. Si no desea enlazar estos dos conjuntos de grupos de seguridad, puede desenlazarlos de los conjuntos de grupos de Cloud Foundry y, a continuación, enlazar el grupo de seguridad con un espacio específico. Para obtener más información, consulte [Enlace de grupos de seguridad de aplicaciones ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window}.

**Nota**: los mandatos siguientes que le permiten trabajar con grupos de seguridad se basan en la versión 1.6 de Cloud Foundry. Para obtener más información, incluidos los campos obligatorios y opcionales, consulte la información de Cloud Foundry sobre [Creación de grupos de seguridad de aplicaciones ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#creating-groups){: new_window}.

### Listado de grupos de seguridad
{: #clilissecgro}

* Para listar todos los grupos de seguridad, utilice el siguiente mandato:

```
cf ba security-groups
```
{: codeblock}

**Sugerencia:** también puede usar **ba sgs** como alias para el nombre de mandato
**ba security-groups** más largo.

* Para mostrar detalles para un grupo de seguridad específico, utilice el mandato siguiente:

```
cf ba security-groups <grupo-seguridad>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;grupo-seguridad&gt;</dt>
<dd class="pd">Nombre del grupo de seguridad</dd>
</dl>

**Sugerencia:** también puede usar **ba sg** como alias para el nombre de mandato
**ba security-groups** más largo con el parámetro `security-group`.


### Creación de un grupo de seguridad
{: #clicreasecgro}

Para obtener más información sobre la creación de grupos de seguridad y las reglas que definen el tráfico de salida, consulte
[Creación de grupos de seguridad de aplicaciones ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#creating-groups){: new_window}.

Para crear un grupo de seguridad, utilice el siguiente mandato:

```
cf ba create-security-group <grupo-seguridad> <vía-acceso-archivo-reglas>
```
{: codeblock}

Cada grupo de seguridad que cree tiene el prefijo
`adminconsole_` añadido al nombre para distinguirlo de los grupos de seguridad creados por IBM.

<dl class="parml">
<dt class="pt dlterm">&lt;grupo-seguridad&gt;</dt>
<dd class="pd">Nombre del grupo de seguridad</dd>
<dt class="pt dlterm">&lt;vía-acceso-archivo-reglas&gt;</dt>
<dd class="pd">Vía de acceso absoluta o relativa al archivo de reglas</dd>
</dl>

**Sugerencia:** También puede usar **ba csg** como alias para un nombre de mandato
de **ba create-security-group** más largo.

### Actualización de un grupo de seguridad
{: #cliupdsecgro}

Para actualizar un grupo de seguridad, utilice el siguiente mandato:

```
cf ba update-security-group <grupo-seguridad> <vía-acceso-archivo-reglas>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;grupo-seguridad&gt;</dt>
<dd class="pd">Nombre del grupo de seguridad</dd>
<dt class="pt dlterm">&lt;vía-acceso-archivo-reglas&gt;</dt>
<dd class="pd">Vía de acceso absoluta o relativa al archivo de reglas</dd>
</dl>

**Sugerencia:** también puede usar **ba usg** como alias para el nombre de mandato
**ba update-security-group** más largo.

### Supresión de un grupo de seguridad
{: #clidelsecgro}

Para suprimir un grupo de seguridad, utilice el siguiente mandato:

```
cf ba delete-security-group <grupo-seguridad>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;grupo-seguridad&gt;</dt>
<dd class="pd">Nombre del grupo de seguridad</dd>
</dl>

**Sugerencia:** También puede usar **ba dsg** como alias para un nombre de mandato
de **ba delete-security-group** más largo.


### Enlace de grupos de seguridad
{: #clibindsecgro}

Para obtener más información sobre el enlace de grupos de seguridad, consulte [Enlace de grupos de seguridad de aplicaciones ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window}.

* Para enlazar con el conjunto de grupos de seguridad Default Staging, utilice el siguiente mandato:

```
cf ba bind-staging-security-group <grupo-seguridad>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;grupo-seguridad&gt;</dt>
<dd class="pd">Nombre del grupo de seguridad</dd>
</dl>

**Sugerencia:** también puede usar **ba bssg** como alias para el nombre de mandato
**ba bind-staging-security-group** más largo.

* Para enlazar con el conjunto de grupos de seguridad Default Running, utilice el siguiente mandato:

```
cf ba bind-running-security-group <grupo-seguridad>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;grupo-seguridad&gt;</dt>
<dd class="pd">Nombre del grupo de seguridad</dd>
</dl>

**Sugerencia:** también puede usar **ba brsg** como alias para un nombre de mandato
de **ba bind-running-security-group** más largo.

* Para enlazar un grupo de seguridad con un espacio, utilice el siguiente mandato:

```
cf ba bind-security-group <grupo-seguridad> <org> <espacio>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;grupo-seguridad&gt;</dt>
<dd class="pd">Nombre del grupo de seguridad</dd>
<dt class="pt dlterm">&lt;org&gt;</dt>
<dd class="pd">Nombre de la organización con la que enlazar el grupo de seguridad</dd>
<dt class="pt dlterm">&lt;espacio&gt;</dt>
<dd class="pd">Nombre del espacio dentro de la organización con el que enlazar el grupo de seguridad</dd>
</dl>

**Sugerencia:** también puede usar **ba bsg** como alias para un nombre de mandato
de **ba bind-security-group** más largo.

### Anulación de enlace de grupos de seguridad
{: #cliunbindsecgro}

Para obtener más información sobre la anulación del enlace de grupos de seguridad, consulte [Anulación del enlace de grupos de seguridad de aplicaciones ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#unbinding-groups){: new_window}.

* Para anular el enlace desde un conjunto de grupos de seguridad Default Staging, utilice el siguiente mandato:

```
cf ba unbind-staging-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;grupo-seguridad&gt;</dt>
<dd class="pd">Nombre del grupo de seguridad</dd>
</dl>

**Sugerencia:** también puede usar **ba ussg** como alias para el nombre de mandato
**ba unbind-staging-security-group** más largo.

* Para anular el enlace desde un conjunto de grupos de seguridad Default Running, utilice el siguiente mandato:

```
cf ba unbind-running-security-group <grupo-seguridad>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;grupo-seguridad&gt;</dt>
<dd class="pd">Nombre del grupo de seguridad</dd>
</dl>

**Sugerencia:** también puede usar **ba brsg** como alias para un nombre de mandato
de **ba bind-running-security-group** más largo.

* Para anular el enlace de un grupo de seguridad con un espacio, utilice el siguiente mandato:

```
cf ba unbind-security-group <grupo-seguridad> <org> <espacio>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;grupo-seguridad&gt;</dt>
<dd class="pd">Nombre del grupo de seguridad</dd>
<dt class="pt dlterm">&lt;org&gt;</dt>
<dd class="pd">Nombre de la organización con la que enlazar el grupo de seguridad</dd>
<dt class="pt dlterm">&lt;espacio&gt;</dt>
<dd class="pd">Nombre del espacio dentro de la organización con el que enlazar el grupo de seguridad</dd>
</dl>

**Sugerencia:** también puede usar **ba usg** como alias para el nombre de mandato
**ba unbind-staging-security-group** más largo.

## Administración de paquetes de compilación
{: #admin_buildpack}

### Listado de paquetes de compilación
{: #clilistbuildpack}

Si tiene permisos de grabación en el catálogo de las apps, puede listar los paquetes de compilación. Para listar todos los paquetes de compilación o para ver un paquete de compilación específico, utilice el siguiente mandato:

```
cf ba buildpacks <nombre_paquete_compilación>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nombre_paquete_compilación&gt;</dt>
<dd class="pd">Un parámetro opcional para especificar un paquete de compilación concreto para ver.</dd>
</dl>

**Sugerencia:** también puede usar **ba lb** como alias para un nombre de mandato
**ba buildpacks** más largo.

### Creación y carga de un paquete de compilación
{: #clicreupbuildpack}

Si tiene permisos de grabación en el catálogo de las apps, puede crear y cargar un paquete de compilación. Puede cargar cualquier archivo comprimido que tenga un tipo de archivo .zip. Para cargar un paquete de compilación, utilice el siguiente mandato:

```
cf ba create-buildpack <nombre_paquete_compilación> <vía_acceso_archivo> <posición>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nombre_paquete_compilación&gt;</dt>
<dd class="pd">Nombre del paquete de compilación que se cargará.</dd>
<dt class="pt dlterm">&lt;vía_acceso_archivo&gt;</dt>
<dd class="pd">Vía de acceso al archivo comprimido del paquete de compilación.</dd>
<dt class="pt dlterm">&lt;posición&gt;</dt>
<dd class="pd">Orden en el que se comprueban los paquetes de compilación durante la detección automática del paquete de compilación.</dd>
</dl>

**Sugerencia:** también puede usar **ba cb** como alias para el nombre de mandato
**ba create-buildpack** más largo.

### Actualización de un paquete de compilación
{: #cliupdabuildpack}

Si tiene permisos de grabación en el catálogo de las apps, puede actualizar un paquete de compilación existente.  Para actualizar un paquete de compilación, utilice el siguiente mandato:

```
cf ba update-buildpack <nombre_paquete_compilación> <posición> <habilitado> <bloqueado>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nombre_paquete_compilación&gt;</dt>
<dd class="pd">Nombre del paquete de compilación que se actualizará.</dd>
<dt class="pt dlterm">&lt;posición&gt;</dt>
<dd class="pd">Orden en el que se comprueban los paquetes de compilación durante la detección automática del paquete de compilación.</dd>
<dt class="pt dlterm">&lt;habilitado&gt;</dt>
<dd class="pd">Indica si el paquete de compilación se utilizará para la transferencia.</dd>
<dt class="pt dlterm">&lt;bloqueado&gt;</dt>
<dd class="pd">Indica si el paquete de compilación está bloqueado para impedir actualizaciones.</dd>
</dl>

**Sugerencia:** también puede usar **ba ub** como alias para un nombre de mandato
**ba update-buildpack** más largo.

### Supresión de un paquete de compilación
{: #clidelbuildpack}

Si tiene permisos de grabación en el catálogo de las apps, puede suprimir un paquete de compilación existente.  Para suprimir un paquete de compilación, utilice el siguiente mandato:

```
cf ba delete-buildpack <nombre_paquete_compilación>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nombre_paquete_compilación&gt;</dt>
<dd class="pd">Nombre del paquete de compilación que se suprimirá.</dd>
</dl>

**Sugerencia:** también puede usar **ba db** como alias para el nombre de mandato
**ba delete-buildpack** más largo.
