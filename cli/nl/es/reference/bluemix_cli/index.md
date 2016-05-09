---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Mandatos {{site.data.keyword.Bluemix_notm}} (bx)
{: #bluemix_cli}

*Última actualización: 15 de abril de 2016*

La interfaz de línea de mandatos (CLI) de {{site.data.keyword.Bluemix_notm}} proporciona un conjunto de mandatos que se agrupan por espacio de nombres para que los usuarios interactúen con {{site.data.keyword.Bluemix_notm}}. Algunos de los mandatos {{site.data.keyword.Bluemix_notm}} son envoltorios de mandatos cf, mientras que otros proporcionan posibilidades ampliadas para usuarios de {{site.data.keyword.Bluemix_notm}}. La información que se indica a continuación lista todos los mandatos soportados por {{site.data.keyword.Bluemix_notm}} CLI e incluye sus nombres, opciones, uso, requisitos previos, descripciones y ejemplos.
{:shortdesc}
 
**Nota:** *Requisitos previos* lista las acciones que son necesarias antes de utilizar el mandato. Los mandatos que no tienen acciones de requisito previo listan **Ninguno**. De lo contrario, los requisitos previos pueden incluir una o varias de las acciones siguientes:
<dl>
<dt>Punto final</dt>
<dd>Un punto final de API se debe establecer por medio de la <code>bluemix api</code> antes de utilizar el mandato.</dd>
<dt>Login</dt>
<dd>El inicio de sesión que utiliza el mandato <code>bluemix login</code> es necesario antes de utilizar este mandato.</dd>
<dt>Target</dt>
<dd>El mandato <code>bluemix target</code> debe utilizarse para establecer un punto de extensión org y un espacio antes de utilizar este mandato.</dd>
<dt>Docker</dt>
<dd>La CLI de Docker CLI (docker) debe estar instalada para poder ejecutar este mandato.</dd>
</dl>

Puede usar los mandatos de {{site.data.keyword.Bluemix_notm}} siguientes:

 <table role="presentation"> 
 <tbody> 
 <tr> 
 <td>[bluemix help
](index.html#bluemix_help)</td> 
 <td>[api de bluemix](index.html#bluemix_api)</td> 
 <td>[inicio de sesión de bluemix](index.html#bluemix_login)</td>
 <td>[cierre de sesión de bluemix](index.html#bluemix_logout)</td>
 <td>[destino de bluemix](index.html#bluemix_target)</td>
 </tr> 
 <tr> 
 <td> 
 [bluemix info](index.html#bluemix_info) </td> 
 <td>[bluemix config](index.html#bluemix_config)</td> 
 <td>[lista de bluemix](index.html#bluemix_list)</td>
 <td>[escala bluemix](index.html#bluemix_scale)</td>
 <td>[curl bluemix](index.html#bluemix_curl)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam orgs](index.html#bluemix_iam_orgs) </td> 
 <td>[bluemix iam org](index.html#bluemix_iam_org)</td> 
 <td>[bluemix iam org-create](index.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](index.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](index.html#bluemix_iam_org_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam org-delete](index.html#bluemix_iam_org_delete) </td> 
 <td>[bluemix iam spaces](index.html#bluemix_iam_spaces)</td> 
 <td>[bluemix iam space](index.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](index.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](index.html#bluemix_iam_space_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam space-delete](index.html#bluemix_iam_space_delete) </td> 
 <td>[bluemix iam account-users](index.html#bluemix_iam_account-users) </td> 
 <td>[bluemix iam account-user-invite](index.html#bluemix_iam_account-user-invite)</td>
 <td>[bluemix iam org-users](index.html#bluemix_iam_org_users)</td>
 <td>[bluemix iam org-role-set](index.html#bluemix_iam_org_role_set)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam org-role-unset](index.html#bluemix_iam_org_role_unset) </td> 
 <td>[bluemix iam space-users](index.html#bluemix_iam_space_users)</td> 
 <td>[bluemix iam space-role-set](index.html#bluemix_iam_space_role_set)</td>
 <td>[bluemix iam space-role-unset](index.html#bluemix_iam_space_role_unset)</td>
 <td>[bluemix app push](index.html#bluemix_app_push)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app list](index.html#bluemix_app_list) </td> 
 <td>[bluemix app show](index.html#bluemix_app_show)</td> 
 <td>[bluemix app scale](index.html#bluemix_app_scale)</td>
 <td>[bluemix app delete](index.html#bluemix_app_delete)</td>
 <td>[bluemix app rename](index.html#bluemix_app_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app start](index.html#bluemix_app_start) </td> 
 <td>[bluemix app stop](index.html#bluemix_app_stop)</td> 
 <td>[bluemix app restart](index.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](index.html#bluemix_app_restage)</td>
 <td>[bluemix app instance-restart](index.html#bluemix_app_instance_restart)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app events](index.html#bluemix_app_events) </td> 
 <td>[bluemix app files](index.html#bluemix_app_files)</td> 
 <td>[bluemix app logs](index.html#bluemix_app_logs)</td>
 <td>[bluemix app env](index.html#bluemix_app_env)</td>
 <td>[bluemix app env-set](index.html#bluemix_app_env_set)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app env-unset](index.html#bluemix_app_env_unset) </td> 
 <td>[bluemix app stacks](index.html#bluemix_app_stacks)</td> 
 <td>[bluemix app stack](index.html#bluemix_app_stack)</td>
 <td>[bluemix app manifest-create](index.html#bluemix_app_manifest_create)</td>
 <td>[bluemix service offerings](index.html#bluemix_service_offerings)</td>
 </tr>
 
 <tr> 
 <td>[bluemix service list](index.html#bluemix_service_list) </td> 
 <td>[bluemix service show](index.html#bluemix_service_show)</td> 
 <td>[bluemix service create](index.html#bluemix_service_create)</td>
 <td>[bluemix service update](index.html#bluemix_service_update)</td>
 <td>[bluemix service delete](index.html#bluemix_service_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix service rename](index.html#bluemix_service_rename) </td> 
 <td>[bluemix service bind](index.html#bluemix_service_bind)</td> 
 <td>[bluemix service unbind](index.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](index.html#bluemix_service_key_create)</td>
 <td>[bluemix service key-delete](index.html#bluemix_service_key_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix service keys](index.html#bluemix_service_keys) </td> 
 <td>[bluemix service key-show](index.html#bluemix_service_key_show)</td> 
 <td>[bluemix service user-provided-create](index.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](index.html#bluemix_service_user_provided_update)</td>
 <td>[bluemix catalog templates](index.html#bluemix_catalog_templates)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix catalog template](index.html#bluemix_catalog_template) </td> 
 <td>[bluemix catalog template-run](index.html#bluemix_catalog_template_run)</td> 
 <td>[regiones de red bluemix](index.html#bluemix_network_regions)</td>
 <td>[bluemix network region-set](index.html#bluemix_network_region_set)</td>
 <td>[bluemix network routes](index.html#bluemix_network_routes)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network route-check](index.html#bluemix_network_route_check)</td> 
 <td>[bluemix network route-map](index.html#bluemix_network_route_map)</td> 
 <td>[bluemix network route-unmap](index.html#bluemix_network_route_unmap)</td>
 <td>[bluemix network route-create](index.html#bluemix_network_route_create)</td>
 <td>[bluemix network route-delete](index.html#bluemix_network_route_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network orphaned-routes-delete](index.html#bluemix_network_orphaned_routes_delete)</td> 
 <td>[bluemix network domains](index.html#bluemix_network_domains)</td> 
 <td>[bluemix network domain-create](index.html#bluemix_network_domain_create)</td>
 <td>[bluemix network domain-delete](index.html#bluemix_network_domain_delete)</td>
 <td>[bluemix network shared-domain-create](index.html#bluemix_network_shared_domain_create)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network shared-domain-delete](index.html#bluemix_network_shared_domain_delete)</td> 
 <td>[bluemix security cert](index.html#bluemix_security_cert)</td> 
 <td>[bluemix security cert-add](index.html#bluemix_security_cert_add)</td>
 <td>[bluemix security cert-remove](index.html#bluemix_security_cert_remove)</td>
 <td>[bluemix plugin repos](index.html#bluemix_plugin_repos)</td>
 </tr>
 
 <tr> 
 <td>[bluemix plugin repo-add](index.html#bluemix_plugin_repo_add)</td> 
 <td>[bluemix plugin repo-remove](index.html#bluemix_plugin_repo_remove)</td> 
 <td>[bluemix plugin repo-plugins](index.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](index.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](index.html#bluemix_plugin_install)</td>
 </tr>
 
 <tr> 
 <td>[bluemix plugin uninstall](index.html#bluemix_plugin_uninstall)</td> 
 <td>[bluemix ic init](index.html#bluemix_ic_init)</td> 
 <td>[bluemix ic attach](index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](index.html#bluemix_ic_build)</td>
 <td>[bluemix ic create](index.html#bluemix_ic_create)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic cpi](index.html#bluemix_ic_cpi)</td> 
 <td>[bluemix ic exec](index.html#bluemix_ic_exec)</td> 
 <td>[bluemix ic groups](index.html#bluemix_ic_groups)</td>
 <td>[bluemix ic group-inspect](index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](index.html#bluemix_ic_group_instances)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic group-create](index.html#bluemix_ic_group_create)</td> 
 <td>[bluemix ic group-update](index.html#bluemix_ic_group_update)</td> 
 <td>[bluemix ic group-remove](index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic images](index.html#bluemix_ic_images)</td>
 <td>[bluemix ic inspect](index.html#bluemix_ic_inspect)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic info](index.html#bluemix_ic_info)</td> 
 <td>[bluemix ic ips](index.html#bluemix_ic_ips)</td> 
 <td>[bluemix ic ip-request](index.html#ip_request)</td>
 <td>[bluemix ic ip-release](index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-bind](index.html#bluemix_ic_ip_bind)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic ip-unbind](index.html#bluemix_ic_ip_unbind)</td> 
 <td>[bluemix ic kill](index.html#bluemix_ic_kill)</td> 
 <td>[bluemix ic namespace-get](index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](index.html#pause)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic unpause](index.html#unpause)</td> 
 <td>[bluemix ic port](index.html#bluemix_ic_port)</td> 
 <td>[bluemix ic ps](index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic restart](index.html#bluemix_ic_restart)</td>
 <td>[bluemix ic rm](index.html#bluemix_ic_rm)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic rmi](index.html#bluemix_ic_rmi)</td> 
 <td>[bluemix ic run](index.html#bluemix_ic_run)</td> 
 <td>[bluemix ic route-map](index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic start](index.html#ic_start)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic stop](index.html#ic_stop)</td> 
 <td>[bluemix ic stats](index.html#bluemix_ic_stats)</td> 
 <td>[bluemix ic top](index.html#bluemix_ic_top)</td>
 <td>[bluemix ic volumes](index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic volume-inspect](index.html#bluemix_ic_volume_inspect)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic volume-create](index.html#bluemix_ic_volume_create)</td> 
 <td>[bluemix ic volume-remove](index.html#bluemix_ic_volume_remove)</td> 
 <td>[bluemix ic volume-fs](index.html#bluemix_ic_volume_fs)</td> 
 <td>[bluemix ic volume-fs-create](index.html#bluemix_ic_volume_fs_create)</td> 
 <td>[bluemix ic volume-fs-remove](index.html#bluemix_ic_volume_fs_remove)</td> 
 </tr>
 
 <tr>
 <td>[bluemix ic volume-fs-inspect](index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](index.html#bluemix_ic_volume_fs_flavors)</td> 
 <td>[bluemix ic wait](index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic version](index.html#bluemix_ic_version)</td>
 </tr>
 
 
 </tbody> 
 </table> 

  

## bluemix help
{: #bluemix_help}
Muestra la ayuda general para mandatos incorporados de primer nivel y nombres de espacios soportados de {{site.data.keyword.Bluemix_notm}} CLI, o la ayuda para un mandato o un nombre de espacio incorporado específico.

```
ayuda de bluemix [COMMAND|NAMESPACE]
```

**Requisitos previos**: Ninguno

**Opciones de mandatos**:

*COMMAND*|*NAMESPACE* (opcional): El mandato o el espacio de nombres para el que se muestra la ayuda. Si no se especifica, se mostrará la ayuda general para {{site.data.keyword.Bluemix_notm}} CLI.

**Ejemplos**:

Visualiza ayuda general para {{site.data.keyword.Bluemix_notm}} CLI:

```
bluemix help
```

Muestra ayuda para el mandato `info`:

```
información de ayuda de bluemix
```

Muestra la ayuda para el espacio de nombres `ic`:

```
bluemix help ic
```

o 

```
bluemix ic help
```

Muestra ayuda para el mandato `group-create` en el espacio de nombres `ic`:

```
bluemix ic help group-create
```


## api de bluemix
{: #bluemix_api}
Establezca o visualice el punto final de su API de {{site.data.keyword.Bluemix_notm}}. Este mandato acomoda el mandato `cf api`.

```
api de bluemix [API_ENDPOINT][--unset]
```

**Requisitos previos**: Ninguno

**Opciones de mandato**:

*API_ENDPOINT* (opcional): El punto final de la API que está destinado, como por ejemplo https://api.ng.bluemix.net.  Si no se especifican ambas opciones *API_ENDPOINT* y `--unset`, se mostrará el punto final de API actual.

`--unset` (opcional): Eliminar el valor de punto final de la API.

**Ejemplos**:

Establezca el punto final de la API a api.ng.bluemix.net:

```
bluemix api api.ng.bluemix.net
```

Visualice el punto final de la API actual:

```
api de bluemix
```

Desestablecer el punto final de la API:

```
bluemix api --unset
```


## inicio de sesión de bluemix
{: #bluemix_login}

Inicio de sesión de usuario. Este mandato acomoda el mandato `cf login`. Las opciones del mandato son las mismas que las opciones del mandato de `cf login`.

```
bluemix login [OPTIONS...]
```

**Requisitos previos**: Punto final

**Opciones de mandato**:
Para obtener información sobre las opciones soportadas por el mandato `login`, consulte la información de uso del mandato `cf login` para que los mandatos cf gestionen apps.


## cierre de sesión de bluemix
{: #bluemix_logout}

Cerrar sesión de usuario. Este mandato acomoda el mandato `cf logout`.

```
cierre de sesión de bluemix
```

**Requisitos previos**:  Ninguno


## destino de bluemix
{: #bluemix_target}


Establezca o visualice el espacio o la organización de destino. Este mandato acomoda el mandato `cf target`.

```
destino bluemix [-o ORG_NAME] [-s SPACE_NAME]
```

**Requisitos previos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

-o *ORG_NAME* (opcional):  El nombre de la organización a la que va dirigida.

-s *SPACE_NAME* (opcional):  El nombre del espacio al que va dirigido.

Si no se especifica -o *ORG_NAME* ni -s *SPACE_NAME*, se mostrará el espacio y la organización actuales.

**Ejemplos**:

Establezca la organización actual en `MyOrg` y el espacio en `MySpace`:

```
destino bluemix -o MyOrg -s MySpace
```

Visualice el espacio y la organización actuales:

```
destino de bluemix
```


## información de bluemix
{: #bluemix_info}

Vea la información básica de {{site.data.keyword.Bluemix_notm}}, incluida la región actual, la versión del controlador de nube y algunos puntos finales útiles, como por ejemplo los puntos finales para el inicio de sesión y el intercambio de señales de acceso.

```
información de bluemix
```

**Requisitos previos**:  Punto final


## bluemix config
{: #bluemix_config}


Escriba valores predeterminados en el archivo de configuración.

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR)
```

**Requisitos previos**:  Ninguno

**Opciones de mandato**:

--http-timeout *TIMEOUT_IN_SECONDS*:  El valor de tiempo de espera excedido para las solicitudes HTTP. El valor predeterminado es de 60 segundos.

--trace true|false|*path/to/file*:  Rastrear las solicitudes HTTP en el archivo terminal o especificado.

--color true|false:  Habilitar o inhabilitar la salida de color. La salida de color está habilitada de forma predeterminada.

--locale *LOCALE*:  Establecer un entorno local predeterminado. Si LOCALE es *CLEAR*, se suprimirá el entorno local anterior.

Sólo se puede especificar una de estas opciones a la vez.

**Ejemplos**:

Establezca el tiempo de espera de solicitud HTTP en 30 segundos:

```
bluemix config --http-timeout 30
```

Habilitar la salida de rastreo para las solicitudes HTTP:

```
bluemix config --trace true
```

Rastrear solicitudes HTTP en un archivo especificado */home/usera/my_trace*:

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


## lista de bluemix
{: #bluemix_list}

Lista todas las apps cf, los contenedores, los grupos de contenedor y los grupos de máquinas virtuales en el espacio actual.

```
lista de bluemix [apps|contenedores|container-groups|vm-groups]
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandatos**:

apps (opcional):  Visualizar sólo la información de las apps.

containers (opcional):  Visualizar sólo la información de los contenedores.

container-groups (opcional):  Visualizar sólo la información de grupos del contenedor.

vm-groups (opcional):  Visualizar sólo la información de los grupos de máquinas virtuales.

Sólo puede especificarse una de los `apps`, `containers`, `container-groups` o `vm-groups` a la vez. Si no se especifica ninguna de ellas, se listarán todas las apps de cf, los contenedores, los grupos de contenedores y los grupos de máquinas virtuales.

**Ejemplos**:

Listar todas las apps de cf:

```
lista de apps de bluemix
```

Lista todas las instancias del contenedor:

```
contenedores de la lista de bluemix
```

Lista todas las apps, contenedores, grupos de contenedores y grupos de máquinas virtuales:

```
lista de bluemix
```


## escala bluemix
{: #bluemix_scale}

Escala verticalmente u horizontalmente la app cf o el grupo de contenedores a un recuento de instancias, cuota de disco y tamaño de memoria específicos.

**Nota:** Sólo puede especificarse un número de instancias para escalar un grupo de contenedores. Si no se especifica ninguna opción, este mandato lista la instancia actual para el grupo de contenedores, y también la cuota de disco y el tamaño de memoria para la app cf.

```
bluemix scale CF_APP_NAME|CONTAINER_GROUP_NAME [-i INSTANCE_COUNT][-k DISK_QUOTA] [-m MEMORY_SIZE]
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandatos**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* (obligatorio):  El nombre de la aplicación cf o del grupo de contenedores que se va a escalar.

-i *INSTANCE_COUNT* (opcional):  El nuevo número de instancia para la aplicación cf o el grupo de contenedores que se va a escalar. Esta opción es la única opción válida para grupos de contenedores que se van a escalar.

-k *DISK_QUOTA* (opcional):  La nueva cuota de disco de la aplicación cf. No es válida para escalar un grupo de contenedores.

-m *MEMORY_SIZE* (opcional):  El nuevo tamaño de memoria para la aplicación cf. No es válida para escalar un grupo de contenedores.

**Ejemplos**:

Mostrar el número de instancias actual para `mi-grupo-contenedor`:

```
escala bluemix mi-grupo-contenedor
```

Escalar `mi-grupo-contenedor` a 2 instancias:

```
escala bluemix mi-grupo-contenedor -i 2
```

Escalar `my-java-app` a 3 instancias, cuota de disco de 8G y tamaño de memoria de 1024M:

```
escala bluemix mi-app-java -i 3 -k 8G -m 1024M
```


## curl bluemix
{: #bluemix_curl}

Ejecuta una solicitud HTTP sin procesar a {{site.data.keyword.Bluemix_notm}}. *Content-Type* se establece en *application/json* de forma predeterminada. Este mandato envía la solicitud a {{site.data.keyword.Bluemix_notm}} Multi-Cloud Control Proxy. Para obtener las vías de acceso admitidas, consulte las definiciones de vías de acceso de API en el [documento de API CloudFoundry](http://apidocs.cloudfoundry.org/){: new_window}.

```
RUTA bluemix curl [OPCIONES...]
```

**Requisitos previos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

*PATH*  (obligatorio):  vía de acceso de la URL del recurso. Por ejemplo, /v2/apps.

*OPTIONS*  (opcional):  las opciones a las que da soporte el mandato `bluemix curl` son las mismas que las del mandato `cf curl`.

**Ejemplos**:

Vea la información para todas las organizaciones de la cuenta actual:

```
bluemix curl /v2/organizations
```


## bluemix iam orgs
{: #bluemix_iam_orgs}

Listar todas las organizaciones

```
bluemix iam orgs [-r REGION --guid]
```

**Requisitos previos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

*-r REGION*  (opcional): para qué región se muestra la información de organización. Si se establece en 'all', se listan todas las organizaciones de todas las regiones. 

*--guid* (opcional): Visualiza la GUID de las organizaciones.

**Ejemplos**:
Listar todas las organizaciones en la región: `us-south` con la GUID visualizada

```
bluemix iam orgs -r us-south --guid
```

## bluemix iam org
{: #bluemix_iam_org}

Mostrar la información para la organización especificada.

```
bluemix iam org ORG_NAME [--guid]
```

**Requisitos previos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

*ORG_NAME* (obligatorio): El nombre de la organización.

*--guid* (opcional): Visualiza la GUID de la organización.


**Ejemplos**:
Muestra la información de la organización `IBM` con el GUID visualizado

```
bluemix iam org IBM --guid
```

## bluemix iam org-create
{: #bluemix_iam_org_create}

Crear una nueva organización. Esta operación solamente puede realizarla el propietario de cuenta.

```
bluemix iam org-create ORG_NAME
```

**Requisitos previos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

*ORG_NAME* (obligatorio): El nombre de la organización que se está creando.

**Ejemplos**: Crear una organización denominada `IBM`.

```
bluemix iam org-create IBM
```


## bluemix iam org-replicate
{: #bluemix_iam_org_replicate}

Replicar una organización desde la región actual a otra región.

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

**Requisitos previos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

*ORG_NAME* (obligatorio):  El nombre de la organización existente que se replicará.

*REGION_NAME*  (obligatorio):  El nombre de la región que aloja la organización replicada.

**Ejemplos**:

Replicar la organización `myorg` en la región `eu-gb`:

```
bluemix iam org-replicate myorg eu-gb
```


## bluemix iam org-rename
{: #bluemix_iam_org_rename}

Cambiar el nombre de una organización. Esta operación solamente la puede llevar a cabo un gestor de organización.

```
bluemix iam org-rename OLD_ORG_NAME NEW_ORG_NAME
```

**Requisitos previos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

*OLD_ORG_NAME* (obligatorio):  El nombre anterior de la organización que se va a renombrar.

*NEW_ORG_NAME*  (obligatorio):  El nuevo nombre de la organización que se ha renombrado.


## bluemix iam org-delete
{: #bluemix_iam_org_delete}

Suprimir la organización especificada en la región actual.

```
bluemix iam org-delete ORG_NAME [-f --all]
```

**Requisitos previos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

*ORG_NAME* (obligatorio):  El nombre de la organización existente que se suprimirá.

*-f* (opcional): Forzar supresión sin confirmación.

*--all* (opcional): Suprimir la organización de todas las regiones.


## bluemix iam spaces
{: #bluemix_iam_spaces}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf spaces`.


## bluemix iam space
{: #bluemix_iam_space}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf space`.


## bluemix iam space-create
{: #bluemix_iam_space_create}

Este mandato tiene la misma función y las mismas opciones que el mandato que el mandato `cf create-space`.


## bluemix iam space-rename
{: #bluemix_iam_space_rename}


Este mandato tiene la misma función y las mismas opciones que el mandato que el mandato `cf rename-space`.


## bluemix iam space-delete
{: #bluemix_iam_space_delete}


Este mandato tiene la misma función y las mismas opciones que el mandato `cf delete-space`.


## bluemix iam account-users
{: #bluemix_iam_account_users}

Muestra usuarios asociados con la cuenta. Esta operación solamente puede llevarla a cabo el propietario de cuenta.

```
bluemix iam account-users
```

## bluemix iam account-user-invite
{: #bluemix_iam_account-user_inviate}


Invita a un usuario a la cuenta con una organización y un rol de espacio ya establecido. Esta operación solamente puede llevarla a cabo el propietario de cuenta.

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

**Requisitos previos**:  Punto final, Inicio de sesión


**Opciones de mandato**:

*USER_NAME* (obligatorio): El nombre del usuario que se invita.

*ORG_NAME* (obligatorio): El nombre de la organización a la que se invita este usuario.

*ORG_ROLE* (obligatorio): El nombre del rol de la organización a la que se invita este usuario. Por ejemplo:

<dl>
<dt>OrgManager</dt>
<dd>Este rol puede invitar y gestionar usuarios, seleccionar y cambiar planes y establecer límites de gasto.</dd>
<dt>BillingManager</dt>
<dd>Este role puede crear y gestionar la cuenta de facturación y la información de pago.</dd>
<dt>OrgAuditor</dt>
<dd>Este rol tiene acceso de sólo lectura a informes e información de organización.</dd>
</dl> 

*SPACE_NAME* (obligatorio): El nombre del espacio al que se invita este usuario.

*SPACE_ROLE* (obligatorio): El nombre del rol de espacio al que se invita este usuario. Por ejemplo:

<dl>
<dt>SpaceManager</dt>
<dd>Este rol puede invitar y gestionar usuarios, y habilitar características para un espacio dado.</dd>
<dt>SpaceDeveloper</dt>
<dd>Este rol puede crear y gestionar apps y servicios, y ver registros e informes.</dd>
<dt>SpaceAuditor</dt>
<dd>Este rol puede ver los registros, informes y valores para el espacio.</dd>
</dl> 

**Ejemplos**:

Invite al usuario `Mary` a la organización `IBM` como rol `OrgManager` y el espacio `Cloud` como rol `SpaceAuditor`:

```
bluemix iam account-user-inviate Mary IBM OrgManager Cloud SpaceAuditor
```

## bluemix iam org-users
{: #bluemix_iam_org_users}

Visualice usuarios en el archivo de organización según el rol.

```
bluemix iam org-users ORG_NAME [-a]
```

**Requisitos previos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

*ORG_NAME* (obligatorio): El nombre de la organización.

*-a* (opcional): Listar todos los usuarios de la organización especificada, no agrupada por role.


## bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

Asignar un rol de organización a un usuario. Esta operación solamente la puede llevar a cabo un gestor de  organización.

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

**Requisitos previos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

*USER_NAME* (obligatorio): El nombre del usuario que se asigna.

*ORG_NAME* (obligatorio): El nombre de la organización a la que se asigna este usuario.

*ORG_ROLE* (obligatorio): El nombre del rol de la organización a la que se asigna este usuario. Por ejemplo:

<dl>
<dt>OrgManager</dt>
<dd>Este rol puede invitar y gestionar usuarios, seleccionar y cambiar planes y establecer límites de gasto.</dd>
<dt>BillingManager</dt>
<dd>Este role puede crear y gestionar la cuenta de facturación y la información de pago.</dd>
<dt>OrgAuditor</dt>
<dd>Este rol tiene acceso de sólo lectura a informes e información de organización.</dd>
</dl> 

**Ejemplos**:

Asigne el usuario `Mary` a la organización `IBM` como rol `OrgManager`. 

```
bluemix iam org-role-set Mary IBM OrgManager
```


## bluemix iam org-role-unset
{: #bluemix_iam_org_role_unset}

Elimine un rol de organización de un usuario. Esta operación solamente la puede llevar a cabo un gestor de  organización.

```
bluemix iam org-role-unset USER_NAME ORG_NAME ORG_ROLE
```

**Requisitos previos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

*USER_NAME* (obligatorio): El nombre del usuario que se elimina.

*ORG_NAME* (obligatorio): El nombre de la organización de la que se elimina el usuario.

*ORG_ROLE* (obligatorio): El nombre del rol de la organización de la que se elimina este usuario. Por ejemplo:

<dl>
<dt>OrgManager</dt>
<dd>Este rol puede invitar y gestionar usuarios, seleccionar y cambiar planes y establecer límites de gasto.</dd>
<dt>BillingManager</dt>
<dd>Este role puede crear y gestionar la cuenta de facturación y la información de pago.</dd>
<dt>OrgAuditor</dt>
<dd>Este rol tiene acceso de sólo lectura a informes e información de organización.</dd>
</dl> 

**Ejemplos**:

Elimine el usuario `Mary` de la organización `IBM` como rol `OrgManager`:

```
bluemix iam org-role-unset Mary IBM OrgManager
```


## bluemix iam space-users
{: #bluemix_iam_space_users}

Visualice usuarios en el espacio especificado según el rol.

```
bluemix iam space-users ORG_NAME SPACE_NAME
```

**Requisitos previos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

*ORG_NAME* (obligatorio): El nombre de la organización

*SPACE_NAME* (obligatorio): El nombre del espacio.


## bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

Asignar un rol de espacio a un usuario. Esta operación solamente la puede llevar a cabo un gestor de espacios.

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

**Requisitos previos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

*USER_NAME* (obligatorio): El nombre del usuario que se asigna.

*ORG_NAME* (obligatorio): El nombre de la organización a la que se asigna este usuario.

*SPACE_NAME* (obligatorio): El nombre del espacio al que se asigna este usuario.

*SPACE_ROLE* (obligatorio): El nombre del rol de espacio al que se asigna este usuario. Por ejemplo:

<dl>
<dt>SpaceManager</dt>
<dd>Este rol puede invitar y gestionar usuarios, y habilitar características para un espacio dado.</dd>
<dt>SpaceDeveloper</dt>
<dd>Este rol puede crear y gestionar apps y servicios, y ver registros e informes.</dd>
<dt>SpaceAuditor</dt>
<dd>Este rol puede ver los registros, informes y valores para el espacio.</dd>
</dl> 


**Ejemplos**:

Asigne el usuario `Mary` a la organización `IBM` y el espacio `Cloud` como rol `SpaceManager`:

```
bluemix iam space-role-set Mary IBM Cloud SpaceManager
```

## bluemix iam space-role-unset
{: #bluemix_iam_space_role_unset}

Elimine un rol de espacio de un usuario. Esta operación solamente la puede llevar a cabo un gestor de espacios.

```
bluemix iam space-role-unset USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

**Requisitos previos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

*USER_NAME* (obligatorio): El nombre del usuario que se elimina.

*ORG_NAME* (obligatorio): El nombre de la organización de la que se elimina el usuario.

*SPACE_NAME* (obligatorio): El nombre del espacio del que se elimina este usuario.

*SPACE_ROLE* (obligatorio): El nombre del rol de espacio del que se elimina este usuario. Por ejemplo:

<dl>
<dt>SpaceManager</dt>
<dd>Este rol puede invitar y gestionar usuarios, y habilitar características para un espacio dado.</dd>
<dt>SpaceDeveloper</dt>
<dd>Este rol puede crear y gestionar apps y servicios, y ver registros e informes.</dd>
<dt>SpaceAuditor</dt>
<dd>Este rol puede ver los registros, informes y valores para el espacio.</dd>
</dl> 

**Ejemplos**:

Elimine el usuario `Mary` de la organización `IBM` y el espacio `Cloud` como rol `SpaceManager`: 

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```


## bluemix app push
{: #bluemix_app_push}

Este mandato tiene la misma función y opciones que el mandato `cf push`.


## bluemix app list
{: #bluemix_app_list}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf apps`.


## bluemix app show
{: #bluemix_app_show}

Este mandato tiene la misma función y opciones que el mandato `cf app`.


## bluemix app scale
{: #bluemix_app_scale}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf scale`.


## bluemix app delete
{: #bluemix_app_delete}

Este mandato tiene la misma función y opciones que el mandato `cf delete`.


## bluemix app rename
{: #bluemix_app_rename}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf rename`.


## bluemix app start
{: #bluemix_app_start}

Este mandato tiene la misma función y opciones que el mandato `cf start`.


## bluemix app stop
{: #bluemix_app_stop}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf stop`.


## bluemix app restart
{: #bluemix_app_restart}

Este mandato tiene la misma función y opciones que el mandato `cf restart`.


## bluemix app restage
{: #bluemix_app_restage}


Este mandato tiene la misma función y las mismas opciones que el mandato `cf restage`.


## bluemix app instance-restart
{: #bluemix_app_instance_restart}


Este mandato tiene la misma función y opciones que el mandato `cf restart-app-instance`.


## bluemix app events
{: #bluemix_app_events}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf events`.


## bluemix app files
{: #bluemix_app_files}

Este mandato tiene la misma función y opciones que el mandato `cf files`.


## bluemix app logs
{: #bluemix_app_logs}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf logs`.


## bluemix app env
{: #bluemix_app_env}

Este mandato tiene la misma función y opciones que el mandato `cf env`.


## bluemix app env-set
{: #bluemix_app_env_set}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf set-env`.


## bluemix app env-unset
{: #bluemix_app_env_unset}

Este mandato tiene la misma función y opciones que el mandato `cf unset-env`.


## bluemix app stacks
{: #bluemix_app_stacks}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf stacks`.


## bluemix app stack
{: #bluemix_app_stack}

Este mandato tiene la misma función y opciones que el mandato `cf stack`.


## bluemix app manifest-create
{: #bluemix_app_manifest_create}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf create-app-manifest`.


## bluemix service offerings
{: #bluemix_service_offerings}


Este mandato tiene la misma función y opciones que el mandato `cf marketplace`.


## bluemix service list
{: #bluemix_service_list}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf services`.


## bluemix service show
{: #bluemix_service_show}

Este mandato tiene la misma función y opciones que el mandato `cf service`.


## bluemix service create
{: #bluemix_service_create}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf create-service`.


## bluemix service update
{: #bluemix_service_update}

Este mandato tiene la misma función y opciones que el mandato `cf update-service`.


## bluemix service delete
{: #bluemix_service_delete}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf delete-service`.


## bluemix service rename
{: #bluemix_service_rename}

Este mandato tiene la misma función y opciones que el mandato `cf rename-service`.


## bluemix service bind
{: #bluemix_service_bind}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf bind-service`.


## bluemix service unbind
{: #bluemix_service_unbind}

Este mandato tiene la misma función y opciones que el mandato `cf unbind-service`.


## bluemix service key-create
{: #bluemix_service_key_create}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf create-service-key`.


## bluemix service key-delete
{: #bluemix_service_key_delete}

Este mandato tiene la misma función y opciones que el mandato `cf delete-service-key`.


## bluemix service keys
{: #bluemix_service_keys}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf service-keys`.


## bluemix service key-show
{: #bluemix_service_key_show}

Este mandato tiene la misma función y opciones que el mandato `cf service-key`.


## bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf create-user-provided-service`.


## bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

Este mandato tiene la misma función y opciones que el mandato `cf update-user-provided-service`.


## bluemix catalog templates
{: #bluemix_catalog_templates}

Visualizar las plantillas de contenedor modelo en Bluemix.

```
plantillas de catálogo de bluemix [-d]
```

**Requisitos previos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

-d (opcional):  Si se especifica la opción `-d`, también se mostrará la descripción de cada plantilla. De lo contrario, sólo se mostrará el ID y el nombre de cada plantilla.


## bluemix catalog template
{: #bluemix_catalog_template}

Ver la información detallada de una plantilla de contenedor modelo especificada.

```
bluemix catalog template TEMPLATE_ID
```

**Requisitos previos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

*TEMPLATE_ID* (obligatorio):  El ID de la plantilla de contenedor modelo. Utilice 'bluemix templates' para ver todos los ID de plantillas.

**Ejemplos**:

Ver detalles de la plantilla `mobileBackendStarter`:

```
bluemix catalog template mobileBackendStarter
```


## bluemix catalog template-run
{: #bluemix_catalog_template_run}

Crea una app cf que se base en la plantilla específica con la URL y la descripción especificadas. De forma predeterminada, la nueva app se iniciará automáticamente.

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*TEMPLATE_ID* (necesario):  La plantilla en la que se basará la app cuando se cree. Utilice `plantillas bluemix` para ver todos los ID de plantillas.

*CF_APP_NAME*  (obligatorio):  el nombre de la app cf que se creará.

-u *URL*  (opcional):  La ruta de la app. Si no se especifica, la ruta se establece mediante {{site.data.keyword.Bluemix_notm}} que se basa automáticamente en el nombre de la app y en el dominio predeterminado.

-d *DESCRIPTION*  (opcional):  descripción de la app.

--no-start  (opcional):  no inicie la app automáticamente después de crearla. Si no se especifica, la app se iniciará automáticamente una vez que se haya creado.

**Ejemplos**:

Crear una aplicación cf `my-app` basada en la plantilla `javaHelloWorld`:

```
bluemix catalog template-run javaHelloWorld my-app
```

Crear una aplicación `my-ruby-app` en función de la plantilla `rubyHelloWorld` con la ruta `myrubyapp.ng.bluemix.net` y la descripción `Mi primera app ruby en {{site.data.keyword.Bluemix_notm}}.`:

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "Mi primera app ruby en {{site.data.keyword.Bluemix_notm}}".
```

Crear una aplicación `my-python-app` basada en la plantilla `pythonHelloWorld` sin inicio automático:

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


## regiones de red bluemix
{: #bluemix_network_regions}

Visualiza la información para todas las regiones en {{site.data.keyword.Bluemix_notm}}.

```
regiones de red bluemix
```

**Requisitos previos**:  Punto final


## bluemix network region-set
{: #bluemix_network_region_set}

Se dirige a la región que se ha especificado. Este mandato vuelve a dirigirse automáticamente a la misma organización y espacio de la nueva región, si es posible. De lo contrario, el mandato solicitará al usuario que seleccione una nueva organización y un nuevo espacio si el usuario ya ha iniciado sesión. El punto final de API cambia en consecuencia.

```
bluemix network region-set REGION_NAME
```

**Requisitos previos**:  Punto final

**Opciones de mandato**:

*REGION_NAME* (obligatorio): El nombre de la región a la que desea cambiar. Puede utilizar el mandato `bluemix network regions` para visualizar todos los nombres de región.

**Ejemplos**:

Establezca la región actual en `eu-gb`:

```
bluemix network region-set eu-gb
```


## bluemix network routes
{: #bluemix_network_routes}

Este mandato tiene la misma función y opciones que el mandato `cf routes`.


## bluemix network route-check
{: #bluemix_network_route_check}

Este mandato tiene la misma función y opciones que el mandato `cf check-route`.


## bluemix network route-map
{: #bluemix_network_route_map}

Correlacione una ruta a una app cf o grupo de contenedores que tenga un dominio y nombre de host específicos.

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandatos**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* (obligatorio):  El nombre de la app o grupo de contenedores cf que se va a correlacionar con una ruta.

*DOMAIN*  (obligatorio):  El dominio de la ruta. Por ejemplo, mybluemix.net o ng.bluemix.net. 

-n *HOST_NAME*  (opcional):  El nombre de host de la ruta. Si no se facilita, el nombre de host se establece en el nombre de la app o grupo de contenedores de forma predeterminada.

**Ejemplos**:

Correlacionar una ruta a `my-app` con un dominio especificado:

```
bluemix network route-map my-app mybluemix.net
```

Correlacione una ruta a 'my-container-group' con el dominio y el nombre de host especificados:

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
{: #bluemix_network_route_unmap}

Elimina la correlación entre la ruta específica y una app cf existente o grupo de contenedores.

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandatos**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*  (obligatorio):  el nombre de la app cf o grupo de contenedores.

*DOMAIN*  (obligatorio):  el dominio de la ruta (por ejemplo, mybluemix.net o ng.bluemix.net). 

-n *HOST_NAME*  (opcional):  El nombre de host de la ruta. Si no se proporciona, el nombre de host se establece en el nombre de la app o en el nombre de grupo de contenedores de forma predeterminada.

**Ejemplos**:

Descorrelacionar `my-app.mybluemix.net` desde `my-app`:

```
bluemix network route-unmap my-app mybluemix.net
```

Descorrelacionar `abc.ng.bluexmix.net` desde `my-container-group`:

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
{: #bluemix_network_route_create}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf create-route`.


## bluemix network route-delete
{: #bluemix_network_route_delete}

Este mandato tiene la misma función y opciones que el mandato `cf delete-route`.


## bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

Este mandato tiene la misma función y opciones que el mandato `cf delete-orphaned-routes`.


## bluemix network domains
{: #bluemix_network_domains}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf domains`.


## bluemix network domain-create
{: #bluemix_network_domain_create}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf create-domain`.


## bluemix network domain-delete
{: #bluemix_network_domain_delete}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf delete-domain`.


## bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf create-shared-domain`.


## bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

Este mandato tiene la misma función y las mismas opciones que el mandato `cf delete-shared-domain`.


## bluemix security cert
{: #bluemix_security_cert}

Liste la información de certificado de un dominio.

```
bluemix security cert DOMAIN_NAME
```

**Requisitos previos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

*DOMAIN_NAME* (obligatorio): El dominio que aloja el certificado.

**Ejemplos**:

Ver la información de certificado del dominio `ibmcxo-eventconnect.com`:

```
bluemix security cert ibmcxo-eventconnect.com
```


## bluemix security cert-add
{: #bluemix_security_cert_add}

Añadir un certificado para el dominio especificado en la organización actual.

```
bluemix security cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD][-i INTERMEDIATE_CERT_FILE] [--verify-client]
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*DOMAIN* (obligatorio):  El dominio al que se añade el certificado.

-k *PRIVATE_KEY_FILE* (obligatorio):  La vía de acceso del archivo de claves privado.

-c *CERT_FILE* (obligatorio):  La vía de acceso del archivo de certificado.

-p *PASSWORD* (opcional):  La contraseña para el certificado.

-i *INTERMEDIATE_CERT_FILE* (opcional):  La vía de acceso del archivo de certificado intermedio.

--verify-client (opcional):  Si debe habilitarse o no la verificación de certificados de cliente.

**Ejemplos**:

Añadir un certificado al dominio `ibmcxo-eventconnect.com`:

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


## bluemix security cert-remove
{: #bluemix_security_cert_remove}

Eliminar un certificado del dominio especificado en la organización actual.

```
bluemix security cert-remove DOMAIN [-f]
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*DOMAIN* (obligatorio):  Dominio a eliminar del certificado.

-f  (opcional):  Forzar supresión sin confirmación.







## bluemix plugin repos
{: #bluemix_plugin_repos}

Cree una lista de todos los repositorios de plugin que se registran en {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin repos
```

**Requisitos previos**:  Ninguno


## bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

Agrega un nuevo repositorio de plugin a {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

**Requisitos previos**:  Ninguno

**Opciones de mandato**:

*REPO_NAME*  (obligatorio):  el nombre del repositorio que se añadirá. Puede volver a definir su propio nombre para cada repositorio.

*REPO_URL*  (obligatorio):  el URL del repositorio que se añadirá. El URL de repositorio debe contener el protocolo (por ejemplo, http://plugins.ng.bluemix.net en lugar de plugins.ng.bluemix.net). http://plugins.ng.bluemix.net es el repositorio de plugins oficial de {{site.data.keyword.Bluemix_notm}} CLI.

**Ejemplos**:

Añadir el repositorio de plugins oficial de Bluemix CLI como `bluemix-repo`:

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
{: #bluemix_plugin_repo_remove}

Elimina el repositorio de plugins de {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin repo-remove REPO_NAME
```

**Requisitos previos**:  Ninguno

**Opciones de mandato**:

*REPO_NAME*  (obligatorio):  el nombre del repositorio que se eliminará.

**Ejemplos**:

Eliminar el repositorio `bluemix-repo` de {{site.data.keyword.Bluemix_notm}} CLI:

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugins
{: #bluemix_plugin_repo_plugins}

Crea una lista de todos los plugins disponibles en todos los repositorios o repositorios específicos.

```
bluemix plugin repo-plugins [-r REPO_NAME]
```

**Requisitos previos**:  Ninguno

**Opciones de mandato**:

-r *REPO_NAME*  (opcional):  crea una lista de sólo los plugins del repositorio especificado.

**Ejemplos**:

Crea una lista de todos los plugins en todos los repositorios añadidos:

```
bluemix plugin repo-plugins
```

Listar todos los plugins del repositorio `bluemix-repo`:

```
bluemix plugin repo-plugins -r bluemix-repo
```


## bluemix plugin list
{: #bluemix_plugin_list}

Crea una lista de todos los plugins instalados en {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin list
```

**Requisitos previos**:  Ninguno


## bluemix plugin install
{: #bluemix_plugin_install}

Instalar la versión específica del plugin en {{site.data.keyword.Bluemix_notm}} CLI desde la vía de acceso o el repositorio especificados.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME][-v VERSION]
```

**Requisitos previos**: Ninguno

**Opciones de mandatos**:

*PLUGIN_PATH*|*PLUGIN_NAME* (obligatorio):  Si `-r *REPO_NAME*` no está especificado, el plugin se instala desde la vía de acceso local o la URL remota especificadas.

-r *REPO_NAME*  (opcional):  El nombre del repositorio donde se encuentra el binario del plugin.
-v *VERSION*  (opcional):  La versión del plugin que se instalará. Si no se proporciona, se instalará la versión más reciente del plugin. Esta opción sólo es válida al instalar el plugin desde el repositorio.

**Ejemplos**:

Instala un plugin desde el archivo local:

```
bluemix plugin install /downloads/new_plugin
```

Instala un plugin desde la URL remota:

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

Instale el plugin `IBM-Containers` de la versión más reciente del repositorio `bluemix-repo`:

```
bluemix plugin install IBM-Containers -r bluemix-repo
```
Instale el plugin `IBM-Containers` con la versión `0.5.800` del repositorio `bluemix-repo`:

```
bluemix plugin install IBM-Containers -r bluemix-repo -v 0.5.800
```






## bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

Desinstala el plugin especificado desde {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin uninstall PLUGIN_NAME
```

**Requisitos previos**:  Ninguno

**Opciones de mandato**:

*PLUGIN_NAME*  (obligatorio):  El nombre del plugin que se desinstalará.

**Ejemplos**:

Desinstalar el plugin `IBM-Containers` que se ha instalado previamente:

```
bluemix plugin uninstall IBM-Containers
```


## bluemix ic init
{: #bluemix_ic_init}

Inicializar el entorno de contenedores en su máquina local para usar todas las posibilidades del servicio IBM Containers.

```
bluemix ic init
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Nota:** antes de la inicialización, asegúrese de que la CLI de Docker (docker) esté instalada y configurada en su variable de entorno PATH. Para cambiar a otra región, utilice el mandato `bluemix region-set`. 

**Ejemplos**:

Cambiar a la región `us-south`:

```
bluemix region-set us-south
```


## bluemix ic attach
{: #bluemix_ic_attach}

Controlar un contenedor en ejecución o ver su resultado. Utilice `CTRL+C` para salir y detener el contenedor. Este mandato llama a la CLI de Docker. Para obtener más información, consulte el mandato [attach](https://docs.docker.com/reference/commandline/attach/){: new_window} en la ayuda de Docker. 

```
bluemix ic attach [--no-stdin][--sig-proxy] CONTAINER
```

**Requisitos previos**:  Endpoint, Login, Target, Docker

**Opciones de mandato**:

--no-stdin  (opcional):  no incluir la entrada estándar.

--sig-proxy  (opcional):  usar proxy de todas las señales recibidas para el proceso. El valor predeterminado es **true**.

*CONTAINER*  (necesario): el nombre de contenedor o ID.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para adjuntar al contenedor `my_container`:
```
bluemix ic attach my_container
```


## bluemix ic build
{: #bluemix_ic_build}

Llama al servicio de compilación de IBM Containers para compilar una imagen Docker en local o en su repositorio privado de {{site.data.keyword.Bluemix_notm}}. Este mandato llama a la CLI de Docker. Para obtener más información, consulte el mandato [build](https://docs.docker.com/reference/commandline/build/){: new_window} en la ayuda de Docker. 

```
bluemix ic build -t TAG|--tag TAG [--no-cache][-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

**Requisitos previos**:  Endpoint, Login, Target, Docker

**Opciones de mandato**:

-t *TAG*|--tag *TAG*  (obligatorio): el nombre de repositorio a aplicar a la imagen que se crea.

--no-cache  (opcional): no utilizar la caché cuando se construye la imagen. El valor predeterminado es **false**.

-p|--pull  (opcional): Intenta obtener (pull) la imagen base del registro, aunque esté en la memoria caché.

-q|--quiet  (opcional): Elimina la salida detallada que generan los contenedores. El valor predeterminado es **false**.

*DOCKERFILE_LOCATION*  (obligatorio): La vía de acceso a Dockerfile y contexto en el host local.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para compilar una imagen llamada *myimage*. El Dockerfile y otros artefactos a utilizar en la compilación están en el mismo directorio que el mandato desde el que se ejecuta. Como el registro y el espacio de nombres se incluyen en el nombre de imagen, la imagen se construye en el repositorio {{site.data.keyword.Bluemix_notm}} privado de su organización.
```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


## bluemix ic create
{: #bluemix_ic_create}

Crear un nuevo contenedor en su repositorio de {{site.data.keyword.Bluemix_notm}}. Este mandato envuelve el mandato `docker create`. Para obtener más información, consulte el mandato [create](https://docs.docker.com/reference/commandline/create/){: new_window} en la ayuda de Docker.


## bluemix ic cpi
{: #bluemix_ic_cpi}

Acceder a una imagen Docker Hub o una imagen desde su registro local y copiar la imagen en su repositorio privado de {{site.data.keyword.Bluemix_notm}}.

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*SOURCE_IMAGE*  (obligatorio): El repositorio de origen y el nombre de la imagen.

*DESTINATION_IMAGE*  (obligatorio): el URL del repositorio {{site.data.keyword.Bluemix_notm}} privado, que incluye el espacio de nombres y el nombre de la imagen de destino. La etiqueta de la imagen es opcional.

**Ejemplos**:

Copiar una imagen del repositorio de origen a su repositorio privado y añadir una etiqueta a la imagen:

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

Copiar la imagen `sinatra` desde el repositorio `training` a su repositorio privado `registry.ng.bluemix.net/mynamespace` y llamar a la imagen `mysinatra`. Añadir una etiqueta `v1` a la imagen `mysinatra`. 

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


## bluemix ic exec
{: #bluemix_ic_exec}


Ejecutar un mandato dentro de un contenedor. Para obtener más información, consulte el mandato [exec](https://docs.docker.com/reference/commandline/exec/){: new_window} en la ayuda de Docker.

```
bluemix ic exec [-d|--detach][-it] [-u USER|--user USER] CONTAINER [CMD]
```

**Requisitos previos**:  Endpoint, Login, Target, Docker

**Opciones de mandato**:

-d|--detach  (opcional): ejecutar el mandato especificado en segundo plano.

-it  (opcional): modalidad interactiva. Mantenga visualizada la entrada estándar. Escriba `exit` para salir.

-u *USER*|--user *USER*  (opcional): El nombre de usuario.

*CONTAINER*  (necesario): el nombre de contenedor o ID.

*CMD*  (opcional): el mandato a ejecutar dentro del contenedor o contenedores especificados.

**Ejemplos**:

Ejecute el mandato `bash` dentro del contenedor `my_container` en modalidad interactiva:

```
bluemix ic exec -it my_container bash
```

Ejecutar el mandato `date` dentro del contenedor `my_container`:

```
bluemix ic exec my_container date
```


## bluemix ic groups
{: #bluemix_ic_groups}

Listar grupos de contenedor en el repositorio privado de {{site.data.keyword.Bluemix_notm}} de la organización.

```
bluemix ic groups
```

**Requisitos previos**:  Punto final, inicio de sesión, destino


## bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

Ver información detallada, como variables de entorno, puertos o memoria, especificada para un grupo de contenedores cuando se crea.

```
bluemix ic group-inspect CONTAINER_GROUP
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*CONTAINER_GROUP*  (obligatorio): el nombre o ID del grupo de contenedores.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para inspeccionar el grupo de contenedores `my_group`:
```
bluemix ic group-inspect my_group
```


## bluemix ic group-instances
{: #bluemix_ic_group_instances}

Listar instancias de un grupo de contenedores especificado.

```
bluemix ic group-instances CONTAINER_GROUP
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*CONTAINER_GROUP*  (obligatorio): el nombre o ID del grupo de contenedores.

**Ejemplos**:

Listar todas las instancias del grupo de contenedores `my_group`:
```
bluemix ic group-instances my_group
```


## bluemix ic group-create
{: #bluemix_ic_group_create}

Crear un grupo de contenedores escalable.

```
bluemix ic group-create [-p PORT|--publish port][-m MEMORY|--memory MEMORY] [-e ENV|--env ENV][-v VOLUME:CONTAINER_PATH] [--min MIN][--max MAX] [--desired DESIRED][--auto] [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] [--name NAME] IMAGE [CMD]
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandatos**:

-m *MEMORY*|--memory *MEMORY*  (opcional): asignar límite de memoria al grupo en MB. Cuando crea un grupo de contenedores desde la CLI, el valor predeterminado para cada contenedor de instancia es `64` MB. Cuando crea un grupo de contenedores desde el Panel de control de {{site.data.keyword.Bluemix_notm}}, el valor predeterminado para cada instancia es `256` MB. Los valores que se aceptan son `64`, `256`, `512`, `1024` y `2048`. Una vez asignado el límite de memoria, el valor no se puede cambiar.

-e *ENV*|--env *ENV*  (opcional):  establecer la variable de entorno, donde **ENV** es un par `key=value`. Listar varias claves por separado. Si se incluyen comillas, inclúyalas para el nombre para el valor de la variable de entorno. Por ejemplo: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`.  En la tabla siguiente se muestran algunas variables de entorno usadas con frecuencia que puede especificar:

|  Variable de entorno                              |     Descripción                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | Enlazar un servicio con un contenedor. Usar la variable de entorno `CCS_BIND_APP` para enlazar una app con el contenedor. La app se enlaza al servicio de destino y actúa como un puente que permite a {{site.data.keyword.Bluemix_notm}} aportar la información de `VCAP_SERVICES` de la app del puente a la instancia de contenedor en ejecución. Para obtener más información sobre la creación de una app de puente, consulte [Enlazar un servicio a un
contenedor](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}. |
| CCS_SSH_KEY=*&lt;public_ssh_key&gt;* | Añadir una clave SSH a un contenedor al crear el contenedor. Puede añadir la clave SSH utilizando la variable de entorno al crear el contenedor desde el panel de instrumentos de {{site.data.keyword.Bluemix_notm}} o desde la CLI. Para obtener más información sobre claves SSH, consulte [Inicio de sesión en un contenedor](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}. |
| LOG_LOCATIONS=*&lt;vía_al_archivo&gt;* | Añadir un archivo de registro para supervisar en el contenedor. Incluir la variable de entorno de `LOG_LOCATIONS` con una vía de acceso al archivo de registro. |
*Tabla 1. Variables de entorno más utilizadas*

-v VOLUME:CONTAINER_PATH[:ro]|--volume VOLUME:CONTAINER_PATH[:ro]  (optional):  adjuntar un volumen a un contenedor especificando los detalles en formato `VolumeId:ContainerPath[:ro]`.

- *VOLUME*: el ID de volumen o nombre.
- *CONTAINER_PATH*: La vía de acceso absoluta al volumen en el contenedor.
- ro: opcional. Si se especifica `ro`, el volumen será de solo lectura, en lugar de tomar el valor predeterminado (lectura/grabación).

-p *PORT*|--publish *PORT*  (opcional):  ofrecer el puerto para el tráfico HTTP. Los contenedores de su grupo deben atender a su puerto HTTP. No se pueden hacer solicitudes HTTPS. Para grupos de contenedor, no puede incluir varios puertos.

Cuando especifique un puerto, haga que su app esté disponible para el equilibrador de carga de {{site.data.keyword.Bluemix_notm}} o los contenedores que intentan establecer contacto con el host en el mismo espacio de {{site.data.keyword.Bluemix_notm}}. A continuación, los contenedores y el equilibrador de carga de {{site.data.keyword.Bluemix_notm}} pueden utilizar el puerto para alcanzar el host y la app en el mismo espacio de {{site.data.keyword.Bluemix_notm}}. Si especifica un puerto en el archivo de Docker para la imagen que está utilizando, incluya dicho puerto.

**Sugerencia:**

- Para la imagen Liberty Server certificada de IBM o una versión modificada, especifique el puerto 9080.
- Para la imagen Node.js certificada de IBM o una versión modificada de esta imagen, especifique el puerto 8000.

--min *MIN*  (opcional):  el número mínimo de instancias. El valor predeterminado es **1**. Si establece un número mínimo de instancias, el valor no se puede cambiar una vez creado el grupo de contenedor.

--max *MAX*  (opcional):  el número máximo de instancias. El valor predeterminado es **2**. Si establece un número máximo de instancias, el valor no se puede cambiar una vez creado el grupo de contenedor.

--desired *DESIRED*  (opcional):  el número de instancias que necesite. El valor predeterminado es **2**.

--auto  (opcional):  cuando el grupo de contenedores se crea y se habilita la recuperación automática, IBM Containers comprueba el estado de cada instancia con una solicitud HTTP para el puerto que se asigna.

Si no se recibe respuesta desde una instancia de contenedor en 2 intervalos subsecuentes de 90 segundos, la instancia se elimina y se sustituye por una instancia nueva. Si el contenedor no responde, no debe llevarse a cabo ninguna acción. Este proceso se repite continuamente. En un espacio de tiempo de 30 minutos, si el número total de contenedores distintos que son miembros del grupo es igual a (o supera) 3 veces el tamaño máximo observado del grupo, la recuperación automática se inhabilita de forma permanente para el grupo de contenedores. Para habilitar de nuevo la recuperación automática, debe volver a crear el grupo de contenedores.

-n *HOST*|--hostname *HOST*  (opcional):  el nombre de host, como `mycontainerhost`. El host y el dominio se combinan para formar un URL de direccionamiento público completo, como `http://mycontainerhost.mybluemix.net`. Cuando revise los detalles de un grupo de contenedores con el mandato `bluemix ic group-inspect`, el host y el dominio se listan juntos como la ruta.

-d *DOMAIN*|--domain *DOMAIN*  (opcional): por lo general, el dominio es `.mybluemix.net`. El host y el dominio se combinan para formar el URL de direccionamiento público completo, como `http://mycontainerhost.mybluemix.net`. Cuando revise los detalles de un grupo de contenedores con el mandato `bluemix ic group-inspect`, el host y el dominio se listan juntos como la ruta.

--name *NAME*  (obligatorio): asignar un nombre al grupo. `-n` está en desuso.

**Sugerencia:** el nombre de contenedor debe empezar por una letra. El nombre puede incluir mayúsculas, minúsculas, números, puntos `.`, subrayados `_` o guiones `-`.

*IMAGE*  (obligatorio): la imagen a incluir en cada instancia de contenedor en el grupo de contenedores. Puede listar mandatos tras la imagen, pero no opciones. Todas las opciones deben ir antes de especificar una imagen.

Si utiliza una imagen en el repositorio {{site.data.keyword.Bluemix_notm}} privado de la organización, especifique la imagen en el formato: `registry.ng.bluemix.net/NAMESPACE/IMAGE`.

Si usa una imagen proporcionada por IBM Containers, no incluya el espacio de nombres de la organización. Especifique la imagen en el formato:
`registry.ng.bluemix.net/IMAGE`.

*CMD*  (opcional): el mandato y los argumentos se pasan al grupo de contenedor a ejecutar. Este mandato debe ser un mandato de larga ejecución. No utilice un mandato breve que no se ejecute durante mucho tiempo, como por ejemplo **/bin/date**, porque los mandatos de vida breve podrían hacer que el contenedor se bloqueara.

**Nota:**
- El mandato y sus argumentos deben finalizar en la línea de mandatos de `bluemix ic run`.
- Si los argumentos del mandato incluyen un guión `-`, como en `-c` en el mandato de ejemplo anterior, el mandato debe ir precedido por dos guiones. `--`.



**Ejemplos**:

Cree un grupo de contenedores `my_container_group` usando la imagen `registry.ng.bluemix.net/ibmnode` que proporciona IBM Containers y luego use el mandato de larga ejecución `ping localhost` sobre dicho grupo de contenedores:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

Cree un grupo de contenedores `my_container_group` usando la imagen `registry.ng.bluemix.net/ibmnode` que proporciona IBM Containers y luego use el mandato de larga ejecución `tail -f /dev/null` sobre dicho grupo de contenedores:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

Cree un grupo escalable `mygroup` con la recuperación automática habilitada usando la imagen
`registry.ng.bluemix.net/ibmliberty`. El puerto es `9080`, el nombre de host es
`mycontainerhost`, el nombre de dominio es `.mybluemix.net`.
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d .mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty 
```


## bluemix ic group-update
{: #bluemix_ic_group_update}

Actualizar un grupo de contenedores.


```
bluemix ic group-update [--min MIN][--max MAX] [--desired DESIRED][--auto] CONTAINER_GROUP
```

**Sugerencia:** para actualizar el nombre de host o dominio de un grupo de contenedores, utilice
`bluemix ic route-map  [-n HOST][-d DOMAIN] CONTAINER_GROUP`.

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

--min *MIN*  (opcional):  el número mínimo de instancias. El valor predeterminado es
**1**. Tras establecer un número mínimo de instancias, el valor no se puede cambiar.

--max *MAX*  (opcional):  el número máximo de instancias. El valor predeterminado es
**2**. Tras establecer un número máximo de instancias, el valor no se puede cambiar.

--desired *DESIRED*  (opcional):  el número de instancias que necesite. El valor predeterminado es **2**.

**Sugerencia:** solo se puede especificar una opción de las siguientes `--min MIN`, `--max MAX` o `--desired DESIRED` de una vez.

--auto  (opcional): reiniciar automáticamente las instancias erróneas habilitando la recuperación automática.

*CONTAINER_GROUP*  (obligatorio): el nombre o ID del grupo de contenedores.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para actualizar el grupo de contenedores `my_group`:
```
bluemix ic group-update --max 5 my_group
```


## bluemix ic group-remove
{: #bluemix_ic_group_remove}

Eliminar un grupo de contenedores desde el repositorio {{site.data.keyword.Bluemix_notm}} privado de la organización.

```
bluemix ic group-remove [-f|--force] CONTAINER_GROUP
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandatos**:

-f|--force  (opcional): fuerza la eliminación de un contenedor erróneo o en ejecución.

*CONTAINER_GROUP*  (obligatorio): el nombre o ID del grupo de contenedores.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para eliminar un grupo de contenedores, donde `my_group` es el nombre del grupo.
```
bluemix ic group-remove my_group
```


## bluemix ic images
{: #bluemix_ic_images}

Ver una lista de todas las imágenes disponibles en el repositorio {{site.data.keyword.Bluemix_notm}} privado de la organización. Para obtener más información, consulte el mandato [images](https://docs.docker.com/reference/commandline/images){: new_window} en la ayuda de Docker. La lista incluye el ID de imagen, la fecha de creación y el nombre de imagen.

```
bluemix ic images [-a|--all][--no-trunc] [-q|--quiet]
```

**Requisitos previos**:  Endpoint, Login, Target, Docker

**Opciones de mandato**:

-a|--all  (opcional): incluye todas las capas de la imagen por cada imagen del repositorio de la organización,
no solo la más reciente.

--no-trunc  (opcional): no trunca la salida.

-q|--quiet  (opcional): muestra solo los id numéricos.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para recibir una lista de imágenes disponibles para la organización:
```
bluemix ic images
```


## bluemix ic inspect
{: #bluemix_ic_inspect}

Ver la información sobre un contenedor. Para obtener más información, consulte el
mandato [inspect](https://docs.docker.com/reference/commandline/inspect){: new_window} en la ayuda de Docker.

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

**Requisitos previos**:  Endpoint, Login, Target, Docker

**Opciones de mandato**:

*IMAGE*  (obligatorio): ver información detallada sobre una imagen específica indicando el nombre o ID de la imagen.

images  (obligatorio): ver información detallada sobre todas las imágenes del repositorio.

*CONTAINER*  (obligatorio): ver información detallada sobre un contenedor específico, mediante la especificación del
nombre de contenedor o el ID.

**Sugerencia:** solo se permite especificar *IMAGE*, images o *CONTAINER* de una vez. 

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para inspeccionar un contenedor llamado `proxy`: 
```
bluemix ic inspect proxy
```


## bluemix ic info
{: #bluemix_ic_info}

Ver un conjunto de información que describe el estado de la instancia de servicio de nube del contenedor. La información incluye
el límite de contenedores, el uso de los contenedores, los contenedores en ejecución, el límite de memoria, el límite de
dirección IP flotante, el uso de dirección IP flotante, el URL de host CCS, el URL de host de registro y estado de la modalidad de
depuración.

```
bluemix ic info
```

**Requisitos previos**:  Punto final, inicio de sesión, destino


## bluemix ic ips
{: #bluemix_ic_ips}

Mostrar una lista de las direcciones IP flotantes disponibles para el usuario que ha iniciado la sesión. La lista incluye direcciones IP y el ID de contenedor al que están enlazadas las direcciones IP. Si la dirección IP no se utiliza, no se mostrará ID de contenedor.

```
bluemix ic ips [-a|--all]
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandatos**:

-a|--all  (opcional): listar todas las direcciones IP. De forma predeterminada, solo se devuelven las direcciones IP disponibles.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para recibir una lista de todas las direcciones IP para la organización, si están disponibles o no para su uso.
```
bluemix ic ips -a
```


## bluemix ic ip-request
{: #ip_request}
Solicitar un nueva dirección IP flotante.

```
bluemix ic ip-request
```

**Requisitos previos**:  Punto final, inicio de sesión, destino


## bluemix ic ip-release
{: #bluemix_ic_ip_release}

Liberar una dirección IP flotante de la instancia de servicio de nube del contenedor.

```
bluemix ic ip-release IP_ADDRESS
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*IP_ADDRESS*  (obligatorio): la dirección IP a liberar.


## bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

Enlazar una dirección IP flotante disponible a un contenedor.

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*IP_ADDRESS*  (obligatorio): la dirección IP a enlazar.

*CONTAINER*  (obligatorio): el ID de contenedor o nombre a enlazar.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para enlazar la dirección IP `192.123.12.12 to` al contenedor `proxy`:
```
bluemix ic ip-bind 192.123.12.12 proxy
```


## bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

Desenlazar una dirección IP flotante de su contenedor.

Las direcciones IP públicas son un recurso limitado en IBM Containers. Por lo tanto, las direcciones IP públicas con permiso asignadas a un espacio y no enlazadas a un contenedor se reclamen de forma periódica desde usuarios de prueba gratuitos, aproximadamente de forma semanal. Las direcciones IP públicas no enlazadas nunca se reclaman a clientes de suscripción o en fórmulas de pago previo.

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*IP_ADDRESS*  (obligatorio): la dirección IP a desenlazar.

*CONTAINER*  (obligatorio): el ID de contenedor o nombre a desenlazar.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para desenlazar la dirección IP `192.123.12.12` del contenedor `proxy`:
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


## bluemix ic kill
{: #bluemix_ic_kill}

Detener un proceso en ejecución en un contenedor sin detener el contenedor. Para obtener más información, consulte el mandato [kill](https://docs.docker.com/reference/commandline/kill/){: new_window} en la ayuda de Docker.

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

**Requisitos previos**:  Punto final, inicio de sesión, destino, Docker

**Opciones de mandatos**:

-s *CMD*|--signal *CMD*  (opcional):  enviar un mandato al proceso que se está ejecutando en el contenedor.

*CONTAINER*  (obligatorio): el ID de contenedor o el nombre.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para terminar el proceso en un contenedor llamado `proxy`:
```
bluemix ic kill proxy
```


## bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

Ver el nombre del repositorio de imágenes {{site.data.keyword.Bluemix_notm}} privado para la organización en la que inicia sesión.

```
bluemix ic namespace-get
```

**Requisitos previos**:  Punto final, inicio de sesión, destino


## bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

Establecer el nombre del repositorio de imágenes {{site.data.keyword.Bluemix_notm}} privado para la organización en la que inicia sesión.

*Restricción*: no puede utilizar un guión `-` en el nombre del espacio de nombres del repositorio.

```
bluemix ic namespace-set NAME
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*NAME*  (obligatorio): función de una sola vez, para establecer el espacio de nombres del repositorio para su organización, si aún no está establecido. Después de establecer el espacio de nombres, reinicialice IBM Containers con el mandato `bluemix ic init` antes de continuar.


## bluemix ic pause
{: #pause}

Colocar en pausa todos los procesos dentro de un contenedor en ejecución. Para obtener más información, consulte el mandato [pause](https://docs.docker.com/reference/commandline/pause/){: new_window} en la ayuda de Docker. Para detener un contenedor, consulte el mandato [bluemix ic unpause](#unpause).

```
bluemix ic pause CONTAINER
```

**Requisitos previos**:  Endpoint, Login, Target, Docker

**Opciones de mandato**:

*CONTAINER*  (necesario): el nombre de contenedor o ID.

**Respuestas**:

- El contenedor se ha puesto en pausa correctamente.

- El mandato ha fallado con un servicio en la nube de contenedor.

 `{message}`
  
 Donde `{message}` es el error relacionado.
 
- El mandato ha fallado: no se ha podido conectar con el servicio en la nube del contenedor.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para poner en pausa un contenedor llamado `proxy`:
```
bluemix ic pause proxy
```


## bluemix ic unpause
{: #unpause}

Reanudar todos los procesos de un contenedor en ejecución. Para obtener más información, consulte el mandato [unpause](https://docs.docker.com/reference/commandline/unpause/){: new_window} en la ayuda de Docker. Para poner en pausa un contenedor, consulte el mandato [bluemix ic pause](#pause).

```
bluemix ic unpause CONTAINER
```

**Requisitos previos**:  Endpoint, Login, Target, Docker

**Opciones de mandato**:

*CONTAINER*  (necesario): el nombre de contenedor o ID.

**Respuestas**:

- El contenedor se ha reactivado de la pausa correctamente.

- El mandato ha fallado con un servicio en la nube de contenedor. 

 `{message}` 
 
 Donde `{message}` es el error relacionado.
 
- El mandato ha fallado: no se ha podido conectar con el servicio en la nube del contenedor.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para sacar de pausa un contenedor llamado `proxy`:
```
bluemix ic unpause proxy
```


## bluemix ic port
{: #bluemix_ic_port}

Listar correlación de puertos o una correlación específica para el contenedor. Este mandato envuelve el mandato `docker port`. Para obtener más información, consulte el mandato [port](https://docs.docker.com/reference/commandline/port/){: new_window} en la ayuda de Docker.


## bluemix ic ps
{: #bluemix_ic_ps}
Ver una lista de los contenedores que se ejecutan en el espacio de nombres del usuario con la sesión iniciada. De forma predeterminada, este mandato muestra solo los contenedores en ejecución. Para obtener más información, consulte el mandato [ps](https://docs.docker.com/reference/commandline/ps/){: new_window} en la ayuda de Docker.

```
bluemix ic ps [-a|--all][-s|--size] [-l NUM|--limit NUM][-q|--quiet]
```

**Requisitos previos**:  Endpoint, Login, Target, Docker

**Opciones de mandato**:

-a|--all  (opcional): mostrar todos los contenedores, en ejecución o detenidos.

-s|--size  (opcional): mostrar los tamaños de los contenedores.

-l *NUM*|--limit *NUM*  (opcional): listar los contenedores más recientes, donde *NUM* es el número de contenedores recientes que desea devolver.

Por ejemplo, si ha creado los contenedores del `node1` al `node5` de forma secuencial, el mandato `bluemix ic ps --limit 2` devuelve node4 y node5, porque son los dos últimos contenedores que se crean.

-q|--quiet  (opcional): mostrar solo los ID de contenedor.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para ver todos los contenedores en ejecución o detenidos:
```
bluemix ic ps -a
```


## bluemix ic restart
{: #bluemix_ic_restart}

Reiniciar un contenedor. Para obtener más información, consulte el mandato [restart](https://docs.docker.com/reference/commandline/restart/){: new_window} en la ayuda de Docker.

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

**Requisitos previos**:  Punto final, inicio de sesión, destino, Docker

**Opciones de mandatos**:

*CONTAINER*  (obligatorio): el nombre de contenedor o ID.

-t *SECS*|--time *SECS*  (opcional): segundos de espera antes de reiniciar el contenedor.

**Respuestas**:

- El contenedor se ha reiniciado correctamente.

- El mandato ha fallado con un servicio en la nube de contenedor. 

 `{message}` 
 
 Donde `{message}` es el error relacionado.
 
- El mandato ha fallado: no se ha podido conectar con el servicio en la nube del contenedor.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para reiniciar un contenedor llamado `proxy`:
```
bluemix ic restart proxy
```


## bluemix ic rm
{: #bluemix_ic_rm}

Eliminar un contenedor. Para obtener más información, consulte el mandato [rm](https://docs.docker.com/reference/commandline/rm/){: new_window} en la ayuda de Docker.

```
bluemix ic rm [-f|--force] CONTAINER
```

**Requisitos previos**:  Punto final, inicio de sesión, destino, Docker

**Opciones de mandatos**:

-f|--force  (opcional): fuerza la eliminación de un contenedor erróneo o en ejecución.

*CONTAINER*  (necesario): el nombre de contenedor o ID.

**Respuestas**:

- El contenedor se ha eliminado correctamente.

- El mandato ha fallado con un servicio en la nube de contenedor. 

 `{message}` 
 
 Donde `{message}` es el error relacionado.
 
- El mandato ha fallado: no se ha podido conectar con el servicio en la nube del contenedor.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para eliminar un contenedor llamado `proxy`:
```
bluemix ic rm proxy
```


## bluemix ic rmi
{: #bluemix_ic_rmi}

Eliminar una imagen del espacio de nombres del usuario con la sesión iniciada. Para obtener más información, consulte el mandato [rmi](https://docs.docker.com/reference/commandline/rmi/){: new_window} en la ayuda de Docker.

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

**Requisitos previos**:  Punto final, inicio de sesión, destino, Docker

**Opciones de mandatos**:

-R *REGISTRY*|--registry *REGISTRY*  (opcional): cambiar el host de registro. El valor predeterminado es usar el registro que especifique en el mandato `bluemix ic init`.

*IMAGE*  (obligatorio): el nombre de la imagen que quiere eliminar. Si no se especifica una etiqueta en el nombre de la imagen, la imagen etiquetada como `latest` se suprime de forma predeterminada.

**Respuestas**:

- Eliminado: `{IMAGE}`

 Donde `{IMAGE}` es el nombre de la imagen que se ha eliminado.
 
- Error. No se ha especificado host de registro.

- Error de eliminación de imagen: no se ha podido conectar al registro de nube de contenedor

- El mandato ha fallado con un servicio en la nube de contenedor. 

 `{message}`
 
 Donde `{message}` es el error relacionado.

**Ejemplos**:

El siguiente ejemplo muestra una solicitud para eliminar la imagen `mynamespace/myimage:latest`:
```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


## bluemix ic run
{: #bluemix_ic_run}

Iniciar un nuevo contenedor en el servicio de nube del contenedor desde un nombre de imagen. Para obtener más información, consulte el mandato [run](https://docs.docker.com/reference/commandline/run/){: new_window} en la ayuda de Docker.



```
bluemix ic run [-p PORT|--publish PORT][-P] [-m MEMORY|--memory MEMORY][-e ENV|--env ENV] [-v VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS][-it] IMAGE [CMD [CMD ...]]
```
**Nota:** Asegúrese de que la herramienta de mandatos de Cloud Foundry esté instalada y de que tiene una señal de Cloud Foundry. El inicio de sesión correcto usando `bluemix login` y `bluemix ic init` genera la señal y certificados necesarios. 


**Requisitos previos**:  Punto final, inicio de sesión, destino, Docker

**Opciones de mandatos**:

-p *PORT*|--publish *PORT*  (opcional):  ofrecer el puerto para el tráfico HTTP. Incluir los puertos que se especifiquen en el archivo de Docker para la imagen que está utilizando. Puede incluir varios puertos con varias opciones `-p`. Al ofrecer un puerto se enlaza automáticamente una dirección IP al contenedor si hay disponible una dirección IP pública.

Si tiene una dirección IP existente en el espacio que quiere enlazar al contenedor, puede especificar la dirección IP en lugar de enlazarlo más adelante. La dirección IP se debe especificar en el formato: *&lt;dirección-ip&gt;:&lt;puerto-contenedor&gt;:&lt;puerto-contenedor&gt;*

Para obtener más información sobre la solicitud de direcciones IP para un espacio, consulte el mandato [bluemix ic ip-request](#ip_request).

Cuando especifica un puerto, hace que la app esté disponible para el equilibrador de carga de {{site.data.keyword.Bluemix_notm}} o los contenedores que están en el mismo espacio de {{site.data.keyword.Bluemix_notm}} y que intentan acceder al host. Si especifica un puerto en el archivo de Docker para la imagen que está utilizando, incluya dicho puerto.

**Sugerencia:**

- Para la imagen Liberty Server certificada de IBM o una versión modificada, especifique el puerto 9080.
- Para la imagen Node.js certificada de IBM o una versión modificada de esta imagen, especifique el puerto 8000.

-P  (opcional):  Ofrecer automáticamente los puertos especificados en el archivo de Docker de la imagen para el tráfico HTTP.

-m *MEMORY*|--memory *MEMORY*  (opcional):  asignar límite de memoria al grupo en MB. Cuando crea un
grupo de contenedores desde la CLI, el valor predeterminado para cada contenedor de instancia es `64` MB.  Cuando crea un grupo de contenedores desde el Panel de control de {{site.data.keyword.Bluemix_notm}}, el valor predeterminado para cada instancia es `256` MB. Los valores que se aceptan son `64`, `256`, `512`, `1024` y `2048`. Una vez asignado el límite de memoria, el valor no se puede cambiar.

-e *ENV*|--env *ENV*  (opcional):  establecer la variable de entorno, donde **ENV** es un par `key=value`. Listar varias claves por separado. Si se incluyen comillas, inclúyalas para el nombre para el valor de la variable de entorno. Por ejemplo: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`. En la tabla siguiente se muestran algunas variables de entorno usadas con frecuencia que puede especificar:

|      Variable de entorno                          |   Descripción                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | Enlazar un servicio con un contenedor. Usar la variable de entorno `CCS_BIND_APP` para enlazar una app con el contenedor. La app se enlaza al servicio de destino y actúa como un puente que permite a {{site.data.keyword.Bluemix_notm}} aportar la información de `VCAP_SERVICES` de la app del puente a la instancia de contenedor en ejecución. Para obtener más información sobre la creación de una app de puente, consulte [Enlazar un servicio a un
contenedor](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}. |
| CCS_SSH_KEY=*&lt;public_ssh_key&gt;* | Añadir una clave SSH a un contenedor al crear el contenedor. Puede añadir la clave SSH utilizando la variable de entorno al crear un contenedor desde el panel de instrumentos de {{site.data.keyword.Bluemix_notm}} o desde la CLI. Para obtener más información sobre claves SSH, consulte [Inicio de sesión en un contenedor](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}. |
| LOG_LOCATIONS=*&lt;vía_al_archivo&gt;* | Añadir un archivo de registro para supervisar en el contenedor. Incluir la variable de entorno de `LOG_LOCATIONS` con una vía de acceso al archivo de registro. |
*Tabla 2. Variables de entorno utilizadas con frecuencia*

-v VOLUME:CONTAINER_PATH[:ro]|--volume VOLUME:CONTAINER_PATH[:ro](optional):  Attach a volume to a container by specifying the details in the following format `VolumeId:ContainerPath[:ro]`.

- *VOLUME*: el ID de volumen o nombre.
- *CONTAINER_PATH*: La vía de acceso absoluta al volumen en el contenedor.
- ro: opcional. Si se especifica `ro`, el volumen será de solo lectura, en lugar de tomar el valor predeterminado (lectura/grabación).

-n *NAME*|--name *NAME*  (obligatorio): asignar un nombre al contenedor.

*Sugerencia:* el nombre de contenedor debe empezar por una letra. El nombre puede incluir mayúsculas, minúsculas, números, puntos `.`, subrayados `_` o guiones `-`.

--link *NAME*:*ALIAS*  (opcional): siempre que quiera que un contenedor se comunique con otro contenedor que esté en ejecución, puede hacer referencia al mismo por medio de un alias para el nombre de host.

-it  (opcional):  ejecute el contenedor en modalidad interactiva. Una vez creado el contenedor, mantenga la entrada estándar visualizada. Escriba `exit` para salir.

*IMAGE*  (obligatorio): la imagen a incluir en el contenedor. Puede listar mandatos tras la imagen, pero no opciones. Todas las opciones deben ir antes de especificar una imagen.

Si utiliza una imagen en el repositorio {{site.data.keyword.Bluemix_notm}} privado de la organización, especifique la imagen en el formato: *registry.ng.bluemix.net/NAMESPACE/IMAGE*.

Si está utilizando una imagen proporcionada por IBM Containers, especifíquela en el formato: *registry.ng.bluemix.net/IMAGE*.

*CMD*  (opcional): el mandato y los argumentos se pasan al contenedor a ejecutar. Este mandato debe ser un mandato de larga ejecución. No utilice un mandato breve que no se ejecute durante mucho tiempo, como por ejemplo `/bin/date`, porque los mandatos de vida breve podrían hacer que el contenedor se bloqueara.



**Ejemplos**:

Ejecute el mandato de larga duración `sh -c "while true; do date; sleep 20; done"` en el contenedor `my_container` que se construye en la imagen `registry.ng.bluemix.net/ibmnode`. 
```
bluemix ic run --name my_container registry.ng.bluemix.net/ibmnode -- sh -c "while true; do date; sleep 20; done"
```


Crear y luego iniciar un contenedor `proxy` con el límite de memoria `1024` MB usando la imagen `my_namespace/nginx`, en la que `my_namespace` es el espacio de nombres asociado a los usuarios con sesión iniciada.
```
bluemix ic run -n proxy -m 1024 registry.ng.bluemix.net/my_namespace/nginx
```

Crear y luego reiniciar un contenedor usando la imagen `my_namespace/blog`; pasar las credenciales como variables de entorno. `my_namespace` es el espacio de nombres asociado a los usuarios con sesión iniciada.
```
bluemix ic run -n my_container -e USER=johnsmith -e PASS=password registry.ng.bluemix.net/my_namespace/blog
```

Añadir un volumen a un contenedor usando la imagen `my_namespace/blog`, donde
`my_namespace` es el espacio de nombres asociado a los usuarios con sesión iniciada.
```
bluemix ic run -n my_container -v VolId1:/first/path -v VolId2:/second/path registry.ng.bluemix.net/my_namespace/blog
```


## bluemix ic route-map
{: #bluemix_ic_route_map}

Establecer la ruta que utiliza el tráfico de Internet para acceder al grupo de contenedores. Puede utilizar este mandato para establecer una nueva ruta o actualizar una ruta existente.

```
bluemix ic route-map [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandatos**:

-n *HOST*|--hostname *HOST*  (opcional): el nombre de host para la ruta. El nombre de host es la primera parte del URL de ruta pública completa, como `mycontainerhost` en el URL `mycontainerhost.mybluemix.net`.

-d *DOMAIN*|--domain *DOMAIN*  (opcional):  el nombre de dominio para la ruta, que es la segunda parte del URL de ruta pública completa. En la mayoría de los casos, el dominio es `mybluemix.net`. También puede utilizar este parámetro para especificar un dominio privado.

*CONTAINER_GROUP*  (obligatorio): el ID o nombre del grupo de contenedores.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para correlacionar la ruta para el grupo denominado `GROUP1`, donde `my_host` es el nombre de host, `organization.com` es el dominio.
```
bluemix ic route-map -n my_host -d organization.com GROUP1
```


## bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

Establecer la ruta que utiliza el tráfico de Internet para acceder al grupo de contenedores. Puede utilizar este mandato para establecer una nueva ruta o actualizar una ruta existente.

```
bluemix ic route-unmap [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandatos**:

-n *HOST*|--hostname *HOST*  (opcional): el nombre de host para la ruta.

-d *DOMAIN*|--domain *DOMAIN*  (opcional):  el nombre de dominio para la ruta.

*CONTAINER_GROUP*  (obligatorio): el ID o nombre del grupo de contenedores.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para cancelar la correlación de la ruta para el grupo denominado `GROUP1`, donde `my_host` es el
nombre de host, `organization.com` es el dominio.
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


## bluemix ic start
{: #ic_start}
Iniciar un contenedor detenido. Para obtener más información, consulte el mandato [start](https://docs.docker.com/reference/commandline/start/){: new_window} en la ayuda de Docker. Para detener un contenedor, consulte el mandato [bluemix ic stop](#ic_stop).

```
bluemix ic start CONTAINER
```

**Requisitos previos**:  Endpoint, Login, Target, Docker

**Opciones de mandato**:

*CONTAINER*  (necesario): el nombre de contenedor o ID.

**Respuestas**:

- El contenedor se ha iniciado correctamente.

- El mandato ha fallado con un servicio en la nube de contenedor.

 `{message}`
  
 Donde `{message}` es el error relacionado.
 
- El mandato ha fallado: no se ha podido conectar con el servicio en la nube del contenedor.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para iniciar un contenedor llamado `proxy`.
```
bluemix ic start proxy
```


## bluemix ic stop  
{: #ic_stop}
Detener un contenedor en ejecución. Para obtener más información, consulte el mandato [stop](https://docs.docker.com/reference/commandline/stop/){: new_window} en la ayuda de Docker. Para iniciar un contenedor, consulte el mandato [bluemix ic start](#ic_start).

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

**Requisitos previos**:  Punto final, inicio de sesión, destino, Docker

**Opciones de mandatos**:

*CONTAINER*  (obligatorio): el nombre de contenedor o ID.

-t *SECS*|--time *SECS*  (opcional): segundos de espera antes de interrumpir el contenedor.

**Respuestas**:

- El contenedor se ha detenido correctamente.

- El mandato ha fallado con un servicio en la nube de contenedor.

 `{message}`
  
 Donde `{message}` es el error relacionado.
 
- El mandato ha fallado: no se ha podido conectar con el servicio en la nube del contenedor.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para detener un contenedor llamado `proxy`.
```
bluemix ic stop proxy
```


## bluemix ic stats
{: #bluemix_ic_stats}

Para uno o varios contenedores, vea las estadísticas de uso activo. Utilice `CTRL+C` para salir. Para obtener más información, consulte el mandato [stats](https://docs.docker.com/reference/commandline/stats/){: new_window} en la ayuda de Docker.

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

**Requisitos previos**:  Endpoint, Login, Target, Docker

**Opciones de mandato**:

*CONTAINER*  (necesario): el nombre de contenedor o ID.

--no-stream  (opcional): mostrar solo el resultado más reciente y no incluir información anterior.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para las estadísticas más recientes sobre un contenedor:
```
bluemix ic stats --no-stream my_container
```


## bluemix ic top
{: #bluemix_ic_top}

Mostrar los procesos que están en ejecución en el contenedor. Para obtener más información, consulte el mandato [top](https://docs.docker.com/reference/commandline/top/){: new_window} en la ayuda de Docker.

```
bluemix ic top CONTAINER [CONTAINER]
```

**Requisitos previos**:  Endpoint, Login, Target, Docker

**Opciones de mandato**:

*CONTAINER*  (necesario): el nombre de contenedor o ID.

**Ejemplos**:

El ejemplo siguiente es una solicitud para mostrar los procesos del contenedor `my_container`.
```
bluemix ic top my_container
```


## bluemix ic volumes
{: #bluemix_ic_volumes}

Listar los volúmenes.

```
bluemix ic volumes
```

**Requisitos previos**:  Punto final, inicio de sesión, destino


## bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

Inspeccionar un volumen.

```
bluemix ic volume-inspect VOLUME_NAME
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*VOLUME_NAME*  (obligatorio): el nombre del volumen.

**Ejemplos**:

El ejemplo siguiente es una solicitud para inspeccionar un volumen, donde `volume_name` es el nombre del volumen.
```
bluemix ic volume-inspect volume_name
```


## bluemix ic volume-create
{: #bluemix_ic_volume_create}

Crea un volumen.

```
bluemix ic volume-create VOLUME_NAME
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*VOLUME_NAME*  (obligatorio): el nombre del volumen. El nombre puede contener letras en minúsculas, números, subrayados
`_` y guiones `-`.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para crear un volumen.
```
bluemix ic volume-create volume_name 
```


## bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

Eliminar un volumen.

```
bluemix ic volume-remove VOLUME_NAME
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*VOLUME_NAME*  (obligatorio): el nombre del volumen.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para eliminar un volumen, donde `volume_name` es el nombre del volumen.
```
bluemix ic volume-remove volume_name
```

## bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

Listar sistemas de archivos.

```
bluemix ic volume-fs
```

## bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

Crear un nuevo sistema de archivos.

```
bluemix ic volume-fs-create FILE_SYSTEM_NAME
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*FILE_SYSTEM_NAME*  (obligatorio):  El nombre del sistema de archivos. El nombre puede contener letras en minúsculas, números, subrayados
`_` y guiones `-`.

**Ejemplos**:

El siguiente ejemplo muestra una solicitud para crear un sistema de archivos:
```
bluemix ic volume-fs-create my_file_system 
```

## bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

Eliminar un sistema de archivos.

```
bluemix ic volume-fs-remove FILE_SYSTEM_NAME
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*FILE_SYSTEM_NAME*  (obligatorio):  El nombre del sistema de archivos. 

**Ejemplos**:

El siguiente ejemplo muestra una solicitud para eliminar un sistema de archivos, donde `my_file_system` es el nombre del sistema de archivos.
```
bluemix ic volume-fs-remove my_file_system
```

## bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

Inspeccionar un sistema de archivos.

```
bluemix ic volume-fs-inspect FILE_SYSTEM_NAME
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*FILE_SYSTEM_NAME*  (obligatorio):  El nombre del sistema de archivos. 

**Ejemplos**:

El siguiente ejemplo es una solicitud para inspeccionar un sistema de archivos, donde `my_file_system` es el nombre del volumen.
```
bluemix ic volume-fs-inspect my_file_system
```
## bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

Listar todos los tipos de sistemas de archivos.

```
bluemix ic volume-fs-flavors
```

**Requisitos previos**:  Punto final, inicio de sesión, destino

## bluemix ic wait
{: #bluemix_ic_wait}

Salir de un contenedor y visualizar el código de salida como confirmación. Para obtener más información, consulte el
mandato [wait](https://docs.docker.com/reference/commandline/wait/){: new_window} en la ayuda de Docker.

```
bluemix ic wait CONTAINER [CONTAINER]
```

**Requisitos previos**:  Endpoint, Login, Target, Docker

**Opciones de mandato**:

*CONTAINER*  (necesario): el nombre de contenedor o ID.

**Ejemplos**:

El ejemplo siguiente muestra una solicitud para salir del contenedor `my_container`:
```
bluemix ic wait my_container
```


## bluemix ic version
{: #bluemix_ic_version}

Muestra la versión de Docker. 

```
bluemix ic version
```

**Requisitos previos**: Docker

Para ver la versión de IBM Containers, ejecute `bluemix ic info`. Para obtener más información, consulte el mandato [version](https://docs.docker.com/reference/commandline/version/){: new_window} en la ayuda de Docker.
