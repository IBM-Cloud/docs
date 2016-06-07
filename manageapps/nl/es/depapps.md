---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Despliegue de apps
{: #deployingapps}

*Última actualización: 9 de mayo de 2016*

Puede desplegar apps en {{site.data.keyword.Bluemix}} utilizando varios métodos, como por ejemplo la interfaz de línea de mandatos y los entornos de desarrollo integrado (IDE). También puede utilizar manifiestos de app para desplegar apps. Si utiliza un manifiesto de app debe reducir el número de detalles de despliegue que debe especificar cada vez que despliega una app en {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

##Despliegue de aplicaciones
{: #appdeploy}

El despliegue de una app en {{site.data.keyword.Bluemix_notm}} incluye dos fases: transferencia de la app e inicio de la app.

###Transferencia de una app

Durante la fase de transferencia, un agente de ejecución de gotas (DEA) utiliza la información que especifica el usuario en la interfaz de la línea de mandatos cf o en el archivo `manifest.yml` para decidir qué se debe crear para la fase de transferencia. El DEA selecciona un paquete de compilación adecuado para transferir la app y el resultado del proceso de transferencia es una gota. Para obtener más información sobre cómo desplegar una app en {{site.data.keyword.Bluemix_notm}}, consulte Arquitectura de [{{site.data.keyword.Bluemix_notm}}, Cómo funciona {{site.data.keyword.Bluemix_notm}}](../public/index.html#publicarch).

Durante el proceso de transferencia, el DEA comprueba si el paquete de compilación coincide con la app. Por ejemplo, un tiempo de ejecución de Liberty para un archivo .war o un tiempo de ejecución Node.js para archivos .js. El DEA crea a continuación un contenedor aislado que contiene el paquete de compilación y el código de app. El componente
Warden es el encargado de gestionar el contenedor. Para obtener más información, consulte [Cómo se transfieren las apps](http://docs.cloudfoundry.org/concepts/how-applications-are-staged.html){:new_window}.

###Inicio de una app

Cuando se inicia una app, se crea la instancia o instancias del contenedor warden. Puede utilizar el mandato **cf files** para ver los archivos almacenados en el sistema de archivos del contenedor Warden, como por ejemplo registros. Si la app no se puede iniciar, el DEA detiene la app y todo el contenido del contenedor Warden se elimina. Por lo tanto, si una app se detiene o si el proceso de transferencia de una app falla, no dispondrá de archivos de registro.

Si los registros de la app dejan de estar disponibles de modo que no se puede utilizar el mandato **cf files** para ver la causa de los errores de transferencia, puede utilizar en su lugar el mandato **cf logs**. El mandato **cf
logs** utiliza el agregador de registros de Cloud Foundry para recopilar detalles sobre los registros de la app y del sistema y puede ver lo que se ha colocado en el almacenamiento intermedio del agregador de registros. Para obtener más información sobre el agregador de registros, consulte [Inicio de una sesión en Cloud Foundry](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}.

**Nota:** El tamaño del almacenamiento intermedio está limitado. Si una app se ejecuta durante mucho rato y no se reinicia, es posible que no se muestren registros cuando se especifique `cf logs nombreapp --recent` ya que puede que el almacenamiento intermedio de registros se haya borrado. Por lo tanto, para depurar errores de transferencia de una app grande, puede especificar `cf logs nombreapp` en una línea de mandatos que no sea la interfaz de línea de mandatos cf para efectuar un seguimiento de los registros cuando despliegue la app.

Si tiene problemas para transferir sus apps en {{site.data.keyword.Bluemix_notm}}, siga los pasos del apartado [Depuración de errores de transferencia](../debug/index.html#debugging-staging-errors) para solucionar el problema.

##Despliegue de apps mediante el mandato cf
{: #dep_apps}

Cuando despliegue sus apps en {{site.data.keyword.Bluemix_notm}} desde la interfaz de línea de mandatos, debe especificar un paquete de compilación como entorno de tiempo ejecución de acuerdo con el lenguaje de la app y la infraestructura. También puede utilizar el servicio Delivery Pipeline para desplegar apps en {{site.data.keyword.Bluemix_notm}}.

{{site.data.keyword.Bluemix_notm}} ofrece paquetes de compilación integrados que dan soporte a Java y a Node.js. Si utiliza estos lenguajes e infraestructuras, no necesita especificar el paquete de compilación cuando despliegue la app mediante la interfaz de línea de mandatos. Puesto que {{site.data.keyword.Bluemix_notm}} se basa en Cloud Foundry, el mandato utiliza como valores predeterminados estos paquetes de compilación.

Si utiliza un paquete de compilación externo, debe especificar el URL del paquete de compilación mediante la opción **-b** cuando despliegue la app en {{site.data.keyword.Bluemix_notm}} desde el indicador de mandatos.

  * Para desplegar paquetes del servidor Liberty en {{site.data.keyword.Bluemix_notm}}, utilice el mandato siguiente, desde su directorio de origen:
  
  ```
  cf push
  ```
  
  Para obtener más información sobre el paquete de compilación de Liberty, consulte el apartado [Liberty para Java](../runtimes/liberty/index.html).
  
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
  
A
                                                  El archivo `package.json` debe estar
                                                  en su app Node.js para que lo reconozca el paquete
                                                  de compilación de Node.js. El archivo `app.js` es el script
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
    
  Para obtener más información acerca de un archivo `package.json`, consulte [package.json](https://www.npmjs.org/doc/files/package.json.html){:new_window}.
  
  * Para desplegar apps PHP, Ruby o Python en {{site.data.keyword.Bluemix_notm}},
utilice el siguiente mandato del directorio que contiene el origen de su app:
  
  ```
  cf push nombre_app
  ```

###Despliegue de una app en varios espacios

Una app es específica del espacio en el que se ha desplegado. No puede mover ni copiar una app de un espacio a otro en {{site.data.keyword.Bluemix_notm}}. Para desplegar una app en varios espacios, debe desplegar la app en cada espacio en el que desee utilizar la app siguiendo estos pasos:

  1. Vaya al espacio en el que desea desplegar la app con el mandato **cf target** con la opción **-s**:
  
  ```
  cf target -s <nombre_espacio>
  ```
  
  2. Acceda al directorio de la app y despliéguela con el mandato **cf push**, donde nombre_app debe ser exclusivo dentro del dominio.
  
  ```
  cf push nombre_app
  ```
  
##Manifiesto de aplicación
{: #appmanifest}

El manifiesto de app contiene opciones que se aplican al mandato **cf       push**. Puede utilizar el manifiesto de app para reducir el número de detalles de despliegue que debe especificar cada vez que envía una app a {{site.data.keyword.Bluemix_notm}}.

En los manifiestos de app, puede especificar opciones como, por ejemplo, el número de instancias de la app que se deben crear, la cantidad de memoria y la cuota de disco que se debe asignar a las apps y otras variables de entorno para la app. También puede utilizar los manifiestos de app para automatizar despliegues de apps. El nombre predeterminado de un archivo de manifiesto es `manifest.yml`.

###Opciones soportadas en el archivo de manifiesto

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
|**services**	|Los servicios que se van a enlazar a la app.	|`services:   - mysql_maptest`|
|**env**	|Las variables de entorno personalizadas de la app.|`env: DEV_ENV: production`|
*Tabla 1. Opciones admitidas en el archivo manifest.yml*

###Un ejemplo de archivo `manifest.yml`

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

##Variables de entorno
{: #app_env}

Las variables de entorno contienen información sobre el entorno de una app desplegada en {{site.data.keyword.Bluemix_notm}}. A parte de las variables de entorno definidas por el *agente de ejecución de gotas (DEA)* y los paquetes de compilación, también puede definir variables de entorno específicas de una app en {{site.data.keyword.Bluemix_notm}}.

Puede ver las siguientes variables de entorno de una app {{site.data.keyword.Bluemix_notm}} en ejecución
mediante el mandato **cf env** o desde la interfaz de usuario {{site.data.keyword.Bluemix_notm}}:
	
  * Variables definidas por el usuario específicas para una app. Para obtener información sobre cómo añadir una variable definida por el usuario a una app, consulte [Cómo añadir variables de entorno definidas por el usuario](#ud_env){:new_window}.
	 
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
        "testapp.AppDomainNameng.mybluemix.net"
    ],
    "version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "name": "testapp",
    "space_name": "dev",
    "space_id": "c6ed3a8e-436b-43ac-9f96-b676ee335000",
    "uris": [
        "testapp.AppDomainNameng.mybluemix.net"
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

Las variables definidas por un paquete de compilación varían según cada paquete de compilación. Consulte [Paquetes de compilación](https://github.com/cloudfoundry-community/cf-docs-contrib/wiki/Buildpacks){:new_window} para conocer los paquetes de compilación compatibles.

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

Para obtener más información sobre cada variable de entorno, consulte el apartado [Variables de entorno de Cloud Foundry](http://docs.cloudfoundry.org/devguide/deploy-apps/environment-variable.html){:new_window}.

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
    1. En el Panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el icono de la app. Se mostrará la página de detalles de la App.
	2. En el panel de navegación izquierdo, pulse **Variables de entorno**.
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
{: #rellinks}

## Enlaces relacionados
{: #general}

* [Despliegue con manifiestos de app](http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){:new_window}
* [CF Manifest Generator](http://cfmanigen.mybluemix.net/){:new_window}
* [Iniciación a cf v6](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html){:new_window}
* [Iniciación a IBM Continuous Delivery Pipeline for Bluemix](../services/DeliveryPipeline/index.html#getstartwithCD)
