{:shortdesc: .shortdesc}

# Mandatos bx para interactuar con {{site.data.keyword.Bluemix_notm}}
{: #bluemix_cli}

*Última actualización:* 19 de octubre de 2015

La interfaz de línea de mandatos (CLI) de {{site.data.keyword.Bluemix}} proporciona un conjunto de mandatos que se agrupan por espacio de nombres para que los usuarios interactúen con {{site.data.keyword.Bluemix_notm}}. Algunos mandatos de CLI de {{site.data.keyword.Bluemix_notm}}, a los que se llama mandatos bx, son envolturas de mandatos cf existentes, y otros son exclusivos de {{site.data.keyword.Bluemix_notm}}. La información que se indica a continuación lista todos los mandatos soportados por {{site.data.keyword.Bluemix_notm}} CLI e incluye sus nombres, opciones, uso, requisitos previos, descripciones y ejemplos.
{:shortdesc}
 
**Nota:** *Requisitos previos* lista las acciones que son necesarias antes de utilizar el mandato. Los mandatos que no tienen acciones de requisito previo listan **Ninguno**. De lo contrario, los requisitos previos pueden incluir una o varias de las acciones siguientes:
<dl>
<dt>**Punto final**</dt>
<dd>Un punto final de API se debe establecer por medio de la `bluemix api` antes de utilizar el mandato.</dd>
<dt>**Login**</dt>
<dd>El inicio de sesión que utiliza el mandato `bluemix login` es necesario antes de utilizar este mandato.</dd>
<dt>**Target**</dt>
<dd>El mandato `bluemix target` debe utilizarse para establecer un punto de extensión org y un espacio antes de utilizar este mandato.</dd>
</dl>

## ayuda de bluemix
Muestra la ayuda general para mandatos incorporados de primer nivel y nombres de espacios soportados de {{site.data.keyword.Bluemix_notm}} CLI, o la ayuda para un mandato o un nombre de espacio incorporado específico.

```
ayuda de bluemix [COMMAND|NAMESPACE]
```

**Prerrequisitos**: Ninguno

**Opciones de mandatos**:

*COMMAND*|*NAMESPACE*  (opcional): El mandato o el espacio de nombres para el que se muestra la ayuda. Si no se especifica, se mostrará la ayuda general para {{site.data.keyword.Bluemix_notm}} CLI.

**Ejemplos**:

Visualiza ayuda general para {{site.data.keyword.Bluemix_notm}} CLI:

```
ayuda de bluemix
```

Muestra ayuda para el espacio de nombres `catálogo`:

```
catálogo de ayuda de bluemix
```

```
ayuda de catálogo de bluemix
```

Muestra ayuda para el mandato `info`:

```
información de ayuda de bluemix
```

Muestra ayuda para el mandato `plantillas` en el espacio de nombres `catálogo`:

```
plantillas de ayuda de catálogo de bluemix
```


## api de bluemix
Establezca o visualice el punto final de su API de {{site.data.keyword.Bluemix_notm}}. Este mandato acomoda el mandato `cf api`.

```
api de bluemix [API_ENDPOINT][--unset]
```

**Prerrequisitos**:  Ninguno

**Opciones de mandato**:

*API_ENDPOINT*  (opcional): El punto final de la API que está destinado, como por ejemplo https://api.ng.bluemix.net. Si no se especifican ambas opciones *API_ENDPOINT* y `--unset`, se mostrará el punto final de API actual.

`--unset`  (opcional):  Eliminar el valor de punto final de la API.

**Ejemplos**:

Establezca el punto final de la API a api.ng.bluemix.net:

```
bluemix api api.ng.bluemix.net
```

Visualice el punto final de la API actual:

```
api de bluemix```

Desestablecer el punto final de la API:

```
bluemix api --unset
```


## inicio de sesión de bluemix
Inicio de sesión de usuario. Este mandato acomoda el mandato `cf login`. Las opciones del mandato son las mismas que las opciones del mandato de `cf login`.

```
bluemix login [OPTIONS...]
```

**Prerrequisitos**:  Punto final

**Opciones de mandato**:
Para obtener información sobre las opciones soportadas por el mandato `login`, consulte la información de uso del mandato `cf login` para que los mandatos cf gestionen aplicaciones.


## cierre de sesión de bluemix
Cerrar sesión de usuario. Este mandato acomoda el mandato `cf logout`.

```
cierre de sesión de bluemix
```

**Prerrequisitos**:  Ninguno


## destino de bluemix
Establezca o visualice el espacio o la organización de destino. Este mandato acomoda el mandato `cf target`.

```
destino bluemix [-o ORG_NAME] [-s SPACE_NAME]
```

**Prerrequisitos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

-o *ORG_NAME*  (opcional):  El nombre de la organización a la que va dirigida.

-s *SPACE_NAME*  (opcional):  El nombre del espacio al que va dirigido. 

Si no se especifica -o *ORG_NAME* ni -s *SPACE_NAME*, se mostrará el espacio y la organización actuales.

**Ejemplos**:

Establezca la organización actual para 'MyOrg' y el espacio para 'MySpace':

```
destino bluemix -o MyOrg -s MySpace
```

Visualice el espacio y la organización actuales:

```
destino de bluemix
```


## información de bluemix
Vea la información básica de {{site.data.keyword.Bluemix_notm}}, incluida la región actual, la versión del controlador de nube y algunos puntos finales útiles, como por ejemplo los puntos finales para el inicio de sesión y el intercambio de señales de acceso.

```
información de bluemix
```

**Prerrequisitos**:  Punto final


## lista de bluemix
Lista todas las aplicaciones cf, los contenedores, los grupos de contenedor y los grupos de máquinas virtuales en el espacio actual.

```
lista de bluemix [apps|contenedores|container-groups|vm-groups]
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandatos**:

apps  (opcional):  Visualizar sólo la información de las aplicaciones.

containers  (opcional):  Visualizar sólo la información de los contenedores.

container-groups  (opcional):  Visualizar sólo la información de grupos del contenedor.

vm-groups  (opcional):  Visualizar sólo la información de los grupos de máquinas virtuales.

Sólo puede especificarse una de los `apps`, `containers`, `container-groups` o `vm-groups` a la vez. Si no se especifica ninguna de ellas, se listarán todas las apps de cf, los contenedores, los grupos de contenedores y los grupos de máquinas virtuales.

**Ejemplos**:

Listar todas las aplicaciones de cf:

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
Escala verticalmente u horizontalmente la aplicación cf o el grupo de contenedores a un recuento de instancias, cuota de disco y tamaño de memoria específicos. 

**Nota:** Solo puede especificarse un número de instancias para escalar un grupo de contenedor. Si no se especifica ninguna opción, este mandato lista la instancia actual para el grupo de contenedores, y también la cuota de disco y el tamaño de memoria para la aplicación cf.

```
escala bluemix CF_APP_NAME|NOMBRE_GRUPO_CONTENEDOR [-i RECUENTO_INSTANCIA] [-k CUOTA_DISCO] [-m TAMAÑO_MEMORIA]
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*  (necesario):  El nombre de la aplicación o del grupo de contenedores de cf que se va a escalar.

-i *INSTANCE_COUNT*  (opcional):  El nuevo número de instancia de la aplicación o del grupo de contenedores cf que se va a escalar. Esta opción es la única opción válida para grupos de contenedores que se van a escalar.

-k *DISK_QUOTA*  (opcional):  La nueva cuota de disco de la aplicación cf. No es válida para escalar un grupo de contenedores.

-m *MEMORY_SIZE*  (opcional):  El nuevo tamaño de memoria para la aplicación cf. No es válido para escalar un grupo de contenedores.

**Ejemplos**:

Muestra el número de instancias actual para 'mi-grupo-contenedor':

```
escala bluemix mi-grupo-contenedor
```

Escala 'mi-grupo-contenedor' a 2 instancias:

```
escala bluemix mi-grupo-contenedor -i 2
```

Escala 'my-java-app' a 3 instancias, cuota de disco de 8G, y tamaño de memoria de 1024M:

```
escala bluemix mi-app-java -i 3 -k 8G -m 1024M
```


## curl bluemix
Ejecuta una solicitud HTTP sin procesar a {{site.data.keyword.Bluemix_notm}}. "Content-Type" se establece como "application/json" de forma predeterminada. Este mandato envía una solicitud al servidor de la consola {{site.data.keyword.Bluemix_notm}} (por ejemplo, https://console.ng.bluemix.net) en lugar del punto final API cf (por ejemplo, https://api.ng.bluemix.net).

```
RUTA bluemix curl [OPCIONES...]
```

**Prerrequisitos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

*PATH*  (obligatorio):  vía de acceso de la URL del recurso. Por ejemplo, /rest/v2/apps.

*OPTIONS*  (opcional):  las opciones a las que da soporte el mandato `bluemix curl` son las mismas que las del mandato `cf curl`.

**Ejemplos**:

Recupera la información para todas las plantillas de contenedor modelo:

```
bluemix curl /rest/templates
```


## bluemix iam orgs
Este mandato tiene la misma función y las mismas opciones que el mandato `cf orgs`.


## bluemix iam org
Este mandato tiene la misma función y las mismas opciones que el mandato `cf org`.


## bluemix iam org-create
Este mandato tiene la misma función y las mismas opciones que el mandato `cf create-org`.


## bluemix iam org-rename
Este mandato tiene la misma función y las mismas opciones que el mandato `cf rename-org`.


## bluemix iam org-delete
Este mandato tiene la misma función y las mismas opciones que el mandato `cf delete-org`.


## bluemix iam spaces
Este mandato tiene la misma función y las mismas opciones que el mandato `cf spaces`.


## bluemix iam space
Este mandato tiene la misma función y las mismas opciones que el mandato `cf space`.


## bluemix iam space-create
Este mandato tiene la misma función y las mismas opciones que el mandato que el mandato `cf create-space`.


## bluemix iam space-rename
Este mandato tiene la misma función y las mismas opciones que el mandato que el mandato `cf rename-space`.


## bluemix iam space-delete
Este mandato tiene la misma función y las mismas opciones que el mandato `cf delete-space`.


## bluemix iam user-create
Este mandato tiene la misma función y las mismas opciones que el mandato `cf create-user`.


## bluemix iam user-delete
Este mandato tiene la misma función y las mismas opciones que el mandato `cf delete-user`.


## bluemix iam org-users
Este mandato tiene la misma función y las mismas opciones que el mandato `cf org-users`.


## bluemix iam org-role-set
Este mandato tiene la misma función y las mismas opciones que el mandato `cf set-org-role`.


## bluemix iam org-role-unset
Este mandato tiene la misma función y las mismas opciones que el mandato `cf unset-org-role`.


## bluemix iam space-users
Este mandato tiene la misma función y las mismas opciones que el mandato `cf space-users`.


## bluemix iam space-role-set
Este mandato tiene la misma función y las mismas opciones que el mandato `cf set-space-role`.


## bluemix iam space-role-unset
Este mandato tiene la misma función y las mismas opciones que el mandato `cf unset-space-role`.


## bluemix catalog templates
Visualizar las plantillas de contenedor modelo en Bluemix.

```
plantillas de catálogo de bluemix [-d]
```

**Prerrequisitos**:  Punto final, Inicio de sesión

**Opciones de mandato**:

-d  (opcional):  Si se especifica la opción '-d', también se mostrará la descripción de cada plantilla. De lo contrario, sólo se mostrará el ID y el nombre de cada plantilla.


## bluemix catalog template-run
Crea una aplicación cf que se base en la plantilla específica con la URL y la descripción especificadas. De forma predeterminada, la nueva app se iniciará automáticamente.

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*TEMPLATE_ID*  (necesario):  La plantilla en la que se basará la aplicación cuando se cree. Utilice 'plantillas bluemix' para ver todas las ID de plantillas.

*CF_APP_NAME*  (obligatorio):  el nombre de la aplicación cf que se creará.

-u *URL*  (opcional):  La ruta de la aplicación. Si no se especifica, la ruta se establece mediante {{site.data.keyword.Bluemix_notm}} que se basa automáticamente en el nombre de la app y en el dominio predeterminado.

-d *DESCRIPTION*  (opcional):  descripción de la aplicación.

--no-start  (opcional):  no inicie la aplicación automáticamente después de crearla. Si no se especifica, la aplicación se iniciará automáticamente una vez que se haya creado.

**Ejemplos**:

Crea una aplicación cf 'my-app' basada en la plantilla 'javaHelloWorld':

```
bluemix catalog template-run javaHelloWorld my-app
```

Crea una aplicación 'my-ruby-app' basada en la plantilla 'rubyHelloWorld' con la ruta 'myrubyapp.ng.bluemix.net' y la descripción 'Mi primera aplicación ruby en {{site.data.keyword.Bluemix_notm}}'.:

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "Mi primera aplicación ruby en {{site.data.keyword.Bluemix_notm}}".
```

Crea una aplicación 'my-python-app' basada en la plantilla 'pythonHelloWorld' sin inicio automático:

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


## regiones de red bluemix
Visualiza la información para todas las regiones en {{site.data.keyword.Bluemix_notm}}.

```
regiones de red bluemix
```

**Prerrequisitos**:  Punto final


## bluemix network region-set
Se dirige a la región que se ha especificado. Este mandato vuelve a dirigirse automáticamente a la misma organización y espacio en la nueva región, si es posible, o le solicita que seleccione una nueva organización y un nuevo espacio si el usuario ya ha iniciado sesión. El punto final de API cambia en consecuencia.

```
bluemix network region-set REGION_NAME
```

**Prerrequisitos**:  Punto final

**Opciones de mandato**:

*REGION_NAME*  (obligatorio):  el nombre de la región a la que desea cambiar. Puede utilizar el mandato `bluemix regions` para visualizar todos los nombres de región.

**Ejemplos**:

Establezca la región actual en 'eu-gb':

```
bluemix network region-set eu-gb
```


## bluemix network routes
Este mandato tiene la misma función y opciones que el mandato `cf routes`.


## bluemix network route-check
Este mandato tiene la misma función y opciones que el mandato `cf check-route`.


## bluemix network route-map
Correlacione una ruta a una aplicación cf o grupo de contenedores que tenga un dominio y nombre de host específicos.

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandatos**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*  (obligatorio):  El nombre de la aplicación o grupo de contenedores cf que se va a correlacionar con una ruta.

*DOMAIN*  (obligatorio):  El dominio de la ruta. Por ejemplo, mybluemix.net o ng.bluemix.net. 

-n *HOST_NAME*  (opcional):  El nombre de host de la ruta. Si no se facilita, el nombre de host se establece en el nombre de la aplicación o grupo de contenedores de forma predeterminada.

**Ejemplos**:

Correlacione una ruta a 'my-app' con un dominio específico:

```
bluemix network route-map my-app mybluemix.net
```

Correlacione una ruta a 'my-container-group' con el dominio y el nombre de host especificados:

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
Elimina la correlación entre la ruta específica y una aplicación cf existente o grupo de contenedores.

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandatos**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*  (obligatorio):  el nombre de la aplicación cf o grupo de contenedores.

*DOMAIN*  (obligatorio):  el dominio de la ruta (por ejemplo, mybluemix.net o ng.bluemix.net). 

-n *HOST_NAME*  (opcional):  El nombre de host de la ruta. Si no se proporciona, el nombre de host se establece en el nombre de la aplicación o en el nombre de grupo de contenedores de forma predeterminada.

**Ejemplos**:

Elimina la correlación entre 'my-app.mybluemix.net' y 'my-app':

```
bluemix network route-unmap my-app mybluemix.net
```

Elimina la correlación entre 'abc.ng.bluexmix.net' y 'my-container-group':

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
Este mandato tiene la misma función y las mismas opciones que el mandato `cf create-route`.


## bluemix network route-delete
Este mandato tiene la misma función y opciones que el mandato `cf delete-route`.


## bluemix network orphaned-routes-delete
Este mandato tiene la misma función y opciones que el mandato `cf delete-orphaned-routes`.


## bluemix network domains
Este mandato tiene la misma función y las mismas opciones que el mandato `cf domains`.


## bluemix network domain-create
Este mandato tiene la misma función y las mismas opciones que el mandato `cf create-domain`.


## bluemix network domain-delete
Este mandato tiene la misma función y las mismas opciones que el mandato `cf delete-domain`.


## bluemix network shared-domain-create
Este mandato tiene la misma función y las mismas opciones que el mandato `cf create-shared-domain`.


## bluemix network shared-domain-delete
Este mandato tiene la misma función y las mismas opciones que el mandato `cf delete-shared-domain`.


## bluemix plugin repos
Cree una lista de todos los repositorios de plugin que se registran en {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin repos
```

**Prerrequisitos**:  Ninguno


## bluemix plugin repo-add
Agrega un nuevo repositorio de plugin a {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

**Prerrequisitos**:  Ninguno

**Opciones de mandato**:

*REPO_NAME*  (obligatorio):  el nombre del repositorio que se añadirá. Puede volver a definir su propio nombre para cada repositorio.

*REPO_URL*  (obligatorio):  el URL del repositorio que se añadirá. El URL de repositorio debe contener el protocolo (por ejemplo, http://plugins.ng.bluemix.net en lugar de plugins.ng.bluemix.net). http://plugins.ng.bluemix.net es el repositorio de plugins oficial de {{site.data.keyword.Bluemix_notm}} CLI.

**Ejemplos**:

Añada el repositorio de plugins oficial de Bluemix CLI como 'bluemix-repo':

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
Elimina el repositorio de plugins de {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin repo-remove REPO_NAME
```

**Prerrequisitos**:  Ninguno

**Opciones de mandato**:

*REPO_NAME*  (obligatorio):  el nombre del repositorio que se eliminará.

**Ejemplos**:

Elimina el repositorio 'bluemix-repo' de {{site.data.keyword.Bluemix_notm}} CLI:

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugin-list
Crea una lista de todos los plugins disponibles en todos los repositorios o repositorios específicos.

```
bluemix plugin repo-plugin-list [-r REPO_NAME]
```

**Prerrequisitos**:  Ninguno

**Opciones de mandato**:

-r *REPO_NAME*  (opcional):  crea una lista de sólo los plugins del repositorio especificado.

**Ejemplos**:

Crea una lista de todos los plugins en todos los repositorios añadidos:

```
bluemix plugin repo-plugin-list
```

Crea una lista de todos los plugins del repositorio 'bluemix-repo':

```
bluemix plugin repo-plugin-list -r bluemix-repo
```


## bluemix plugin list
Crea una lista de todos los plugins instalados en {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin list
```

**Prerrequisitos**:  Ninguno


## bluemix plugin install
Instala el plugin a {{site.data.keyword.Bluemix_notm}} CLI desde la vía de acceso o el repositorio especificados.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME]
```

**Prerrequisitos**: Ninguno

**Opciones de mandatos**:

*PLUGIN_PATH*|*PLUGIN_NAME*  (obligatorio):  Si '-r *REPO_NAME*' no está especificado, el plugin se instala desde la vía de acceso local o la URL remota especificadas.

-r *REPO_NAME*  (opcional):  El nombre del repositorio donde se encuentra el binario del plugin.

**Ejemplos**:

Instala un plugin desde el archivo local:

```
bluemix plugin install /downloads/new_plugin
```

Instala un plugin desde la URL remota:

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

Instala el plugin 'IBM-Containers' desde el repositorio 'bluemix-repo':

```
bluemix plugin install IBM-Containers -r bluemix-repo
```


## bluemix plugin uninstall
Desinstala el plugin especificado desde {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin uninstall PLUGIN_NAME
```

**Prerrequisitos**:  Ninguno

**Opciones de mandato**:

*PLUGIN_NAME*  (obligatorio):  El nombre del plugin que se desinstalará.

**Ejemplos**:

Desinstala el plugin 'IBM-Containers' que se ha instalado previamente:

```
bluemix plugin uninstall IBM-Containers
```
