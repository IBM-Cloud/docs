---

copyright:
  years: 2015, 2016
lastupdated: "2016-12-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Gestión de Liberty y Node.js
{: #app_management}


App Management es un conjunto de programas de utilidad de desarrollo y depuración que se pueden habilitar en las apps Liberty y Node.js para {{site.data.keyword.Bluemix}}.
{:shortdesc}

## Programas de utilidad App Management
{: #Utilities}

### Estos programas de utilidad admiten Liberty y Node.js
{: #liberty_and_node_utilities}

#### proxy
{: #proxy}

El *proxy* proporciona la gestión de aplicaciones mínima entre la aplicación y {{site.data.keyword.Bluemix_notm}}.

Cuando esta opción está habilitada, el paquete de compilación inicia un agente de proxy que se encuentra entre el contenedor y el tiempo de ejecución de la app. El programa de utilidad *proxy* gestiona todas las solicitudes que recibe la app. En función del tipo de solicitud, realiza una acción de App Management o reenvía la solicitud a la app. *proxy* permite la habilitación de la mayoría de los programas de utilidad de App Management. Al habilitar *proxy*, el contenedor de la app sigue en funcionamiento aunque la app se cuelga. El agente de proxy también permite las actualizaciones incrementales de archivos, que habilitan el modo "Live Edit" para las apps Node.js.

#### devconsole
{: #devconsole}

El programa de utilidad de la consola de desarrollo (*devconsole*) es accesible en el siguiente URL:
```
  http://<nombreapp>.mybluemix.net/bluemix-debug/manage
```

Con la consola de desarrollo, los usuarios pueden reiniciar, detener o suspender sus apps. Los usuarios también pueden habilitar o acceder al shell y a los programas de utilidad de inspección.

Para Node versión 6.3.0 o posterior, la consola de desarrollo proporciona un botón de reinicio para la aplicación y el acceso al programa de utilidad de shell. Consulte el debate de *inspector* para obtener más información.

El programa de utilidad devconsole también inicia *proxy*.

#### hc
{: #hc}

El agente de Health Center (*hc*) permite que su app se supervise con el cliente de Health Center.

Health Center admite el análisis del rendimiento de las apps Liberty y Node.js mediante las herramientas de diagnóstico y supervisión de IBM. Para obtener más información, consulte [Cómo analizar el rendimiento de las apps Liberty Java o Node.js en {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){:new_window}.</p></li>

#### shell
{: #shell}

El programa de utilidad *shell* permite un shell basado en web. Se puede acceder a él desde el programa de utilidad *devconsole* o accediendo al siguiente URL:

```
  http://<nombre_app>.mybluemix.net/bluemix-debug/shell
```

Se muestra una ventana de terminal con acceso de shell en la app después de acceder al programa de utilidad del *shell*. Puede hacer todo lo que esté admitido en un shell normal, como por ejemplo editar archivos, comprobar el uso de memoria o ejecutar mandatos de diagnóstico.

El programa de utilidad *shell* también inicia *proxy*.

### Estos programas de utilidad solo admiten Liberty
{: #liberty_utilities}

#### debug
{: #debug}

El programa de utilidad *debug* pone la app Liberty en modalidad de depuración y permite que los clientes como IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} establezcan una sesión de depuración remota con la app.

Para obtener más información, consulte [Depuración remota](/docs/manageapps/eclipsetools/eclipsetools.html#remotedebug).

El programa de utilidad *debug* también inicia *proxy*.

#### jmx
{: #jmx}

El programa de utilidad *jmx* permite al conector JMX REST permitir que un cliente JMX remoto gestione la app mediante las credenciales de usuario de {{site.data.keyword.Bluemix_notm}}.

Para obtener más información sobre la configuración de un conector JMX, consulte [Configuración de una conexión JMX segura con el perfil de Liberty](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}.

El programa de utilidad *jmx* no inicia el proxy.

### Estos programas de utilidad solo admiten Node.js
{: #node_utilities}

#### inspector
{: #inspector}

Para las versiones de Node.js anteriores a la 6.3.0, *inspector* habilita la interfaz del depurador del inspector de nodos, accesible desde el programa de utilidad *devconsole* o en *https://myApp.mybluemix.net/bluemix-debug/inspector.*

El proceso del *inspector* se ejecuta en el contenedor de la app. Utilice este programa de utilidad para crear perfiles de uso de CPU, añadir puntos de interrupción y depurar código, todo mientras la app se ejecuta en {{site.data.keyword.Bluemix_notm}}. Para obtener más información sobre el módulo del inspector de nodos, consulte [node-inspector en GitHub](https://github.com/node-inspector/node-inspector){:new_window}.

El programa de utilidad *inspector* también inicia *proxy*.

Para Node.js versiones 6.3.0 y posteriores, el *inspector* utiliza el [V8 Inspector Integration for Node.js](https://nodejs.org/dist/latest-v6.x/docs/api/debugger.html#debugger_v8_inspector_integration_for_node_js){:new_window}. En los registros de la app, encontrará un URL que se puede utilizar para adjuntar Chrome DevTools a la app. Los mensajes de registro serán similares a los siguientes:

```
  2016-11-30T16:40:56.03-0500 [APP/0]      OUT Starting app with 'node-hc --inspect=9229  app.js '
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR Debugger listening on port 9229.
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR To start debugging, open the following URL in Chrome:
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR     chrome-devtools://devtools/remote/serve_file...
```

La *devconsole* **no** mostrará un enlace al *inspector* en este caso de ejemplo, porque el URL no existe.

El *proxy* no direccionará el tráfico al *inspector* en este caso de ejemplo. Necesitará crear un túnel SSH para la app para que funcione el URL de Chrome DevTools. Para crear el túnel SSH, utilice el mandato 'cf ssh' en un modo similar al siguiente:

```
  cf ssh -N -T -L <port>:127.0.0.1:<hostport> <appName>
```

En este mandato, *hostport* debe ser el valor de puerto desde el mensaje de registro "Debugger listening on port xxxx", y *port* es cualquier puerto disponible en el sistema desde el que se emite el mandato "cf ssh".

#### trace
{: #trace}

El programa de utilidad *trace* le permite establecer dinámicamente niveles de rastreo si la app utiliza módulos de registro *log4js*, *ibmbluemix* o *bunyan*.

**Nota:** Versiones de dependencia admitidas:
* log4js:(0.6.0 - 0.6.24)
* bunyan: (1.0.0, 1.0.1, 1.1.0 - 1.1.3, 1.2.0 - 1.2.3, 1.3.0 - 1.3.5)
* ibmbluemix: (1.0.0-20140707-1250)-(1.0.0-20150409-1328)

Vaya a la página Detalles de instancia en la consola web de {{site.data.keyword.Bluemix_notm}} y seleccione **Acciones** para ver la interfaz de usuario.

La utilidad de *rastreo* no está disponible si la aplicación se ha iniciado utilizando la opción "-b buildpack".

El programa de utilidad *trace* no inicia *proxy*.

##  Cómo configurar App Management
{: #configure}

Para habilitar las utilidades de App Management, defina la variable de entorno *BLUEMIX_APP_MGMT_ENABLE* y reinicie su app. Se pueden habilitar múltiples utilidades al separar con “+”.

Por ejemplo, para habilitar los programas de utilidad *devconsole* y *shell*, ejecute el siguiente mandato:

```
cf set-env myApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

Vuelva a transferir la app después de establecer la variable de entorno:

```
cf restage myApp
```

Si no desea que los programas de utilidad App Management se instalen con la app, establezca la variable de entorno
*BLUEMIX_APP_MGMT_INSTALL* en 'false' y vuelva a transferir la app.

Por ejemplo:

```
cf set-env myApp BLUEMIX_APP_MGMT_INSTALL false
cf restage myApp
```

## Restricciones
{: #restrictions}

* App Management solo admite apps de instancias individuales.
* Los cambios que realice en la app utilizando App Management son transitorios y se perderán al salir de esta modalidad. Esta modalidad es solo para uso de desarrollo temporal, y no está concebida para su uso como entorno de producción debido a su rendimiento.
* La mayoría de los programas de utilidad de App Management no funcionan si establece el mandato de inicio en el archivo manifest.yml (mandato) o CF CLI (-c). Dichos métodos son alteraciones temporales de paquetes de compilación y son antipatrones para iniciar apps Node.js. Para obtener los mejores resultados, establezca el mandato de inicio en el archivo package.json o Procfile.

## Modalidad de desarrollo de Eclipse Tools
{: #devmode}

La modalidad de desarrollo es una característica de [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools) que proporciona a los desarrolladores la posibilidad de trabajar con sus apps mientras se ejecutan en la nube.

Mientras están trabajando con sus apps en {{site.data.keyword.Bluemix_notm}}, es posible que los desarrolladores tengan la sensación de que no pueden realizar actividades de desarrollo normales como lo harían en un entorno local. Para afrontar este problema, la modalidad de desarrollo mediante Eclipse Tools proporciona una forma de trabajar en la nube estando en un espacio de trabajo seguro y temporal.

La modalidad de desarrollo está admitida tanto en las apps Liberty como Node.js. Con la modalidad de desarrollo habilitada en su app Liberty o Node.js, puede actualizar los archivos de la app incrementalmente sin necesidad de volver a enviar por push la app. También puede establecer una sesión de depuración de errores con su app. La modalidad de desarrollo para apps Liberty equivale a habilitar las utilidades de App Management de depuración y jmx. En las apps Node.js, equivale a habilitar los programas de utilidad *devconsole*, *inspector* y *shell*.
