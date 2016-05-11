---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Opciones para enviar aplicaciones Liberty
{: #options_for_pushing}

*Última actualización: 23 de marzo de 2016*

El comportamiento del servidor Liberty en Bluemix se controla mediante el paquete de compilación de Liberty. Los paquetes de compilación pueden ofrecer un entorno de tiempo de ejecución completo para una determinada clase de aplicaciones. Constituyen la clave para ofrecer portabilidad entre nubes y contribuir a una arquitectura de nube abierta. El paquete de compilación de Liberty proporciona un contenedor WebSphere Liberty capaz de ejecutar aplicaciones Java EE 7 y OSGi. Admite infraestructura extendidas, como Spring e incluye IBM JRE. WebSphere Liberty permite desarrollar rápidamente aplicaciones adaptadas a la nube. El paquete de compilación de Liberty da soporte a varias aplicaciones que se despliegan en un único servidor Liberty. Como parte de la integración del paquete de compilación de Liberty en Bluemix, el paquete de compilación garantiza que las variables de entorno para los servicios de enlace se muestran como variables de configuración en el servidor Liberty.

Puede utilizar los siguientes métodos para desplegar aplicaciones Liberty en Bluemix.

* Envío de una aplicación autónoma
* Envío por push de un directorio del servidor
* Envío por push de un servidor empaquetado

Importante: Cuando despliegue una aplicación con el paquete de compilación de Liberty, especifique un mínimo de 512 M como límite de memoria para las aplicaciones. Para obtener más información, consulte [Límites de memoria y el paquete de compilación de Liberty](memoryLimits.html).

## Apps autónomas
{: #stand_alone_apps}

Las aplicaciones autónomas, como los archivos WAR o EAR, se pueden desplegar en Liberty en Bluemix.

Para desplegar una aplicación autónoma, ejecute el mandato cf push con el parámetro -p que apunte al archivo WAR o EAR.
Por ejemplo:

```
    $ cf push <yourappname> -p myapp.war
```
{: #codeblock}

Cuando se despliega una aplicación autónoma, se proporciona una configuración predeterminada de Liberty para la aplicación. La configuración predeterminada activa las siguientes características de Liberty:

* beanValidation-1.1
* [cdi-1.2](optionsForPushing.html#cdi12)
* ejbLite-3.2
* el-3.0
* jaxrs-2.0
* jdbc-4.1
* jndi-1.0
* jpa-2.1
* jsf-2.2
* jsonp-1.0
* jsp-2.3
* managedBeans-1.0
* servlet-3.1
* websocket-1.1
* icap:managementConnector-1.0
* appstate-1.0

Estas características corresponden a las características de Java EE 7 Web Profile. Puede especificar un conjunto distinto de características de Liberty estableciendo la variable de entorno JBP_CONFIG_LIBERTY. Por ejemplo, para habilitar solo características de jsp-2.3 y websocket-1.1, ejecute el mandato y vuelva a transferir la aplicación:

```
    $ cf set-env myapp JBP_CONFIG_LIBERTY "app_archive: {features: [jsp-2.3, websocket-1.1]}"
```
{: #codeblock}

Nota: Para obtener los mejores resultados, establezca las características de Liberty con la variable de entorno JBP_CONFIG_LIBERTY o despliegue su aplicación como un [directorio de servidor](optionsForPushing.html#server_directory) o [servidor empaquetado](optionsForPushing.html#packaged_server) con un archivo server.xml personalizado. Setting this environment variable ensures that your application uses only the feature that it needs and it is not affected by the buildpack's default Liberty feature set changes. Si necesita proporcionar configuración adicional de Liberty más allá del conjunto de características, utilice el 					[directorio de servidor](optionsForPushing.html#server_directory) o la opción [servidor empaquetado](optionsForPushing.html#packaged_server) para desplegar su aplicación.

Si ha desplegado un archivo WAR, la aplicación web estará accesible bajo la raíz de contexto según lo establecido en el archivo ibm-web-ext.xml incorporado. Si el archivo ibm-web-ext.xml no existe, o no especifica la raíz de contexto, se puede acceder a la aplicación bajo el contexto raíz. Por ejemplo,

```
    http://<yourappname>.mybluemix.net/
```
{: #codeblock}

Si ha desplegado un archivo EAR, se puede acceder a la aplicación web incorporada bajo la raíz de contexto definida en el descriptor de despliegue de EAR. Por ejemplo,

```
    http://<yourappname>.mybluemix.net/acme/
```
{: #codeblock}

A continuación se muestra el archivo predeterminado de configuración de Liberty server.xml completo:
```
    <server>
       <featureManager>
          <feature>beanValidation-1.1</feature>
          <feature>cdi-1.2</feature>
          <feature>ejbLite-3.2</feature>
          <feature>el-3.0</feature>
          <feature>jaxrs-2.0</feature>
          <feature>jdbc-4.1</feature>
          <feature>jndi-1.0</feature>
          <feature>jpa-2.1</feature>
          <feature>jsf-2.2</feature>
          <feature>jsonp-1.0</feature>
          <feature>jsp-2.3</feature>
          <feature>managedBeans-1.0</feature>
          <feature>servlet-3.1</feature>
          <feature>websocket-1.1</feature>
          <feature>icap:managementConnector-1.0</feature>
          <feature>appstate-1.0</feature>
       </featureManager>

       <application name='myapp' location='myapp.war' type='war' context-root='/'/>
       <httpEndpoint id='defaultHttpEndpoint' host='*' httpPort='${port}'/>
       <webContainer trustHostHeaderPort='true' extractHostHeaderPort='true'/>
       <include location='runtime-vars.xml'/>
       <logging logDirectory='${application.log.dir}' consoleLogLevel='INFO'/>
       <httpDispatcher enableWelcomePage='false'/>
       <applicationMonitor dropinsEnabled='false' updateTrigger='mbean'/>
       <config updateTrigger='mbean'/>
       <cdi12 enableImplicitBeanArchives='false'/>
       <appstate appName='myapp' markerPath='${home}/../.liberty.state'/>
    </server>
```
{: #codeblock}

### CDI 1.2
{: #cdi12}

Por razones del rendimiento, al desplegar únicamente los archivos WAR y EAR, la [exploración de archivos de beans implícita de CDI 1.2](https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_cdi_behavior.html) está inhabilitado de forma predeterminada. La exploración de archivos de beans implícito puede habilitarse utilizando la variable de entorno JBP_CONFIG_LIBERTY.
Por ejemplo:

```
    $ cf set-env myapp JBP_CONFIG_LIBERTY "app_archive: { implicit_cdi: true }"
```    
{: #codeblock}

Importante: Para que los cambios en las variables de entorno de su entorno se hagan efectivos, debe volver a transferir su aplicación:

```
    $ cf restage myapp
```
{: #codeblock}

## Directorio de servidor
{: #server_directory}

En algunos casos, puede resultar necesario proporcionar una configuración personalizada del servidor Liberty con la aplicación. Esta configuración personalizada puede ser necesaria al desplegar un archivo WAR o EAR y el archivo server.xml predeterminado no tiene los valores determinados que necesita su aplicación.

Si ha instalado el perfil de Liberty en la estación de trabajo y ya ha creado un servidor Liberty con la aplicación, puede enviar por push el contenido de dicho directorio a Bluemix.
Por ejemplo, su el servidor Liberty se denomina defaultServer, ejecute el mandato:

```
    $ cf push <yourappname> -p wlp/usr/servers/defaultServer
```
{: #codeblock}

Si un perfil de Liberty no está instalado en la estación de trabajo, puede utilizar los pasos siguientes para crear un directorio del servidor con la aplicación:

1. Cree un directorio llamado defaultServer.
2. Cree un directorio apps en el directorio defaultServer.
3. Copie el archivo WAR o EAR en el directorio defaultServer/apps.
4. En el directorio defaultServer, cree un archivo server.xml con el siguiente contenido de ejemplo.  Además:
  * Asegúrese de actualizar el atributo location o type del elemento de la aplicación para que coincida con el nombre de archivo y el tipo de la aplicación.
  * El archivo server.xml del diagrama muestra un conjunto de características mínimas. Es posible que tenga que ajustar el conjunto de características en función de los requisitos de la aplicación.

```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
        </featureManager>

        <httpEndpoint id="defaultHttpEndpoint" host="*" httpPort="8080" />

        <application name="myapp" context-root="/" type="war" location="myapp.war"/>
    </server>
```
{: #codeblock}

Cuando el directorio del servidor esté listo, puede desplegarlo en Bluemix.

```
    $ cf push <yourappname> -p defaultServer
```
{: #codeblock}

Nota: Se puede acceder a las aplicaciones web desplegadas como parte del directorio del servidor bajo la [raíz de contexto, tal como determina el perfil de Liberty](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/twlp_dep_war.html?cp=SSAW57_8.5.5%2F1-3-11-0-5-6). Por ejemplo:

```
    http://<yourappname>.mybluemix.net/acme/
```
{: #codeblock}

## Servidor empaquetado
{: #packaged_server}

Puede enviar por push un archivo del servidor empaquetado a Bluemix. El archivo del servidor empaquetado se crea mediante el mandato server package de Liberty. Además de los archivos de la aplicación y de configuración, el archivo del servidor empaquetado puede contener recursos compartidos y las características de usuario de Liberty que necesita la aplicación.

Para empaquetar un servidor Liberty, utilice el mandato ./bin/server package desde el directorio de instalación de Liberty. Especifique el nombre del servidor e incluya la opción '––include=usr'.
Por ejemplo, si el servidor Liberty es defaultServer, ejecute el mandato:

```
    $ wlp/bin/server package defaultServer --include=usr
```
{: #codeblock}

Este mandato genera un archivo serverName.zip en el directorio del servidor. Luego puede enviar por push este archivo comprimido a Bluemix con el mandato cf push.
Por ejemplo:

```
    $ cf push <yourappname> -p wlp/usr/servers/defaultServer/defaultServer.zip
```
{: #codeblock}

Nota: Se puede acceder a las aplicaciones web desplegadas como parte del servidor empaquetado bajo la raíz de contexto, tal como determina el perfil de Liberty.

### Modificación del archivo server.xml
{: #modifications_of_serverxml}

Cuando se envía un servidor empaquetado o un directorio del servidor Liberty, el paquete de compilación de Liberty detecta el archivo server.xml junto con la aplicación. El paquete de compilación de Liberty realiza las siguientes modificaciones en el archivo server.xml.

* El paquete de compilación se asegura de que haya exactamente un elemento httpEndpoint en el archivo.
* El paquete de compilación se asegura de que el atributo httpPort del elemento httpEndpoint apunte a una variable del sistema llamada ${port}. El paquete de compilación también sustituye el atributo host.
* El paquete de compilación establece el atributo logDirectory en el elemento logging de modo que apunte a un directorio de registro del sistema.
* El paquete de compilación se asegura de que un archivo runtime-vars.xml se fusione de forma lógica con el archivo server.xml. En concreto, el paquete de compilación añade la línea *&lt;include location="runtime-vars.xml" /&gt;* al archivo server.xml.

### Variables a las que se puede hacer referencia
{: #referenceable_variables}

Las siguientes variables están definidas en el archivo runtime-vars.xml y se hace referencia a las mismas desde un archivo server.xml enviado. Todas las variables son sensibles a mayúsculas y minúsculas.

* ${port}: el puerto HTTP en el que escucha el servidor Liberty.
* ${vcap_console_port}: el puerto en el que se ejecuta la consola vcap (suele coincidir con ${port}).
* ${vcap_app_port}: el puerto en el que escucha el servidor de app (suele coincidir con ${port}).
* ${vcap_console_ip}: la dirección IP de la consola vcap (suele ser la dirección IP en la que escucha el servidor Liberty).
* ${application_name}: el nombre de la aplicación, que se define mediante las opciones del mandato cf push.
* ${application_version}: la versión de esta instancia de la aplicación, que tiene el formato de un UUID, como por ejemplo b687ea75-49f0-456e-b69d-e36e8a854caa. Esta variable cambia con cada envío sucesivo de la aplicación que contiene código nuevo o cambios en los artefactos de la aplicación.
* ${host}: la dirección IP del DEA que está ejecutando la aplicación (suele coincidir con ${vcap_console_ip}).
* ${application_uris}: una matriz de tipo JSON de puntos finales que se puede utilizar para acceder a esta aplicación; por ejemplo: myapp.mydomain.com.
* ${start}: la fecha y hora en que se ha iniciado la aplicación, con un formato parecido al siguiente: 2013-08-22 10:10:18 -0400.

### Acceso a la información de los servicios enlazados
{: #accessing_info_of_bound_services}

Cuando desee enlazar un servicio con la aplicación, se incluirá información acerca del servicio, como por ejemplo las credenciales de conexión, en la [variable de entorno VCAP_SERVICES](http://docs.run.pivotal.io/devguide/deploy-apps/environment-variable.html#VCAP-SERVICES) que
				Cloud Foundry establece para la aplicación. Para [servicios configurados automáticamente](autoConfig.html), el paquete de compilación de Liberty generará o
				actualizará entradas de enlace de servicios en el archivo server.xml. El contenido de las entradas de enlace de servicio
				puede estar en una de las formas siguientes:

* cloud.services.&lt;service-name&gt;.&lt;property&gt;, que describe la información como nombre, tipo y plan del servicio.
* cloud.services.&lt;service-name&gt;.connection.&lt;property&gt;, que describe la información de conexión para el servicio.

El conjunto de información típico es el siguiente:
* name: el nombre del servicio. Por ejemplo, mysql-e3abd.
label: el tipo de servicio creado. Por ejemplo, mysql-5.5.
* plan: el plan del servicio, indicado por el identificador exclusivo del plan. Por ejemplo, 100.
connection.name: identificador exclusivo de la conexión, que adopta el formato de UUID. Por ejemplo, d01af3a5fabeb4d45bb321fe114d652ee.
* connection.hostname: nombre de host del servidor que ejecuta el servicio. Por ejemplo, mysql-server.mydomain.com.
* connection.host: la dirección IP del servidor que ejecuta el servicio. Por ejemplo, 9.37.193.2.
* connection.port: el puerto en el que el servicio está a la escucha de conexiones entrantes. Por ejemplo, 3306,3307.
* connection.user: el nombre de usuario que se utiliza para autenticar esta aplicación ante el servicio. Cloud Foundry genera automáticamente el nombre de usuario. Por ejemplo: unHwANpjAG5wT.
* connection.username: alias de connection.user.
* connection.password: la contraseña que se utiliza para autenticar esta aplicación ante el servicio. Cloud Foundry genera automáticamente la contraseña. Por ejemplo: pvyCY0YzX9pu5.

Para los servicios enlazados que el paquete de compilación de Liberty no configura automáticamente, la aplicación tiene que gestionar por su cuenta el acceso del recurso de fondo.

# rellinks
## general
* [Tiempo de ejecución de Liberty](index.html)
* [Visión general del perfil de Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
