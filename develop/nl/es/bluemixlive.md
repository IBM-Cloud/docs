---



copyright:
  years: 2015，2017
lastupdated: "2017-3-10"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}

#{{site.data.keyword.Bluemix_notm}} Live Sync
{: #live-sync}

 
Si está creando una app Node.js, puede utilizar {{site.data.keyword.Bluemix}} Live Sync para actualizar rápidamente la instancia de la app que se ejecuta en {{site.data.keyword.Bluemix_notm}} y desarrollarla sin redespliegue manual.    
{: shortdesc}

Cuando realice un cambio, puede verlo de inmediato en la app {{site.data.keyword.Bluemix_notm}} en ejecución. {{site.data.keyword.Bluemix_notm}} Live Sync funciona 
<!--from both the command line and -->
en Eclipse Orion Web IDE (Web IDE). Puede depurar apps escritas en Node.js utilizando {{site.data.keyword.Bluemix_notm}} Live Sync.  

{{site.data.keyword.Bluemix_notm}} Live Sync consta de dos características. 
<!-- three -->

<!--
**Desktop Sync**  

You can synchronize any desktop directory tree with a cloud-based project workspace similar to the way Dropbox works. The Web IDE directly edits the same cloud-based workspace, so both stay in sync. Desktop Sync works for any kind of application. To use Desktop Sync, you need to download and install the BL command line interface.  
-->

**Edición en directo**

Puede hacer cambios en una app Node.js que se ejecuta en {{site.data.keyword.Bluemix_notm}} y probarlos en el navegador inmediatamente. Todos los cambios que haga en Web IDE se propagarán
inmediatamente al sistema de archivos de la app.  

**Debug**  

Mientras una app Node.js está en la modalidad de edición en directo puede aplicarle un shell y depurarla. Con el depurador de node Inspector puede, de manera dinámica, editar el código, insertar puntos de interrupción, recorrer el código, reiniciar el tiempo de ejecución, entre otras características.  

<!-- You can use Desktop Sync to keep your desktop workspace in sync with the cloud-based project workspace that you edit directly with the Web IDE. -->

Puede utilizar la característica Edición en directo para propagar los cambios en su espacio de trabajo de proyectos basados en la nube
a la app en ejecución. 
<!-- You can use one or both of these features. And if you use Desktop Sync or -->
Si utiliza la edición en directo para colocar su
app en la modalidad de edición en directo, puede depurar la app en ejecución.En el siguiente diagrama se muestra el proceso de Bluemix Live Sync.    

Figura 1. Proceso de Bluemix Live Sync
    

![Imagen del proceso de Bluemix Live Sync](images/bluemix-live-sync.png)

Si está desarrollando una app Java
que se ejecuta en Liberty, puede depurarla de forma remota mediante [Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools).


##Edición en directo {: #live-edit}

Si está creando una app Node.js, al efectuar cambios en el proyecto mediante Web IDE, la característica de edición en directo de {{site.data.keyword.Bluemix_notm}} Live Sync puede actualizar rápidamente la instancia de app que se ejecuta en {{site.data.keyword.Bluemix_notm}}. La edición en directo le permite desarrollar como lo haría en el escritorio sin tener que volver a desplegar.

La característica Edición en directo solo se admite en las apps Node.js.

En Eclipse Orion Web IDE (Web IDE), pulse **Edición en directo** en la barra de ejecución.

![Imagen de la barra de ejecución con la edición en directo](images/bluemix-live-sync-light.png)

Edición en directo le permite obtener una vista previa rápida de los cambios en las apps Node.js
que se ejecutan en {{site.data.keyword.Bluemix_notm}}. Al actualizar
el código con la característica Edición en directo activada, puede renovar la ventana del navegador de su app web
para ver dichos cambios reflejados pocos segundos después de efectuarlos.

<!--
For a tutorial on using the Live Edit feature of {{site.data.keyword.Bluemix_notm}} Live Sync, see the tutorial [Test and debug a Node.js app with Bluemix Live Sync![External link icon](../icons/launch-glyph.svg "External link icon")](https://hub.jazz.net/tutorials/livesync){:new_window}.
-->

Al cambiar los archivos de Web IDE, se volverán a desplegar
automáticamente en la app que se ejecuta en {{site.data.keyword.Bluemix_notm}}. Si tiene que reiniciar la app Node, puede utilizar el botón **Reiniciar**
de la barra de ejecución.

**NOTA:** Para obtener una experiencia más coherente al utilizar la característica Edición en directo de {{site.data.keyword.Bluemix_notm}}, son necesarios 256 MB de memoria adicional y se añadirán.

##{{site.data.keyword.Bluemix_notm}} Live
Debug {: #live-debug}

Puede acceder a la característica de {{site.data.keyword.Bluemix_notm}} Live Sync Debug cuando {{site.data.keyword.Bluemix_notm}} Live Sync esté habilitado para la app Node.js.

Con la característica debug, puede editar código, insertar puntos de interrupción, recorrer el código,
reiniciar el tiempo de ejecución de forma dinámica, entre otras características, mientras la app está en servicio en {{site.data.keyword.Bluemix_notm}}. Puede desarrollar la app de forma incremental con agilidad mientras elige entre una larga lista de servicios de {{site.data.keyword.Bluemix_notm}}.

{{site.data.keyword.Bluemix_notm}} Live
Debug incluye las siguientes características:

* Control del tiempo de ejecución de la aplicación
* Depurar utilizando [node-inspector![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/node-inspector/node-inspector){:new_window}
* Acceso a shell

###Control del tiempo de ejecución de la aplicación {: #app-runtime}

Con el control del tiempo de ejecución de la app, puede utilizar Debug
para inspeccionar el estado de la app en el momento inicial. Esta función resulta útil para solucionar los problemas de una app que falla al iniciarse.

Mientras esté desarrollando la app, puede elegir entre las siguientes acciones:

* Realizar un reinicio rápido de la app
* Suspender la app antes de que se ejecute ningún código de la app

###Depurar {: #debug}

Debug incluye las siguientes funciones:

**Restricción:** Se necesita Google Chrome.

* Establecer puntos de interrupción en el código de la app para detener la ejecución en una línea específica.
* Editar las condiciones de los puntos de interrupción cuando se cumplan ciertos criterios.
* Inspeccionar el estado de las variables locales y los campos.
* Visualizar la salida de la depuración de manera inmediata desde las llamadas `console.log()`. Esta opción es más rápida que la supervisión de registros cf.
* Utilizar el editor de código fuente incorporado para introducir cambios inmediatos (aunque temporales) al código de la app en ejecución.

###Shell {: #shell}

Esta herramienta le da acceso de shell al contenedor en el que se ejecuta la app. Con el uso de este terminal puede ejecutar, de manera remota, mandatos de diagnóstico de shell para administrar la app.

Supervise el uso de la memoria y de la CPU en la instancia que utiliza mandatos estándares de Linux, como por ejemplo **top**, **ps** y **kill**.

###Configuración de una app para habilitar {{site.data.keyword.Bluemix_notm}} Live
Debug {: #configure_app_debug}

La app debe usar el paquete de compilación IBM SDK for Node.js. No se da soporte a los paquetes de compilación personalizados.

1. Permita que el paquete de compilación detecte el mandato de inicio de la app. El paquete de compilación debe detectar automáticamente el mandato start y no se debe establecer en el archivo `manifest.yml`.  

    a. Asegúrese de que el archivo `package.json` contenga un script
de inicio que incluya un mandato start para la app.  
    b. Si el archivo `manifest.yml` de la app contiene un mandato, establézcalo en null.  

2. Establezca la variable de entorno.  

    a. En el archivo `manifest.yml`, añada esta variable:
	```
	env:
      ENABLE_BLUEMIX_DEV_MODE: "true"
	```

3. Aumente la memoria.  

    a. En el archivo `manifest.yml` de la app, añada 128M o más al valor especificado para el atributo memory.

Una vez instalado {{site.data.keyword.Bluemix_notm}} Live
Debug, puede utilizar las herramientas de depuración.

Envíe la app y luego vaya a `https://app-host.mybluemix.net/bluemix-debug/manage` para acceder a la interfaz de usuario de depuración de {{site.data.keyword.Bluemix_notm}}. Cuando se le solicite que se autentique, especifique su ID y su señal de acceso personal o su ID de IBM y contraseña.    

<!--
   **Note**: Your user ID for DevOps Services can be either an IBMid or a federated ID (corporate ID). If you use federated authentication, to log in to your Bluemix Live Sync command-line client, you must use a personal access token instead of a password. If you don't use federated authentication, your IBMid and password work with all clients. For more information about creating a personal access token, see [What's federated authentication and how does it affect me?![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/devops-services/2016/06/23/whats-federated-authentication-and-how-does-it-affect-me/){:new_window}
   -->

###Restauración de configuraciones de app e inhabilitación de Bluemix Live
Debug {: #restore_live_debug}

1. Elimine la variable de entorno ENABLE_BLUEMIX_DEV_MODE del archivo `manifest.yml` de la app.

2. Restaure el mandato start y el valor memory originales de la app.

3. Envíe la app por push.


## Enlaces relacionados
{: #general}

* [Eclipse tools for Bluemix![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://www.ng.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html){:new_window}
