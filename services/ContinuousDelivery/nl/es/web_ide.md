---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Edición de código con Eclipse Orion {{site.data.keyword.webide}}
{: #web_ide}

Última actualización: 26 de octubre de 2016
{: .last-updated}

Eclipse Orion {{site.data.keyword.webide}} es un entorno de desarrollo basado en navegador donde puede desarrollar para la web. Puede desarrollar en JavaScript, HTML y CSS con la ayuda de asistencia de contenido, finalización del código y comprobación de errores. {{site.data.keyword.webide}} funciona con casi cualquier idioma y ofrece realce de la sintaxis para la mayoría de los [tipos de archivos (el enlace se abre en una nueva ventana)](https://hub.jazz.net/docs/overview/#dev_support){: new_window}. El control de origen se crea mediante Git o Jazz SCM, y puede desplegar código de forma local para probar y depurar las apps.
{:shortdesc}

Lo mejor de todo es que {{site.data.keyword.webide}} está basado en la web. No tiene que instalar, mantener ni escalar nada. Puede desarrollar en cualquier lugar donde tenga conexión a Internet.

## Configuración del editor
{: #editorsetup}

{{site.data.keyword.webide}} se puede personalizar para que pueda elegir los esquemas de colores, las herramientas técnicas y los valores que cumplan sus necesidades de desarrollo. Para ver y modificar los valores, desde el menú de la izquierda, pulse el icono **Valores** <img class="inline" src="./images/webide_settings_icon_light.png"  alt="El icono Valores">.

Si necesita a menudo cambiar determinados valores mientras edita, puede acceder a dichos valores rápidamente desde el icono **Valores de editor local** <img class="inline" src="./images/webide_local_settings_icon_light.png"  alt="icono Valores de editor local"> en la esquina superior derecha del editor

![Valores de editor local](images/webide_local_editor_settings_light.png)

De forma predeterminada, siempre se muestran los valores para el estilo del editor y el tamaño de fuente. Para incluir otros valores de editor en el menú, siga estos pasos:

1. Pulse el icono **Valores de editor local** <img class="inline" src="./images/webide_local_settings_icon_light.png"  alt="icono Valores de editor local">.

2. Pulse **Valores del editor**.

3. Para incluir o excluir un valor del menú **Valores del editor local**, pulse el círculo que hay junto al valor.

![Conmutador Valores de editor](images/webide_editor_settings_toggle_light.png)


## Edición de código
{: #editcode}

{{site.data.keyword.webide}} tiene dos secciones principales. La primera sección es el navegador de archivos de la izquierda, que muestra los archivos del proyecto en una estructura de árbol. Desde el navegador de archivos, puede crear, cambiar el nombre, suprimir y gestionar los archivos y carpetas.

**Consejo:** para cargar archivos en el navegador de archivos, arrástrelos desde el sistema al navegador de archivos.

La segunda sección es el panel del editor a la derecha. El editor proporciona varias características de codificación, incluida la asistencia de contenido y la validación de sintaxis.

![Web IDE](images/webide_light.png)

### Cómo trabajar con varios archivos
1. Para trabajar con dos archivos a la vez, pulse el icono **Cambiar modo de editor de división** <img class="inline" src="./images/webide_split_editor_icon_light.png"  alt="icono Editor de división"> en la parte superior del editor.
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

{{site.data.keyword.webide}} se integra con herramientas de gestión de código fuente. Para trabajar con el repositorio de Git, pulse el icono **Repositorio de Git** <img class="inline" src="./images/webide_git_icon_light.png"  alt="icono Repositorio de Git">. Para obtener más información, consulte [Control de origen con Git (el enlace se abre en una nueva ventana)](https://hub.jazz.net/docs/git/){: new_window}.


## Despliegue de una app desde el espacio de trabajo
{: #deploy}

1. Para desplegar la app, desde la barra de ejecución, seleccione o [cree (el enlace se abre en una nueva ventana)](https://hub.jazz.net/tutorials/livesync/#launch_configuration){: new_window} una configuración de lanzamiento.
1. Pulse el icono de despliegue <img class="inline" src="./images/webide_deploy_button_light.png"  alt="icono de despliegue">. Se desplegará una instancia de la app utilizando el contenido actual del espacio de trabajo y del entorno definido en la configuración de lanzamiento. 
2. Una vez que se despliegue la app, puede utilizar la barra de ejecución para detener, reiniciar o depurar la app, ver registros, etc.
![Barra de ejecución](images/webide_runbar_light.png)

 ## Edición fuera del {{site.data.keyword.webide}}
{: #editlocal}

Para utilizar un editor distinto a {{site.data.keyword.webide}}, configure {{site.data.keyword.Bluemix_live}} para que pueda trabajar directamente con los archivos de proyectos en cualquier herramienta. {{site.data.keyword.Bluemix_live_notm}} es una aplicación de línea de mandatos que sincroniza los cambios del sistema de archivos local con el espacio de trabajo de la nube en {{site.data.keyword.jazzhub}}. 

### Antes de empezar 

Descargue e instale la interfaz de línea de mandatos de [{{site.data.keyword.Bluemix_live_notm}} (el enlace se abre en una nueva ventana)](http://livesyncdownload.ng.bluemix.net){: new_window}.

### Sincronización del entorno local con {{site.data.keyword.Bluemix_notm}}
{: #edit_local_download}

1. Abra una ventana de línea de mandatos.
2. Inicie una sesión en {{site.data.keyword.Bluemix_notm}}:

	```
	bl login
	```
	{: pre}

3. Cuando se le solicite, especifique su ID de IBM y su contraseña.
4. Visualice una lista de los proyectos de {{site.data.keyword.Bluemix_notm}}: 

	```
	bl projects
	```
	{: pre}

4. Sincronice el entorno local con el proyecto en {{site.data.keyword.Bluemix_notm}}:

	```
	bl sync projectName
	```
	{: pre}

donde `projectName` es el nombre de la aplicación de {{site.data.keyword.Bluemix_notm}}.

Cuando haya terminado de editar, especifique `q` para finalizar la sincronización.

### Habilitación de la característica Desktop Sync para editar código de forma local

La característica Desktop Sync es como la modalidad Live Edit para la línea de mandatos. Necesita la característica Desktop Sync para depurar en la línea de mandatos.
1. En otra ventana de línea de mandatos, habilite la característica Desktop Sync:

	```
	cd localDirectory
	bl start
	```
	{: codeblock}

2. Utilice la configuración de lanzamiento que haya creado en {{site.data.keyword.webide}}. Tras seleccionar la configuración de lanzamiento, la característica Desktop Sync estará habilitada en el entorno local. En la ventana de línea de mandatos que acaba de abrir, puede ver el URL de la aplicación, de depuración, de gestión, y ver el estado de {{site.data.keyword.Bluemix_live_notm}}.

3. Renueve el navegador y verifique que puede ver los cambios que ha guardado en archivos estáticos en el espacio de trabajo local. 

### Inhabilitación de la característica Desktop Sync

1. En la segunda ventana de la línea de mandatos, especifique `bl stop`.
2. En la primera ventana de la línea de mandatos, especifique `q`.
