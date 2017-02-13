---

copyright:
  years: 2016, 2017
lastupdated: "2016-12-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilización de un iniciador de código para crear un proyecto
{: #projects_code}

Puede utilizar un [iniciador de código](starters.html#Code_Starter) en el panel de control de {{site.data.keyword.Bluemix}} Mobile para crear un proyecto en el entorno de {{site.data.keyword.Bluemix_notm}}. Este procedimiento no se aplica a los proyectos que utilizan los Iniciadores de IU. Consulte [Creación de un proyecto con un Iniciador de IU](projects_ui.html) para obtener instrucciones para los Iniciadores de IU. 
{:shortdesc}

Complete los pasos siguientes para crear un proyecto con un Iniciador de código:

1. Cree un nuevo proyecto de panel de control de Mobile en {{site.data.keyword.Bluemix_notm}}.

 Empiece con el separador *Guía de inicio* tras seleccionar el catálogo de Mobile. Hay descripciones de iniciadores seleccionados que puede utilizar y las formas distintas de crear un proyecto que depende de cuánta ayuda necesite. Si sólo desea comenzar, seleccione **Crear proyecto**.

 Si ya tiene proyectos, también puede empezar con el separador *Proyectos* seleccionado. Desde la vista **Proyectos** del panel de control de {{site.data.keyword.Bluemix_notm}} Mobile, puede seleccionar un proyecto con el que trabajar, utilizar las *Acciones* para un proyecto para suprimirlo o descargar el código para el mismo, o crear un nuevo proyecto.

	1. En la Consola de {{site.data.keyword.Bluemix_notm}}, seleccione **Mobile** tras expandir el menú con las tres líneas junto al logotipo de {{site.data.keyword.Bluemix_notm}}. 
	
	2. Seleccione **Crear proyecto**. 

	  De forma alternativa, puede seleccionar el separador **Proyectos** para ver los proyectos que ya se encuentran en el entorno móvil y crear un proyecto nuevo pulsando **Crear proyecto**.

	3. Pulse **Iniciadores de código**.  

	4. Seleccione el iniciador que coincide mejor con el tipo de aplicación que desea crear y seleccione **Crear proyecto**. Estos son **Iniciadores de IU** e **Iniciadores de código**. Consulte [Iniciadores](starters.html) para obtener más información sobre los iniciadores y cómo utilizarlos. 
	
	5. Especifique un nombre para el proyecto y seleccione **Crear**.
	
2. Realice las selecciones en la pantalla **Visión general del proyecto**.  La pantalla **Visión general del proyecto** muestra información sobre el proyecto y los servicios opcionales que puede añadir al mismo, como por ejemplo {{site.data.keyword.mobilepushshort}} y Autenticación.  

	1. Opcional: Seleccione **Añadir** para añadir uno de los servicios listados al proyecto. Edite el **Nombre de servicio** para el servicio y pulse **Crear**. Cuando añade un servicio al proyecto, enlaza con la página de {{site.data.keyword.Bluemix_notm}} correspondiente a dicho servicio. Configure el servicio especificando la información necesaria para el mismo.
	
	2. Opcional: Repita el paso *a* para cualquier prestación adicional que desee añadir al proyecto.

3. Opcional: Seleccione **Datos** para conectar una base de datos Cloudant NoSQL o un servicio Object Storage. 
	1. Pulse **Crear** para configurar una nueva base de datos Cloudant NoSQL o servicio Object Storage. 
	
	Nota: Si crea una instancia del servicio Object Storage, se le guiará fuera del proyecto para crearlo y añadir las credenciales necesarias. Vuelva al proyecto después de crearlo y seleccione **Añadir existente** para conectar el servicio al proyecto. 
	
	Si ya tiene una instancia existente que no está conectada a otro proyecto que desea conectar a este, seleccione **Añadir existente**. 
	
	2. Compruebe que el mosaico de la base de datos Cloudant NoSQL o del servicio Object Storage con el que ha conectado se muestra en el separador Datos del proyecto. 

4.  Descargue el proyecto y complete la configuración.

    1. Pulse **Descargar código** y seleccione el idioma preferido.
   
    2. Extraiga el archivado y visualice el archivo `README.md` en un visor Markdown para completar la configuración.

5.  Pruebe la aplicación. 


