---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-11"
---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Despliegue de apps
{: #deployingapps}

Puede desplegar apps en {{site.data.keyword.Bluemix}} utilizando varios métodos, como por ejemplo la interfaz de línea de mandatos y los entornos de desarrollo integrado (IDE). También puede utilizar manifiestos de app para desplegar apps. Si utiliza un manifiesto de app debe reducir el número de detalles de despliegue que debe especificar cada vez que despliega una app en {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Despliegue de aplicaciones
{: #appdeploy}

El despliegue de una app en {{site.data.keyword.Bluemix_notm}} incluye dos fases: transferencia de la app e inicio de la app.

Cloud Foundry admite Diego, que es la nueva arquitectura predeterminada de tiempo de ejecución que ofrece un conjunto de funciones que mejoran el desarrollo de aplicaciones para albergar y construir plataformas en la nube. Esta actualización de arquitectura ofrece una mejora en el funcionamiento general y en el rendimiento de la plataforma Cloud Foundry. La nueva arquitectura ofrece soporte para diversas tecnologías de contenedor de aplicaciones, que incluyen Garden y Windows, un paquete SSH que permite el inicio de sesión directo con el contenedor de aplicaciones y otros cambios innovadores. Para obtener más información sobre la reciente actualización de la arquitectura, consulte [{{site.data.keyword.Bluemix_notm}} Cloud Foundry: Diego is live ![icono de enlace externo](../icons/launch-glyph.svg)](https://www.ibm.com/blogs/bluemix/2017/01/bluemix-cloud-foundry-diego-live/){: new_window}.


Todas las nuevas aplicaciones que cree se ejecutarán en Diego; debe comenzar a migrar sus aplicaciones existentes que se ejecuten en DEA a la nueva arquitectura Diego.

**Nota**: la arquitectura Diego de Cloud Foundry afecta a todos los entornos de región pública de {{site.data.keyword.Bluemix_notm}}. Los entornos {{site.data.keyword.Bluemix_notm}} dedicado y {{site.data.keyword.Bluemix_notm}} local se actualizarán más adelante.

### Transferencia de una app
{: #diego}

Durante la fase de transferencia, Diego se encarga de todos los aspectos relacionados con la orquestación del contenedor de aplicaciones. Cuando envía una app, el controlador en la nube envía una solicitud de transferencia a Diego, que se encarga de asignar las instancias de la app. El programa de fondo Diego coordina los contenedores de aplicaciones para garantizar la tolerancia de errores y la coherencia a largo plazo, que equilibra la carga entre una serie de máquinas virtuales denominadas células. Además, Diego garantiza que los usuarios puedan acceder a los registros de sus apps. Todos los componentes de Diego están diseñados para poderse agrupar en clúster, lo que significa que puede crear distintas zonas de disponibilidad.

Para validar el estado de las apps, Diego da soporte a las mismas comprobaciones basadas en puerto que se han utilizado para DEA. Sin embargo, Diego está diseñado para poder tener opciones más genéricas, como comprobaciones de estado basadas en URL, que se habilitarán en el futuro.

#### Transferencia de una nueva app
{: #stageapp}

Todas las apps nuevas se despliegan en la arquitectura de Diego. Para transferir una nueva aplicación, despliegue la app con el mandato **cf push**:

  1. Despliegue la aplicación:
  ```
  $ cf push APPLICATION_NAME
  ```

Para ver más detalles sobre el mandato **cf push**, consulte [cf push](/docs/cli/reference/cfcommands/index.html#cf_push).

### Migración de una app existente a Diego
{: #migrateapp}

Diego es la arquitectura predeterminada de Cloud Foundry para {{site.data.keyword.Bluemix_notm}} y se retirará el soporte para DEA, de modo que debe migrar todas sus aplicaciones existentes actualizando cada app. Comience la migración de sus apps a Diego actualizando la aplicación con el distintivo Diego. La aplicación intentará inmediatamente ejecutarse en Diego y dejará de ejecutarse en los DEA.

A medida que la aplicación se actualiza desde la arquitectura DEA a Diego, es posible que se produzca un breve intervalo de inactividad, o quizás un intervalo de inactividad prolongado, si la aplicación no es compatible con Diego. Para limitar este intervalo de inactividad, realice un [despliegue de tipo blue-green](/docs/manageapps/updapps.html#blue_green) desplegando una copia de la aplicación en Diego y luego intercambiando rutas y escalando hacia abajo la aplicación DEA.

Siga estos pasos para migrar su app a Diego:

 1.  Instale la [CLI cf ![icono de enlace externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window} y el [plugin de CLI Diego-Enabler ![icono de enlace externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-incubator/Diego-Enabler){:new_window}.
 2. Revise la [lista de problemas conocidos](depapps.html#knownissues).
 3. Establezca el distintivo Diego para cambiar la app de modo que se ejecute en Diego:
  ```
  $ cf enable-diego APPLICATION_NAME
  ```

Después de actualizar la app, compruebe que la app se ha iniciado. Si la app migrada no se puede iniciar, permanecerá fuera de línea hasta que identifica y solucione el problema; luego reinicie la app.

IBM le avisará del periodo de migración obligatoria cuando se retire el soporte de la arquitectura DEA; si para entonces aún no ha migrado sus apps, lo hará el equipo de operaciones.

Para validar el programa de fondo en el que ejecuta la aplicación, utilice el siguiente mandato:

  ```
  $ cf has-diego-enabled APPLICATION_NAME
  ```

#### Problemas conocidos de la migración a Diego
{: #knownissues}

Estos son los problemas conocidos que quizás deba solucionar cuando migre sus apps a Diego:

  * Las aplicaciones de Worker desplegadas con la opción `--no-route` no se indican como aplicaciones en buen estado. Para evitar este problema, inhabilite la comprobación de estado basada en puerto con el mandato `cf set-health-check APP_NAME none`.
  * El mandato **cf files** ya no recibe soporte. Se ha sustituido por el mandato **cf ssh**. Para ver más detalles sobre el mandato **cf ssh**, consulte [cf ssh](/docs/cli/reference/cfcommands/index.html#cf_ssh).
  * Algunas apps utilizan un número alto de descriptores de archivo (inodes). Si detecta este problema, debe aumentar la cuota de disco para la app con el mandato `cf scale APP_NAME [-k DISK]`.

Para ver una lista completa de problemas conocidos, consulte la página de documentación de Cloud Foundry sobre [Migración a Diego ![icono de enlace externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/diego-design-notes/blob/master/migrating-to-diego.md){: new_window}.

Hasta que se retire el soporte para la arquitectura DEA antigua, puede ejecutar el siguiente mandato para volver a utilizar DEA: `cf disable-diego APPLICATION_NAME`. También puede seguir desplegando nuevas apps en la arquitectura DEA hasta que se retire el soporte:

**Nota**: debe tener instalada la [CLI cf ![icono de enlace externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window} y el [plugin de CLI Diego-Enabler ![icono de enlace externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-incubator/Diego-Enabler){:new_window} para poder utilizar el mandato `disable-diego`.

1. Despliegue la aplicación sin iniciarla:
```
$ cf push APPLICATION_NAME --no-start
```
2. Ejecute el mandato disable-diego:
```
$ cf disable-diego APPLICATION_NAME
```
3. Inicie la aplicación:
```
$ cf start APPLICATION_NAME
```

### Inicio de una app
{: #startapp}

Cuando se inicia una app, se crea la instancia o instancias del contenedor de aplicaciones. Para aplicaciones que se ejecutan en Diego, puede utilizar el mandato **cf ssh** o **cf scp** para acceder al sistema de archivos del contenedor de aplicaciones que incluye los registros. El mandato **cf files** no funciona para las apps que se ejecutan en la arquitectura Diego.

**Nota**: si aún tiene aplicaciones que se ejecutan en DEA, puede utilizar el mandato **cf files** para ver los archivos del contenedor de aplicaciones hasta que se retire el soporte de DEA.

Si la app no se puede iniciar, la aplicación se detiene y todo el contenido del contenedor de aplicaciones se elimina. Por lo tanto, si una app se detiene o si el proceso de transferencia de una app falla, no dispondrá de archivos de registro.

Si los registros de la aplicación dejan de estar disponibles de modo que no se pueden utilizar los mandatos **cf ssh**, **cf scp** o **cf files** para ver la causa de los errores de transferencia en el contenedor de aplicaciones, puede utilizar en su lugar el mandato **cf logs**. El mandato **cf
logs** utiliza el agregador de registros de Cloud Foundry para recopilar detalles sobre los registros de la app y del sistema y puede ver lo que se ha colocado en el almacenamiento intermedio del agregador de registros. Para obtener más información sobre el agregador de registros, consulte [Inicio de una sesión en Cloud Foundry ![icono de enlace externo](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}..

**Nota:** El tamaño del almacenamiento intermedio está limitado. Si una aplicación se ejecuta durante mucho rato y no se reinicia, es posible que no se muestren registros cuando escriba el mandato `cf logs appname --recent` porque el almacenamiento intermedio de registros se haya borrado. Por lo tanto, para depurar errores de transferencia de una aplicación grande, puede especificar el mandato `cf logs nombreapp` en una línea de mandatos que no sea la interfaz de línea de mandatos cf para efectuar un seguimiento de los registros cuando despliegue la aplicación.

Si tiene problemas para transferir sus apps en {{site.data.keyword.Bluemix_notm}}, siga los pasos del apartado [Depuración de errores de transferencia](/docs/debug/index.html#debugging-staging-errors) para solucionar el problema.


## Despliegue de apps mediante el mandato cf
{: #dep_apps}

Cuando despliegue sus apps en {{site.data.keyword.Bluemix_notm}} desde la interfaz de línea de mandatos, debe especificar un paquete de compilación como entorno de tiempo ejecución de acuerdo con el lenguaje de la app y la infraestructura. También puede utilizar el servicio Delivery Pipeline para desplegar apps en {{site.data.keyword.Bluemix_notm}}.

{{site.data.keyword.Bluemix_notm}} ofrece paquetes de compilación integrados que dan soporte a Java y a Node.js. Si utiliza estos lenguajes e infraestructuras, no necesita especificar el paquete de compilación cuando despliegue la app mediante la interfaz de línea de mandatos. Puesto que {{site.data.keyword.Bluemix_notm}} se basa en Cloud Foundry, el mandato utiliza como valores predeterminados estos paquetes de compilación.

Si utiliza un paquete de compilación externo, debe especificar el URL del paquete de compilación mediante la opción **-b** cuando despliegue la app en {{site.data.keyword.Bluemix_notm}} desde el indicador de mandatos.

  * Para desplegar paquetes del servidor Liberty en {{site.data.keyword.Bluemix_notm}}, utilice el mandato siguiente, desde su directorio de origen:

  ```
  cf push
  ```

  Para obtener más información sobre el paquete de compilación de Liberty, consulte el apartado [Liberty para Java](/docs/runtimes/liberty/index.html).

  * Para desplegar apps Java Tomcat en {{site.data.keyword.Bluemix_notm}}, utilice el mandato siguiente:

  ```
  cf push appname -b https://github.com/cloudfoundry/java-buildpack.git -p app_path
  ```

  * Para desplegar paquetes WAR en {{site.data.keyword.Bluemix_notm}},
utilice el mandato siguiente:

  ```
  cf push nombre_app -p app.war
  ```
  O, puede especificar un directorio que contenga los archivos de app mediante el mandato siguiente:

  ```
  cf push nombre_app -p "./app"
  ```

  * Para desplegar apps Node.js en {{site.data.keyword.Bluemix_notm}}, utilice el mandato siguiente:

  ```
  cf push appname -p app_path
  ```

El archivo `package.json` debe estar en su app Node.js para que lo reconozca el paquete de compilación de Node.js. El archivo `app.js` es el script
de entrada de la app, que se puede especificar en el archivo `package.json`. El ejemplo siguiente muestra un archivo `package.json` sencillo:

  ```
  {
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": ">=3.4.7 <4",
                "jade": ">=1.1.4"
        },
        "scripts": {
                "start": "node app.js"
        },
        "engines": {
                "node": ">=0.10.0"
        },
        "repository": {}
  }
  ```

  Para obtener más información acerca de un archivo `package.json`, consulte [package.json ![icono de enlace externo](../icons/launch-glyph.svg)](https://www.npmjs.org/doc/files/package.json.html){:new_window}.

  * Para desplegar apps PHP, Ruby o Python en {{site.data.keyword.Bluemix_notm}},
utilice el siguiente mandato del directorio que contiene el origen de su app:

  ```
  cf push nombre_app
  ```

### Despliegue de una app en varios espacios

Una app es específica del espacio en el que se ha desplegado. No puede mover ni copiar una app de un espacio a otro en {{site.data.keyword.Bluemix_notm}}. Para desplegar una app en varios espacios, debe desplegar la app en cada espacio en el que desee utilizar la app siguiendo estos pasos:

  1. Vaya al espacio en el que desea desplegar la app con el mandato **cf target** con la opción **-s**:

  ```
  cf target -s <nombre_espacio>
  ```

  2. Acceda al directorio de la app y despliéguela con el mandato **cf push**, donde nombre_app debe ser exclusivo dentro del dominio.

  ```
  cf push nombre_app
  ```

## Manifiesto de aplicación
{: #appmanifest}

El manifiesto de app contiene opciones que se aplican al mandato **cf push**. Puede utilizar el manifiesto de app para reducir el número de detalles de despliegue que debe especificar cada vez que envía una app a {{site.data.keyword.Bluemix_notm}}.

En los manifiestos de app, puede especificar opciones como, por ejemplo, el número de instancias de la app que se deben crear, la cantidad de memoria y la cuota de disco que se debe asignar a las apps y otras variables de entorno para la app. También puede utilizar los manifiestos de app para automatizar despliegues de apps. El nombre predeterminado de un archivo de manifiesto es `manifest.yml`.

### Opciones soportadas en el archivo de manifiesto

La tabla siguiente muestra las opciones soportadas que puede utilizar en un archivo de manifiesto de la app. Si elige utilizar un nombre que no sea `manifest.yml`, debe utilizar la opción **-f** con el mandato **cf push**. En el ejemplo siguiente, `appManifest.yml` es el nombre del archivo:

```
cf push -f appManifest.yml
```

<p>  </p>


|Opciones	|Descripción	|Uso o ejemplo|
|:----------|:--------------|:---------------|
|**buildpack**	|El URL o el nombre del paquete de compilación.	|`buildpack: ` *URL_paquete_compilación*|
|**disk_quota**	|La cuota de disco que se debe asignar a la app. El valor predeterminado es 1 G.	|`disk_quota: 500M`|
|**domain**	|El nombre de dominio de la app en {{site.data.keyword.Bluemix_notm}}.	|`dominio:` ng.bluemix.net|
|**host**	|El nombre de host de la app en {{site.data.keyword.Bluemix_notm}}. Este valor debe ser exclusivo en el entorno de {{site.data.keyword.Bluemix_notm}}.	|`host: ` *nombre_host*|
|**nombre**	|El nombre de la app en {{site.data.keyword.Bluemix_notm}}. Este valor debe ser exclusivo en el entorno de {{site.data.keyword.Bluemix_notm}}.	|`name: ` *nombre_app*|
|**path**	|La ubicación de la app. Este valor puede ser una vía de acceso relativa o absoluta.	|`path: ` *vía_acceso_a_app*|
|**command**	|El mandato de inicio personalizado para la app o el mandato para ejecutar archivos script..	|`command:` *mandato_personalizado* `command:` *bash ./run.sh*|
|**memory**	|La cantidad de memoria que se debe asignar a la app. El valor predeterminado es 1 G.	|`memory: 512M`|
|**instances**	|El número de instancias que van a crear para la app.	|`instances: 2`|
|**timeout**	|El intervalo máximo de tiempo, en segundos, que se utiliza para iniciar la app. El valor predeterminado es de 60 segundos.	|`timeout: 80`|
|**no-route**	|Un valor booleano para impedir que se asigne una ruta a la app si la app sólo se está ejecutando como programa de fondo. El valor predeterminado es **false**.	|`no-route: true`|
|**random-route**	|Un valor booleano para asignar una ruta aleatoria a la app. El valor predeterminado es **false**.	|`random-route: true`|
|**services**	|Los servicios que se van a enlazar a la app.	|`services: - mysql_maptest`|
|**env**	|Las variables de entorno personalizadas de la app.|`env: DEV_ENV: production`|
{: caption="Table 1. Supported options in the manifest YAML file" caption-side="top"}

### Un archivo de ejemplo manifest.yml

En el ejemplo siguiente se muestra un archivo de manifiesto para una app Node.js que utiliza el paquete de compilación Node.js integrado de la comunidad en {{site.data.keyword.Bluemix_notm}}.

```
---
- name: myNodejsapp
  memory: 256M
  disk_quota: 512M
  path: /dev/myNodejsApp
  buildpack: nodejs_buildpack
  host: nodejs001
  domain: mybluemix.net
  command: node app.js
  timeout: 80
  services:
  - mongo_8917
  env:
    env_type: production
```
{:codeblock}

## Variables de entorno
{: #app_env}

Las variables de entorno contienen información sobre el entorno de una app desplegada en {{site.data.keyword.Bluemix_notm}}. A parte de las variables de entorno definidas por el *agente de ejecución de gotas (DEA)* y los paquetes de compilación, también puede definir variables de entorno específicas de una app en {{site.data.keyword.Bluemix_notm}}.

Puede ver las siguientes variables de entorno de una app {{site.data.keyword.Bluemix_notm}} en ejecución
mediante el mandato **cf env** o desde la interfaz de usuario {{site.data.keyword.Bluemix_notm}}:

  * Variables definidas por el usuario específicas para una app. Para obtener información sobre cómo añadir una variable definida por el usuario a una app, consulte [Cómo añadir variables de entorno definidas por el usuario ![icono de enlace externo](../icons/launch-glyph.svg)](#ud_env){:new_window}.

  * La variable VCAP_SERVICES, que contiene la información de conexión para acceder a una instancia de servidor. Si su app está enlazada a varios servicios, la variable VCAP_SERVICES contiene la información de conexión para cada instancia de servicio. Por ejemplo:

  ```
  {
   "VCAP_SERVICES": {
    "AppScan Dynamic Analyzer": [
     {
      "credentials": {
       "bindingid": "0ab3162a-867e-4137-a2e7-39463a89472e",
       "password": "xE/jh/PlRj3ruuy8RCl8JNyEywaivRH1xXSZcbVExKg="
      },
      "label": "AppScan Dynamic Analyzer",
      "name": "AppScan Dynamic Analyzer-9q",
      "plan": "standard",
      "tags": [
       "Security",
       "security",
       "ibm_created"
      ]
     }
    ],
    "mysql-5.5": [
     {
      "credentials": {
       "host": "23.246.200.38",
       "hostname": "23.246.200.38",
       "name": "d296abcc06c9e418b94abcaafdf547620",
       "password": "peRiYCG4ZYqu3",
       "port": 3307,
       "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620",
       "user": "uzpGf7eGJ7mtB",
       "username": "uzpGf7eGJ7mtB"
      },
      "label": "mysql-5.5",
      "name": "mysql-ix",
      "plan": "300",
      "tags": [
       "mysql",
       "relational",
       "data_management",
       "ibm_experimental"
      ]
     }
    ]
   }
  }
  ```

También tiene acceso a las variables de entorno establecidas por DEA y los paquetes de compilación.

Las siguientes variables están definidas por el DEA:

<dl>
  <dt><strong>HOME</strong></dt>
  <dd>El directorio raíz de la app desplegada.</dd>
  <dt><strong>MEMORY_LIMIT</strong></dt>
  <dd>Cantidad máxima de memoria que puede utilizar cada instancia de la app. Puede especificar el valor de la app en el archivo <span class="ph filepath">manifest.yml</span> o en la línea de mandatos cuando envíe la app.</dd>
  <dt><strong>PORT</strong></dt>
  <dd>El puerto del DEA correspondiente a la comunicación con la app. El DEA asigna un puerto para la app en el momento de la transferencia.</dd>
  <dt><strong>PWD</strong></dt>
  <dd>El directorio de trabajo actual en el que se ejecuta el paquete de compilación.</dd>
  <dt><strong>TMPDIR</strong></dt>
  <dd>El directorio en que se guardan los archivos temporales y de transferencia.</dd>
  <dt><strong>USER</strong></dt>
  <dd>El ID de usuario bajo el cual se ejecuta el DEA.</dd>
  <dt><strong>VCAP_APP_HOST</strong></dt>
  <dd>La dirección IP del host del DEA.</dd>
  <dt><strong>VCAP_APPLICATION</strong></dt>
  <dd>Una cadena JSON que contiene la información sobre la app desplegada. La información incluye el nombre de la app, los URI, los límites de memoria, la indicación de fecha y hora en que la app ha alcanzado su estado actual, etc. Por ejemplo:
  <pre class="pre codeblock"><code>
  {
    "limits": {
        "mem": 512,
        "disk": 1024,
        "fds": 16384
    },
    "application_version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "application_name": "testapp",
    "application_uris": [
        "testapp.AppDomainName.mybluemix.net"
    ],
    "version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "name": "testapp",
    "space_name": "dev",
    "space_id": "c6ed3a8e-436b-43ac-9f96-b676ee335000",
    "uris": [
        "testapp.AppDomainName.mybluemix.net"
    ],
    "users": null,
    "application_id": "e984bb73-4c4e-414b-84b7-c28c87f84003",
    "instance_id": "09f50e22848d4ec0b943e9e487c23569",
    "instance_index": 0,
    "host": "0.0.0.0",
    "port": 61399,
    "started_at": "2015-01-16 06:50:51 +0000",
    "started_at_timestamp": 1421391051,
    "start": "2015-01-16 06:50:51 +0000",
    "state_timestamp": 1421391051
}
</code></pre></dd>
  <dt><strong>VCAP_SERVICES</strong></dt>
  <dd>Una cadena JSON que contiene información sobre el servicio que está enlazado a la app desplegada. Por ejemplo:
  <pre class="pre codeblock"><code>
  {
    "mysql-5.5": [
        {
            "name": "mysql-ix",
            "label": "mysql-5.5",
            "tags": [
                "mysql",
                "relational",
                "data_management",
                "ibm_experimental"
            ],
            "plan": "300",
            "credentials": {
                "name": "d296abcc06c9e418b94abcaafdf547620",
                "hostname": "23.246.200.38",
                "host": "23.246.200.38",
                "port": 3307,
                "user": "uzpGf7eGJ7mtB",
                "username": "uzpGf7eGJ7mtB",
                "password": "peRiYCG4ZYqu3",
                "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620"
            }
        }
    ]
}
</code></pre></dd>

</dl>

Las variables definidas por un paquete de compilación varían según cada paquete de compilación. Consulte [Paquetes de compilación ![icono de enlace externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-community/cf-docs-contrib/wiki/Buildpacks){:new_window} para conocer los paquetes de compilación compatibles.

<ul>
    <li>Las variables siguientes están definidas por el paquete de compilación de Liberty:

	  <dl>
	  <dt><strong>JAVA_HOME</strong></dt>
	  <dd>La ubicación del SDK de Java que ejecuta la app.</dd>
	  <dt><strong>IBM_JAVA_OPTIONS</strong></dt>
	  <dd>Las opciones de SDK de Java que se utilizarán cuando se ejecute la app.</dd>
	  <dt><strong>IBM_JAVA_COMMAND_LINE</strong></dt>
	  <dd>El mandato Java para iniciar una instancia de servidor de un perfil de Liberty en el DEA.</dd>
	  <dt><strong>WLP_USR_DIR</strong></dt>
	  <dd>La ubicación de recursos compartidos y de las definiciones de servidor al iniciar una instancia de servidor de un perfil de Liberty en el DEA.</dd>
	  <dt><strong>WLP_OUTPUT_DIR</strong></dt>
	  <dd>La ubicación de las salidas que se generen como archivos de registro y directorios de trabajo de una instancia de servidor de un perfil de Liberty en ejecución.</dd>
	  </dl>
</li>
<li>Las variables siguientes están definidas por el paquete de compilación de Node.js:
	<dl>
	<dt><strong>BUILD_DIR</strong></dt>
	<dd>El directorio del entorno de ejecución de Node.js.</dd>
	<dt><strong>CACHE_DIR</strong></dt>
	<dd>El directorio que utiliza el entorno de tiempo de ejecución de Node.js para la colocación en memoria caché.</dd>
	<dt><strong>PATH</strong></dt>
	<dd>La vía de acceso del sistema que utiliza el entorno de ejecución Node.js.</dd>
	</dl>
</li>
</li>
</ul>

Puede utilizar el código de ejemplo siguiente de Node.js para obtener el valor de la variable de entorno VCAP_SERVICES:

```
if (process.env.VCAP_SERVICES) {
    var env = JSON.parse (process.env.VCAP_SERVICES);
    myvar = env.foo[bar].foo;
}
```

Para obtener más información sobre cada variable de entorno, consulte el apartado [Variables de entorno de Cloud Foundry ![icono de enlace externo](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/environment-variable.html){:new_window}.

## Personalización de despliegues de apps
{: #customize_dep}

Puede personalizar las tareas de despliegue de apps. Por ejemplo, puede especificar los mandatos de inicio de las apps y puede configurar el entorno de arranque de las apps.
{:shortdesc}

### Especificación de mandatos de inicio

Para especificar mandatos de inicio para la app, puede utilizar uno de los siguientes métodos. Los mandatos de inicio que especifique prevalecerán sobre los mandatos de inicio predeterminados que proporciona el paquete de compilación.

**Nota:** Si desea que prevalezcan los mandatos de inicio del paquete de compilación, especifique **null** como mandato de inicio.

  * Utilice el mandato **cf push** y especifique el parámetro -c. Por ejemplo, cuando despliegue una
app Node.js, puede especificar el mandato de inicio **node app.js** en el parámetro -c:

  ```
  cf push appname -p app_path -c "node app.js"
  ```

  * Utilice el parámetro command del archivo `manifest.yml`. Por ejemplo, cuando despliegue una app Node.js, puede especificar el mandato de inicio **node app.js** en el archivo de manifiesto:

  ```
  command: node app.js
  ```


### Cómo añadir variables de entorno definidas por el usuario
{: #ud_env}

Las variables de entorno definidas por el usuario son específicas para una aplicación. Tiene las siguientes opciones para añadir una variable de entorno definida por el usuario a una app en ejecución:

  * Utilice la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}. Siga estos pasos:
    1. En el Panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el mosaico de la app. Se mostrará la página de detalles de la App.
	2. Pulse **Variables de entorno**.
	3. Pulse **USER-DEFINED** y, a continuación, pulse **ADD**.
	4. Rellene los campos obligatorios y, a continuación, pulse **SAVE**.
  * Utilice la interfaz de línea de mandatos cf. Añada una variable definida por el usuario utilizando el mandato `cf set-env`. Por ejemplo:
    ```
    cf set-env appname env_var_name env_var_value
    ```

  * Utilice el archivo `manifest.yml`. Añada los pares de valores en el archivo. Por ejemplo:
    ```
	env:
      VAR1:value1
      VAR2:value2
    ```

Tras añadir una variable de entorno definida por el usuario, puede usar el código de ejemplo Node.js siguiente para obtener el
valor de la variable que ha definido:

```
var myEnv = process.env.env_var_name;
console.log("My user defined = " + myEnv);
```

### Configuración del entorno de arranque

Para configurar el entorno de arranque para la app, puede añadir scripts de shell en el directorio `/.profile.d`. El directorio `/.profile.d` está bajo el directorio build de la app. {{site.data.keyword.Bluemix_notm}} ejecuta los scripts del directorio `/.profile.d` antes de que se ejecute la app. Por ejemplo, puede establecer la variable de entorno NODE_ENV en **production** colocando un archivo `node_env.sh` con el siguiente contenido bajo el directorio `/.profile.d`:

```
export NODE_ENV=production;
```

###Cómo evitar que se carguen archivos y directorios

Cuando utilice la interfaz de línea de mandatos cf para desplegar una app, puede ahorrar tiempo de carga si omite ciertos archivos y directorios que {{site.data.keyword.Bluemix_notm}} puede obtener de cualquier otro sitio. Para evitar que estos archivos y directorios se carguen en {{site.data.keyword.Bluemix_notm}}, puede crear un archivo `.cfignore` en el directorio raíz de la app.

**Nota:** El archivo `.cfignore` debe tener el formato UTF-8.

El archivo `.cfignore` contiene los nombres de los archivos y directorios que desea omitir, nombre por línea. Puede utilizar un asterisco (*) como carácter comodín. Cuando especifique un directorio, también se omiten todos los archivos y subdirectorios que hay bajo dicho directorio. Por ejemplo, el siguiente contenido del archivo `.cfignore` indica que todos los archivos `.swp` y todos los archivos y subdirectorios que haya bajo el directorio `tmp/` no se cargarán en {{site.data.keyword.Bluemix_notm}}.

```
*.swp
tmp/
```

# Enlaces relacionados
{: #rellinks notoc}

## Enlaces relacionados
{: #general}

* [Despliegue con manifiestos de app ![icono de enlace externo](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){:new_window}
* [CF Manifest Generator ![icono de enlace externo](../icons/launch-glyph.svg)](http://cfmanigen.mybluemix.net/){:new_window}
* [Iniciación a cf v6 ![icono de enlace externo](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html){:new_window}
* [Iniciación a IBM Continuous Delivery Pipeline for Bluemix](/docs/services/DeliveryPipeline/index.html#getstartwithCD)
