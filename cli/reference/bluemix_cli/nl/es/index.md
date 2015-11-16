{:shortdesc: .shortdesc}

# mandatos bluemix
{: #bluemix_cli}

*Última actualización:* 19 de octubre de 2015

La Interfaz de línea de mandatos de Bluemix (CLI) proporciona
un conjunto de mandatos que se agrupan por espacio de nombres para
que los usuarios interactúen con Bluemix. Algunos mandatos de Bluemix
CLI son derivadores de mandatos existentes y otros son exclusivos
para Bluemix. La información que sigue nombra todos los mandatos
compatibles con Bluemix CLI e incluye sus nombres, opciones, uso,
requisitos previos, descripciones y ejemplos.
{:shortdesc}
 
**Nota:** Los *requisitos
previos* ofrecen una lista de las acciones que son necesarias
antes de utilizar un mandato. Los mandatos que no requieren acciones
previas aparecen en la lista como **Ninguno**. En
caso contrario, los requisitos previos pueden incluir una o varias de
estas acciones:
<dl>
<dt>**Punto final**</dt>
<dd>Antes de utilizar este mandato debe establecerse un punto final
API a través de `bluemix
api`.</dd>
<dt>**Inicio de sesión**</dt>
<dd>Es necesario iniciar sesión utilizando el mandato de
`bluemix login` antes de utilizar este mandato.</dd>
<dt>**Destino**</dt>
<dd>El mandato `bluemix target` debe utilizarse para
definir la organización y el espacio antes de utilizar este mandato.</dd>
</dl>

## ayuda bluemix 
Muestra la ayuda general para mandatos incorporados de primer
nivel y espacios de nombres soportados de Bluemix CLI, o la ayuda
para un espacio de nombres o mandato incorporado específico.

```
ayuda bluemix [COMMAND|NAMESPACE]
```

**Requisitos previos**:  Ninguno 

**Opciones de mandatos**:

*COMMAND*|*NAMESPACE* 
(opcional):  mandato o nombre del espacio para el que se muestra la
ayuda. Si no se especifica lo contrario, se muestra la ayuda general
de Bluemix CLI.

**Ejemplos**:

Muestra la ayuda general para Bluemix CLI:

```
ayuda bluemix ```

Muestra la ayuda para el espacio de nombres
`catalog`:

```
catálogo de ayuda bluemix
```

```
catálogo de ayuda bluemix
```

Muestra la ayuda para el mandato `info`:

```
blue1mix help info
```

Muestra la ayuda para el mandato `templates`
bajo
el espacio de nombres `catalog`:

```
plantillas del catálogo de ayuda de bluemix
```


## bluemix api
Establecer o visualizar el punto final de Bluemix. Este mandato
recalcula el mandato `cf api`.

```
bluemix api [API_ENDPOINT][--unset]
```

**Requisitos previos**:  Ninguno

**Opciones de mandato**:

*API_ENDPOINT*  (optional):  el punto final de API
al que está dirigido, por ejemplo, https://api.ng.bluemix.net. Si
ambas opciones *API_ENDPOINT* y
`–unset` no están especificadas, se muestra el punto
final API actual.

`--unset`  (optional):  elimine la
configuración del punto final de API.

**Ejemplos**:

Establece el punto final de API en api.ng.bluemix.net:

```
bluemix api api.ng.bluemix.net
```

Visualizar el punto final API actual:

```
bluemix api
```

Desactiva el punto final de API:

```
bluemix api --unset
```


## inicio de sesión de bluemix
Inicio de sesión de usuario. Este mandato recalcula el mandato
`cf login`. Las opciones de mandato son iguales a
las opciones del mandato `cf login`.

```
inicio de sesión de bluemix [OPCIONES...]
```

**Requisitos previos**: Punto final

**Opciones de mandato**:
Para obtener información acerca de las opciones que soporta el
mandato
`login`, consulte la información de uso del mandato
`cf login`
de mandatos cf para gestionar aplicaciones.


## bluemix logout
Cerrar sesión de usuario. Este mandato recalcula el mandato
`cf logout`.

```
bluemix logout
```

**Requisitos previos**:  Ninguno


## bluemix target
Establecer o visualizar la organización o el espacio del punto. Este
mandato recalcula el mandato `cf target`.

```
destino bluemix [-o NOMBRE_ORG] [-s NOMBRE_ESPACIO]
```

**Requisitos previos**:  Punto final,
inicio de sesión

**Opciones de mandato**:

-o *NOMBRE_ORG*  (opcional):  nombre de la
organización a la que se dirige.

-s *NOMBRE_ESPACIO*  (optional): nombre del
espacio al que se dirige. 

Si no se especifica nada en -o *NOMBRE_ORG* o
-s
*NOMBRE_ESPACIO*, se muestran la organización y el
espacio actuales.

**Ejemplos**:

Establece la organización actual a
'MyOrg' y espacio a
'MySpace':

```
destino bluemix -o MyOrg -s MySpace
```

Visualiza la organización y el espacio actuales:

```
destino bluemix```


## información bluemix
Visualiza la información básica de Bluemix, incluyendo la
región actual, la versión del controlador de nube, y algunos puntos
finales útiles, como los puntos finales para iniciar sesión e
intercambiar señales de acceso.

```
información bluemix
```

**Requisitos previos**: Punto final


## lista bluemix
Crea una lista de todas las aplicaciones, contenedores, grupos
de
contenedores, y grupos VM en el espacio actual.

```
lista bluemix
[apps|contenedores|grupos-contenedores|grupos-vm]
```

**Requisitos previos**:  Punto final, Inicio de sesión,
Destino

**Opciones de mandatos**:

apps  (opcional):  muestra solo la información de las
aplicaciones.

contenedores  (opcional):  muestra solo la información de
los contenedores.

container-groups  (opcional):  muestra solo la información
de los grupos de contenedores.

grupos-vm  (opcional):  muestra solo la información de
grupos VM.

Solo puede especificarse un `apps`, `contenedores`,
`grupos-contenedores`, o
`grupos-vm a la vez. Si no se especifica ninguno, se listarán todas
las aplicaciones cf, todos los contenedores, grupos de contenedores y
grupos VM.

**Ejemplos**:

Lista todas las aplicaciones cf:

```
aplicaciones de lista bluemix
```

Lista todas las instancias de contenedores:

```
contenedores de lista bluemix
```

Lista todas las aplicaciones, contenedores, grupos de
contenedores, y grupos de VM:

```
lista bluemix```


## escala bluemix 
Escala verticalmente u horizontalmente la aplicación cf o el
grupo de contenedores a un recuento de instancias, cuota de disco
y tamaño de memoria específicos. 

**Nota:** Solo puede especificarse un número de instancias para
escalar un grupo de contenedor. Si no se especifica ninguna opción,
este mandato lista la instancia actual para el grupo de contenedores,
y también la cuota de disco y el tamaño de memoria para la aplicación
cf.

```
escala bluemix
NOMBRE_APP_CF|NOMBRE_GRUPO_CONTENEDOR [-i RECUENTO_INSTANCIA] [-k CUOTA_DISCO] [-m
TAMAÑO_MEMORIA]
```

**Requisitos previos**:
Punto final, inicio de sesión, Destino

**Opciones de mandato**:

*NOMPRE_APP_CF*|*NOMBRE_GRUPO_CONTENEDOR* 
(obligatorio):  El nombre de la aplicación cf o grupo de
contenedor
que va a escalarse.

-i *CONTAJE_INSTANCIA*  (opcional):  el número de la nueva
instancia para la aplicación cf o grupo de contenedores que va a
escalarse. Esta opción es la única opción válida para el grupo de
contenedores que debe escalarse.

-k *CUOTA_DISCO*  (opcional):  la nueva cuota de disco de la
aplicación cf. No es válido para escalar un grupo de contenedores.

-m *TAMAÑO_MEMORIA*  (opcional):  nuevo tamaño de memoria
para la aplicación cf. No es válido para escalar un grupo de
contenedores.

**Ejemplos**:

Muestra el número de instancias actual para
'mi-grupo-contenedor':

```
escala bluemix mi-grupo-contenedor
```

Escala 'mi-grupo-contenedor' a 2 instancias: 

```
escala bluemix mi-grupo-contenedor -i 2
```

Escala 'my-java-app' a 3 instancias, cuota de disco de 8G, y
tamaño de memoria de 1024M:

```
escala bluemix mi-app-java -i 3 -k 8G -m 1024M
```


## curl bluemix 
Ejecuta una solicitud HTTP sin procesar a
Bluemix. "Content-Type" se establece como "application/json" de forma
predeterminada. Este mandato envía una solicitud al servidor de la
consola de Bluemix (por ejemplo,
https://console.ng.bluemix.net)
en lugar del punto final cf API (por ejemplo,
https://api.ng.bluemix.net).

```
RUTA bluemix curl [OPCIONES...]
```

**Requisitos previos**:  Punto final, inicio de sesión

**Opciones de mandatos**:

*PATH*  (obligatorio):  vía de acceso de la URL del recurso. Por
ejemplo,
/rest/v2/apps.

*OPTIONS*  (opcional):  las opciones a las que da soporte el
mandato `bluemix
curl` son las mismas que las del mandato `cf curl`.

**Ejemplos**:

Recupera la información para todas las plantillas de contenedor
modelo:

```
bluemix curl /rest/templates
```


## bluemix iam orgs
Este mandato tiene la misma función y las mismas opciones que el
mandato `cf
orgs`.


## bluemix iam org
Este mandato tiene la misma función y las mismas opciones que el
mandato
`cf orgs`.


## bluemix iam org-create
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf
create-org`.


## bluemix iam org-rename
Este mandato tiene la misma función y las mismas opciones
que el mandato `cf
rename-org`.


## bluemix iam org-delete
Este mandato tiene la misma función y las mismas opciones
que el mandato
`cf
delete-org`.


## bluemix iam spaces
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf spaces`.


## bluemix iam space
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf space`.


## bluemix iam space-create
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf create-space`.


## bluemix iam space-rename
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf rename-space`.


## bluemix iam space-delete
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf delete-space`.


## bluemix iam user-create
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf create-user`.


## bluemix iam user-delete
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf delete-user`.


## bluemix iam org-users
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf org-users`.


## bluemix iam org-role-set
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf set-org-role`.


## bluemix iam org-role-unset
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf unset-org-role`.


## bluemix iam space-users
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf space-users`.


## bluemix iam space-role-set
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf set-space-role`.


## bluemix iam space-role-unset
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf unset-space-role`.


## bluemix catalog templates
Visualizar las plantillas de contenedor modelo en
Bluemix.

```
plantillas de catálogo de bluemix [-d]
```

**Requisitos previos**:  Punto final, inicio de sesión

**Opciones de mandatos**:

-d  (opcional):  si se especifica la opción '-d', se
muestra la descripción de cada plantilla. De lo contrario,
solo se muestran el ID y el nombre de cada plantilla.


## bluemix catalog template-run
Crea una aplicación cf que se base en la plantilla
específica con la URL y la descripción especificadas. La nueva
aplicación se inicia automáticamente de forma predeterminada.

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

**Requisitos previos**:  Punto final, Inicio de sesión, Destino

**Opciones de mandatos**:

*TEMPLATE_ID*  (obligatorio):  la plantilla en la que se basará
la aplicación cuando se cree. Utilice 'plantillas bluemix' para
visualizar todas las ID de plantillas.

*CF_APP_NAME*  (obligatorio): el nombre de la aplicación cf que
se creará.

-u *URL*  (opcional):  la ruta de la aplicación. Si no se
especifica, Blumix establece la ruta automáticamente basándose en
su nombre de aplicación y dominio predeterminado.

-d *DESCRIPTION*  (opcional):  descripción de la
aplicación.

--no-start  (opcional):  no inicie la aplicación automáticamente
después de crearla. Si no se especifica lo contrario, la aplicación
se inicia automáticamente después de haberse creado.

**Ejemplos**:

Crea una aplicación cf 'my-app' basada en la plantilla
'javaHelloWorld':

```
bluemix catalog template-run javaHelloWorld my-app
```

Crea una aplicación 'my-ruby-app' basada en la plantilla
'rubyHelloWorld' con la ruta 'myrubyapp.ng.bluemix.net' y la
descripción 'Mi primera aplicación ruby en Bluemix.':

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u
myrubyapp.ng.bluemix.net -d "Mi primera aplicación ruby en
Bluemix."
```

Crea una aplicación 'my-python-app' basada en la plantilla
'pythonHelloWorld' sin inicio automático:

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


## bluemix network regions
Visualiza la información para todas las regiones en
Bluemix.

```
bluemix network regions
```

**Requisitos previos**:  Punto final


## bluemix network region-set
Se dirige a la región que se ha especificado. Este mandato vuelve a
dirigirse automáticamente a la misma organización y espacio en la
nueva región, si es posible, o le solicita que seleccione
una nueva organización y un nuevo espacio si el usuario ya ha iniciado
sesión. El
punto final de
API cambia en consecuencia .

```
bluemix network region-set REGION_NAME
```

**Requisitos previos**:  Punto final

**Opciones de mandatos**:

*REGION_NAME*  (obligatorio):  el nombre de la región a la que
desea cambiar. Puede utilizar el mandato `bluemix
regions` para visualizar todos los nombres de región.

**Ejemplos**:

Establezca la región actual a 'eu-gb':

```
bluemix network region-set eu-gb
```


## bluemix network routes
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf routes`.


## bluemix network route-check
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf check-route`.


## bluemix network route-map
Correlacione una ruta a una aplicación cf o grupo de
contenedores que
tenga un dominio y nombre de host específicos.

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**Requisitos previos**: Punto final, inicio
de sesión, Destino

**Opciones de mandato**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* 
(obligatorio):  el nombre de la aplicación cf o grupo de contenedores
que debe correlacionarse con una ruta.

*DOMAIN*  (obligatorio): el dominio de la ruta. Por ejemplo,
mybluemix.net or ng.bluemix.net. 

-n *HOST_NAME*  (opcional):  nombre de host de la ruta. Si no
se se facilita, el nombre de host se establece en el nombre de la
aplicación o grupo de contenedores de forma predeterminada.

**Ejemplos**:

Correlacione una ruta a 'my-app' con un dominio específico:

```
bluemix network route-map my-app mybluemix.net
```

Correlacione una ruta a 'my-container-group' con el dominio y
el nombre de host específicados:

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
Elimina la correlación entre la ruta específica y una
aplicación cf existente o grupo de contenedores.

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**Requisitos previos**:  Punto final,
Inicio de sesión, Destino

**Opciones de mandato**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* 
(obligatorio):  el nombre de la aplicación cf o grupo de contenedores.

*DOMAIN*  (obligatorio):  El dominio de la ruta (por ejemplo,
mybluemix.net o ng.bluemix.net). 

-n *HOST_NAME*  (opcional):  El nombre de host de la ruta. Si
no se facilita, el nombre del host se establecerá en el nombre de
la aplicación o el nombre del grupo de forma determinada.

**Ejemplos**:

Elimina la correlación entre 'my-app.mybluemix.net' y
'my-app':

```
bluemix network route-unmap my-app mybluemix.net
```

Elimina la correlación entre 'abc.ng.bluexmix.net' y
'my-container-group':

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf create-route`.


## bluemix network route-delete
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf delete-route`.


## bluemix network orphaned-routes-delete
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf delete-orphaned-routes`.


## bluemix network domains
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf domains`.


## bluemix network domain-create
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf create-domain`.


## bluemix network domain-delete
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf delete-domain`.


## bluemix network shared-domain-create
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf create-shared-domain`.


## bluemix network shared-domain-delete
Este mandato tiene la misma función y las mismas opciones que
el mandato `cf delete-shared-domain`.


## bluemix plugin repos
Cree una lista de todos los repositorios de plugin que se
registran en Bluemix
CLI.

```
bluemix plugin repos
```

**Requisitos previos**:  Ninguno 


## bluemix plugin repo-add
Agrega un nuevo repositorio de plugin a Bluemix
CLI.

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

**Requisitos previos**:  Ninguno 

**Opciones de mandatos**:

*REPO_NAME*  (obligatorio):  el nombre del repositorio que se
añadirá. Puede volver a definir su propio nombre para cada repositorio.

*REPO_URL*  (obligatorio):  la URL del repositorio que se
añadirá. La URL de repositorio debe contener el protocolo (por
ejemplo,
http://plugins.ng.bluemix.net instead of plugins.ng.bluemix.net). http://plugins.ng.bluemix.net
es el repositorio de plugins oficial de Bluemix
CLI.

**Ejemplos**:

Añada el repositorio de plugins oficial de Bluemix CLI como
'bluemix-repo':

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
Elimina el repositorio de plugins de Bluemix
CLI.

```
bluemix plugin repo-remove REPO_NAME
```

**Requisitos previos**:  Ninguno 

**Opciones de mandatos**:

*REPO_NAME*  (obligatorio):  el nombre del repositorio que se
eliminará.

**Ejemplos**:

Elimina el repositorio 'bluemix-repo' de
Bluemix
CLI:

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugin-list
Crea una lista de todos los plugins disponibles en todos los
repositorios o repositorios específicos.

```
bluemix plugin repo-plugin-list [-r REPO_NAME]
```

**Requisitos previos**:  Ninguno 

**Opciones de mandatos**:

-r *REPO_NAME*  (opcional):  crea una lista de sólo los
plugins del repositorio especificado.

**Ejemplos**:

Crea una lista de todos los plugins en todos los repositorios
añadidos:

```
bluemix plugin repo-plugin-list
```

Crea una lista de todos los plugins del repositorio
'bluemix-repo':

```
bluemix plugin repo-plugin-list -r bluemix-repo
```


## bluemix plugin list
Crea una lista de todos los plugins instalados en
Bluemix
CLI.

```
bluemix plugin list
```

**Requisitos previos**:  Ninguno 


## bluemix plugin install
Instala el plugin a Bluemix CLI desde la vía de acceso o el
repositorio especificados.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME]
```

**Requisitos previos**:  Ninguno

**Opciones de mandato**:

*PLUGIN_PATH*|*PLUGIN_NAME* 
(obligatorio):  Si '-r *REPO_NAME*' no está especificado, el plugin
se instala desde la vía de acceso local o la URL remota especificadas.

-r *REPO_NAME*  (opcional):  El nombre del repositorio donde
se encuentra el binario del plugin.

**Ejemplos**:

Instala un plugin desde el archivo local:

```
bluemix plugin install /downloads/new_plugin
```

Instala un plugin desde la URL remota:

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

Instala el plugin 'IBM-Containers' desde el repositorio
'bluemix-repo':

```
bluemix plugin install IBM-Containers -r bluemix-repo
```


## bluemix plugin uninstall
Desinstala el plugin especificado desde Bluemix
CLI.

```
bluemix plugin uninstall PLUGIN_NAME
```

**Requisitos previos**:  Ninguno 

**Opciones de mandatos**:

*PLUGIN_NAME*  (obligatorio):  Nombre del plugin que se
instalará.

**Ejemplos**:

Desisntala el plugin 'IBM-Containers' que se ha instalado
previamente:

```
bluemix plugin uninstall IBM-Containers
```
