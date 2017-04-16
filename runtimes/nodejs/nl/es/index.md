---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# SDK for Node.js
{: #nodejs_runtime}

El tiempo de ejecución de Node.js en {{site.data.keyword.Bluemix}} está basado en el paquete de compilación de sdk-for-nodejs.
El paquete de compilación sdk-for-nodejs proporciona un entorno de ejecución completo para apps Node.js.
{: shortdesc}

El paquete de compilación sdk-for-nodejs se utiliza cuando la aplicación contiene un archivo **package.json** en el directorio raíz.

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una aplicación de inicio Node.js.  La aplicación de inicio Node.js es una sencilla app Node.js que ofrece una plantilla que puede utilizar para su app. Puede experimentar con la app de inicio, y realizar y enviar los cambios al entorno de Bluemix. Consulte [Utilización de las aplicaciones de iniciador](/docs/cfapps/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de inicio.

## Mandato de inicio
{: #starup_commmand}

Para especificar un mandato de inicio para la aplicación Node.js de Bluemix, se recomienda utilizar un archivo **Procfile** o **package.json**.

Especifique un mandato de inicio en el **Procfile** en el formulario que se indica a continuación. Aquí, app.js es el script js de inicio de la aplicación.
```
web: node app.js
```
{: codeblock}

Guarde **Procfile** en el directorio raíz de la aplicación.

Si un **Procfile** no está presente, el paquete de compilación IBM Bluemix Node.js comprobará si existe una entrada scripts.start en el archivo **package.json**. De nuevo, en el siguiente ejemplo, app.js es el script js de inicio de la aplicación.
```
{
    ...   
    "scripts": {
      "start": "node app.js"
    }
}
```
{: codeblock}

Si existe una entrada de script en el archivo **package.json**, se genera un
**Procfile** automáticamente. El contenido del **Procfile** generado automáticamente es:
```
    web: npm start
```
{: codeblock}

Para obtener más información sobre el archivo **Procfile** y **package.json**, consulte [Consejos para aplicaciones Node.js](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html).

## Consejos para ejecutar la aplicación Node.js de forma local
{: #hints}

Utilice esta información para facilitar la ejecución de la aplicación Node.js localmente y en Bluemix.

El ejemplo siguiente muestra parte de la fuente para un archivo **js**:
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

Con este código, cuando la aplicación se esté ejecutando en Bluemix, la variable de entorno PORT contiene el valor de puerto que es interno de Bluemix y en el que la app escucha conexiones entrantes. Cuando la aplicación se ejecuta localmente, PORT no está definido, de modo que se utiliza **3000** como número de puerto. Grabados de esta forma, puede ejecutar la aplicación localmente a efectos de prueba y en Bluemix sin realizar más cambios.

## Modo fuera de línea
{: #offline_mode}

Consulte [Modo fuera de línea](offlineMode.html) para ver información sobre el control del acceso al paquete de compilación a sitios externos. 

## App Management
{{site.data.keyword.Bluemix}} proporciona un número de programas de utilidad para gestionar y depurar la app de Node.js. Consulte [Gestión de app](/docs/manageapps/app_mng.html) para ver más detalles.   

## Versiones disponibles
{: #available_versions}

{{site.data.keyword.Bluemix}} proporciona todos los [modos de ejecución de Node.js
disponibles actualmente](http://nodejs.org/dist/). De esos, IBM proporciona versiones que contienen las mejoras y los arreglos de errores. Consulte [Últimas actualizaciones del paquete de compilación Node.js](/docs/runtimes/nodejs/updates.html) para obtener más información.

El paquete de compilación Node.js de IBM almacena en caché las versiones de tiempo de ejecución de IBM. Por este motivo, si utiliza IBM SDK para el tiempo de ejecución Node.js en la aplicación, obtiene el rendimiento de la aplicación más rápido si la aplicación se envía por push a Bluemix.

Utilice el parámetro **nodo** en la sección **motores** del archivo **package.json** para especificar la versión de tiempo de ejecución de Node.js que desee ejecutar.

Utilice el parámetro **npm** en la sección **motores** del archivo **package.json** si necesita especificar una versión de npm que no sea la versión empaquetada con Node.js.  

Consulte el siguiente ejemplo:

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "2.11.3"
  }
}
```
{: codeblock}

Debería especificarse siempre una versión de nodo en el archivo **package.json**. Si no, se utilizará la versión del nodo más reciente.

## Opciones de configuración
{: #configuration_options}

### Scripts NPM
{: #npm_scripts}
NPM proporciona un recurso de creación de scripts que le permite ejecutar scripts, incluidos los scripts **previos a la instalación** y **posteriores a la instalación** que se aplican antes y después de que estén instalados los node_modules.  Consulte [npm-scripts](https://docs.npmjs.com/misc/scripts) para obtener más detalles.

### Comportamiento de la memoria caché
{: #cache_behavior}
{{site.data.keyword.Bluemix}} mantiene un directorio de memoria caché por aplicación de nodo, que es persistente entre las compilaciones. La memoria caché almacena dependencias resueltas para que no se descargue ni se instale cada vez que se despliegue la app.  Por ejemplo, suponga que myapp depende de **express**.  A continuación, la primera vez que se despliegue myapp, se descargará el módulo **express**.  En los despliegues posteriores de myapp, se utilizará la instancia en memoria caché de **express**. El comportamiento predeterminado es almacenar en memoria caché todos los node_modules instalados por NPM y los bower_components instalados por bower.

Utilice la variable NODE_MODULES_CACHE para determinar si el paquete de compilación de nodos utiliza o no tiene en cuenta la memoria caché desde compilaciones anteriores. El valor predeterminado es true.  Para inhabilitar el almacenamiento en memoria caché del conjunto NODE_MODULES_CACHE en false, por ejemplo a través de la línea de mandatos de cf:
```
    $ cf set-env myapp NODE_MODULES_CACHE false
```
{: codeblock}

Tenga en cuenta que los node_modules que se incluyen en la aplicación no se almacenan en la memoria caché.

Puede utilizar una matriz **cacheDirectories** en el **package.json** de nivel superior para conseguir un control específico a través de los módulos que se almacenan en la memoria caché.  Cuando el elemento **cacheDirectories** ya se encuentra presente en el **package.json**, solo se almacenarán en la memoria caché los módulos que se encuentren en la matriz **cacheDirectories**.  En el ejemplo siguiente, solo se almacenan en la memoria caché los node_modules y bower_components.
```
{
  "cacheDirectories": ["node_modules","bower_components"],
  ...
}
```
{: codeblock}

### FIPS MODE
{: #fips_mode}

Las versiones del paquete de compilación de Nodejs v3.2-20160315-1257 y posteriores soportan [FIPS](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards).  Para utilizar el motor de nodos habilitado para FIPS, establezca la variable de entorno FIPS_MODE en true.
Por ejemplo:

```
    $ cf set-env myapp FIPS_MODE true
```
{: codeblock}

Es importante comprender que cuando FIPS_MODE es true algunos módulos de nodo pueden no funcionar.  Por ejemplo, **los módulos de nodo que utilizan [MD5](https://en.wikipedia.org/wiki/MD5) fallarán**, como por ejemplo [Express](http://expressjs.com/).  Para Express, el establecimiento de [etag](http://expressjs.com/en/api.html) en false en la app
Expess puede ayudar a solucionarlo. Por ejemplo, puede realizar lo siguiente en el código:
```
    app.set('etag', false);
```
{: codeblock}
Consulte esta [publicación de stackoverflow](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js)
para obtener más información.

**NOTA** [App Management](/docs/manageapps/app_mng.html) y FIPS_MODE *NO* están soportados simultáneamente.  Si se ha establecido la variable de entorno BLUEMIX_APP_MGMT_ENABLE y la variable de entorno FIPS_MODE se ha establecido en true, la app no se podrá transferir.

A continuación se muestran varios métodos para comprobar el estado de FIPS_MODE:
<ul>
<li> Puede comprobar staging_task.log para la aplicación para obtener un mensaje parecido al siguiente:
    

  <pre>
  Instalación de IBM SDK habilitado para FIPS para Node.js (4.4.3) desde la memoria caché
  </pre>
  {: codeblock}

Este mensaje indica que se está ejecutando un motor de node.js habilitado para FIPS pero no necesariamente que FIPS se está ejecutando
</li>

<li> Puede comprobar el valor de **process.versions.openssl**. Por ejemplo:

  <pre>
  console.log('ssl version is [' +process.versions.openssl +']');
  </pre>
  {: codeblock}

Si la versión SSL contiene "fips", la versión de SSL que está en uso da soporte a FIPS.  
</li>

<li> Para node.js versión 6 y posterior, puede comprobar el valor devuelto por crypto.fips en el código como el siguiente:

  <pre>
  console.log('crypto.fips== [' +crypto.fips +']');
  </pre>
  {: codeblock}

Si el valor devuelto es 1, FIPS está en uso. Tenga en cuenta que crypto.fips devolverá *undefined* para las versiones de node.js anteriores a 6.
</li>
</ul>

#### Nodejs v4
{: #nodejs_v4_fips}

La siguiente tabla explica el comportamiento de node.js v4 con FIPS:

|                 | Result        |
| :-------------- | :------------ |
|FIPS_MODE=true   |success (1)    |
|FIPS_MODE !=true |success (2)    |

* success (1)
  * FIPS está en uso.
  * staging_task.log incluirá el mensaje *Instalación de IBM SDK habilitado para FIPS para Node.js*.
  * El valor devuelto por process.versions.openssl incluirá "fips".
* success (2)
  * FIPS *NO* está en uso.
  * staging_task.log *NO* incluirá el mensaje *Instalación de IBM SDK habilitado para FIPS para Node.js*.
  * El valor devuelto por process.versions.openssl *NO* incluirá "fips".

#### Nodejs v6
{: #nodejs_v6_fips}

Para ejecutar en modalidad FIPS con Node.js versión 6 además de establecer **FIPS_MODE=true**, también debe incluir
**--enable-fips** en el mandato de inicio como en el siguiente ejemplo:
```
{
    ...   
    "scripts": {
      "start": "node --enable-fips app.js"
    }
}
```
{: codeblock}

La siguiente tabla explica el comportamiento de node.js v6 con FIPS.

|                 |--enable-fips  |NO --enable-fips |
| :-------------- | :------------ | :-------------- |
|FIPS_MODE=true   |success (1)    |success (2)      |
|FIPS_MODE !=true |failure (3)    |success (4)      |

* success (1)
  * FIPS está en uso.
  * staging_task.log incluirá el mensaje *Instalación de IBM SDK habilitado para FIPS para Node.js*.
  * El valor devuelto por process.versions.openssl incluirá "fips"
  * crypto.fips devolverá 1, lo que indica que FIPS está en uso
* success (2)
  * FIPS *NO* está en uso.
  * staging_task.log incluirá el mensaje *Instalación de IBM SDK habilitado para FIPS para Node.js*.
  * El valor devuelto por process.versions.openssl incluirá "fips"
  * crypto.fips devolverá 0, lo que indica que FIPS *NO* está en uso
* failure (3)
  * FIPS *NO* está en uso.
  * staging_task.log *NO* incluirá el mensaje *Instalación de IBM SDK habilitado para FIPS para Node.js*.
  * la transferencia fallará con el mensaje "ERR node: bad option: --enable-fips"
* success (4)
  * FIPS *NO* está en uso.
  * staging_task.log *NO* incluirá el mensaje *Instalación de IBM SDK habilitado para FIPS para Node.js*.
  * El valor devuelto por process.versions.openssl *NO* incluirá "fips"
  * crypto.fips devolverá 0, lo que indica que FIPS *NO* está en uso


## Paquetes de compilación Node.js

Bluemix proporciona varias versiones del paquete de compilación Node.js.
* El paquete de compilación **sdk-for-nodejs** creado por IBM es el paquete de compilación predeterminado que se utiliza para aplicaciones Node.js en Bluemix.
* **nodejs_buildpack** es un paquete de compilación de comunidad proporcionado por la comunidad de Cloud Foundry.

El paquete de compilación **sdk-for-nodejs** tendrá precedencia sobre el **nodejs_buildpack** en Bluemix. Si desea utilizar **nodejs_buildpack** con la aplicación en lugar del paquete de compilación **sdk-for-nodejs**, debe especificar el paquete de compilación, por ejemplo, utilizando la opción -b con el mandato **cf push**.

Normalmente, están disponibles el paquete de compilación **sdk-for-nodejs** actual y una versión de nivel anterior.  Para ver todos los paquetes de compilación disponibles, utilice el mandato **cf buildpacks**.  Por ejemplo:
<pre>
      cf buildpacks
      Getting buildpacks...

      buildpack                                 position   enabled   locked   filename   

      sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
      nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
      sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
</pre>
{: codeblock}

# rellinks
{: #rellinks}
## general
{: #general}
* [Últimas actualizaciones del paquete de compilación Node.js](/docs/runtimes/nodejs/updates.html)
* [App Management](/docs/manageapps/app_mng.html)
* [Node.js](https://nodejs.org)
* [IBM API Connect](https://strongloop.com/)
