{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}

#{{site.data.keyword.Bluemix_notm}} Live Sync {: #live-sync}

*Última actualización: 8 de diciembre de 2015*  

Si está creando una app Node.js, puede utilizar {{site.data.keyword.Bluemix}} Live Sync para actualizar rápidamente la instancia de la app que se ejecuta en {{site.data.keyword.Bluemix_notm}} y desarrollarla como lo haría en el escritorio sin tener que volver a desplegarla.    
{: shortdesc} 

Cuando realice un cambio, puede verlo de inmediato en la app {{site.data.keyword.Bluemix_notm}} en ejecución. {{site.data.keyword.Bluemix_notm}} Live Sync funciona tanto con la línea de mandatos
como con Web IDE. Puede depurar apps escritas en Node.js utilizando {{site.data.keyword.Bluemix_notm}} Live Sync.   

{{site.data.keyword.Bluemix_notm}} Live Sync consta de tres características. 

**Desktop Sync**  
    Puede sincronizar cualquier árbol de directorio de escritorio con un espacio de trabajo de proyectos basados en la nube similar al modo de trabajo de Dropbox.
Web IDE edita directamente el mismo espacio de trabajo basado en la nube, de manera que ambos están sincronizados.  Desktop
Sync funciona para cualquier tipo de app. Para utilizar Desktop Sync debe descargar e instalar la interfaz de línea de mandatos BL.  
	
**Edición en directo**	
    Puede hacer cambios en una app Node.js que se ejecuta en {{site.data.keyword.Bluemix_notm}} y probarlos en el navegador inmediatamente. Todos los cambios que haga en un directorio de escritorio sincronizado o en Web IDE se propagarán
inmediatamente al sistema de archivos de la app.  
	
**Debug**  
    Mientras una app Node.js está en la modalidad de edición en directo puede aplicarle un shell y depurarla. Con el depurador de node Inspector puede, de manera dinámica, editar el código, insertar puntos de interrupción, recorrer el código, reiniciar el tiempo de ejecución, entre otras características.  

Puede utilizar Desktop Sync para mantener actualizado su espacio de trabajo de escritorio
con el espacio de trabajo de proyectos basados en la nube que edita directamente con Web IDE.
Puede utilizar la característica Edición en directo para propagar los cambios en su espacio de trabajo de proyectos basados en la nube
a la app en ejecución. Puede utilizar una o ambas características. Además, si utiliza Desktop Sync o Edición en directo para colocar su
app en la modalidad de edición en directo, puede depurar la app en ejecución.

En el siguiente diagrama se muestra el proceso de Bluemix Live Sync. 	

*Figura 1. Proceso de Bluemix Live Sync*
![Imagen del proceso de Bluemix Live Sync](images/bluemix-live-sync.png)
 
