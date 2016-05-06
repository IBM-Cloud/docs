---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Gestión de Liberty y Node.js
{: #app_management}

*Última actualización: 17 de marzo de 2016*

App Management es un conjunto de programas de utilidad de desarrollo y depuración que se pueden habilitar en las apps Liberty y Node.js para {{site.data.keyword.Bluemix}}.
{:shortdesc}

##Programas de utilidad App Management
{: #Utilities}

Estos programas de utilidad admiten Liberty y Node.js.

  1. *proxy*: Gestión de apps mínima que sirve como proxy entre la app y {{site.data.keyword.Bluemix_notm}}.

    Cuando esta opción está habilitada, el paquete de compilación inicia un agente de proxy que se encuentra entre el contenedor y el tiempo de ejecución de la app. El programa de utilidad *proxy* gestiona todas las solicitudes que recibe la app. En función del tipo de solicitud, realiza una acción de App Management o reenvía la solicitud a la app. *proxy* permite la habilitación de la mayoría de los programas de utilidad de App Management. Al habilitar *proxy*, el contenedor de la app sigue en funcionamiento aunque la app se cuelga. El agente de proxy también permite las actualizaciones incrementales de archivos, que habilitan el modo "Live Edit" para las apps Node.js.
	
  2. *devconsole*: Habilita el programa de utilidad de la consola de desarrollo, accesible en el siguiente URL:
    ```
    http://<nombreapp>.mybluemix.net/bluemix-debug/manage
    ```
	
    Con la consola de desarrollo, los usuarios pueden reiniciar, detener o suspender sus apps. Los usuarios también pueden habilitar o acceder al shell y a los programas de utilidad de inspección.

    El programa de utilidad devconsole también inicia *proxy*.
	
  3. *hc*: Agente de Health Center que permite que su app se supervise con el cliente de Health Center.

    Health Center admite el análisis del rendimiento de las apps Liberty y Node.js mediante las herramientas de diagnóstico y supervisión de IBM. Para obtener más información, consulte [Cómo analizar el rendimiento de las apps Liberty Java o Node.js en {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){:new_window}.</p></li>
	
  4. *shell*: Habilita un shell basado en web al que se puede acceder desde el programa de utilidad devconsole o desde el siguiente URL:
    ```
    http://<nombre_app>.mybluemix.net/bluemix-debug/shell
    ```
	
    Se muestra una ventana de terminal con acceso de shell en la app después de acceder al programa de utilidad del shell. Puede hacer todo lo que esté admitido en un shell normal, como por ejemplo editar archivos, comprobar el uso de memoria o ejecutar mandatos de diagnóstico.
	
    El programa de utilidad *shell* también inicia *proxy*.

Estos programas de utilidad solo admiten Liberty.

  1. *debug*: Habilita la app Liberty en modalidad de depuración y permite que los clientes como IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} establezcan una sesión de depuración remota con la app.
  
   Para obtener más información, consulte [Depuración remota](../manageapps/eclipsetools/eclipsetools.html#remotedebug).
   
   El programa de utilidad *debug* también inicia *proxy*.
   
  2. *jmx*: Habilita el conector JMX REST para permitir que un cliente JMX remoto gestione la app mediante las credenciales de usuario de {{site.data.keyword.Bluemix_notm}}.
  
  Para obtener más información sobre la configuración de un conector JMX, consulte [Configuración de una conexión JMX segura con el perfil de Liberty](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}.
  
  El programa de utilidad *jmx* no inicia el proxy.

Estos programas de utilidad solo admiten Node.js.

  1. *inspector*: Habilita la interfaz del depurador del inspector de nodos, accesible desde el programa de utilidad *devconsole* o en *https://myApp.mybluemix.net/bluemix-debug/inspector.*
  
  El proceso del inspector se ejecuta en el contenedor de la app. Utilice este programa de utilidad para crear perfiles de uso de CPU, añadir puntos de interrupción y depurar código, todo mientras la app se ejecuta en {{site.data.keyword.Bluemix_notm}}. Para obtener más información sobre el módulo del inspector de nodos, consulte [node-inspector en GitHub](https://github.com/node-inspector/node-inspector){:new_window}.
  
  El programa de utilidad *inspector* también inicia *proxy*.
  
  2. *strongpm*: Habilita el uso de [StrongLoop Arc](https://strongloop.com/node-js/arc){:new_window} para analizar la app Node.js con programas de utilidad tales como [StrongLoop Metrics, Profiling y Tracing](https://strongloop.com/node-js/devops-tools/){:new_window}.
    
  El programa de utilidad *strongpm* también inicia *proxy*.
  
  Lleve a cabo los pasos siguientes para configurar la app Node.js con [StrongLoop Arco](https://strongloop.com/node-js/arc){:new_window}.

    1. Configure la variable de entorno *strongpm* BlUEMIX_APP_MGMT_ENABLE y vuelva a transferir la app.
    
	```
    cf set-env <appname> BLUEMIX_APP_MGMT_ENABLE strongpm
    cf restage <appname>
    ```
	
    2. Desde la línea de mandatos de Cloud Foundry, añada una ruta a la app donde la ruta tenga adjunto "-pm" al nombre de la app, como por ejemplo, <nombreapp>-pm.mybluemix.net.
    
	```
    cf map-route <appname> ng.bluemix.net -n <appname>-pm
    ```
	
    3. Instale el [módulo StrongLoop npm](https://www.npmjs.com/package/strongloop){:new_window} en su estación de trabajo local.
    
	```
    npm install -g strongloop
    ```
	
    4. Cree una cuenta en el [sitio web de StrongLoop](https://strongloop.com/register/){:new_window}.
    5. Inicie Arco en su estación de trabajo local e inicie sesión con la cuenta que ha creado.
    
	```
    slc arc
    ```
	
    6. Vaya a la vista Gestor de procesos en Arc. Indique la ruta recién creada con el puerto 80 en el Gestor de procesos. Pulse el botón Activar. Consulte la [documentación completa sobre cómo utilizar Arc](https://docs.strongloop.com/display){:new_window} para obtener más detalles.
	
  3. *trace*: Establece dinámicamente niveles de rastreo si la app utiliza módulos de registro *log4js*, *ibmbluemix* o *bunyan*.
  
  **Nota:** Versiones de dependencia admitidas:

    * log4js:(0.6.0 - 0.6.24)
    * bunyan: (1.0.0, 1.0.1, 1.1.0 - 1.1.3, 1.2.0 - 1.2.3, 1.3.0 - 1.3.5)
    * ibmbluemix: (1.0.0-20140707-1250)-(1.0.0-20150409-1328)
  
  Vaya a la página Detalles de instancia en la consola web de {{site.data.keyword.Bluemix_notm}} y seleccione **Acciones** para ver la interfaz de usuario.

  El programa de utilidad *trace* no inicia *proxy*.

##Cómo configurar App Management
{: #configure}

Para habilitar las utilidades de App Management, defina la variable de entorno *BLUEMIX_APP_MGMT_ENABLE* y reinicie su app. Se pueden habilitar múltiples utilidades al separar con “+”.

Por ejemplo, para habilitar los programas de utilidad devconsole y *shell*, ejecute el siguiente mandato:

```
cf set-env myApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

No se olvide de volver a transferir la app después de establecer la variable de entorno:

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

##Restricciones
{: #restrictions}

* App Management solo admite apps de instancias individuales.
* Los cambios que realice en la app utilizando App Management son transitorios y se perderán al salir de esta modalidad. Esta modalidad es solo para uso de desarrollo temporal, y no está concebida para su uso como entorno de producción debido a su rendimiento.
* La mayoría de los programas de utilidad de App Management no funcionan si establece el mandato de inicio en el archivo manifest.yml (mandato) o CF CLI (-c). Dichos métodos son alteraciones temporales de paquetes de compilación y son antipatrones para iniciar apps Node.js. Para obtener los mejores resultados, establezca el mandato de inicio en el archivo package.json o Procfile.

##Modalidad de desarrollo de Eclipse Tools
{: #devmode}

La modalidad de desarrollo es una característica de [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](../manageapps/eclipsetools/eclipsetools.html#eclipsetools) que proporciona a los desarrolladores la posibilidad de trabajar con sus apps mientras se ejecutan en la nube.

Mientras están trabajando con sus apps en {{site.data.keyword.Bluemix_notm}}, es posible que los desarrolladores tengan la sensación de que no pueden realizar actividades de desarrollo normales como lo harían en un entorno local. Para afrontar este problema, la modalidad de desarrollo mediante Eclipse Tools proporciona una forma de trabajar en la nube estando en un espacio de trabajo seguro y temporal.

La modalidad de desarrollo está admitida tanto en las apps Liberty como Node.js. Con la modalidad de desarrollo habilitada en su app Liberty o Node.js, puede actualizar los archivos de la app incrementalmente sin necesidad de volver a enviar por push la app. También puede establecer una sesión de depuración de errores con su app. La modalidad de desarrollo para apps Liberty equivale a habilitar las utilidades de App Management de depuración y jmx. En las apps Node.js, equivale a habilitar los programas de utilidad *devconsole*, *inspector* y *shell*.
