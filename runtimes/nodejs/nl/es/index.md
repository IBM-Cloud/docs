{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*Última actualización: 12 de enero de 2016*

# Tiempo de ejecución de Node.js
{: #nodejs_runtime}

El tiempo de ejecución de Node.js en {{site.data.keyword.Bluemix}} está basado en el paquete de compilación de sdk-for-nodejs.
El paquete de compilación sdk-for-nodejs proporciona un entorno de ejecución completo para las aplicaciones de Node.js.
{: shortdesc}

El paquete de compilación Node.js se utiliza cuando la aplicación contiene un archivo **package.json** en el directorio raíz.

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona aplicaciones de inicio Node.js. La aplicación de inicio Node.js es una aplicación Node.js sencilla que proporciona una plantilla que puede utilizar para la aplicación. Puede experimentar con la aplicación de iniciador, y realizar y enviar por push los cambios al entorno de Bluemix. Consulte [Utilización de las aplicaciones de iniciador](../../cfapps/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de iniciador.

## Mandato de inicio
{: #starup_commmand}

Las formas recomendadas para especificar un mandato de inicio para la aplicación Bluemix Node.js son utilizar un **Procfile** o un archivo **package.json**.

Especifique un mandato de inicio en **Procfile** de la forma que se indica a continuación. Aquí, app.js es el script js de inicio de la aplicación.
```
web: node app.js
```
{: codeblock}

Guarde **Procfile** en el directorio raíz de la aplicación.

Si no está presente un **Procfile**, el paquete de compilación IBM Bluemix Node.js comprobará si existe una entrada scripts.start en el archivo **package.json**. De nuevo, en el siguiente ejemplo app.js es el script js de inicio de la aplicación.
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

Para obtener más información sobre **Procfile** y el archivo **package.json**, consulte los [consejos para las aplicaciones Node.js](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html).

## Consejos para ejecutar la aplicación Node.js de forma local
{: #hints}

Utilice esta información para facilitar la ejecución de la aplicación Node.js de forma local y en Bluemix.

El ejemplo siguiente muestra parte del origen del archivo **js**:
```
var port = (process.env.VCAP_APP_PORT || 3000);
var host = (process.env.VCAP_APP_HOST || 'localhost');
```
{: codeblock}

Con este código, cuando la aplicación se ejecuta en Bluemix, las variables de entorno VCAP_APP_HOST y VCAP_APP_PORT contienen los valores de host y puerto que son internos a Bluemix, y en los que la app está a la escucha para conexiones entrantes. Cuando la aplicación se ejecuta localmente, VCAP_APP_HOST y VCAP_APP_PORT no están definidos, por lo que se utiliza **localhost** como el host y **3000** se utiliza como el número de puerto. Escrito de este modo, puede ejecutar la aplicación localmente para fines de prueba y en Bluemix sin efectuar más cambios.

## App Management
{{site.data.keyword.Bluemix}} proporciona un número de programas de utilidad para gestionar y depurar la app Node.js. Consulte [App Management](../../manageapps/app_mng.html) para obtener más detalles.

## Versiones disponibles
{: #available_versions}

{{site.data.keyword.Bluemix}} proporciona todos los [modos de ejecución de Node.js
disponibles actualmente](http://nodejs.org/dist/). De estos, IBM proporciona versiones que contienen mejoras y arreglos para errores. Consulte [Últimas actualizaciones del paquete de compilación Node.js](updates.html) para obtener más información.

El paquete de compilación IBM Node.js almacena en caché todas las versiones de tiempo de ejecución de IBM. Por consiguiente, si utiliza IBM SDK para el tiempo de ejecución de Node.js en la aplicación, el rendimiento de la aplicación es más rápido cuando envía por push la aplicación a Bluemix.

Utilice el parámetro **node** de la sección **engines** del archivo **package.json** para especificar la versión de tiempo de ejecución de Node.js que desea ejecutar.

Utilice el parámetro **npm** de la sección **engines** del archivo **package.json** si debe especificar una versión de npm distinta a la versión empaquetada con Node.js.  

Consulte el ejemplo siguiente:

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4"
     "npm": "2.11.3"
  }
}
```
{: codeblock}

Siempre debe especificar una versión de nodo en el archivo **package.json**. De lo contrario, se utilizará la versión más reciente del nodo.

## Opciones de configuración
{: #configuration_options}

### Scripts de NPM
{: #npm_scripts}
NPM proporciona un recurso de script que le permite ejecutar scripts, incluidos los scripts **preinstall** y **postinstall**, que se aplican antes y después de que se instalen los node_modules. Consulte [npm-scripts](https://docs.npmjs.com/misc/scripts) para obtener más detalles.

### Comportamiento de la memoria caché
{: #cache_behavior}
{{site.data.keyword.Bluemix}} mantiene un directorio de memoria caché por aplicación de nodo, que es persistente entre compilaciones. La memoria caché almacena dependencias resueltas, por lo que no se descargan ni instalan cada vez que se despliega la app. Por ejemplo, suponga que myapp depende de **express**. Así, la primera vez que se despliega myapp, se descargará el módulo **expess**. En despliegues posteriores de myapp, se utilizará la instancia almacenada en caché de **express**.

Utilice la variable NODE_MODULES_CACHE para determinar si el paquete de compilación de Nodos utiliza u omite la memoria caché de compilaciones anteriores. El valor predeterminado es true. Para inhabilitar almacenar en memoria caché el conjunto NODE_MODULES_CACHE en false, por ejemplo mediante la línea de mandatos de cf:
```
cf set-env myapp NODE_MODULES_CACHE false
```
{: codeblock}

Tenga en cuenta que los node_modules que están incluidos en la aplicación no se almacenan en la memoria caché.

Puede utilizar una matriz **cacheDirectories** en el **package.json** de nivel superior para conseguir un control detallado sobre qué módulos se almacenan en la memoria caché. Cuando el elemento **cacheDirectories** está presente en **package.json**, sólo se almacenarán en la memoria caché los módulos que se encuentran en la matriz **cacheDirectories**. En el ejemplo siguiente, sólo se almacenan en memoria caché node_modules y bower_components.
```
{
  "cacheDirectories": ["node_modules","bower_components"],
  ...
}
```
{: codeblock}

## Paquetes de compilación de Node.js

Bluemix proporciona varias versiones del paquete de compilación Node.js.
* El paquete de compilación **sdk-for-nodejs** creado por IBM es el paquete de compilación predeterminado que se utiliza para las aplicaciones Node.js en Bluemix.
* **nodejs_buildpack** es el paquete de compilación externo proporcionado por la comunidad Cloud Foundry.

El paquete de compilación **sdk-for-nodejs** tiene prioridad sobre **nodejs_buildpack** en Bluemix. Si desea utilizar **nodejs_buildpack** con la aplicación en vez del paquete de compilación **sdk-for-nodejs**, debe especificar el paquete de compilación, por ejemplo, utilizando la opción -b con el mandato **cf push**.

Normalmente, estarán disponibles el paquete de compilación **sdk-for-nodejs** actual y una versión de nivel anterior. Para ver todos los paquetes de compilación disponibles, utilice el mandato **cf buildpacks**. Por ejemplo:
```
cf buildpacks
Getting buildpacks...

buildpack                      position          enabled          locked          filename   
...
sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
```
{: codeblock}


## ENLACES RELACIONADOS
{: #related_links}
* [Últimas actualizaciones del paquete de compilación Node.js](updates.html)
* [App Management](../../manageapps/app_mng.html)
* [Node.js](https://nodejs.org)
* [StrongLoop](https://strongloop.com)