Si está desarrollando una app Java
que se ejecuta en Liberty, puede depurarla de forma remota mediante [Eclipse Tools for Bluemix](../manageapps/eclipsetools/eclipsetools.html#eclipsetools).

##Desktop Sync {: #desktop-sync} 

Puede utilizar la característica Desktop Sync de Bluemix Live Sync para
actualizar con rapidez la instancia de app en {{site.data.keyword.Bluemix_notm}} y desarrollarla como lo haría en el escritorio.  

Desktop Sync tiene las siguientes consideraciones: 
* Desktop Sync se ejecuta en estos sistemas operativos: 
  * Windows 7 u 8
  * Mac OS X versión 10.9 o posterior
      **Nota:** Windows requiere .NET Framework versión 4.5. Si no tiene .NET instalado, se le solicitará que lo instale cuando instale la interfaz de línea de mandatos (CLI) de {{site.data.keyword.Bluemix_notm}} Live Sync.  
* No es necesario clonar el repositorio Git. 
* Independientemente del tipo de app que esté desarrollando, puede sincronizar su proyecto de escritorio con el espacio de trabajo en la nube. 
* Si la app está escrita en Node.js, puede propagar los cambios en las apps que están en ejecución.

Para obtener más detalles sobre los mandatos, consulte la documentación de la CLI de [ Live Sync](../cli/reference/bl/index.html). 

<ol>
<li>Descargue e instale la línea de mandatos bl de {{site.data.keyword.Bluemix_notm}} Live Sync.   
<p>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/blive_setup.msi" target="_blank" title="(se abre en un separador o ventana nueva)"><img class="image" src="images/bl_gs_icons_windows_b.svg" alt="Botón Descargar la línea de mandatos bl de Windows" /> </a> <a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/BluemixLive.pkg" target="_blank" title="(se abre en un separador o ventana nueva)"><img class="image" src="images/bl_gs_icons_mac-osx_b.svg" alt="Botón Descargar la línea de mandatos bl de Mac" /> </a>
</p>  

<strong>Importante:</strong> La herramienta de línea de mandatos bl solo está disponible para Windows 7 y 8 y Mac OS X versión 10.9 o posterior.</li>
<li>En una línea de mandatos, inicie sesión con el mandato siguiente. Se le solicitará su ID y contraseña de IBM.  
<pre class="codeblock">bl login</pre>
</li>

<li>Consulte la lista de proyectos disponibles para sincronizar {{site.data.keyword.Bluemix_notm}} Live Sync introduciendo el siguiente mandato:
<pre class="codeblock">bl projects</pre>
<p>Busque el nombre de proyecto en la lista que coincida con la app. El nombre del proyecto tiene el formato de su <i>alias</i> | <i>nombre app</i>.</p>
</li>
<li>Sincronice el entorno local con el proyecto en {{site.data.keyword.Bluemix_notm}} especificando
el siguiente mandato. Si es el propietario del proyecto, solo debe especificar nombre-app para nombreProyecto.<pre class="codeblock">bl sync nombre_proyecto -d directorio_local --verbose</pre>
<p>Este mandato seguirá ejecutándose (y la sincronización continuará) hasta que se especifique una "q". La opción --verbose muestra la información de estado e inicio de sesión. Si alguno de los argumentos contiene un espacio,
deberá escribir el nombre entre comillas. </p></li>
<li>En otra ventana de la línea de mandatos del directorio local,
despliegue la app en {{site.data.keyword.Bluemix_notm}} en la
modalidad de edición en directo especificando el siguiente mandato:
<pre class="codeblock">bl start</pre>
</li>
</ol>

Cuando cambie los archivos en su directorio local, los cambios
se propagarán automáticamente en la app que se ejecuta
en {{site.data.keyword.Bluemix_notm}} y
en el espacio de trabajo de la nube del proyecto. Si tiene que reiniciar la app Node
puede utilizar el siguiente mandato:
```
bl start --restart 
```

##Edición en directo {: #live-edit} 

Si está creando una app Node.js, al efectuar cambios en el proyecto mediante Web IDE, la característica de edición en directo de {{site.data.keyword.Bluemix_notm}} Live Sync puede actualizar rápidamente la instancia de app que se ejecuta en {{site.data.keyword.Bluemix_notm}}.
La edición en directo le permite desarrollar como lo haría en el escritorio sin tener que volver a desplegar. 

La característica Edición en directo solo se admite en las apps Node.js. 

En Web IDE, en la barra de ejecución, pulse **Edición en directo**. 

![Imagen de la barra de ejecución con la edición en directo](images/run-bar-live-edit.png) 

Edición en directo le permite obtener una vista previa rápida de los cambios en las apps Node.js
que se ejecutan en {{site.data.keyword.Bluemix_notm}}.
Al actualizar
el código con la característica Edición en directo activada, puede renovar la ventana del navegador de su app web
para ver dichos cambios reflejados pocos segundos después de efectuarlos. 

Para ver un tutorial sobre cómo utilizar la característica Edición en directo de {{site.data.keyword.Bluemix_notm}} Live Sync, vea el tutorial [Pruebe y depure una app Node.js con Bluemix Live Sync](https://hub.jazz.net/tutorials/livesync).

Al cambiar los archivos de Web IDE, se volverán a desplegar
automáticamente en la app que se ejecuta en {{site.data.keyword.Bluemix_notm}}.
Si tiene que reiniciar la app Node, puede utilizar el botón **Reiniciar**
de la barra de ejecución.

##{{site.data.keyword.Bluemix_notm}} Live
Debug {: #live-debug}

Puede acceder a la característica de {{site.data.keyword.Bluemix_notm}} Live Sync Debug cuando {{site.data.keyword.Bluemix_notm}} Live Sync esté habilitado para la app Node.js. 

Con la característica debug, puede editar código, insertar puntos de interrupción, recorrer el código,
reiniciar el tiempo de ejecución de forma dinámica, entre otras características, mientras la app está en servicio en {{site.data.keyword.Bluemix_notm}}.
Puede desarrollar la app de forma incremental con agilidad mientras elige entre una larga lista de servicios de {{site.data.keyword.Bluemix_notm}}. 

{{site.data.keyword.Bluemix_notm}} Live
Debug incluye las siguientes características:

* Control del tiempo de ejecución de la aplicación
* Depuración mediante [node-inspector](https://github.com/node-inspector/node-inspector)
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

Envíe la app por push y vaya a `https://app-host.mybluemix.net/bluemix-debug/manage` para acceder a la interfaz de usuario de depuración de {{site.data.keyword.Bluemix_notm}}. Cuando se le solicite, escriba el ID y la contraseña de IBM para autenticarse. 

###Restauración de configuraciones de app e inhabilitación de Bluemix Live
Debug{: #restore_live_debug} 

1. Elimine la variable de entorno ENABLE_BLUEMIX_DEV_MODE del archivo `manifest.yml` de la app.

2. Restaure el mandato start y el valor memory originales de la app. 

3. Envíe la app por push.


># Enlaces relacionados {:class="linklist"}
>## Guías de aprendizaje y ejemplos {:id="samples"}
>* [Pruebe y depure una app Node.js con Bluemix Live Sync](https://hub.jazz.net/tutorials/livesync)
>
># Enlaces relacionados {:class="linklist"}
>## Enlaces relacionados {:id="general"}
>* [mandatos bl](https://www.ng.bluemix.net/docs/cli/bl_cli.html)   
>
>{:elementKind="article" id="rellinks"}
