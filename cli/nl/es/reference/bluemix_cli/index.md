---



copyright:

  years: 2015, 2017
lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Iniciación a la CLI de {{site.data.keyword.Bluemix_notm}}
{: #getting-started}

{{site.data.keyword.Bluemix_notm}} CLI ofrece un método unificado para interactuar con aplicaciones, servidores virtuales, contenedores y otros servicios mediante una interfaz de línea de mandatos. La CLI de {{site.data.keyword.Bluemix_notm}} también integra herramientas de la comunidad, como CLI de Cloud Foundry, CLI de Docker, CLI de OpenStack e inicializa valores del entorno para que pueda interactuar con distintos tipos de equipos.

**Restricción**: la CLI de {{site.data.keyword.Bluemix_notm}} no se admite en Cygwin, de modo que no utilice la CLI de {{site.data.keyword.Bluemix_notm}} en la ventana de línea de mandatos de Cygwin.

**Nota**: si la red contiene un servidor proxy HTTP entre el host que ejecuta la CLI y {{site.data.keyword.Bluemix_notm}}, debe especificar el nombre de host y la dirección IP del servidor proxy en la variable HTTP_PROXY.

## Instalación de la CLI de {{site.data.keyword.Bluemix_notm}}
{: #install_bluemix_cli}

Antes de instalar {{site.data.keyword.Bluemix_notm}} CLI, instale la [CLI de cf ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}.

Para Mac OS y Windows, descargue el [paquete de CLI de {{site.data.keyword.Bluemix_notm}}](/docs/cli/index.html#downloads) y ejecute el instalador.

Para Linux, siga estos pasos:

  1. Descargue el paquete y extráigalo. Por ejemplo:

  ```
  ~$ tar -xvf Bluemix_CLI.tar.gz
  Bluemix_CLI/
  Bluemix_CLI/update_global_config
  Bluemix_CLI/install_bluemix_cli
  Bluemix_CLI/bx/
  Bluemix_CLI/bx/bash_autocomplete
  Bluemix_CLI/bx/zsh_autocomplete
  Bluemix_CLI/bin/
  Bluemix_CLI/bin/bluemix
  ~$
  ```

  2. Vaya al directorio `Bluemix_CLI` y ejecute el mandato `./install_bluemix_cli` con el permiso root. Puede ejecutar el mandato como usuario root o puede utilizar el mandato `sudo` para obtener el permiso root. Por ejemplo:

  ```
  ~# cd Bluemix_CLI
  ~/Bluemix_CLI# sudo ./install_bluemix_cli
  Superuser privileges are required to run this script.
  The Cloud Foundry CLI version 6.15 is already installed.
  Copying files...
  The Bluemix CLI installed successfully. To get started, open a new Linux terminal and enter "bluemix help", or enter "bx help" as short name.
  ~/Bluemix_CLI#
  ```

Ahora puede empezar a utilizar {{site.data.keyword.Bluemix_notm}} CLI o instalar plug-ins adicionales.

## Instalación de un plugin
{: #install_plug-in}

Al igual que la CLI de Cloud Foundry, {{site.data.keyword.Bluemix_notm}} CLI admite una infraestructura de ampliación de plug-in para integrar otros mandatos además de los que vienen integrados.

Para instalar un plugin desde el entorno local, siga estos pasos:

  1. Descargue el plugin. Por ejemplo:

  ```
  ~$ wget http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2--2016-02-18 14:02:12-- http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2
  Resolving public.dhe.ibm.com... 9.17.248.112
  Connection to public.dhe.ibm.com|9.17.248.112|:80... connected.
  HTTP request sent, awaiting response... 200 OK
  Length: 9857792 (9.4M) [text/plain]
  Saving to: 'auto-scaling-darwin-amd64-0.2.2'

  auto-scaling-darwin-0.2.2 100%[===================>] 9.40M 518KB/s in 22s

  2016-02-18 14:02:34 (443 KB/s) - `auto-scaling-darwin-amd64-0.2.2' saved [9857792/9857792]
  ```

  2. Para sistemas de tipo UNIX, debe convertir el archivo descargado en ejecutable mediante el mandato `chmod`. Por ejemplo:

  ```
  ~$ sudo chmod 755 auto-scaling-darwin-amd64-0.2.2
  Password:
  ~$
  ```

  3. Instale el plugin con el mandato `bluemix plugin install`. Por ejemplo:

  ```
  ~$ bluemix plugin install ./auto-scaling-darwin-amd64-0.2.2
  Installing pluign './auto-scaling-darwin-amd64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

Para instalar desde un servidor remoto, siga estos pasos:

  1. Instale el plugin desde un URL remoto directamente con el mandato `bluemix plugin install`. Por ejemplo:

  ```
  ~$ bluemix plugin install http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64-0.2.2
  Attempting to download the binary file...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload274645142/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

También puede instalar un plugin desde el repositorio. {{site.data.keyword.Bluemix_notm}} tiene repositorios que contienen plugins de la CLI de {{site.data.keyword.Bluemix_notm}} y plugins de la CLI de Cloud Foundry:

  * [Repositorio de plugins de la CLI de Cloud Foundry ](http://clis.ng.bluemix.net/ui/repository.html#cf-plugins){: new_window} ![icono de enlace externo](../../../icons/launch-glyph.svg), que contiene plugins para la CLI de Cloud Foundry.
  * [Repositorio de plugins de la CLI de {{site.data.keyword.Bluemix_notm}}](http://clis.ng.bluemix.net/ui/repository.html#bluemix-plugins){: new_window} ![icono de enlace externo](../../../icons/launch-glyph.svg), que contiene plug-ins específicos de la CLI de {{site.data.keyword.Bluemix_notm}}.

Para instalar desde el repositorio, siga estos pasos:

  1. Busque el plugin en el repositorio. Después de instalar la CLI de {{site.data.keyword.Bluemix_notm}}, el repositorio oficial `Bluemix` se añade de forma predeterminada. Puede ver los plugins del repositorio de `Bluemix` con el mandato `bluemix plugin repo-plugins`. Por ejemplo:

  ```
  ~$ bluemix plugin repo-plugins -r Bluemix
  Getting plug-ins from repository 'Bluemix'...

  Repository: Bluemix
  Name           Description                                    Versions
  auto-scaling   Bluemix CLI plugin for Auto-Scaling service    0.2.1, 0.2.2
  nsg            Bluemix Network Security Group plugin          0.1.1

  ~$
  ```

  2. Instale el plug-in desde el repositorio de `Bluemix` con el mandato `bluemix plugin install`. Por ejemplo:

  ```
  ~$ bluemix plugin install auto-scaling -r Bluemix
  Looking up 'auto-scaling' from repository 'Bluemix'...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload062468676/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

## Inicio de sesión en la CLI de {{site.data.keyword.Bluemix_notm}}
{: #log_bmcli}

Después de instalar {{site.data.keyword.Bluemix_notm}} CLI, puede iniciar sesión en {{site.data.keyword.Bluemix_notm}} con su ID y contraseña de IBM. Por ejemplo:

```
~$ bluemix login -a https://api.ng.bluemix.net
API endpoint: https://api.ng.bluemix.net

Email> demo_user@foo.com

Password>
Authenticating...
OK
```

Ahora está listo para utilizar los mandatos integrados de {{site.data.keyword.Bluemix_notm}}. Por ejemplo, ejecute el mandato `bluemix catalog templates` para obtener una lista de todas las plantillas del contenedor modelo de {{site.data.keyword.Bluemix_notm}}:

```
~$ bluemix catalog templates
Listing Bluemix boilerplate templates...

ID                      Name
pi-wdc-java-starter     Personality Insights Java Web Starter
xpages-starter          XPages Web Starter
mobileBackendStarter    Mobile Cloud
pi-wdc-nodejs-starter   Personality Insights Node.js Web Starter
mobileFirstPlatform     MobileFirst Services Starter
xspHelloWorld           IBM XPages
javacloudantbp          Java Cloudant Web Starter
```

# Mandatos {{site.data.keyword.Bluemix_notm}} (bx)
{: #bluemix_cli}

Versión: 0.4.6

La interfaz de línea de mandatos (CLI) de {{site.data.keyword.Bluemix_notm}} proporciona un conjunto de mandatos que se agrupan por espacio de nombres para que los usuarios interactúen con {{site.data.keyword.Bluemix_notm}}. Algunos mandatos {{site.data.keyword.Bluemix_notm}} son envoltorios de mandatos cf, mientras que otros proporcionan posibilidades ampliadas para usuarios de {{site.data.keyword.Bluemix_notm}}. En la siguiente información se indican los mandatos admitidos por la CLI de {{site.data.keyword.Bluemix_notm}}, y se indica información sobre nombre, opciones, uso, requisitos previos, descripción y ejemplos.
{:shortdesc}

**Nota:** *Requisitos previos* lista las acciones que son necesarias antes de utilizar el mandato. Los mandatos que no tienen acciones de requisito previo listan **Ninguno**. De lo contrario, los requisitos previos pueden incluir una o varias de las acciones siguientes:

<dl>
<dt>Punto final</dt>
<dd>Un punto final de API se debe establecer por medio de la <code>bluemix api</code> antes de utilizar el mandato.</dd>
<dt>Login</dt>
<dd>El inicio de sesión que utiliza el mandato <code>bluemix login</code> es necesario antes de utilizar este mandato. Si inicia sesión con un ID federado, utilice la opción '--sso' para autenticarse con un código de acceso de una sola vez.</dd>
<dt>Target</dt>
<dd>El mandato <code>bluemix target</code> debe utilizarse para establecer un punto de extensión org y un espacio antes de utilizar este mandato.</dd>
<dt>Docker</dt>
<dd>La CLI de Docker CLI (docker) debe estar instalada para poder ejecutar este mandato.</dd>
</dl>

## Índice de mandatos de bluemix
{: #bx_commands_index}

Utilice los índices de las tablas siguientes para consultar los mandatos de Bluemix que se utilizan con mayor frecuencia.

**Nota:** puede utilizar el formato abreviado de los mandatos de bluemix; por ejemplo, `bx api` es la abreviatura de `bluemix api`.


<table summary="Mandatos generales bluemix">
<caption>Tabla 1. Mandatos generales de bluemix</caption>
 <thead>
 <th colspan="5">Mandatos generales bluemix</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix help](index.html#bluemix_help)</td>
 <td>[bluemix api](index.html#bluemix_api)</td>
 <td>[bluemix_login](index.html#bluemix_login)</td>
 <td>[bluemix logout](index.html#bluemix_logout)</td>
 <td>[bluemix target](index.html#bluemix_target)</td>
 </tr>
 <tr>
 <td>[bluemix info](index.html#bluemix_info) </td>
 <td>[bluemix config](index.html#bluemix_config)</td>
 <td>[bluemix curl](index.html#bluemix_curl)</td>
 </tr>
  </tbody>
 </table>


<table summary="Mandatos bluemix puede utilizar para gestionar organizaciones, espacios y usuarios.">
<caption>Tabla 2. Mandatos para gestionar organizaciones, espacios y usuarios</caption>
 <thead>
 <th colspan="5">Mandatos para gestionar organizaciones, espacios y usuarios</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix iam orgs](index.html#bluemix_iam_orgs)</td>
 <td>[bluemix iam org](index.html#bluemix_iam_org)</td>
 <td>[bluemix iam org-create](index.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](index.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](index.html#bluemix_iam_org_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-delete](index.html#bluemix_iam_org_delete)</td>
 <td>[bluemix iam spaces](index.html#bluemix_iam_spaces)</td>
 <td>[bluemix iam space](index.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](index.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](index.html#bluemix_iam_space_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-delete](index.html#bluemix_iam_space_delete)</td>
 <td>[bluemix iam account-users](index.html#bluemix_iam_account_users)</td>
 <td>[bluemix iam account-users-delete](index.html#bluemix_iam_account_users_delete)</td>
 <td>[bluemix iam account-user-invite](index.html#bluemix_iam_account_user_invite)</td>
 <td>[bluemix iam account-user-reinvite](index.html#bluemix_iam_account_user_reinvite)</td>
 <td>[bluemix iam org-users](index.html#bluemix_iam_org_users)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-user-add](index.html#bluemix_iam_org_user_add)</td>
 <td>[bluemix iam org-user-remove](index.html#bluemix_iam_org_user_remove)</td>
 <td>[bluemix iam org-role-set](index.html#bluemix_iam_org_role_set)</td>
 <td>[bluemix iam org-role-unset](index.html#bluemix_iam_org_role_unset)</td>
 <td>[bluemix iam space-users](index.html#bluemix_iam_space_users)</td>
 <td>[bluemix iam space-role-set](index.html#bluemix_iam_space_role_set)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-role-unset](index.html#bluemix_iam_space_role_unset)</td>
 </tr>
 </tbody>
 </table>


<table summary="Mandatos bluemix que se pueden utilizar para gestionar las apps de Cloud Foundry">
<caption>Tabla 3. Mandatos para gestionar apps cf</caption>
 <thead>
 <th colspan="5">Mandatos para gestionar apps cf</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix app push](index.html#bluemix_app_push)</td>
 <td>[bluemix app list](index.html#bluemix_app_list)</td>
 <td>[bluemix app show](index.html#bluemix_app_show)</td>
 <td>[bluemix app scale](index.html#bluemix_app_scale)</td>
 <td>[bluemix app delete](index.html#bluemix_app_delete)</td>
 </tr>
 <tr>
 <td>[bluemix app rename](index.html#bluemix_app_rename)</td>
 <td>[bluemix app start](index.html#bluemix_app_start)</td>
 <td>[bluemix app stop](index.html#bluemix_app_stop)</td>
 <td>[bluemix app restart](index.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](index.html#bluemix_app_restage)</td>
 </tr>
 <tr>
 <td>[bluemix app instance-restart](index.html#bluemix_app_instance_restart)</td>
 <td>[bluemix app events](index.html#bluemix_app_events)</td>
 <td>[bluemix app files](index.html#bluemix_app_files)</td>
 <td>[bluemix app logs](index.html#bluemix_app_logs)</td>
 <td>[bluemix app env](index.html#bluemix_app_env)</td>
 </tr>
 <tr>
 <td>[bluemix app env-set](index.html#bluemix_app_env_set)</td>
 <td>[bluemix app env-unset](index.html#bluemix_app_env_unset)</td>
 <td>[bluemix app stacks](index.html#bluemix_app_stacks)</td>
 <td>[bluemix app stack](index.html#bluemix_app_stack)</td>
 <td>[bluemix app manifest-create](index.html#bluemix_app_manifest_create)</td>
 </tr>
  </tbody>
 </table>


<table summary="Mandatos bluemix que se pueden utilizar para gestionar servicios Bluemix.">
<caption>Tabla 4. Mandatos para gestionar servicios Bluemix</caption>
 <thead>
 <th colspan="5">Mandatos para gestionar servicios Bluemix</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix service offerings](index.html#bluemix_service_offerings)</td>
 <td>[bluemix service list](index.html#bluemix_service_list)</td>
 <td>[bluemix service show](index.html#bluemix_service_show)</td>
 <td>[bluemix service create](index.html#bluemix_service_create)</td>
 <td>[bluemix service update](index.html#bluemix_service_update)</td>
 </tr>
 <tr>
 <td>[bluemix service delete](index.html#bluemix_service_delete)</td>
 <td>[bluemix service rename](index.html#bluemix_service_rename)</td>
 <td>[bluemix service bind](index.html#bluemix_service_bind)</td>
 <td>[bluemix service unbind](index.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](index.html#bluemix_service_key_create)</td>
 </tr>
 <tr>
 <td>[bluemix service key-delete](index.html#bluemix_service_key_delete)</td>
 <td>[bluemix service keys](index.html#bluemix_service_keys)</td>
 <td>[bluemix service key-show](index.html#bluemix_service_key_show)</td>
 <td>[bluemix service user-provided-create](index.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](index.html#bluemix_service_user_provided_update)</td>
 </tr>
  </tbody>
 </table>


<table summary="Mandatos bluemix que puede utilizar para gestionar los valores de catálogo, plug-ins, facturación y seguridad de Bluemix.">
<caption>Tabla 5. Mandatos para gestionar los valores de catálogo, plug-ins, facturación y seguridad de Bluemix</caption>
 <thead>
 <th colspan="5">Mandatos para gestionar los valores de catálogo, plug-ins, facturación y seguridad de Bluemix</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix catalog templates](index.html#bluemix_catalog_templates)</td>
 <td>[bluemix catalog template](index.html#bluemix_catalog_template)</td>
 <td>[bluemix catalog template-run](index.html#bluemix_catalog_template_run)</td>
 <td>[bluemix plugin repos](index.html#bluemix_plugin_repos)</td>
 <td>[bluemix plugin repo-add](index.html#bluemix_plugin_repo_add)</td>
 </tr>
 <tr>
 <td>[bluemix plugin repo-remove](index.html#bluemix_plugin_repo_remove)</td>
 <td>[bluemix plugin repo-plugins](index.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](index.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](index.html#bluemix_plugin_install)</td>
 <td>[bluemix plugin uninstall](index.html#bluemix_plugin_uninstall)</td>
 </tr>
 <tr>
 <td>[bluemix bss account-usage](index.html#bluemix_bss_account_usage)</td>
 <td>[bluemix bss org-usage](index.html#bluemix_bss_org_usage)</td>
 <td>[bluemix bss orgs-usage-summary](index.html#bluemix_orgs_usage_summary)</td>
 <td>[bluemix security cert](index.html#bluemix_security_cert)</td>
 <td>[bluemix security cert-add](index.html#bluemix_security_cert_add)</td>
 </tr>
 <tr>
 <td>[bluemix security cert-remove](index.html#bluemix_security_cert_remove)</td>
 <td></td>
 <td></td>
 </tr>
  </tbody>
 </table>


<table summary="Mandatos bluemix que se pueden utilizar para gestionar la configuración de la red">
<caption>Tabla 6. Mandatos para gestionar la configuración de la red</caption>
 <thead>
 <th colspan="5">Mandatos para gestionar la configuración de la red</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix network regions](index.html#bluemix_network_regions)</td>
 <td>[bluemix network region-set](index.html#bluemix_network_region_set)</td>
 <td>[bluemix network routes](index.html#bluemix_network_routes)</td>
 <td>[bluemix network route-check](index.html#bluemix_network_route_check)</td>
 <td>[bluemix network route-map](index.html#bluemix_network_route_map)</td>
 </tr>
 <tr>
 <td>[bluemix network route-unmap](index.html#bluemix_network_route_unmap)</td>
 <td>[bluemix network route-create](index.html#bluemix_network_route_create)</td>
 <td>[bluemix network route-delete](index.html#bluemix_network_route_delete)</td>
 <td>[bluemix network orphaned-routes-delete](index.html#bluemix_network_orphaned_routes_delete)</td>
 <td>[bluemix network domains](index.html#bluemix_network_domains)</td>
 </tr>
 <tr>
 <td>[bluemix network domain-create](index.html#bluemix_network_domain_create)</td>
 <td>[bluemix network domain-delete](index.html#bluemix_network_domain_delete)</td>
 <td>[bluemix network shared-domain-create](index.html#bluemix_network_shared_domain_create)</td>
 <td>[bluemix network shared-domain-delete](index.html#bluemix_network_shared_domain_delete)</td>
 <td></td>
 </tr>
  </tbody>
 </table>



### bluemix help
{: #bluemix_help}
Muestra la ayuda general para mandatos incorporados de primer nivel y espacios de nombres soportados de {{site.data.keyword.Bluemix_notm}} CLI, o la ayuda para un mandato o un nombre de espacio incorporado específico.

```
bluemix help [COMMAND|NAMESPACE]
```

<strong>Requisitos previos</strong>: Ninguno

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>COMMAND|NAMESPACE (opcional)</dt>
   <dd>Mandato o espacio de nombres para el que se visualiza ayuda. Si no se especifica, se mostrará la ayuda general para {{site.data.keyword.Bluemix_notm}} CLI.</dd>
   </dl>



<strong>Ejemplos</strong>:

Visualiza ayuda general para {{site.data.keyword.Bluemix_notm}} CLI:

```
bluemix help
```

Muestra ayuda para el mandato `info`:

```
bluemix help info
```



### bluemix api
{: #bluemix_api}
Establezca o visualice el punto final de su API de {{site.data.keyword.Bluemix_notm}}. Este mandato acomoda el mandato `cf api`.

```
bluemix api [API_ENDPOINT] [--unset]
```

<strong>Requisitos previos</strong>: Ninguno

<strong>Opciones de mandato</strong>:
   <dl>
   <dt>API_ENDPOINT (opcional)</dt>
   <dd>Punto final de API de destino, por ejemplo, `https://api.chinabluemix.net`. Si no se especifican ambas opciones *API_ENDPOINT* y `--unset`, se mostrará el punto final de API actual.</dd>
   <dt>--unset (opcional)</dt>
   <dd>Elimina la configuración del punto final de la API.</dd>
    </dl>
<strong>Ejemplos</strong>:

Establecer el punto final de la API en api.chinabluemix.net:

```
bluemix api api.chinabluemix.net
```

Visualice el punto final de la API actual:

```
bluemix api
```

Desestablecer el punto final de la API:

```
bluemix api --unset
```


### bluemix login
{: #bluemix_login}

Inicio de sesión de usuario. Este mandato acomoda el mandato `cf login`. Las opciones del mandato son las mismas que las opciones del mandato de `cf login`.

```
bluemix login [OPTIONS...]
```

<strong>Requisitos previos</strong>:  Punto final

<!-- staging comment for Atlas 45: might need prereq for federated ID/SSO option unless we expect them to just view the details from the cf login command -->

<strong>Opciones de mandato</strong>:
Para obtener información sobre las opciones soportadas por el mandato `login`, consulte la información de uso del mandato `cf login` para que los mandatos cf gestionen apps.

<strong>Nota</strong>:
Si inicia sesión con un ID federado, utilice la opción '--sso' para autenticarse con un código de acceso de una sola vez.

### bluemix logout
{: #bluemix_logout}

Cerrar sesión de usuario. Este mandato acomoda el mandato `cf logout`.

```
bluemix logout
```

<strong>Requisitos previos</strong>:  Ninguno


### bluemix target
{: #bluemix_target}


Establezca o visualice el espacio o la organización de destino. Este mandato acomoda el mandato `cf target`.

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:
   <dl>
   <dt>-o <i>ORG_NAME</i> (opcional)</dt>
   <dd>Nombre de la organización de destino.</dd>
   <dt>-s <i>SPACE_NAME</i> (opcional)</dt>
   <dd>Nombre del espacio de destino.</dd>
   </dl>
Si no se especifica -o *ORG_NAME* ni -s *SPACE_NAME*, se mostrará el espacio y la organización actuales.
<strong>Ejemplos</strong>:

Establezca la organización actual en `MyOrg` y el espacio en `MySpace`:

```
bluemix target -o MyOrg -s MySpace
```

Visualice el espacio y la organización actuales:

```
bluemix target
```


### bluemix info
{: #bluemix_info}

Vea la información básica de {{site.data.keyword.Bluemix_notm}}, incluida la región actual, la versión del controlador de nube y algunos puntos finales útiles, como por ejemplo los puntos finales para el inicio de sesión y el intercambio de señales de acceso.

```
bluemix info
```

<strong>Requisitos previos</strong>:  Punto final


### bluemix config
{: #bluemix_config}


Escriba valores predeterminados en el archivo de configuración.

```
bluemix config --http-timeout TIEMPO_ESPERA_EN_SEGUNDOS | --trace (true|false|vía-acceso-archivo) | --color (true|false) | --locale (LOCALE|CLEAR) | --check-version (true|false)
```

<strong>Requisitos previos</strong>:  Ninguno

<strong>Opciones de mandato</strong>:
   <dl>
   <dt>--http-timeout <i>TIEMPO_ESPERA_EN_SEGUNDOS</i></dt>
   <dd>Valor de tiempo de espera para solicitudes HTTP. El valor predeterminado es de 60 segundos.</dd>
   <dt>--trace true|false|<i>path-to-file</i></dt>
   <dd>Rastrear solicitudes HTTP al terminal o archivo especificado.</dd>
   <dt>--color true|false</dt>
   <dd>Habilitar o inhabilitar la salida de color. La salida de color está habilitada de forma predeterminada.</dd>
   <dt>--locale <i>LOCALE|CLEAR</i></dt>
   <dd>Establecer un entorno local predeterminado. Si LOCALE es <i>CLEAR</i>, el entorno local anterior se elimina.</dd>
   <dt>--check-version true|false</dt>
   <dd>Habilitar o inhabilitar la comprobación de la versión de la CLI.</dd>
   </dl>

Sólo se puede especificar una de estas opciones a la vez.

<strong>Ejemplos</strong>:

Establezca el tiempo de espera de solicitud HTTP en 30 segundos:

```
bluemix config --http-timeout 30
```

Habilitar la salida de rastreo para las solicitudes HTTP:

```
bluemix config --trace true
```

Rastrear solicitudes HTTP a un archivo determinado */home/usera/my_trace*:

```
bluemix config --trace /home/usera/my_trace
```

Inhabilitar la salida de color:

```
bluemix config --color false
```

Establecer el entorno local en zh_Hans:

```
bluemix config --locale zh_Hans
```

Borrar los valores de entorno local:

```
bluemix config --locale CLEAR
```


### bluemix curl
{: #bluemix_curl}

Ejecuta una solicitud HTTP sin procesar a {{site.data.keyword.Bluemix_notm}}. *Content-Type* se establece en *application/json* de forma predeterminada. Este mandato envía la solicitud a {{site.data.keyword.Bluemix_notm}} Multi-Cloud Control Proxy. Para obtener las vías de acceso admitidas, consulte las definiciones de vías de acceso de API en el [documento de API CloudFoundry ](http://apidocs.cloudfoundry.org/){: new_window} ![icono de enlace externo](../../../icons/launch-glyph.svg).

```
bluemix curl PATH [OPTIONS...]
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:
   <dl>
   <dt><i>PATH</i> (necesario)</dt>
   <dd>URL del recurso. Por ejemplo, /v2/apps.</dd>
   <dt><i>OPTIONS</i> (opcional)</dt>
   <dd>Las opciones admitidas por el mandato `bluemix curl` son las mismas que las del mandato `cf curl`.</dd>
   </dl>

<strong>Ejemplos</strong>:

Vea la información para todas las organizaciones de la cuenta actual:

```
bluemix curl /v2/organizations
```


### bluemix iam orgs
{: #bluemix_iam_orgs}

Listar todas las organizaciones

```
bluemix iam orgs [-r REGION --guid]
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:
   <dl>
   <dt>-r <i>REGION</i> (opcional)</dt>
   <dd>Indica para qué región se muestra información sobre la organización. Si se establece en 'all', se listan todas las organizaciones de todas las regiones.</dd>
   <dt>--guid (opcional)</dt>
   <dd>Muestra el GUID de las organizaciones.</dd>
   </dl>

<strong>Ejemplos</strong>:

Muestra una lista de todas las organizaciones de la región: `us-south` con el GUID.

```
bluemix iam orgs -r us-south --guid
```

### bluemix iam org
{: #bluemix_iam_org}

Mostrar la información para la organización especificada.

```
bluemix iam org ORG_NAME [--guid]
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:
   <dl>
   <dt>ORG_NAME (necesario)</dt>
   <dd>Nombre de la organización.</dd>
   <dt>--guid (opcional)</dt>
   <dd>Muestra el GUID de la organización.</dd>
   </dl>

<strong>Ejemplos</strong>:

Muestra la información de la organización `IBM` con el GUID visualizado

```
bluemix iam org IBM --guid
```

### bluemix iam org-create
{: #bluemix_iam_org_create}

Crear una nueva organización. Esta operación solamente puede realizarla el propietario de cuenta.

```
bluemix iam org-create ORG_NAME
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:
   <dl>
   <dt>ORG_NAME (necesario)</dt>
   <dd>Nombre de la organización que se está creando.</dd>
   </dl>

<strong>Ejemplos</strong>:

Cree una organización denominada `IBM`.

```
bluemix iam org-create IBM
```


### bluemix iam org-replicate
{: #bluemix_iam_org_replicate}

Replicar una organización desde la región actual a otra región.

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:
   <dl>
   <dt>ORG_NAME (necesario)</dt>
   <dd>Nombre de la organización existente que se debe replicar.</dd>
   <dt>REGION_NAME (necesario)</dt>
   <dd>Nombre de la región que aloja la organización replicada.</dd>
   </dl>

<strong>Ejemplos</strong>:

Replicar la organización `myorg` en la región `eu-gb`:

```
bluemix iam org-replicate myorg eu-gb
```


### bluemix iam org-rename
{: #bluemix_iam_org_rename}

Cambiar el nombre de una organización. Esta operación solamente la puede llevar a cabo un gestor de organización.

```
bluemix iam org-rename OLD_ORG_NAME NEW_ORG_NAME
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:
   <dl>
   <dt>OLD_ORG_NAME (necesario)</dt>
   <dd>Nombre antiguo de la organización que se debe renombrar.</dd>
   <dt>NEW_ORG_NAME (necesario)</dt>
   <dd>Nombre de la nueva organización.</dd>
   </dl>

### bluemix iam org-delete
{: #bluemix_iam_org_delete}

Suprimir la organización especificada en la región actual.

```
bluemix iam org-delete ORG_NAME [-f --all]
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:
   <dl>
   <dt>ORG_NAME (necesario)</dt>
   <dd>Nombre de la organización existente que se debe eliminar.</dd>
   <dt>-f (opcional)</dt>
   <dd>Forzar la eliminación sin confirmación.</dd>
   <dt>--all (opcional)</dt>
   <dd>Eliminar la organización de todas las regiones.</dd>
   </dl>


### bluemix iam spaces
{: #bluemix_iam_spaces}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf spaces`.


### bluemix iam space
{: #bluemix_iam_space}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf space`.


### bluemix iam space-create
{: #bluemix_iam_space_create}

Este mandato tiene la misma función y las mismas opciones que el mandato que el mandato `cf create-space`.


### bluemix iam space-rename
{: #bluemix_iam_space_rename}


Este mandato tiene la misma función y las mismas opciones que el mandato que el mandato `cf rename-space`.


### bluemix iam space-delete
{: #bluemix_iam_space_delete}


Este mandato tiene la misma función y las mismas opciones que el mandato `cf delete-space`.


### bluemix iam account-users
{: #bluemix_iam_account_users}

Muestra usuarios asociados con la cuenta. Esta operación solamente puede llevarla a cabo el propietario de cuenta.

```
bluemix iam account-users
```

### bluemix iam account-user-invite
{: #bluemix_iam_account_user_invite}


Invita a un usuario a la cuenta con una organización y un rol de espacio ya establecido. Esta operación solamente puede llevarla a cabo el propietario de cuenta.

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión


<strong>Opciones de mandato</strong>:

   <dl>
   <dt>USER_NAME (necesario)</dt>
   <dd>Nombre del usuario al que se invita.</dd>
   <dt>ORG_NAME (necesario)</dt>
   <dd>Nombre de la organización en la que se invita al usuario.</dd>
   <dt>ORG_ROLE (necesario)</dt>
   <dd>Nombre del rol de la organización al que se invita a este usuario. Por ejemplo:
   <ul>
  <li>OrgManager: este rol puede invitar y gestionar usuarios, seleccionar y cambiar planes y establecer límites de gasto.</li>
  <li>BillingManager: este rol puede crear y gestionar la cuenta de facturación y la información de pago.</li>
  <li>OrgAuditor: este rol tiene acceso de sólo lectura a informes e información de organización.</li>
  </ul> </dd>
   <dt>SPACE_NAME (necesario)</dt>
   <dd>Nombre del espacio en el que se invita al usuario.</dd>
   <dt>SPACE_ROLE (necesario)</dt>
   <dd>Nombre del espacio en el que se invita al usuario. Nombre del rol del espacio al que se invita a este usuario. Por ejemplo:
   <ul>
<li>SpaceManager: este rol puede invitar y gestionar usuarios, y habilitar características para un espacio dado.</li>
<li>SpaceDeveloper: este rol puede crear y gestionar apps y servicios, y ver registros e informes.</li>
<li>SpaceAuditor: este rol puede ver los registros, informes y valores para el espacio.</li>
</ul>
</dd>
</dl>

<strong>Ejemplos</strong>:

Invite al usuario `Mary` a la organización `IBM` como rol `OrgManager` y el espacio `Cloud` como rol `SpaceAuditor`:

```
bluemix iam account-user-invite Mary IBM OrgManager Cloud SpaceAuditor
```


### bluemix iam account-user-reinvite
{: #bluemix_iam_account_user_reinvite}

Reenviar la invitación a un usuario (es necesario ser gestor de organización o propietario de cuenta)
```
 bluemix iam account-user-reinvite USER_EMAIL ORG_NAME
```


### bluemix iam org-users
{: #bluemix_iam_org_users}

Visualice usuarios en el archivo de organización según el rol.

```
bluemix iam org-users ORG_NAME [-a]
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:
   <dl>
   <dt>ORG_NAME (necesario)</dt>
   <dd>Nombre de la organización.</dd>
   <dt>-a (opcional)</dt>
   <dd>Lista todos los usuarios de la organización especificada, no agrupada por rol.</dd>
    </dl>

### bluemix iam org-user-add
{: #bluemix_iam_org_user_add}

Añadir un usuario a la organización (es necesario ser gestor de organización).
```
 bluemix iam org-user-add USER_NAME ORG
```

### bluemix iam org-user-remove
{: #bluemix_iam_org_user_remove}

Eliminar un usuario de la organización (gestor de organización o usuario mismo solamente)
```
   bluemix iam org-user-remove USER_NAME ORG [-f, --force]
```

<strong>Opciones de mandato</strong>:
  <dl>
   <dt>--force, -f</dt>
   <dd>Forzar la eliminación sin confirmación.</dd>
 </dl>

### bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

Asignar un rol de organización a un usuario. Esta operación solamente la puede llevar a cabo un gestor de organización.

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:
  <dl>
   <dt>USER_NAME (necesario)</dt>
   <dd>Nombre del usuario al que se asigna.</dd>
   <dt>ORG_NAME (necesario)</dt>
   <dd>Nombre de la organización en la que se asigna al usuario.</dd>
   <dt>ORG_ROLE (necesario)</dt>
   <dd>Nombre del rol de la organización al que se asigna a este usuario. Por ejemplo:
   <ul>
   <li>OrgManager: este rol puede invitar y gestionar usuarios, seleccionar y cambiar planes y establecer límites de gasto.</li>
   <li>BillingManager: este rol puede crear y gestionar la cuenta de facturación y la información de pago.</li>
   <li>OrgAuditor: este rol tiene acceso de sólo lectura a informes e información de organización.</li>
   </ul>
   </dd>
    </dl>

<strong>Ejemplos</strong>:

Asigne el usuario `Mary` a la organización `IBM` como rol `OrgManager`:

```
bluemix iam org-role-set Mary IBM OrgManager
```


### bluemix iam org-role-unset
{: #bluemix_iam_org_role_unset}

Elimine un rol de organización de un usuario. Esta operación solamente la puede llevar a cabo un gestor de organización.

```
bluemix iam org-role-unset USER_NAME ORG_NAME ORG_ROLE
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:
   <dl>
   <dt>USER_NAME (necesario)</dt>
   <dd>Nombre del usuario al que se elimina.</dd>
   <dt>ORG_NAME (necesario)</dt>
   <dd>Nombre de la organización de la que se elimina al usuario.</dd>
   <dt>ORG_ROLE (necesario)</dt>
   <dd>Nombre del rol de la organización de la que se elimina al usuario. Por ejemplo:
   <ul>
   <li>OrgManager: este rol puede invitar y gestionar usuarios, seleccionar y cambiar planes y establecer límites de gasto.</li>
   <li>BillingManager: este rol puede crear y gestionar la cuenta de facturación y la información de pago.</li>
   <li>OrgAuditor: este rol tiene acceso de sólo lectura a informes e información de organización.</li>
   </ul>
   </dd>
    </dl>

<strong>Ejemplos</strong>:

Elimine el usuario `Mary` de la organización `IBM` como rol `OrgManager`:

```
bluemix iam org-role-unset Mary IBM OrgManager
```


### bluemix iam space-users
{: #bluemix_iam_space_users}

Visualice usuarios en el espacio especificado según el rol.

```
bluemix iam space-users ORG_NAME SPACE_NAME
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:
   <dl>
   <dt>ORG_NAME (necesario)</dt>
   <dd>Nombre de la organización.</dd>
   <dt>SPACE_NAME (necesario)</dt>
   <dd>El nombre del espacio.</dd>
   </dl>


### bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

Asignar un rol de espacio a un usuario. Esta operación solamente la puede llevar a cabo un gestor de espacios.

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>USER_NAME (necesario)</dt>
   <dd>Nombre del usuario al que se asigna.</dd>
   <dt>ORG_NAME (necesario)</dt>
   <dd>Nombre de la organización en la que se asigna al usuario.</dd>
   <dt>SPACE_NAME (necesario)</dt>
   <dd>Nombre del espacio en el que se asigna al usuario.</dd>
   <dt>SPACE_ROLE (necesario)</dt>
   <dd>Nombre del rol del espacio al que se asigna a este usuario. Por ejemplo:
   <ul>
   <li>SpaceManager: este rol puede invitar y gestionar usuarios, y habilitar características para un espacio dado.</li>
   <li>SpaceDeveloper: este rol puede crear y gestionar apps y servicios, y ver registros e informes.</li>
   <li>SpaceAuditor: este rol puede ver los registros, informes y valores para el espacio.</li>
   </ul></dd>
    </dl>

<strong>Ejemplos</strong>:

Asigne el usuario `Mary` a la organización `IBM` y el espacio `Cloud` como rol `SpaceManager`:

```
bluemix iam space-role-set Mary IBM Cloud SpaceManager
```

### bluemix iam space-role-unset
{: #bluemix_iam_space_role_unset}

Elimine un rol de espacio de un usuario. Esta operación solamente la puede llevar a cabo un gestor de espacios.

```
bluemix iam space-role-unset USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>USER_NAME (necesario)</dt>
   <dd>Nombre del usuario al que se elimina.</dd>
   <dt>ORG_NAME (necesario)</dt>
   <dd>Nombre de la organización de la que se elimina al usuario.</dd>
   <dt>SPACE_NAME (necesario)</dt>
   <dd>Nombre del espacio del que se elimina al usuario.</dd>
   <dt>SPACE_ROLE (necesario)</dt>
   <dd>Nombre del rol del espacio del que se elimina al usuario. Por ejemplo:
   <ul>
   <li>SpaceManager: este rol puede invitar y gestionar usuarios, y habilitar características para un espacio dado.</li>
   <li>SpaceDeveloper: este rol puede crear y gestionar apps y servicios, y ver registros e informes.</li>
   <li>SpaceAuditor: este rol puede ver los registros, informes y valores para el espacio.</li>
   </ul></dd>
    </dl>


<strong>Ejemplos</strong>:

Elimine el usuario `Mary` de la organización `IBM` y el espacio `Cloud` como rol `SpaceManager`:

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```


### bluemix app push
{: #bluemix_app_push}

Este mandato tiene la misma función y opciones que el mandato `cf push`.


### bluemix app list
{: #bluemix_app_list}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf apps`.


### bluemix app show
{: #bluemix_app_show}

Este mandato tiene la misma función y opciones que el mandato `cf app`.


### bluemix app scale
{: #bluemix_app_scale}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf scale`.


### bluemix app delete
{: #bluemix_app_delete}

Este mandato tiene la misma función y opciones que el mandato `cf delete`.


### bluemix app rename
{: #bluemix_app_rename}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf rename`.


### bluemix app start
{: #bluemix_app_start}

Este mandato tiene la misma función y opciones que el mandato `cf start`.


### bluemix app stop
{: #bluemix_app_stop}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf stop`.


### bluemix app restart
{: #bluemix_app_restart}

Este mandato tiene la misma función y opciones que el mandato `cf restart`.


### bluemix app restage
{: #bluemix_app_restage}


Este mandato tiene la misma función y las mismas opciones que el mandato `cf restage`.


### bluemix app instance-restart
{: #bluemix_app_instance_restart}


Este mandato tiene la misma función y opciones que el mandato `cf restart-app-instance`.


### bluemix app events
{: #bluemix_app_events}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf events`.


### bluemix app files
{: #bluemix_app_files}

Este mandato tiene la misma función y opciones que el mandato `cf files`.


### bluemix app logs
{: #bluemix_app_logs}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf logs`.


### bluemix app env
{: #bluemix_app_env}

Este mandato tiene la misma función y opciones que el mandato `cf env`.


### bluemix app env-set
{: #bluemix_app_env_set}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf set-env`.


### bluemix app env-unset
{: #bluemix_app_env_unset}

Este mandato tiene la misma función y opciones que el mandato `cf unset-env`.


### bluemix app stacks
{: #bluemix_app_stacks}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf stacks`.


### bluemix app stack
{: #bluemix_app_stack}

Este mandato tiene la misma función y opciones que el mandato `cf stack`.


### bluemix app manifest-create
{: #bluemix_app_manifest_create}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf create-app-manifest`.


### bluemix service offerings
{: #bluemix_service_offerings}


Este mandato tiene la misma función y opciones que el mandato `cf marketplace`.


### bluemix service list
{: #bluemix_service_list}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf services`.


### bluemix service show
{: #bluemix_service_show}

Este mandato tiene la misma función y opciones que el mandato `cf service`.


### bluemix service create
{: #bluemix_service_create}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf create-service`.


### bluemix service update
{: #bluemix_service_update}

Este mandato tiene la misma función y opciones que el mandato `cf update-service`.


### bluemix service delete
{: #bluemix_service_delete}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf delete-service`.


### bluemix service rename
{: #bluemix_service_rename}

Este mandato tiene la misma función y opciones que el mandato `cf rename-service`.


### bluemix service bind
{: #bluemix_service_bind}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf bind-service`.


### bluemix service unbind
{: #bluemix_service_unbind}

Este mandato tiene la misma función y opciones que el mandato `cf unbind-service`.


### bluemix service key-create
{: #bluemix_service_key_create}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf create-service-key`.


### bluemix service key-delete
{: #bluemix_service_key_delete}

Este mandato tiene la misma función y opciones que el mandato `cf delete-service-key`.


### bluemix service keys
{: #bluemix_service_keys}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf service-keys`.


### bluemix service key-show
{: #bluemix_service_key_show}

Este mandato tiene la misma función y opciones que el mandato `cf service-key`.


### bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf create-user-provided-service`.


### bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

Este mandato tiene la misma función y opciones que el mandato `cf update-user-provided-service`.


### bluemix catalog templates
{: #bluemix_catalog_templates}

Visualizar las plantillas de contenedor modelo en Bluemix.

```
bluemix catalog templates [-d]
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>-d (opcional)</dt>
   <dd>Si se especifica la opción <i>-d</i>, también se mostrará la descripción de cada plantilla. De lo contrario, sólo se mostrará el ID y el nombre de cada plantilla.</dd>
   </dl>


### bluemix catalog template
{: #bluemix_catalog_template}

Ver la información detallada de una plantilla de contenedor modelo especificada.

```
bluemix catalog template TEMPLATE_ID
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:
   <dl>
   <dt>TEMPLATE_ID (necesario)</dt>
   <dd>ID de la plantilla de contenedor modelo. Utilice <i>bluemix templates</i> para ver los ID de todas las plantillas.</dd>
   </dl>


<strong>Ejemplos</strong>:

Ver detalles de la plantilla `mobileBackendStarter`:

```
bluemix catalog template mobileBackendStarter
```


### bluemix catalog template-run
{: #bluemix_catalog_template_run}

Crea una app cf que se base en la plantilla específica con el URL y la descripción especificados. De forma predeterminada, la nueva app se iniciará automáticamente.

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:
   <dl>
   <dt>TEMPLATE_ID (necesario)</dt>
   <dd>Plantilla en la que se basará la app cuando se cree. Utilice <i>bluemix templates</i> para ver el ID de todas las plantillas.</dd>
   <dt>CF_APP_NAME (necesario)</dt>
   <dd>Nombre de la aplicación cf que se debe crear.</dd>
   <dt>-u <i>URL</i> (opcional)</dt>
   <dd>Ruta de la aplicación. Si no se especifica, Bluemix establece la ruta automáticamente basándose en el nombre de su app y el dominio predeterminado.</dd>
   <dt>-d <i>DESCRIPTION</i> (opcional)</dt>
   <dd>Descripción de la aplicación.</dd>
   <dt>--no-start (opcional)</dt>
   <dd>No inicie la app automáticamente después de crearla. Si no se especifica, la app se iniciará automáticamente una vez que se haya creado.</dd>
   </dl>


<strong>Ejemplos</strong>:

Crear una aplicación cf `my-app` basada en la plantilla `javaHelloWorld`:

```
bluemix catalog template-run javaHelloWorld my-app
```

Crear una aplicación `my-ruby-app` en función de la plantilla `rubyHelloWorld` con la ruta `myrubyapp.chinabluemix.net` y la descripción `Mi primera app ruby en {{site.data.keyword.Bluemix_notm}}.`:

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.chinabluemix.net -d "My first ruby app on {{site.data.keyword.Bluemix_notm}}."
```

Crear una aplicación `my-python-app` basada en la plantilla `pythonHelloWorld` sin inicio automático:

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


### bluemix network regions
{: #bluemix_network_regions}

Visualiza la información para todas las regiones en {{site.data.keyword.Bluemix_notm}}.

```
bluemix network regions
```

<strong>Requisitos previos</strong>:  Punto final


### bluemix network region-set
{: #bluemix_network_region_set}

Se dirige a la región que se ha especificado. Este mandato vuelve a dirigirse automáticamente a la misma organización y espacio de la nueva región, si es posible. De lo contrario, el mandato solicitará al usuario que seleccione una nueva organización y un nuevo espacio si el usuario ya ha iniciado sesión. El punto final de API cambia en consecuencia.

```
bluemix network region-set REGION_NAME
```

<strong>Requisitos previos</strong>:  Punto final

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>REGION_NAME (necesario)</dt>
   <dd>Nombre de la región al a que desea cambiar. Puede utilizar el mandato <i>bluemix network regions</i> para visualizar todos los nombres de región.</dd>
    </dl>

<strong>Ejemplos</strong>:

Establezca la región actual en `eu-gb`:

```
bluemix network region-set eu-gb
```


### bluemix network routes
{: #bluemix_network_routes}

Este mandato tiene la misma función y opciones que el mandato `cf routes`.


### bluemix network route-check
{: #bluemix_network_route_check}

Este mandato tiene la misma función y opciones que el mandato `cf check-route`.


### bluemix network route-map
{: #bluemix_network_route_map}

Correlacione una ruta a una app cf o grupo de contenedores que tenga un dominio y nombre de host específicos.

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>CF_APP_NAME|CONTAINER_GROUP_NAME (necesario)</dt>
   <dd>Nombre de la aplicación cf o del grupo de contenedores que debe correlacionarse con una ruta.</dd>
   <dt>DOMAIN (necesario)</dt>
   <dd>Dominio de la ruta. Por ejemplo, mychinabluemix.net o chinabluemix.net. </dd>
   <dt>-n <i>HOST_NAME</i> (opcional)</dt>
   <dd>Nombre de host de la ruta. Si no se facilita, el nombre de host se establece en el nombre de la app o grupo de contenedores de forma predeterminada.</dd>
   </dl>

<strong>Ejemplos</strong>:

Correlacionar una ruta a `my-app` con un dominio especificado:

```
bluemix network route-map my-app mychinabluemix.net
```

Correlacione una ruta a 'my-container-group' con el dominio y el nombre de host especificados:

```
bluemix network route-map my-container-group chinabluemix.net -n abc
```


### bluemix network route-unmap
{: #bluemix_network_route_unmap}

Elimina la correlación entre la ruta específica y una app cf existente o grupo de contenedores.

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>CF_APP_NAME|CONTAINER_GROUP_NAME (necesario)</dt>
   <dd>Nombre de la aplicación cf o del grupo de contenedores.</dd>
   <dt>DOMAIN (necesario)</dt>
   <dd>Dominio de la ruta (por ejemplo, mychinabluemix.net o chinabluemix.net).</dd>
   <dt>-n <i>HOST_NAME</i> (opcional)</dt>
   <dd>Nombre de host de la ruta. Si no se proporciona, el nombre de host se establece en el nombre de la app o en el nombre de grupo de contenedores de forma predeterminada.</dd>
   </dl>

<strong>Ejemplos</strong>:

Descorrelacionar `my-app.mychinabluemix.net` desde `my-app`:

```
bluemix network route-unmap my-app mychianbluemix.net
```

Descorrelacionar `abc.chinabluexmix.net` desde `my-container-group`:

```
bluemix network route-unmap my-container-group chinabluemix.net -n abc
```


### bluemix network route-create
{: #bluemix_network_route_create}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf create-route`.


### bluemix network route-delete
{: #bluemix_network_route_delete}

Este mandato tiene la misma función y opciones que el mandato `cf delete-route`.


### bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

Este mandato tiene la misma función y opciones que el mandato `cf delete-orphaned-routes`.


### bluemix network domains
{: #bluemix_network_domains}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf domains`.


### bluemix network domain-create
{: #bluemix_network_domain_create}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf create-domain`.


### bluemix network domain-delete
{: #bluemix_network_domain_delete}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf delete-domain`.


### bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf create-shared-domain`.


### bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf delete-shared-domain`.



### bluemix bss account-usage
{: #bluemix_bss_account_usage}

Mostrar el uso y coste mensual de la cuenta.

```
bluemix bss account-usage [-d YYYY-MM] [--json]
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:

<dl>
  <dt>-d MONTH_DATE (opcional)</dt>
  <dd>Mostrar datos para el mes y la fecha especificados utilizando el formato AAAA-MM. Si no se especifica, se muestra el uso en el mes actual.</dd>
  <dt>--json (opcional)</dt>
  <dd>Mostrar el resultado del uso en formato JSON.</dd>
</dl>

<strong>Ejemplos</strong>:

Mostrar el informe de uso y coste de mi cuenta en 2016-06:

```
bluemix bss account-usage -d 2016-06
```

### bluemix bss org-usage
{: #bluemix_bss_org_usage}

Mostrar los detalles de uso mensual de una organización. Esta operación solo la puede llevar a cabo un gestor de facturación de la organización.

```
bluemix bss org-usage ORG_NAME [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:

<dl>
  <dt>ORG_NAME (necesario)</dt>
  <dd>Nombre de la organización.</dd>
  <dt>-d MONTH_DATE (opcional)</dt>
  <dd>Mostrar datos para el mes y la fecha especificados utilizando el formato AAAA-MM. Si no se especifica, se muestra el uso en el mes actual.</dd>
  <dt>-r REGION_NAME</dt>
  <dd>Nombre de la región en que se encuentra la organización. Si se establece en 'todas', se muestra el uso de la organización en todas las regiones.</dd>
  <dt>--json (opcional)</dt>
  <dd>Mostrar el resultado del uso en formato JSON.</dd>
</dl>



### bluemix bss orgs-usage-summary
{: #bluemix_bss_orgs_usage_summary}

Mostrar el resumen de uso mensual de las organizaciones de mi cuenta.

```
bluemix bss orgs-usage-summary [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:

<dl>
  <dt>-d MONTH_DATE (opcional)</dt>
  <dd>Mostrar datos para el mes y la fecha especificados utilizando el formato AAAA-MM. Si no se especifica, se muestra el uso en el mes actual.</dd>
  <dt>-r REGION_NAME</dt>
  <dd>Nombre de la región en que se encuentran las organizaciones. Si se establece en 'todas', se muestra el resumen de uso de las organizaciones en todas las regiones.</dd>
  <dt>--json (opcional)</dt>
  <dd>Mostrar el resultado del uso en formato JSON.</dd>
</dl>



### bluemix security cert
{: #bluemix_security_cert}

Liste la información de certificado de un dominio.

```
bluemix security cert DOMAIN_NAME
```

<strong>Requisitos previos</strong>:  Punto final, Inicio de sesión

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>DOMAIN_NAME (necesario)</dt>
   <dd>Nombre del dominio que aloja el certificado.</dd>
   </dl>



<strong>Ejemplos</strong>:

Ver la información de certificado del dominio `ibmcxo-eventconnect.com`:

```
bluemix security cert ibmcxo-eventconnect.com
```


### bluemix security cert-add
{: #bluemix_security_cert_add}

Añadir un certificado para el dominio especificado en la organización actual.

```
bluemix security cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD] [-i INTERMEDIATE_CERT_FILE] [--verify-client]
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:
   <dl>
   <dt>DOMAIN (necesario)</dt>
   <dd>Dominio al que se añade el certificado.</dd>
   <dt>-k <i>PRIVATE_KEY_FILE</i> (necesario)</dt>
   <dd>Vía de acceso del archivo de claves privado.</dd>
   <dt>-c <i>CERT_FILE</i> (necesario)</dt>
   <dd>Vía de acceso del archivo de certificado.</dd>
   <dt>-p <i>PASSWORD</i> (opcional)</dt>
   <dd>Contraseña del certificado.</dd>
   <dt>-i <i>INTERMEDIATE_CERT_FILE</i> (opcional)</dt>
   <dd>Vía de acceso del archivo de certificado intermedio.</dd>
   <dt>--verify-client (opcional)</dt>
   <dd>Indica si debe habilitarse o no la verificación de certificados de cliente.</dd>
   </dl>


<strong>Ejemplos</strong>:

Añadir un certificado al dominio `ibmcxo-eventconnect.com`:

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


### bluemix security cert-remove
{: #bluemix_security_cert_remove}

Eliminar un certificado del dominio especificado en la organización actual.

```
bluemix security cert-remove DOMAIN [-f]
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>DOMAIN (necesario)</dt>
   <dd>Dominio a eliminar del certificado.</dd>
   <dt>-f  (opcional)</dt>
   <dd>Forzar la eliminación sin confirmación.</dd>
   </dl>



### bluemix plugin repos
{: #bluemix_plugin_repos}

Cree una lista de todos los repositorios de plugin que se registran en {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin repos
```

<strong>Requisitos previos</strong>:  Ninguno


### bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

Agrega un nuevo repositorio de plugin a {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

<strong>Requisitos previos</strong>:  Ninguno

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>REPO_NAME (necesario)</dt>
   <dd>Nombre del repositorio que se debe añadir. Puede volver a definir su propio nombre para cada repositorio.</dd>
   <dt>REPO_URL (necesario)</dt>
   <dd>URL del repositorio que se debe añadir. El URL de repositorio debe contener el protocolo (por ejemplo, http://plugins.ng.bluemix.net en lugar de plugins.ng.bluemix.net). http://plugins.ng.bluemix.net
es el repositorio de plugins oficial de Bluemix
CLI.</dd>
    </dl>


<strong>Ejemplos</strong>:

Añadir el repositorio de plugins oficial de Bluemix CLI como `bluemix-repo`:

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


### bluemix plugin repo-remove
{: #bluemix_plugin_repo_remove}

Elimina el repositorio de plugins de {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin repo-remove REPO_NAME
```

<strong>Requisitos previos</strong>:  Ninguno

<strong>Opciones de mandato</strong>:
   <dl>
   <dt>REPO_NAME (necesario)</dt>
   <dd>Nombre del repositorio que se debe eliminar.</dd>
   </dl>

<strong>Ejemplos</strong>:

Eliminar el repositorio `bluemix-repo` de {{site.data.keyword.Bluemix_notm}} CLI:

```
bluemix plugin repo-remove bluemix-repo
```


### bluemix plugin repo-plugins
{: #bluemix_plugin_repo_plugins}

Crea una lista de todos los plugins disponibles en todos los repositorios o repositorios específicos.

```
bluemix plugin repo-plugins [-r REPO_NAME]
```

<strong>Requisitos previos</strong>:  Ninguno

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>-r <i>REPO_NAME</i> (opcional)</dt>
   <dd>Lista únicamente los plugins del repositorio indicado.</dd>
   </dl>

<strong>Ejemplos</strong>:

Crea una lista de todos los plugins en todos los repositorios añadidos:

```
bluemix plugin repo-plugins
```

Listar todos los plugins del repositorio `bluemix-repo`:

```
bluemix plugin repo-plugins -r bluemix-repo
```


### bluemix plugin list
{: #bluemix_plugin_list}

Crea una lista de todos los plugins instalados en {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin list
```

<strong>Requisitos previos</strong>:  Ninguno


### bluemix plugin install
{: #bluemix_plugin_install}

Instalar la versión específica del plugin en {{site.data.keyword.Bluemix_notm}} CLI desde la vía de acceso o el repositorio especificados.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME] [-v VERSION]
```

<strong>Requisitos previos</strong>:  Ninguno

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>PLUGIN_PATH|PLUGIN_NAME (necesario)</dt>
   <dd>Si -r <i>REPO_NAME</i> no se especifica, el plugin se instala desde la vía de acceso local o el URL remoto indicados.</dd>
   <dt>-r <i>REPO_NAME</i> (opcional)</dt>
   <dd>Nombre del repositorio en el que se encuentra el binario del plugin.</dd>
   <dt>-v <i>VERSION</i> (opcional)</dt>
   <dd>Versión del plugin que se debe instalar. Si no se proporciona, se instalará la versión más reciente del plugin. Esta opción sólo es válida al instalar el plugin desde el repositorio.</dd>
    </dl>

<strong>Ejemplos</strong>:

Instala un plugin desde el archivo local:

```
bluemix plugin install /downloads/new_plugin
```

Instala un plugin desde el URL remoto:

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

Instale el plugin `container-service` de la versión más reciente del repositorio `bluemix-repo`:

```
bluemix plugin install container-service -r bluemix-repo
```
Instale el plugin `container-service` con la versión `0.5.800` del repositorio `bluemix-repo`:

```
bluemix plugin install container-service -r bluemix-repo -v 0.1.217
```






### bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

Desinstala el plugin especificado desde {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin uninstall PLUGIN_NAME
```

<strong>Requisitos previos</strong>:  Ninguno

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>PLUGIN_NAME (necesario)</dt>
   <dd>Nombre del plugin que se debe desinstalar.</dd>
    </dl>

<strong>Ejemplos</strong>:

Desinstale el plugin `container-service` que se ha instalado previamente:

```
bluemix plugin uninstall container-service
```



# Enlaces relacionados
{: #rellinks}

## Enlaces relacionados
{: #general}

* [bx tool ](http://clis.ng.bluemix.net/ui/home.html){: new_window} ![icono de enlace externo](../../../icons/launch-glyph.svg)
