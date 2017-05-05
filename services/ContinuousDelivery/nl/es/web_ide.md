---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-31"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Edición de código con el IDE de Eclipse Orion 
{: #web_ide}

Eclipse Orion {{site.data.keyword.webide}} es un entorno de desarrollo basado en navegador donde puede desarrollar para la web. Puede desarrollar en JavaScript, HTML y CSS con la ayuda de asistencia de contenido, finalización del código y comprobación de errores. {{site.data.keyword.webide}} funciona con casi cualquier lenguaje y ofrece resaltado de la sintaxis para la mayoría de los tipos de archivos. El control de origen está integrado y puede desplegar código de forma local para probar y depurar las apps.
{:shortdesc}

Lo mejor de todo es que {{site.data.keyword.webide}} está basado en la web. No tiene que instalar, mantener ni escalar nada. Puede desarrollar en cualquier lugar donde tenga conexión a Internet.

## Configuración del editor
{: #editorsetup}

{{site.data.keyword.webide}} se puede personalizar para que pueda elegir los esquemas de colores, las herramientas técnicas y los valores que cumplan sus necesidades de desarrollo. Para ver y modificar los valores, desde el menú de la izquierda, pulse el icono **Valores** <img class="inline" src="images/webide_settings_icon_light_small.png"  alt="El icono Valores">. 

Si necesita a menudo cambiar determinados valores mientras edita, puede acceder a dichos valores rápidamente desde el icono **Valores de editor local** <img class="inline" src="images/webide_local_settings_icon_light_small.png"  alt="Icono Valores de editor local">.  

![Valores de editor local](images/webide_local_editor_settings_light.png)

De forma predeterminada, siempre se muestran los valores para el estilo del editor y el tamaño de fuente. Para incluir otros valores de editor en el menú, siga estos pasos:

1. Pulse el icono **Valores de editor local** <img class="inline" src="images/webide_local_settings_icon_light_small.png"  alt="Icono valores de editor local">. 

2. Pulse **Valores del editor**.

3. Para incluir o excluir un valor del menú **Valores del editor local**, pulse la estrella que hay junto a cada valor. 

![Conmutador Valores de editor](images/webide_editor_settings_toggle_light.png)


## Edición de código
{: #editcode}

{{site.data.keyword.webide}} tiene dos secciones principales. La primera sección es el navegador de archivos, que muestra los archivos del proyecto en una estructura de árbol. Desde el navegador de archivos, puede crear, cambiar el nombre, suprimir y gestionar los archivos y carpetas.

**Consejo:** para cargar archivos en el navegador de archivos, arrástrelos desde el sistema al navegador de archivos.

La segunda sección es el panel del editor. El editor proporciona varias características de codificación, incluida la asistencia de contenido y la validación de sintaxis.

![Web IDE](images/webide_light.png)

### Cómo trabajar con varios archivos
1. Para trabajar con dos archivos a la vez, pulse el icono **Cambiar modo de editor de división** <img class="inline" src="images/webide_split_editor_icon_light_small.png"  alt="Icono Editor de división">. 
2. Desde el menú que se abre, seleccione una vista.

 Tras seleccionar una vista, si ya se ha abierto un archivo en el editor, se mostrará en ambas vistas de editor.

 Para abrir o cambiar un archivo que se muestra en una de las vistas del editor:
 1. Mueva el cursor a la vista de editor que desee cambiar.
 2. En el navegador de archivos, pulse un archivo.

### Accesos directos de teclado
Sólo se puede acceder a la mayoría de los mandatos de {{site.data.keyword.webide}} mediante accesos directos de teclado.

Para ver una lista de los accesos directos de teclado en el editor, pulse Alt+Mayús+?. Si está utilizando un Mac OS, pulse Ctrl+Mayús+?.

## Gestión del código fuente
{: #sourcecontrol}

{{site.data.keyword.webide}} se integra con herramientas de gestión de código fuente. Para trabajar con el repositorio de Git, pulse el icono **Repositorio de Git** <img class="inline" src="images/webide_git_icon_light_small.png"  alt="El icono Repositorio de Git">.  

 **Consejo**: Si utiliza {{site.data.keyword.webide}} con cadenas de herramientas abiertas, el espacio de trabajo ya contiene su GitHub, {{site.data.keyword.ghe_short}} o repositorios de Git Repos and Issue Tracking. Los repositorios que están asociados a la cadena de herramientas actual aparecen resaltados.


## Despliegue de una app desde el espacio de trabajo
{: #deploy}

1. Para desplegar la app, desde la barra de ejecución, seleccione o cree una configuración de inicio. 
1. Pulse el icono de despliegue <img class="inline" src="images/webide_deploy_button_light_small.png"  alt="icono de despliegue">. Se desplegará una instancia de la app utilizando el contenido actual del espacio de trabajo y del entorno definido en la configuración de lanzamiento. 
2. Una vez que se despliegue la app, puede utilizar la barra de ejecución para detener, reiniciar o depurar la app, ver registros, etc.
![Barra de ejecución](images/webide_runbar_light.png)    

<!-- 3/6/2016: bl commands don't work with V2/CD 
## Editing outside of the {{site.data.keyword.webide}}
{: #editlocal}

To use an editor besides the {{site.data.keyword.webide}}, set up {{site.data.keyword.Bluemix_live}} so that you can work directly with your project files in any tool. {{site.data.keyword.Bluemix_live_notm}} is a command-line application that synchronizes the changes in your local file system with your cloud workspace in {{site.data.keyword.jazzhub}}. 

### Before you begin 

Download and install the [{{site.data.keyword.Bluemix_live_notm}} command-line interface![External link icon](../../icons/launch-glyph.svg "External link icon")](http://livesyncdownload.ng.bluemix.net){: new_window}.

### Synchronizing your local environment with {{site.data.keyword.Bluemix_notm}}
{: #edit_local_download}

1. Open a command-line window.
2. Sign in to {{site.data.keyword.Bluemix_notm}}:

	```
	bl login
	```
	{: pre}

3. When you are prompted, enter your IBMid and password.
4. View a list of your {{site.data.keyword.Bluemix_notm}} projects: 

	```
	bl projects
	```
	{: pre}

4. Synchronize your local environment with your project on {{site.data.keyword.Bluemix_notm}}:

	```
	bl sync projectName
	```
	{: pre}

where `projectName` is your {{site.data.keyword.Bluemix_notm}} app's name.

When you are finished editing, enter `q` to end synchronization.

### Enabling the Desktop Sync feature to edit code locally

The Desktop Sync feature is like Live Edit mode for the command line. You need the Desktop Sync feature to debug on the command line.
1. In another command-line window, enable the Desktop Sync feature:

	```
	cd localDirectory
	bl start
	```
	{: codeblock}

2. Use the launch configuration that you created in the {{site.data.keyword.webide}}. After you select the launch configuration, the Desktop Sync feature is enabled in your local environment. In the command-line window that you just opened, you can view the app's URL, the debug URL, the manage URL, and view the {{site.data.keyword.Bluemix_live_notm}} state.

3. Refresh the browser and verify that you can see the changes that you saved to static files in the local workspace. 

### Disabling the Desktop Sync feature

1. In the second command-line window, enter `bl stop`.
2. In the first command-line window, enter `q`.

--> 
